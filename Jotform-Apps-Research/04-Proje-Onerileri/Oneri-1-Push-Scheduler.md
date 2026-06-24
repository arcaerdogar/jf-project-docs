---
tags: [jotform/apps, proje, firsat]
status: olgun
updated: 2026-06-24
---

# ⭐ Öneri 1 — Zamanlanmış & Tekrarlayan Push + Uygulama İçi Bildirim Merkezi

> [!success] ANA ÖNERİ — canlıya çıkma şansı en yüksek

## 🧩 Çözdüğü Şikayet
[[Sikayet-Push]] — Push var ama olgun değil (zamanlama, tetikleme, merkez eksik). İlgili durum: [[Apps-Mevcut-Durum-2026]].

## 📐 Kapsam
Üç dilim — her biri bağımsız değer üretir:

- **(a) Scheduler:** İleri tarihli gönderim + tekrarlama kuralı (**günlük / haftalık / aylık**).
  - Örn. "Her Cuma 16:00 timesheet hatırlatması."
- **(b) Submission-tetikli push:** Forma yeni gönderim gelince otomatik bildirim.
- **(c) Uygulama içi bildirim merkezi:** Geçmiş bildirimlerin saklandığı liste — iOS'taki **mesaj kaybını çözer**.

## 💡 Neden Bu Öneri
- Mevcut **push altyapısı üstüne kurulur** — sıfırdan başlamıyoruz.
- **Kapsam net**, sınırları belli.
- **Demosu görsel** — sunumda canlı gösterilebilir.
- **Her dilim tek başına değer üretir** → kısmi teslimat bile faydalı, canlıya çıkma şansı en yüksek.

## 🛠️ Teknik Uygunluk
- **Backend ağırlıklı** — staj için öğretici ve ölçülebilir.
- **Zamanlanmış iş kuyruğu:** BullMQ / Redis ile cron benzeri tekrarlama.
- **Net API yüzeyi:** zamanlama oluştur/listele/iptal uçları.
- **CTR metriği zaten var** — başarı ölçümü hazır.

## 📊 Skor (bkz. [[03-Firsat-Haritasi]])
| Talep | Değer | Kapsam netliği | 1 ayda canlı |
|---|---|---|---|
| Yüksek | Yüksek | **Çok net** | ✅ Yüksek |

## 🪜 Bir Aylık Dilimleme (öneri)
1. **Hafta 1:** Scheduler veri modeli + iş kuyruğu iskeleti (tek seferlik ileri tarihli gönderim).
2. **Hafta 2:** Tekrarlama kuralları (günlük/haftalık/aylık) + yönetim arayüzü.
3. **Hafta 3:** Submission-tetikli push.
4. **Hafta 4:** Uygulama içi bildirim merkezi + metrik entegrasyonu + cila.

> [!tip] Sıra
> [[05-Tavsiye-ve-Sonraki-Adimlar]]'a göre **ilk sırada bu öneri** sunulmalı.

İlgili öneriler: [[Oneri-2-Offline-Mode]] · [[Oneri-3-Portal]]
[[00-MOC|← MOC]]

#jotform/apps #proje #firsat
