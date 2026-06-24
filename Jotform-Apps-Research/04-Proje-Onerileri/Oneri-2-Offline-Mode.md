---
tags: [jotform/apps, proje, firsat]
status: olgun
updated: 2026-06-24
---

# 🟠 Öneri 2 — App Builder Uygulamaları için Offline Mod

> [!warning] En yüksek etki — ama daha yüksek teknik risk

## 🧩 Çözdüğü Şikayet
[[Sikayet-Offline]] — App Builder PWA'ları internet yokken açılmıyor; sahada veri toplama bozuluyor.

## 📐 Kapsam
- **PWA service worker** ile uygulamanın offline açılması.
- **Yerel kuyruk (IndexedDB):** Form gönderimini cihazda sakla.
- **Otomatik sync:** Bağlantı geri gelince kuyruğu sunucuya gönder.

> [!important] MVP Sınırı (kritik)
> MVP'yi **"offline açılma + formu kuyruğa alma + online olunca sync"** ile sınırla.
> **Faz 2'ye ertele:** çakışma çözümü (conflict resolution) ve medya/dosya yükleme. Bunlar bir aya sığmaz.

## 💡 Neden Değerli
- İnceleme sitelerinde **en sık övülen kullanım** (saha/etkinlik veri toplama) tam da bu senaryo.
- "Mobile Forms" zaten offline çalışıyor → yetenek kurumda var, App Builder'a taşınması net bir hedef.

## ⚠️ Risk
- **Service worker + sync + çakışma yönetimi** bir ay için riskli.
- **Kapsamı agresif sınırla** — aksi halde demo edilebilir bir çıktı çıkmaz.
- Bu yüzden [[05-Tavsiye-ve-Sonraki-Adimlar]]'da **ikinci sıra**: yalnızca ekip iştahı yüksekse, sıkı sınırlanmış MVP olarak.

## 🛠️ Teknik Uygunluk
- Front-end ağırlıklı (service worker, IndexedDB, sync API).
- Test edilebilir net davranış: "uçağa al / wifi kapat → doldur → aç → sync."

## 📊 Skor (bkz. [[03-Firsat-Haritasi]])
| Talep | Değer | Kapsam netliği | 1 ayda canlı |
|---|---|---|---|
| Yüksek | **Çok yüksek** | Orta | ⚠️ Orta |

İlgili öneriler: [[Oneri-1-Push-Scheduler]] ⭐ · [[Oneri-3-Portal]]
[[00-MOC|← MOC]]

#jotform/apps #proje #firsat
