---
tags: [jotform/apps, bildirim, gelistirme, deney]
status: tamamlandi
updated: 2026-06-26
---

# 🧪 Deney 01a — Sunucuda Kalıcı Process Kaldırılabiliyor mu?

> [!success] Durum: ✅ TAMAMLANDI (2026-06-26) — **Seçenek B uygulanabilir.** Process SSH kopunca yaşıyor. Bkz. "Bulgular".
> Bağlam: [[01-Cron-Motoru]] "Çalıştırma Seçenekleri" → Seçenek B (intern sunucuda kalıcı process) doğrulaması.

## 🎯 Hipotez
Intern sunucuda, container olmadan, **kalıcı bir PHP process** başlatabiliriz; bu process oturum kapansa da yaşamaya devam eder, **çıktısı görülebilir**, ve **aynı anda birden çok** çalışabilir.

## ❓ Cevaplanacak Alt Sorular
1. **Spawn:** Arka planda uzun-ömürlü bir PHP CLI process başlatabiliyor muyuz?
2. **Persistence:** Başlatan oturum/istek bitince yaşıyor mu? Host uzun process'i öldürüyor mu?
3. **Observability:** Çıktısını (log) görebiliyor muyuz?
4. **Concurrency:** N adet eşzamanlı, ayırt edilebilir biçimde koşabiliyor mu?
5. **Lifecycle:** Durdurabiliyor/yeniden başlatabiliyor muyuz? Deploy'da ölüyor mu?

## 🔑 Erişim: SSH var ✅ (onaylandı)
Shell yolunu kullanıyoruz — web endpoint'leri (`heartbeat_start.php` / `heartbeat_log.php`) **gerekmez** (yalnızca shell'siz senaryo için referans olarak duruyor). `disable_functions`/`exec` derdi de yok; `php` doğrudan CLI'dan çalıştırılır.

> [!warning] Asıl belirsizlik SSH'te buraya kayar: **logout sonrası yaşam**
> Paylaşımlı/systemd sunucularda `logind` **`KillUserProcesses=yes**` olabilir → SSH oturumu kapanınca `nohup` ile başlatılan process bile **öldürülür**. Bu yüzden `setsid` ile oturumdan tam koparıyoruz; gerekirse `tmux`/`screen` fallback. Gerçek test: **çık, bekle, geri bağlan, hâlâ yaşıyor mu?**

## 🧰 Deney Artefaktları (çalıştırılabilir)

### 1) Ortam yetenek kontrolü — `env_check.php`
```php
<?php
header('Content-Type: text/plain; charset=utf-8');
echo "php_sapi: " . PHP_SAPI . "\n";
echo "php_version: " . PHP_VERSION . "\n";
$disabled = array_map('trim', explode(',', (string) ini_get('disable_functions')));
foreach (['exec','shell_exec','proc_open','popen'] as $f) {
    $ok = function_exists($f) && !in_array($f, $disabled, true);
    echo "$f: " . ($ok ? 'AÇIK' : 'KAPALI') . "\n";
}
echo "max_execution_time (web): " . ini_get('max_execution_time') . "\n";
// CLI php yolu var mı (exec açıksa):
if (function_exists('exec') && !in_array('exec', $disabled, true)) {
    @exec('which php 2>/dev/null', $o); echo "which php: " . (implode(' ', $o) ?: '(bulunamadı)') . "\n";
}
```

### 2) Kalıcı process — `heartbeat.php`
```php
<?php
// Kullanım (CLI): php heartbeat.php A 1800
//   argv[1]=instance id, argv[2]=saniye (varsayılan 1800=30dk; GÜVENLİK: süresiz değil)
$id  = preg_replace('/[^A-Za-z0-9]/', '', $argv[1] ?? 'A');
$ttl = (int)($argv[2] ?? 1800);
$log = __DIR__ . "/heartbeat_{$id}.log";
$pid = getmypid();
$t0  = time();
$w = fn($m) => file_put_contents($log, sprintf("[%s] %s id=%s pid=%d\n", date('c'), $m, $id, $pid), FILE_APPEND | LOCK_EX);
$w('START');
while (time() - $t0 < $ttl) { $w('beat'); sleep(5); }
$w('STOP');
```

### 3) Çıktı okuma ucu — `heartbeat_log.php` *(SSH varken GEREKMEZ; sadece shell'siz referans)*
```php
<?php
header('Content-Type: text/plain; charset=utf-8');
$id = preg_replace('/[^A-Za-z0-9]/', '', $_GET['id'] ?? 'A');
$log = __DIR__ . "/heartbeat_{$id}.log";
echo is_file($log) ? file_get_contents($log) : "log yok: $id";
```

### 4) Process başlatma ucu — `heartbeat_start.php` *(SSH varken GEREKMEZ; sadece shell'siz referans)*
```php
<?php
// ⚠️ GÜVENLİK: exec'i webe açar — basit token ile koru, DENEY SONRASI SİL.
if (($_GET['token'] ?? '') !== 'DENEY_GIZLI_TOKEN') { http_response_code(403); exit('forbidden'); }
$id = preg_replace('/[^A-Za-z0-9]/', '', $_GET['id'] ?? 'A');
$script = escapeshellarg(__DIR__ . '/heartbeat.php');
exec(sprintf('nohup php %s %s 1800 > /dev/null 2>&1 &', $script, escapeshellarg($id)));
echo "started: $id";
```

