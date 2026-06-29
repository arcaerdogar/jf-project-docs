---
tags: [jotform/apps, sektor, firsat]
status: olgun
updated: 2026-06-24
---

# 🌱 Erişilebilir Yeni Sektörler (Beyaz Alan)

> [!abstract] Çerçeve
> Bugün Jotform Apps'e zayıf bağlı ama App Builder ile **kazanılabilecek** sektörler. Bir sektör "kazanılabilir" sayılırken kritik eşik: bizdeki boşluğun (offline / zamanlı push / portal / analitik / workflow) o sektör için *belirleyici* olup olmadığı. Not: fitness/kilise/emlak Jotform'un **zaten şablonla hedeflediği** alanlar → "beyaz alan" değil, "zayıf konumlanma".

## Aday Tablosu
| # | Sektör | Bugünkü bağlılık | Kritik eksik (boşluk) | Erişim |
|---|---|---|---|---|
| 1 | **Üyelik dernekleri / meslek odaları** ⭐ | Zayıf | **Portal** + workflow | Kolay-Orta |
| 2 | **Amatör spor kulüpleri / ligler** ⭐ | Zayıf | Zamanlı **push** + RSVP | Kolay |
| 3 | **Tarım / çiftlik kayıt** ⭐ | Çok zayıf | **Offline** | Orta |
| 4 | Seyahat acentesi / tur operatörü | Zayıf | **Offline** itinerary | Orta-Zor |
| 5 | HOA / site-apartman yönetimi | Zayıf | **Portal** + ödeme | Kolay-Orta |
| 6 | Restoran (müşteri sipariş/sadakat) | Zayıf-orta | Sadakat/**analitik** + native push | Orta-Zor |
| 7 | Ev hizmetleri / esnaf (tek kişi) | Zayıf | Derin scheduling **workflow** | Zor |

## ⭐ En Umut Verici 3
1. **Üyelik dernekleri / meslek odaları** — Mevcut yeteneklerle (ödeme+etkinlik+kayıt) ~%70 hazır; **tek kilit boşluk PORTAL** (üye girişi, aidat durumu, üye kartı, member-only içerik). Masaüstü ağırlıklı → PWA dezavantajı yok. Rakipler: Wild Apricot (15.000+ kuruluş, pahalı bulunuyor), Glue Up, Neon CRM. → [[Oneri-3-Portal]] yatırımı bu sektörü kilitler.
2. **Amatör spor kulüpleri / ligler** — Form+ödeme gücüyle hazır; **tek kilit boşluk ZAMANLANMIŞ PUSH + RSVP** ("maç hatırlatması + geliyor musun?"). Rakipler ücretsiz (TeamSnap, Spond, BenchApp) → farklılaşma "tek uygulamada ödeme+kayıt+iletişim". → [[Oneri-1-Push-Scheduler]] + [[Sektorden-Dogan-Fikirler|RSVP elementi]].
3. **Tarım / çiftlik kayıt** — Jotform'un **hiç dokunmadığı** taze beyaz alan; saf form gücüyle örtüşüyor; **tek kilit boşluk OFFLINE**. Rakiplerin ana argümanı sinyalsiz tarlada offline+sync (Farmbrite, Forms On Fire). → [[Oneri-2-Offline-Mode]].

## 🧭 Stratejik Örüntü (tek boşluk → çok sektör)
- **Portal** → dernek + HOA (+ mevcut emlak/eğitim)
- **Zamanlanmış push** → spor + restoran-iç (+ mevcut etkinlik/perakende)
- **Offline** → tarım + seyahat + saha denetim (+ mevcut kamu)

> [!important] Çıkarım
> Hangi boşluğa yatırım yapılırsa, hem **mevcut** bir sektör kümesini derinleştiriyor hem de bir **yeni** sektör kümesini açıyor. Bu, [[05-Tavsiye-ve-Sonraki-Adimlar|önceliklendirme]] için ek bir argüman.

## ⚠️ Belirsizlikler
- PWA dezavantajı **restoran ve ev hizmetlerinde** sert (App Store beklentisi) — boşluk kapatılsa bile tam çözülmez.
- Pazar büyüklüğü/fiyat rakamları rakip blog kaynaklı, bağımsız doğrulanmadı.
- ~~Jotform'un bu boşluklara kısmi destek eklemiş olabileceği teyit edilmedi~~ → ✅ **Doğrulandı:** [[Guncel-Durum-Dogrulama]] (Haz 2026). Push & offline hâlâ açık; portal pazarlama düzeyinde ilerledi (AI Portal Builder) ama **per-kullanıcı filtre + canlı durum hâlâ yok** (16 Nisan 2026 teyidi) → [[Oneri-3-Portal]] daraltılmalı.

[[00-Sektor-MOC]] · [[03-Firsat-Haritasi]] · #jotform/apps #sektor #firsat
