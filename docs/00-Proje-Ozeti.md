---
tags: [jotform/apps, proje, bildirim]
status: olgun
updated: 2026-06-26
---

# 📣 Proje: Jotform Apps — Bildirim & E-posta Gönderim Sistemi

> [!success] Karar
> Birden çok aday arasından **bu proje seçildi** (Haz 2026): App Builder uygulamaları için **çok-kanallı (push + e-posta) gönderim sistemi** — zamanlanmış / tekrarlayan / koşullu gönderim + uygulama içi bildirim merkezi. Bu doküman, implementasyon ajanı için **kendi içinde yeterli** proje brifidir; derin araştırma bağlamı `archive/Jotform-Apps-Research/`'tedir (varsayılan olarak okunması gerekmez).

> [!abstract] Kapsam tek cümlede
> İki kanal **asimetrik** (Haz 2026 kısıtı): **E-posta tam kapsam** (anlık/cron/scheduled + transactional + koşullu + kişi-bazlı); **Push kısıtlı** (yalnızca **broadcast** cron/scheduled — kişi-bazlı/transactional yok, sadece ana repodan tetiklenir). Gönderilenler bir **bildirim merkezinde** saklanıp listelenir.

## 🎯 Problem (kapatılacak boşluklar)
Jotform Apps'te push **var ama olgun değil**; e-posta tarafında ise app özelinde düzenleme yok. Eksik davranış katmanı:
- **Zamanlama + tekrarlama yok** — gönderim elle, anlık.
- **Olaya dayalı (koşullu) tetikleme yok** — "submission gelince gönder" akışı yok.
- **Uygulama içi bildirim merkezi yok** — iOS'ta bildirime dokununca mesaj kayboluyor, geçmiş görünmüyor; app üzerinden **süreç durum takibi** yapılamıyor.
- **App özelinde e-posta düzenlenemiyor** — form tarafında autoresponder tamamen özelleştirilebilirken app komponentinde bu açılmıyor. *(Arşiv kanıtı: `archive/Jotform-Apps-Research/02-Bulgular/Sikayet-Product-Table.md`.)*
- **Push'ta hedef-kitle segmentasyonu yok** — gönderim ya tüm abonelere ya hiç kimseye. ⚠️ Bu bir **kalıcı kısıt** (ana repo kişi-bazlı push desteklemiyor), kapatılacak bir boşluk değil → kişi-bazlı ihtiyaçlar **e-posta** ile karşılanacak.

**Durum teyidi (Haz 2026):** Boşluk hâlâ açık; zamanlanmış push talepleri **geliştiricilere eskale**. Jotform bugün "hatırlatma"yı **zamanlanmış e-posta autoresponder** ile çözüyor — bu projede push + e-posta **tek sistemde** birleştirilecek.

## 📐 Kapsam — Üç Eksen + Kanal Asimetrisi
Sistem üç eksenin (**Kanal × Gönderim Türü × Tetikleme**) bileşimi. **Belirleyici kısıt (Haz 2026):** push ile e-posta **simetrik değil** — aşağıdaki yetenek matrisi esas alınmalı.

### ⚠️ Kanal Yetenek Matrisi
| Özellik | Push | E-posta |
|---|---|---|
| Anlık / commercial | ✅ *(zaten var, **broadcast**)* | ✅ |
| Cron (tekrarlayan) | ✅ broadcast | ✅ |
| Scheduled (ileri tarih) | ✅ broadcast | ✅ |
| **Transactional** (kişi-bazlı, olay-tetikli) | ❌ | ✅ |
| Koşullu tetikleme | ⚠️ yalnızca broadcast | ✅ tam |
| Kişi-bazlı / segment hedefleme | ❌ *(herkese gider)* | ✅ |
| Tetikleme yeri | **yalnızca ana repo** | tam kapsam |

> [!danger] Push kısıtı (kalıcı)
> Push **yalnızca ana repodan tetiklenebiliyor** ve **abone olan herkese broadcast** ediyor — kişi-bazlı gönderim yok. Dolayısıyla **transactional push kapsam dışı.** Push'a yalnızca **cron + scheduled (broadcast)** ekliyoruz. **E-posta tam kapsamla devam.**

### Eksen 1 — Kanal
- **E-posta — *tam kapsam.*** App özelinde düzenlenebilir şablon (bugün eksik) + tüm gönderim türleri + transactional + koşullu + kişi-bazlı.
- **Push — *kısıtlı.*** Broadcast cron + scheduled (+ mevcut anlık). Kişi-bazlı/transactional yok.
- **Uygulama içi bildirim merkezi** — gönderim geçmişini saklayan/listeleyen yüzey (aşağıda).

### Eksen 2 — Gönderim Türü
1. **Anlık / commercial** — *(zaten var)*.
2. **Cron** — tekrarlayan (günlük/haftalık/aylık).
3. **Scheduled** — tek seferlik ileri tarih.

