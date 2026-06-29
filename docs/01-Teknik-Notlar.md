---
tags: [jotform/apps, bildirim, reference]
status: olgun
updated: 2026-06-26
---

# 🔧 Teknik Notlar — Gönderim Mekanizmaları

> [!abstract] Amaç
> Gönderim sistemini implemente ederken bilinmesi gereken teknik gerçekler. [00-Proje-Ozeti](00-Proje-Ozeti.md) için teknik ek.
> **Kapsam dışı:** offline mod. Offline veri toplama, client-side zamanlanmış bildirim (Notification Triggers / Periodic Background Sync) ve native-wrapper tartışmaları artık geçersiz; tam metin arşivde: `archive/Jotform-Apps-Research/01-Baglam/Teknik-Bildirim-Mekanizmalari.md`.

## 1. ⚠️ Push kapsam kısıtı (Haz 2026 — belirleyici)
- Push **yalnızca ana repodan** tetiklenebiliyor (intern API kendi tetikleyemiyor).
- Ana repo **kişi-bazlı push desteklemiyor** → her gönderim **abone olan herkese broadcast**.
- Sonuç: **transactional / kişi-bazlı / segmentli push kapsam dışı.** Push'a yalnızca **broadcast cron + scheduled** ekliyoruz.
- Kişi-bazlı tüm ihtiyaçlar (transactional, koşullu-hedefli, segment, kişi-bazlı durum takibi) **e-posta kanalına** taşındı (§3).

## 2. Push teslim modeli
- Akış: **ana repo → push servisi (FCM/APNs) → cihaz.** Scheduler/cron zamanını **intern API** tutar; ateşlenince **ana repoya broadcast isteği** atar (akış: [03-Gelistirme-Ortami](03-Gelistirme-Ortami.md)).
- Teslim için cihazda bağlantı gerekir; cihaz o an bağlı değilse push servisi mesajı **TTL ile kuyruğa alır**, cihaz bağlanınca teslim eder. (Zamanlama sunucuda kaçmaz; teslim bağlantıya bağlı.)
- iOS'ta web push **kurulu PWA** için destekli (iOS 16.4+).

## 3. Uygulama-içi bildirim merkezi
- Zil/rozet/banner + geçmiş listesi = OS push değil, **app UI'ı** (yerel/IndexedDB'den okur).
- Yalnızca kullanıcı uygulamayı **açtığında** görünür (proaktif dürtemez).
- **Badging API** (`setAppBadge`): uygulama ikonunda sayı rozeti (kısmi destek).
- **Süreç durum takibi** değeri buradan gelir — ama veri **kişi-bazlı** olduğundan **e-posta/transactional kayda** dayanmalı (push broadcast bu değeri taşıyamaz).

## 4. E-posta — birincil kanal, tam kapsam
- E-posta **birinci sınıf kanal**: anlık/cron/scheduled + transactional + koşullu + kişi-bazlı.
- **Avantaj:** sunucu-taraflı; teslim için cihaz bağlantısı/uygulama kurulumu gerekmez → zamanlı/koşullu/kişi-bazlı senaryolarda güvenilir.
- **Mevcut zemin:** Jotform e-posta altyapısı (autoresponder, şablon) zaten var, form tarafında tamamen özelleştirilebilir.
- **Kapatılan boşluk:** App özelinde e-posta düzenlenemiyor — autoresponder yeteneklerini app'e açmak bu projenin parçası. API'nin ne kadarı app'e açılabiliyor, haritalanmalı.
- (SMS, ileride eklenebilecek üçüncü kanal — kapsam dışı.)

## 🔗 İlgili: App ↔ Workflow
- App içi **form gönderimi**, forma bağlı bir **Workflow'u tetikler** (ortak form üzerinden). → Submission-tetikli **transactional e-posta** (kişi-bazlı) bu event'e bağlanabilir. *(Submission-tetikli push olmaz — push broadcast.)*
- Workflow durumu app'e geri yansımıyor (bu projenin kapsamı dışı; ayrı bir fikir).

İlgili: [00-Proje-Ozeti](00-Proje-Ozeti.md) · [02-Kaynaklar](02-Kaynaklar.md) · [03-Gelistirme-Ortami](03-Gelistirme-Ortami.md)
