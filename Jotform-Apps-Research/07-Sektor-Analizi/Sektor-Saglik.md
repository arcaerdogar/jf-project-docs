---
tags: [jotform/apps, sektor, firsat]
status: olgun
updated: 2026-06-24
---

# 🏥 Sektör: Sağlık

> [!warning] Konum: Güçlü kullanım (HIPAA/Health App), ama **HIPAA/PHI projeyi karmaşıklaştıran bir kısıt**.

## Kullanım Kanıtı
- Jotform Health App (mobilde hassas tıbbi veri), HIPAA sayfaları, Enterprise Healthcare.
- Terapi/randevu: therapy software, medical scheduling, HIPAA Appointment Reminder şablonu.
- Bağımsız teyit: HIPAA Journal.

## Tipik Senaryolar
Hasta intake/kayıt, onam (consent) formları, randevu talebi, kopay/fatura tahsilatı, tıbbi kayıt yönetimi, hasta geri bildirimi.

## İhtiyaç → Boşluk Eşlemesi
- **PUSH (en güçlü, ama dikkat):** Randevu hatırlatma → **no-show azaltma** sağlığın bir numaralı ihtiyacı. ⚠️ Jotform bunu bugün **zamanlanmış e-posta autoresponder** ile çözüyor — zamanlanmış push ile değil (bkz. [[Sektorden-Dogan-Fikirler]] kanal-kayması içgörüsü). HIPAA/PHI nedeniyle bildirim içeriği kısıtlı (sadece "randevunuz var" gibi). → [[Oneri-1-Push-Scheduler]].
- **PORTAL:** Hasta portalı (kendi randevuları, onam, sonuçları) — "patient portal" anılıyor ama gerçek kimlik doğrulamalı portal Apps'te yok. → [[Sikayet-Portal]].
- **OFFLINE:** Ev ziyareti / saha sağlığı — gerçek ama yine Mobile Forms'ta, App Builder'da değil. → [[Sikayet-Offline]].
- **WORKFLOW:** Sevk/onam onay durumunun hastaya yansıması. → [[Sikayet-Workflow]].

## En Çok Yankı
1. **Zamanlı/tekrarlayan Push** (randevu → no-show) — ama HIPAA komplikasyonunu hesaba kat · 2. **Portal** (hasta).

> [!danger] Risk notu
> Sağlık en güçlü push hikâyesini veriyor ama HIPAA, demo/pilot'u yavaşlatabilir. Sunumda "ilk pilot sektör" olarak HIPAA'sız bir sektör (etkinlik/eğitim) seçmek daha güvenli.

[[00-Sektor-MOC]] · #jotform/apps #sektor #firsat
