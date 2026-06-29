---
tags: [jotform/apps, bildirim, gelistirme]
status: taslak
updated: 2026-06-26
---

# 🔔 Aşama 03 — Push Entegrasyonu (Broadcast)

> [!info] Durum: ⚪ Planlandı · Bağımlılık: [[01-Cron-Motoru]], [[02-Gonderim-Motoru-ve-Kural-Modeli]]

## 🎯 Amaç
Zamanlanmış/cron iş tetiklenince **ana repoya broadcast push isteği** atmak.

## ⚠️ Kısıt (sabit)
Push **yalnızca ana repodan** tetiklenir ve **abone olan herkese broadcast** — kişi-bazlı/transactional **yok** (bkz. [01-Teknik-Notlar](../01-Teknik-Notlar.md) §1). Bu aşama yalnızca **broadcast** kapsar.

## 📐 Kapsam
- Intern API → ana repo broadcast çağrısı (akış: [03-Gelistirme-Ortami](../03-Gelistirme-Ortami.md) — doğrudan mı, frontend köprü mü?).
- Gönderim sonucu/teslim bilgisini geri alma (metrik/merkez için).

## ❓ Açık Sorular
- Ana reponun broadcast endpoint'i hangisi, auth nasıl?
- Intern API ana repoya **doğrudan** ulaşabiliyor mu (yoksa frontend köprü)?
- Teslim/CTR verisi geri nasıl alınıyor?

[[00-Yol-Haritasi|← Yol Haritası]]
