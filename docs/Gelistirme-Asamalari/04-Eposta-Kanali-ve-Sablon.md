---
tags: [jotform/apps, bildirim, gelistirme]
status: taslak
updated: 2026-06-26
---

# ✉️ Aşama 04 — E-posta Kanalı & Şablon Editörü

> [!info] Durum: ⚪ Planlandı · Bağımlılık: [[02-Gonderim-Motoru-ve-Kural-Modeli]]
> E-posta = **tam kapsam** kanal (anlık/cron/scheduled + transactional + koşullu + kişi-bazlı).

## 🎯 Amaç
App özelinde **düzenlenebilir e-posta şablonu** + gönderim. Bugün eksik olan "app'te e-posta düzenleme" boşluğunu kapatır.

## 📐 Kapsam
- App-native şablon editörü (form autoresponder yetenekleriyle parite).
- Kişi-bazlı gönderim + dinamik alan gömme (form alanları).
- Tüm gönderim türleriyle çalışır (motor üzerinden).

## ❓ Açık Sorular
- Mevcut autoresponder **API'sinin ne kadarı app'e açılabiliyor**? (haritalanmalı)
- E-posta gönderimi/kişi-bazlı hedefleme **intern API'den mi, ana repodan mı**?
- Editör: form editörünü yeniden mi kullanır, app-native mi?

[[00-Yol-Haritasi|← Yol Haritası]]
