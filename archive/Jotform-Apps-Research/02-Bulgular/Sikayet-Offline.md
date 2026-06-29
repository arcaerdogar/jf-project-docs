---
tags: [jotform/apps, sikayet, firsat]
status: olgun
updated: 2026-06-24
---

# 🔴 Şikayet: Offline Çalışmama

> [!danger] Öncelik: Yüksek değer / net senaryo (kapsam orta)

## Problem
App Builder ile yapılan **PWA uygulamalar internet yokken açılmıyor** — kullanıcı "no internet connection" ekranıyla karşılaşıyor. Markalı uygulama tamamen kullanılamaz hale geliyor.

## Önemli Ayrım
- Jotform'un **ayrı "Mobile Forms"** uygulaması offline çalışıyor. ✅
- Ama kullanıcının **kendi markaladığı App Builder uygulaması** offline çalışmıyor. ❌
- Yani yetenek kurumda mevcut, ama App Builder ürününe taşınmamış.

## Kanıt
- Destek forumunda **tekrar tekrar geliştiricilere eskale edilmiş** bir konu.
- İnceleme sitelerinde **en sık övülen kullanım amaçlarından biri** saha/etkinlik veri toplama — ki tam da bu senaryoda offline kritik.

## Senaryo (neden değerli)
Net ve somut bir kullanım: **sahada / etkinlikte / zayıf sinyalde veri toplama.**
- Anket görevlisi etkinlik alanında, fuarda, kırsalda form dolduruyor.
- Sinyal kesik → uygulama açılmıyor → veri kaybı / iş duruyor.

## Değerlendirme
| Boyut | Durum |
|---|---|
| Talep | Yüksek |
| Değer | **Çok yüksek** |
| Kapsam netliği | Orta (teknik olarak ağır) |
| 1 ayda canlı | ⚠️ Orta — service worker + sync + çakışma riski |

> [!note] Bağlantı
> Bu şikayet → [[Oneri-2-Offline-Mode]] önerisiyle çözülüyor. Kapsam riski yüksek olduğu için MVP agresif sınırlanmalı.

[[03-Firsat-Haritasi]] · [[00-MOC|← MOC]]

#jotform/apps #sikayet #firsat
