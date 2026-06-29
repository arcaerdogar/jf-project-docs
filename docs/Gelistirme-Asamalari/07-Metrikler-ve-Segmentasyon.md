---
tags: [jotform/apps, bildirim, gelistirme]
status: taslak
updated: 2026-06-26
---

# 📊 Aşama 07 — Metrikler & Segmentasyon (Faz 2)

> [!info] Durum: ⚪ Planlandı · Bağımlılık: [[03-Push-Entegrasyonu]], [[04-Eposta-Kanali-ve-Sablon]]

## 🎯 Amaç
Gönderim başarısını ölçmek + (faz 2) e-posta hedeflemeyi inceltmek.

## 📐 Kapsam
- **Metrikler:** push CTR **zaten var**; e-posta için teslim/açılma metrikleri eklenir.
- **Segmentasyon (faz 2, yalnızca e-posta):** etiket/segment bazlı hedefleme.
  - ⚠️ Push segmentasyonu **kalıcı olarak imkânsız** (ana repo broadcast) — bu kapsam yalnızca e-posta.

## ❓ Açık Sorular
- E-posta açılma/teslim metriği hangi kaynaktan?
- Segment tanımı (etiket, form alanı, geçmiş davranış?) nasıl modellenir?
- Metrikler bildirim merkezine mi, ayrı panele mi?

[[00-Yol-Haritasi|← Yol Haritası]]
