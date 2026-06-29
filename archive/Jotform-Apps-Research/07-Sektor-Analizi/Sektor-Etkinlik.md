---
tags: [jotform/apps, sektor, firsat]
status: olgun
updated: 2026-06-24
---

# 🎪 Sektör: Etkinlik Yönetimi

> [!info] Konum: Güçlü şablon kapsamı (konferans, düğün, fuar, kayıt). **Push olgunluğu boşluğunun en temiz eşleşmesi.**

## Kullanım Kanıtı
Event Planner Apps, Event Registration App, Enterprise Event App, Wedding Invitation App; use-case sayfaları (Event Registration, Wedding Planning).

## Tipik Senaryolar
Kayıt + ücret toplama, etkinlik gündemi/program listeleme, konuşmacı profilleri, kaynak linkleri (tek profesyonel app'te); düğün: checklist, geri sayım, gider, davetli listesi.

## İhtiyaç → Boşluk Eşlemesi
- **PUSH (zamanlama — en kritik):** "Oturum 30 dk sonra başlıyor", "Yarın kayıt açılıyor" gibi **zamanlanmış/tetikli** hatırlatmalar etkinlik yönetiminin özü. Mevcut push yalnızca manuel/anlık; Enterprise Event App sayfasında bildirim özelliği hiç anılmıyor. → [[Sikayet-Push]] / [[Oneri-1-Push-Scheduler]].
- **PORTAL:** Katılımcının "benim biletim / benim oturumlarım" görünümü zayıf. → [[Sikayet-Portal]].
- **ANALİTİK:** Organizatöre kayıt sayısı grafiği (in-app) yok. → [[Sikayet-Analitik]].

## En Çok Yankı
1. **Zamanlanmış/tetikli Push** (etkinlik takvimi belli → doğal ve yüksek değerli) · 2. Katılımcı portalı.

> [!success] Pilot adayı
> HIPAA gibi kısıtı olmadığı için [[Oneri-1-Push-Scheduler]]'ın **en temiz demo/pilot sektörü** burası olabilir.

[[00-Sektor-MOC]] · #jotform/apps #sektor #firsat
