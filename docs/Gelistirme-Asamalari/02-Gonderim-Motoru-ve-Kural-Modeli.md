---
tags: [jotform/apps, bildirim, gelistirme]
status: taslak
updated: 2026-06-26
---

# 🧠 Aşama 02 — Gönderim Motoru & Birleşik Kural Modeli

> [!info] Durum: ⚪ Planlandı · Bağımlılık: [[01-Cron-Motoru]] (iş deposu) · Çekirdeğin diğer yarısı

## 🎯 Amaç
Tek birleşik **kural şeması** (kanal × tür × tetikleme × içerik) + **dispatch** mantığı: bir iş tetiklendiğinde doğru kanala/alıcıya yollar.

## 📐 Kapsam
- **Kural şeması:** kanal (push/e-posta), tür (anlık/cron/scheduled), tetikleme (manuel/koşullu), içerik/şablon ref, hedef.
- **Kanal yetenek farkını taşı:** push = broadcast scheduled/cron; e-posta = tam. Geçersiz kombinasyon (ör. transactional push) **şema/UI seviyesinde engellenmeli** (bkz. [00-Proje-Ozeti](../00-Proje-Ozeti.md) yetenek matrisi).
- **Dispatch:** kanal-bazlı fan-out (→ [[03-Push-Entegrasyonu]] / [[04-Eposta-Kanali-ve-Sablon]]).

## ❓ Açık Sorular
- Kural ve iş (job) ayrı tablolar mı, tek model mi?
- Geçersiz kombinasyon engelleme nerede (DB constraint / API validation / UI)?
- Çok-kanallı tek kural (aynı anda push+e-posta) nasıl temsil edilir?

[[00-Yol-Haritasi|← Yol Haritası]]