*(Her üçü iki kanalda da var; push'ta yalnızca **broadcast** biçiminde.)*

### Eksen 3 — Tetikleme (gönderim/iş nasıl oluşur)
- **Manuel / admin panel** *(öncelikli yol)* — yönetici cron veya scheduled işi **doğrudan panelden** oluşturur/tetikler. **Submission'a bağlı olmak zorunda değil.** Ör. "Her Cuma 16:00 tüm abonelere broadcast push" veya "şu tarihte e-posta" — hiçbir olay gerekmez. Cron işlerinin asıl oluşturma yolu budur.
- **Koşullu / olay-tabanlı** *(ek yol)* — bir olay (ör. form doldurulması) gönderim/iş tetikler; **esas olarak e-posta** (kişi-bazlı):
  - Submission → **transactional e-posta** (anlık).
  - Submission → **scheduled e-posta** (ör. *+7 saat sonrasına*).
  - Submission → **cron e-posta serisi**.
  - *(Push'ta koşullu tetikleme yalnızca broadcast düzeyinde anlamlı — kişiye özel değil.)*

### + Bildirim Merkezi & Durum Takibi
- Gönderim geçmişinin **saklanması + listelenmesi**. iOS mesaj kaybını çözer.
- **Süreç durum takibi** (kişi-bazlı "benim durumum") artık **e-posta/transactional + merkez** üzerinden taşınır — push broadcast olduğundan bu değeri taşıyamaz.
- Bildirim merkezi gösterimi **yerel/IndexedDB tabanlı** (geçmiş app içinde tutulur) — bkz. [01-Teknik-Notlar](01-Teknik-Notlar.md).

> [!note] Zihinsel model
> Tek motor (kural + zamanlama + tetikleme), **kanal-bazlı yetenek farkıyla** fan-out eder. Zengin kişi-bazlı/transactional davranış **e-postada**; push **broadcast scheduled/cron** ile sınırlı.

> [!fail] Kapsam Dışı
> **Offline mod** (offline veri toplama, service worker kuyruğu/sync, client-side zamanlanmış bildirim, native-wrapper) **tamamen kapsam dışı**. İlgili araştırma arşivde: `archive/Jotform-Apps-Research/` (Sikayet-Offline, Oneri-2-Offline-Mode, Oneri-5-Saha-Modu). Ayrıca: per-kullanıcı portal, in-app analitik, e-ticaret paritesi de bu projenin dışında.

## 🧱 Talep Kanıtı
- Birebir kullanıcı istekleri: "Her Cuma 16:00 timesheet hatırlatması", "haftalık öğrenci planlayıcı hatırlatması", "submission gelince otomatik push", "kime göndereceğimi seçebilmeli miyim?".
- Dahili: zamanlanmış push talepleri eskale; en az 1 L3 ticket bildirimlerle ilgili.
- Sektörel yankı: etkinlik (oturum hatırlatma), perakende (kampanya/segment), nonprofit (acil/kampanya), sağlık (randevu — *HIPAA içerik kısıtı*). Detay sektör analizi arşivde.

## 🛠️ Teknik Çerçeve (üst düzey — detaylar sonra)
- **Tek gönderim motoru, çok kanal.** Gönderim kuralı (tür + tetikleme + içerik) kanaldan bağımsız tanımlanır; motor push ve e-postaya fan-out eder.
- **Backend ağırlıklı.** Zamanlanmış iş kuyruğu (ör. BullMQ/Redis benzeri) + cron kuralı + scheduled (tek seferlik) iş.
- **Koşullu tetikleme:** submission-event → kural değerlendirme → gönderim türü (anlık/scheduled/cron) tetikleme. Event akışı mevcut webhook/event altyapısına bağlanacak.
- Net API yüzeyi: kural **oluştur / listele / iptal**; tür (anlık/cron/scheduled); tetikleyici (manuel/koşullu); kanal seçimi (push/e-posta).
- **E-posta tarafı:** app özelinde **düzenlenebilir şablon** (form autoresponder yetenekleriyle parite). E-posta sunucu-taraflı → push'un teslim/offline kısıtları yok; koşullu/zamanlı senaryolarda güvenilir kanal.
- **CTR metriği zaten var** (push) → başarı ölçümü hazır; e-posta için açılma/teslim metrikleri eklenebilir.
- Bildirim merkezi: frontend + yerel depolama (IndexedDB), gönderim geçmişini saklar/listeler.
- ⚠️ Push teslimi: scheduler/cron zamanı **intern API'de** tutulur, ateşlenince **ana repoya broadcast isteği** atılır. Teslim cihaz bağlantısına bağlı (bağlı değilse push servisi TTL ile kuyruğa alır). Ayrıntı: [01-Teknik-Notlar](01-Teknik-Notlar.md).

## 🪜 Önerilen Dilimleme (taslak — implementasyon ajanı netleştirecek)
1. **Çekirdek motor:** Birleşik gönderim kuralı veri modeli + iş kuyruğu; **scheduled** (tek seferlik) ile başla.
2. **Cron:** tekrarlama kuralları (günlük/haftalık/aylık) + yönetim arayüzü.
3. **Push entegrasyonu:** ana repoya **broadcast** tetikleme (scheduled/cron). *(Kişi-bazlı/transactional yok.)*
4. **E-posta kanalı:** app özelinde düzenlenebilir şablon + tam kapsam fan-out.
5. **Koşullu + transactional (e-posta):** submission-event → e-posta (anlık/scheduled/cron, kişi-bazlı).
6. **Bildirim merkezi:** gönderim geçmişi saklama/listeleme + süreç durum takibi + metrikler.
7. *(faz 2)* E-posta segmentasyonu.

> [!warning] Kapsam notu
> Push kısıtı kapsamı **bir miktar düşürdü** (transactional/kişi-bazlı push yok) ama e-posta tarafı **tam kapsam** olduğundan toplam iş hâlâ büyük (iki kanal, 3 tür, koşullu/transactional e-posta, merkez). Bir aylık MVP'ye sığması için implementasyon ajanıyla **kesin MVP sınırı** çizilmeli — muhtemel MVP: tek motor + scheduled/cron (push broadcast + e-posta); transactional/koşullu e-posta ve merkez hızlı takip.

## ❓ İmplementasyon Öncesi Açık Sorular
- **Kural modeli:** Tek birleşik kural şeması, ama **kanal-bazlı yetenek farkını** taşımalı (push = broadcast scheduled/cron; e-posta = tam). Geçersiz kombinasyon (ör. transactional push) UI/şemada engellenmeli.
- **Push tetikleme:** Scheduled/cron ateşlenince ana repoya broadcast isteği nasıl atılacak? (intern API → ana repo doğrudan mı, yoksa frontend köprü mü — bkz. [03-Gelistirme-Ortami](03-Gelistirme-Ortami.md).)
- **E-posta editörü:** Form autoresponder editörü app'te yeniden mi kullanılacak, yoksa app-native mi? Mevcut autoresponder API'sinin ne kadarı app'e açılabiliyor? E-posta gönderimi/kişi-bazlı hedefleme intern API'den mi, ana repodan mı?
- **Koşullu tetikleme (e-posta):** submission-event hangi mevcut webhook/event altyapısına bağlanacak? Koşul tanımı (hangi form, hangi alan) nasıl modellenecek?
- **Scheduled gecikme:** "+7 saat" göreli zamanlama submission anına göre mi? Zaman dilimi yönetimi?
- **Cron granülerliği:** saat/dakika, zaman dilimi, bitiş tarihi/iterasyon limiti?
- **E-posta segmentasyonu** MVP'de mi, faz 2'de mi? *(Push segmentasyonu kalıcı olarak imkânsız — soru yalnızca e-posta için.)*
- **Bildirim merkezi:** push (broadcast) geçmişi + e-posta/transactional geçmişi + süreç durumu nasıl birleşecek? Saklama nerede (yerel/sunucu/ikisi)?

## 🏗️ Mimari Kısıt (kritik)
İki backend reposu var: **ana Jotform reposu** (istek atılır, **düzenlenemez**) ve **intern API** (düzenlenebilir ama **kısıtlı**). Tüm yeni kod intern API'de; ana repo yalnızca istekle kullanılır. Varsayılan workaround = frontend köprü; tercih = doğrudan intern→ana. Tam detay + akış diyagramları: **[03-Gelistirme-Ortami](03-Gelistirme-Ortami.md)**.

## 🗂️ Repo Yapısı
- `docs/` — bu proje brifi + teknik notlar + **geliştirme ortamı/mimari** + kaynaklar (odaklı çalışma seti).
- `docs/Gelistirme-Asamalari/` — **yol haritası** (aşama dosyaları; 01 Cron Motoru = aktif odak). Giriş: [Gelistirme-Asamalari/00-Yol-Haritasi](Gelistirme-Asamalari/00-Yol-Haritasi.md).
- `archive/Jotform-Apps-Research/` — projeyi seçmeye götüren **tam araştırma vault'u** (37 not: diğer adaylar, sektör analizi, doğrulamalar). Implementasyon için gerekli değil; yalnızca derin bağlam için.
- İmplementasyon kodu buraya eklenecek (sonraki ajan).

İlgili: [01-Teknik-Notlar](01-Teknik-Notlar.md) · [02-Kaynaklar](02-Kaynaklar.md) · [03-Gelistirme-Ortami](03-Gelistirme-Ortami.md)
