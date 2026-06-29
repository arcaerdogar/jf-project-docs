---
tags: [jotform/apps, bildirim, gelistirme]
status: taslak
updated: 2026-06-26
---

# 📥 Aşama 06 — Bildirim Merkezi & Durum Takibi

> [!info] Durum: ⚪ Planlandı · Bağımlılık: gönderim mevcut ([[03-Push-Entegrasyonu]] / [[04-Eposta-Kanali-ve-Sablon]])

## 🎯 Amaç
Gönderilen mesajların **saklanması + listelenmesi** (app içi merkez). iOS mesaj kaybını çözer; app üzerinden **süreç durum takibi** eksiğini kapatır.

## 📐 Kapsam
- App içi geçmiş listesi (zil/rozet/banner) — yerel/IndexedDB gösterim.
- **Durum takibi:** kişi-bazlı olduğundan **e-posta/transactional kayda** dayanır (push broadcast bu değeri taşımaz — [01-Teknik-Notlar](../01-Teknik-Notlar.md) §3).

## ❓ Açık Sorular
- Merkez verisi: push (broadcast) geçmişi + e-posta/transactional geçmişi nasıl **birleşir**?
- Saklama nerede: yerel (IndexedDB) / sunucu (intern API) / ikisi?
- Kişi-bazlı durum için kullanıcı kimliği app'te nasıl çözülüyor?

[[00-Yol-Haritasi|← Yol Haritası]]
