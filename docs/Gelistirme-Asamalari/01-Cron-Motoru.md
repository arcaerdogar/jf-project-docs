---
tags: [jotform/apps, bildirim, gelistirme]
status: aktif
updated: 2026-06-26
---

# ⏱️ Aşama 01 — Cron / Zamanlama Motoru

> [!info] Durum: 🔵 Aktif odak · Bağımlılık: yok (çekirdek)
> Tüm zamanlı/tekrarlayan davranışın temeli. **scheduled** (tek seferlik) + **cron** (tekrarlayan) işleri vadesi gelince tetikler.

## 🎯 Amaç
"Vadesi gelen gönderim işlerini bul ve tetikle" mekanizması. Kanal-bağımsız: tetiklenen iş, dispatch'e (→ [[02-Gonderim-Motoru-ve-Kural-Modeli]]) devredilir; o da push (broadcast) veya e-postaya yollar.

> [!note] İş nasıl oluşur (2 kaynak)
> 1. **Admin panel (öncelikli):** cron/scheduled iş doğrudan panelden oluşturulur — **submission gerekmez** (ör. "Her Cuma 16:00 broadcast"). 2. **Koşullu (ek):** bir olay (submission) iş oluşturur ([[05-Kosullu-Tetikleme]]). Motor her iki kaynaktan gelen işi **aynı iş deposunda** işler — kaynak, çalıştırma mantığını değiştirmez.

## ❗ Neden ayrı bir motor (OS cron değil)
- Tüm intern repoları **aynı sunucuda ve container'sız** duruyor → işletim sistemi cron'u ile uğraşmak **şu an pratik değil/imkânsız**.
- Bu yüzden zamanlamayı **uygulama seviyesinde** kendi motorumuzla yöneteceğiz.

## 🏗️ Çalıştırma Seçenekleri
Tick (saat darbesi) kaynağı nerede koşacak? Üç seçenek:

| Seçenek | Artı | Eksi / koşul |
|---|---|---|
| **A. Ayrı sunucuda servis** | İzole; **dil serbest** (PHP dışı mümkün); temiz | Infra/izin tahsisi gerek; ağ/auth köprüsü |
| **B. Intern sunucuda kalıcı process (daemon)** | Aynı sunucu, basit erişim | **İzin gerek**; container yok → process'i canlı tutma/restart sorunu; dil muhtemelen mevcut runtime'larla sınırlı |
| **C. Harici pinger + "tick" endpoint** ⭐ | Kalıcı process gerekmez; **PHP/intern API içinde kalır**; en düşük friction | Harici zamanlayıcı (başka sunucu crontab'ı / cron-job.org / uptime monitor) + endpoint auth gerek; dakika hassasiyeti pinger'a bağlı |

> [!success] KARAR (2026-06-26): **Seçenek B** — deney 01a ile doğrulandı
> [[01a-Deney-Sunucu-Process]]: `setsid nohup php …` ile başlatılan process **SSH kopunca ölmüyor**, arka planda yaşıyor. Yani cron motoru intern sunucuda **resident daemon** olarak yazılabilir. (C, fallback olarak duruyor.)
> **Kalan:** reboot sonrası otomatik kalkma + auto-restart için **process yöneticisi** (systemd/supervisor) gerekir = izin sorusu (aşağı).

## 🌐 Dil Kararı
- **External servis** (Seçenek A) ise PHP dışı bir dil mümkün — ama **izin olup olmadığı öğrenilmeli**.
- **Intern API içinde** (Seçenek C) ise PHP'de kalınır.
- Karar, çalıştırma seçeneğine ve izne bağlı.

## 🔒 Çözülecek İzinler / Sorular (BLOKER — önce netleştir)
- [x] Intern sunucuda **kalıcı process** kaldırabiliyor muyuz? (Seçenek B) → ✅ **EVET** ([[01a-Deney-Sunucu-Process]]: SSH kopunca yaşıyor)
- [ ] **Reboot sonrası** otomatik kalkma / auto-restart için **process yöneticisi** (systemd service / supervisor) izni var mı?
- [ ] **Ayrı sunucu/servis** tahsis edilebiliyor mu? (Seçenek A)
- [ ] **PHP dışı runtime**'a izin var mı? (external servis ise)
- [ ] Harici bir pinger'ın intern API ucuna erişimi (auth/güvenlik) nasıl sağlanır? (Seçenek C)
- [ ] Tick sıklığı ne olmalı (dakikalık yeterli mi)?

## 🧩 Tasarım İlkesi — Tick'i çekirdekten ayır
İş/zamanlama deposu **intern API DB'sinde** yaşar. Çekirdek mantık = **"vadesi gelen işleri bul ve işle"** (saf fonksiyon). Tick kaynağı (A/B/C) bunu yalnızca *çağırır*. Böylece altyapı kararı çekirdeği bağlamaz; seçenekler arası geçiş kolay.

## 🧱 Tasarım Kararları (kesinleşti — Haz 2026)
**Model: B1 (tembel üretim) + sabit tampon.** İki tablo: **kural** (iş tanımı = üretici + şablon) ve **job** (somut occurrence).

- **Reconciler + tampon:** Her tick'te, her aktif cron kuralı için **en az 3** (gerekirse 4-5) gelecek **işlenmemiş** job satırı tutulur; eksikse üretilir. Üretimi tetiklemeden ayırır, gecikmeye marj verir.
- **Job kendine yeter (snapshot):** job satırı dispatch için yeterli bilgiyi taşır → kanal + içerik + hedef zaman (UTC) + `işlendi`. Dispatcher **her zaman job okur**; standalone ve kural-üretimi job aynı görünür → tek tip dispatch yolu.
- **`rule_id` nullable + ON DELETE CASCADE:** NULL = **standalone** job (tek-sefer scheduled / koşullu üretilmiş); dolu = kurala bağlı, kural silinince **cascade**.
- **Kural düzenlenince:** o kurala bağlı **işlenmemiş** job'lar **silinip yeniden üretilir** (snapshot güncel kalsın).
- **Instant motora GİRMEZ:** anında ortak **dispatcher**'dan gönderilir (UX; ~yarım dk gecikmeyi önler). Ortak dispatcher hem instant hem motor tarafından çağrılır; **log da orada** yazılır.
- **Zaman:** UTC uçtan uca; motor içi UTC'ye sabit; en küçük birim **dakika**.

## ⚙️ Güvenilirlik
- **Dispatch sorgusu (asıl garanti):** `aktif AND scheduled_at <= now() AND işlenmemiş` → motor geç kalsa/düşse de kaçanı **yakalar** (düşürmez). At → `işlendi=true`.
- **İdempotency:** tick örtüşmesine karşı satır claim/kilit **veya** `(rule_id, scheduled_at)` unique.
- **Tampon:** üretim gecikmesine marj (yukarı).
- **Hata/retry:** dispatch başarısızsa yeniden deneme politikası (tanımlanacak).
- *(Opsiyonel)* **Bayatlama penceresi:** çok geç kalmış (ör. >1 saat) işi atma — sonra bakılır.

## ❓ Kalan Açık Sorular
- Cron ifade formatı: standart 5-alanlı cron mu, yapısal alanlar mı? (en küçük birim dakika.)
- İdempotency: satır kilidi mi, `(rule_id, scheduled_at)` unique mi?
- Retry politikası detayı.
- Tablo DDL'leri → [[02-Gonderim-Motoru-ve-Kural-Modeli]]'de netleştirilecek.

[[00-Yol-Haritasi|← Yol Haritası]] · Sonraki: [[02-Gonderim-Motoru-ve-Kural-Modeli]]
