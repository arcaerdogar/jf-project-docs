---
tags: [jotform/apps, bildirim, gelistirme]
status: aktif
updated: 2026-06-26
---

# 🗺️ Geliştirme Yol Haritası

> [!abstract] Amaç
> Bildirim & e-posta gönderim sisteminin geliştirme aşamaları. Her aşama ayrı dosyada (scope, bağımlılık, açık sorular, durum). Proje kapsamı: [00-Proje-Ozeti](../00-Proje-Ozeti.md) · Mimari kısıt: [03-Gelistirme-Ortami](../03-Gelistirme-Ortami.md).

## 📋 Aşamalar ve Durum

| # | Aşama | Bağımlılık | Durum |
|---|---|---|---|
| 01 | [[01-Cron-Motoru]] — zamanlama/cron motoru | — | 🔵 **Aktif odak** |
| 01a | [[01a-Deney-Sunucu-Process]] — sunucuda kalıcı process testi | — | ✅ **Tamam** (Seçenek B viable) |
| 02 | [[02-Gonderim-Motoru-ve-Kural-Modeli]] — birleşik kural + dispatch | 01 (iş deposu) | ⚪ Planlandı |
| 03 | [[03-Push-Entegrasyonu]] — ana repoya broadcast | 01, 02 | ⚪ Planlandı |
| 04 | [[04-Eposta-Kanali-ve-Sablon]] — app-editable e-posta | 02 | ⚪ Planlandı |
| 05 | [[05-Kosullu-Tetikleme]] — submission-event → e-posta | 02, 04 | ⚪ Planlandı |
| 06 | [[06-Bildirim-Merkezi]] — geçmiş + durum takibi | 03/04 (gönderim var) | ⚪ Planlandı |
| 07 | [[07-Metrikler-ve-Segmentasyon]] — metrik + (faz 2) segment | 03, 04 | ⚪ Planlandı |

## 🔗 Bağımlılık Mantığı
```
01 Cron Motoru ─┐
                ├─▶ 03 Push (broadcast)  ─┐
02 Kural+Dispatch┘                        ├─▶ 06 Bildirim Merkezi
                └─▶ 04 E-posta ─▶ 05 Koşullu ┘
                                            └─▶ 07 Metrik / Segment
```
- **01 + 02 = çekirdek.** Cron motoru "vadesi gelen işi işle" tick'ini sağlar; kural modeli neyin gönderileceğini tanımlar.
- **03 / 04 = kanal adaptörleri** (push broadcast / e-posta tam kapsam).
- **05 = tetikleyici katmanı** (koşullu/transactional, e-posta odaklı).
- **06 / 07 = üst katmanlar** (geçmiş/durum, metrik/segment).

## 🎯 Önerilen Başlangıç
**01 Cron Motoru** ile başla — tüm zamanlı/tekrarlayan davranışın temeli. Ama önce **altyapı/izin sorularını** netleştir (nerede koşacak, hangi dil) — bkz. [[01-Cron-Motoru]] "Çözülecek İzinler".

> [!tip] Tasarım ilkesi (baştan)
> İş/zamanlama deposu **intern API DB'sinde**; "clock/tick" mekanizması **takılıp-çıkarılabilir** olmalı. Çekirdek mantık = "vadesi gelen işleri bul ve işle"; tick kaynağı (process / ayrı sunucu / harici pinger) bunu yalnızca tetikler. Böylece altyapı/izin kararı çekirdeği bağlamaz.

[[00-Proje-Ozeti|← Proje Özeti]]
