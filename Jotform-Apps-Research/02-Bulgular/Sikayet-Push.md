---
tags: [jotform/apps, sikayet, firsat]
status: olgun
updated: 2026-06-24
---

# 🔴 Şikayet: Push Bildirimleri Olgun Değil

> [!danger] Öncelik: Yüksek değer / **en net kapsam**

## Problem
Push bildirimleri var (bkz. [[Apps-Mevcut-Durum-2026]]) **ama olgun değil.** Altyapı kurulu — izin modalı, gönderim geçmişi, CTR metriği mevcut — fakat üzerine inşa edilmesi gereken davranış katmanı eksik.

## Forumdaki Somut, Tekrar Eden İstekler

### 1. ⏰ Zamanlama + tekrarlama yok
Kullanıcılar ileri tarihli ve tekrar eden bildirim istiyor:
- "Her **Cuma 16:00** timesheet hatırlatması"
- "**Haftalık** öğrenci planlayıcı hatırlatması"
- Bugün yalnızca **anlık/manuel** gönderim mümkün.

### 2. ⚡ Olaya dayalı tetikleme yok
- "Forma **submission gelince otomatik push**" gibi tetikleyici akış yok.
- Her bildirim elle gönderiliyor.

### 3. 📭 Uygulama içi bildirim merkezi yok
- iOS'ta bildirime dokununca **mesaj kayboluyor**, geçmiş görünmüyor.
- Kullanıcı geçmiş bildirimleri uygulama içinde göremiyor.

### 4. 📱 Mobilden gönderim akışı zayıf
- Mobil cihazdan kolay bildirim gönderme deneyimi yetersiz.

## Değerlendirme
| Boyut | Durum |
|---|---|
| Talep | Yüksek |
| Değer | Yüksek |
| Kapsam netliği | **Çok net** |
| 1 ayda canlı | ✅ Yüksek |

> [!success] Neden Bu En İyi Aday
> Altyapı **zaten var** — sıfırdan başlamıyoruz. CTR metriği hazır, API yüzeyi net, her özellik dilimi (scheduler / tetikleme / merkez) **tek başına değer üretiyor** ve demosu görsel.

> [!note] Bağlantı
> Bu şikayet → [[Oneri-1-Push-Scheduler]] (⭐ ana öneri) ile çözülüyor.

[[03-Firsat-Haritasi]] · [[00-MOC|← MOC]]

#jotform/apps #sikayet #firsat