## 🪜 Prosedür (SSH — shell komutları)
```bash
# 0) Ortam kontrolü
php -v ; which php
php -r 'echo PHP_SAPI," ",PHP_VERSION,"\n";'
php -i | grep -i max_execution_time            # CLI genelde 0 (sınırsız) — iyi
# Logout'ta process öldürülüyor mu? (kritik)
loginctl show-user "$USER" -p KillUserProcesses -p Linger 2>/dev/null

# 1) heartbeat.php'yi sunucuya koy (intern repo dizinine), oraya cd et

# 2) Başlat — setsid ile oturumdan KOPAR (3 eşzamanlı instance)
setsid nohup php heartbeat.php A 1800 </dev/null >heartbeat_A.out 2>&1 &
setsid nohup php heartbeat.php B 1800 </dev/null >heartbeat_B.out 2>&1 &
setsid nohup php heartbeat.php C 1800 </dev/null >heartbeat_C.out 2>&1 &

# 3) PID'leri ve canlılığı gör
ps -ef | grep heartbeat.php | grep -v grep

# 4) Çıktıyı izle
tail -f heartbeat_A.log

# 5) PERSISTENCE testi (asıl soru):
#    şu anki saati not et → `exit` ile SSH'ten çık → 10–15 dk bekle →
#    geri bağlan → log çıkış aralığında büyümeye DEVAM etmiş mi?
tail -n 5 heartbeat_A.log ; ps -ef | grep heartbeat.php | grep -v grep

# 6) Temizlik
pkill -f heartbeat.php ; rm -f heartbeat_*.log heartbeat_*.out
```

### Fallback — `setsid` logout'ta yetmezse
```bash
# tmux/screen ile kalıcı oturum (varsa)
tmux new -d -s hb 'php heartbeat.php A 1800'   # tmux ls ile gör, tmux kill-session -t hb ile bitir
```
Eğer hem `setsid` hem `tmux` logout'ta ölüyorsa → **kullanıcı process'leri logout'ta öldürülüyor** → resident daemon için **process yöneticisi** (systemd service / supervisor) gerekir, ki bu **izin sorusu** (aşağı).

### Lifecycle (bonus)
- Bir **deploy** yap → process ölüyor mu? (yeniden başlatma stratejisi için.)
- **Reboot** sonrası otomatik kalkması = ayrı mesele → systemd/supervisor (izin gerek).

## ✅ Başarı Kriterleri
- **S1 Spawn:** ilk `beat` log'a düşüyor.
- **S2 Persistence:** başlatan oturum yokken log ≥10 dk büyümeye devam.
- **S3 Observability:** çıktı istendiğinde okunabiliyor.
- **S4 Concurrency:** 3 instance eşzamanlı, ayrı PID, hepsi yazıyor.
- **S5 Lifecycle:** durdurma çalışıyor; deploy'da davranış biliniyor.

## 🧭 Sonuç → Karar Eşlemesi
| Gözlem | Anlamı | Cron motoru kararı |
|---|---|---|
| S1–S4 geçer, **logout'a rağmen yaşıyor** | Kalıcı process mümkün | **Seçenek B uygulanabilir** — resident daemon |
| Çalışır ama logout/süre sonrası ölüyor (setsid + tmux de kurtarmıyor) | User process'leri öldürülüyor | B ancak **process yöneticisi** (systemd/supervisor) ile mümkün → **izin sorusu**; yoksa **Seçenek C** (harici pinger + tick endpoint) |
| tmux/setsid ile yaşıyor ama **reboot'ta** gidiyor | Yarı-kalıcı | Kısa vade B (tmux), uzun vade process yöneticisi ya da **C** |

## ⚠️ Riskler / Etik
- **Fork-bomb yok:** TTL sınırlı (süresiz değil), döngüde `sleep` var (CPU).
- **Paylaşımlı sunucu:** hafif tut, diğer intern repolarını rahatsız etme.
- **Güvenlik:** `heartbeat_start.php` exec'i webe açar → token ile koru ve **deney biter bitmez sil**.
- **Temizlik:** PID'leri not et, kill edebil; log + deney dosyalarını kaldır.

## 📌 Bulgular (2026-06-26)
- **Spawn:** ✅ `php` CLI çalışıyor; script arka planda başlatılabiliyor (`setsid nohup php heartbeat.php A …`).
- **Persistence:** ✅ **Process SSH bağlantısı kopunca KAPANMIYOR** — arka planda çalışmaya devam ediyor. (logout'ta öldürülme sorunu yok.)
- **Not (yanılgı):** `setsid … &` sonrası bash "[1]+ Done" der; bu setsid sarmalayıcısının çıkışıdır, php çocuğu yaşar — `ps -ef | grep heartbeat.php` ile doğrulandı.
- **Concurrency:** teknik engel yok (setsid ayrı oturum); çoklu instance ayrıca stres-test edilmedi, gerekirse A/B/C ile bakılır.
- **✅ KARAR: Seçenek B uygulanabilir** — cron motoru **resident daemon** olarak yazılabilir.

## ⏭️ Kalan Takip (üretim sağlamlığı)
- **Reboot sonrası** otomatik kalkma: `setsid` logout'a dayanıyor ama reboot'ta gider → **process yöneticisi** (systemd service / supervisor) gerekir = **izin sorusu**.
- **Auto-restart / monitoring:** process çökerse kim ayağa kaldıracak?
- Bunlar [[01-Cron-Motoru]] tasarımında ele alınacak; deney "B teknik olarak mümkün"ü kanıtladı, üretim yönetimi ayrı adım.

[[01-Cron-Motoru|← Cron Motoru]] · [[00-Yol-Haritasi]]
