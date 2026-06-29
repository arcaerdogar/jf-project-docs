---
tags: [jotform/apps, baglam, reference]
status: olgun
updated: 2026-06-24
---

# 🔧 Teknik Not — PWA'da Bildirim Mekanizmaları

> [!abstract] Amaç
> "Push dışında bildirim tetiklenebilir mi?" sorusunun dürüst cevabı. [[Oneri-1-Push-Scheduler]], [[Oneri-5-Saha-Modu]] ve [[Sikayet-Push]] için teknik referans.

## İki Kategori
Bildirimi ikiye ayırmak şart: **(1) proaktif/OS-seviyesi** (uygulama kapalıyken kullanıcıyı dürtmek) vs **(2) uygulama-içi** (uygulama açıkken göstermek).

## 1. Proaktif (uygulama kapalı) — pratikte push gerekir
| Mekanizma | Durum |
|---|---|
| **Web Push** (sunucu-tetikli) | ✅ Güvenilir yol. iOS'ta da **kurulu PWA** için destekleniyor (iOS 16.4+). Teslim için bağlantı gerekir; offline'da push servisi TTL ile kuyruğa alır, online olunca iner. |
| **Notification Triggers API** (`TimestampTrigger`) | ❌ Chromium denemesi, stabile geçmedi; **iOS yok**. Güvenilmez. |
| **Periodic Background Sync** | ❌ Sadece Chromium + kurulu PWA, **throttle'lı** (kesin saat veremez), **iOS yok**. |
| **`showNotification()` doğrudan** | ⚠️ Yalnızca SW/sayfa çalışırken; geleceğe zamanlanamaz. |

→ **Uygulama kapalıyken kesin saatte dürtmek için saf-istemci yolu yok.** Push (veya alternatif kanal) gerekir.

## 2. Uygulama-içi (uygulama açık) — %100 offline çalışır
- **Uygulama içi bildirim merkezi / zil / rozet / banner** = OS push değil, sadece uygulama UI'ı (IndexedDB'den okur).
- Push hiç olmasa bile çalışır; cross-platform; **offline-güvenli**.
- Kısıt: yalnızca kullanıcı uygulamayı **açtığında** görünür (proaktif dürtemez).
- Zaten talep: iOS'ta bildirim dokununca kaybolması → bkz. [[Sikayet-Push]] madde 3.
- İlgili: **Badging API** (`setAppBadge`) ile uygulama ikonunda sayı rozeti — kısmi destek.

## 3. Alternatif Kanal — e-posta / SMS
- Zamanlanmış hatırlatmayı push yerine **e-posta/SMS** ile yolla.
- Jotform'un **altyapısı zaten var** (autoresponder, SMS).
- Sunucu scheduler → e-posta/SMS, PWA push sınırlarını tamamen atlar; uygulama kurulu olmasa bile çalışır.

## ❌ Değerlendirilip Elenen: "Ekstra/yerel bildirim sunucusu"
> [!question] Soru: "Aynı makinede ekstra bir notification server çalıştırsak?"
> Kısıt, sunucunun *zamanlama* yeteneği değil — **son hop**: bildirimi offline cihazın ekranına düşürmek. Ekstra sunucu çoğu okumada yanlış katmana dokunuyor.

| Okuma | Sonuç |
|---|---|
| **Backend yanında ekstra sunucu** | Bu zaten scheduler worker'ı (Oneri-1). Kaç sunucu olsa da push yine push servisine gider, cihaz **online olmadıkça inemez** → offline fiziği değişmez. |
| **Son kullanıcı cihazında ekstra sunucu** | ❌ PWA tarayıcı sandbox'ında; telefonda localhost daemon **başlatılamaz** (iOS yasaklar). Cihazdaki tek yakın şey SW — o da sürekli süreç değil, kapalıyken geleceğe bildirim fırlatamaz. |

**Gerçekten offline zamanlanmış yerel bildirim = native/wrapper** (Capacitor; iOS `UNUserNotificationCenter`, Android `AlarmManager`). Çalışır, ama **native paket = App Store/Play** demek → Jotform'un bilinçli PWA tercihiyle çelişir ([[Apps-Mevcut-Durum-2026]] / [[Kapsam-Disi]]). Yani **ürün stratejisi kararı**, staj kapsamının üstünde.

**İstisna:** kiosk / depo tableti / prize takılı **adanmış cihaz** → native helper veya Electron sarmalayıcı yerel zamanlayıcı çalıştırabilir. Ama bu "saha çalışanı telefonu" personasından farklı.

## 🔁 İlgili: Background Sync (offline'ın doğru aracı)
- **One-off Background Sync:** bağlantı geri gelince offline kuyruğunu (form gönderimleri) sunucuya boşaltmak için. Zaman-bazlı bildirim için değil → [[Oneri-2-Offline-Mode]] / [[Sikayet-Offline]].

## 🧩 Çıkarım (birleşik fikre etkisi)
[[Oneri-5-Saha-Modu]]'nun **offline-güvenli yarısı = uygulama içi bildirim merkezi.**
- Push (sunucu) → proaktif dürtme, bağlantı gelince iner.
- Uygulama içi merkez (yerel) → offline'ken bile uygulama açıldığında kaçırılanlar görünür.
- İkisi birlikte → "offline olsa bile bildirim iletilir" hissinin **gerçekten buildable** hâli.

[[00-MOC|← MOC]] · [[Oneri-1-Push-Scheduler]] · [[Oneri-5-Saha-Modu]]

#jotform/apps
