---
tags: [jotform/apps, bildirim, gelistirme]
status: taslak
updated: 2026-06-26
---

# ⚡ Aşama 05 — Koşullu / Transactional Tetikleme

> [!info] Durum: ⚪ Planlandı · Bağımlılık: [[02-Gonderim-Motoru-ve-Kural-Modeli]], [[04-Eposta-Kanali-ve-Sablon]]
> **E-posta odaklı** (kişi-bazlı olduğundan); push'ta yalnızca broadcast düzeyinde anlamlı.

> [!note] Bu yalnızca **ek** bir tetikleme kaynağı
> Cron ve scheduled işler **öncelikle admin panelinden doğrudan** oluşturulur (submission gerekmez — [[01-Cron-Motoru]] / [00-Proje-Ozeti](../00-Proje-Ozeti.md) Eksen 3). Bu aşama, o işlerin **bir de olaya bağlı** (submission) oluşturulabilmesini ekler — zorunlu değil, opsiyonel bir kaynak.

## 🎯 Amaç
Bir olay (ör. **form doldurulması**) gönderimi tetikler. Üç türle bestelenir:
- Submission → **transactional e-posta** (anlık)
- Submission → **scheduled e-posta** (ör. +7 saat)
- Submission → **cron e-posta serisi**

## 📐 Kapsam
- Submission-event'e abone olma (mevcut webhook/event altyapısı).
- Koşul tanımı (hangi form, hangi alan değeri) modeli.
- Göreli zamanlama (submission anına +N saat) → [[01-Cron-Motoru]] iş oluşturma.

## ❓ Açık Sorular
- Submission-event hangi mevcut altyapıya bağlanacak (webhook?)
- Koşul ifadesi nasıl modellenecek (basit alan-eşitliği mi, daha zengin mi)?
- Göreli zaman + zaman dilimi hesabı.

[[00-Yol-Haritasi|← Yol Haritası]]
