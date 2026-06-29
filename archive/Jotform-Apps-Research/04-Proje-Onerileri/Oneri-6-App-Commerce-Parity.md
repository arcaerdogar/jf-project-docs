---
tags: [jotform/apps, proje, firsat]
status: olgun
updated: 2026-06-24
---

# 🛒 Öneri 6 — App Alışveriş Komponentini Form Paritesine Getirmek (FİNALİST)

> [!success] Mentör-önerili finalist. [[Oneri-1-Push-Scheduler]] ile birlikte iki finalistten biri.
> Çözdüğü şikayet: [[Sikayet-Product-Table]].

## 🧩 Problem
App alışveriş komponenti, form tarafındaki **Product List**'in kısıtlı alt kümesi (kupon/kargo/vergi/stok/e-posta düzenleme yok). Kullanıcılar form'da çözülmüş şeylere app'te takılıyor.

## 💡 Çekirdek İçgörü
Bu özellikler **backend'de zaten var** (form Product List). App sadece UI'da açmıyor — Jotform'un kendi workaround'u bile *"form kullan"*. Yani iş **yeni özellik değil, var olanı app yüzeyine açmak**.

## 📐 Çözüm (mentör + stajyer muhakemesi)
App alışveriş ayarlarını, **arka tarafta form ile aynı API'yi** kullanan ama **app için özelleştirilmiş bir frontend** üzerinden aç. Kullanıcı app'ten çıkmadan tüm form-seviyesi ayarlara (kupon, kargo, vergi, stok, sipariş e-postası) erişir.

## ⚖️ Mimari Tartışma (kayıt için)
- **Forma-bağlı lehine:** Şirket felsefesi "her şey forma bağlı"; tutarlılık; problem zaten form tarafında çözülü. Ayrı bir app komponenti mimari olarak gereksiz ikilik.
- **Karşı argüman:** Kullanıcıyı **iki farklı tab'da yormamak**. App'ten e-ticaret yürüten kişi ekstra form'la uğraşmak istemez.
- **Çözüm (sentez):** App-native frontend + paylaşılan form API → kullanıcı app'te kalır, backend form sistemini yeniden kullanır. İki argüman da karşılanır. *(Arka tarafta sistem zaten aynı işliyor; özellikler app komponenti oluşturunca açılmıyor sadece.)*

> [!success] KARAR (Haz 2026): **App-native frontend.**
> Gömülü form **zaten var** — Jotform'un kupon için önerdiği resmî workaround bu ([[Sikayet-Product-Table]]). Yani gömülü form "yapılacak iş" değil, **statüko**. Projenin tüm değeri kullanıcıyı form tab'ına göndermeden aynı backend'i **app içinde** açmakta. Gömülü-form seçeneği elendi; "iki tab'da yorma" karşı-argümanını çözen tek yol app-native frontend.

## 🎯 Kapsam (öncelik = en çok ticket'lı özellikler)
MVP: kupon kodları + kargo ücreti + özelleştirilebilir sipariş/onay e-postası. Faz 2: vergi, stok yönetimi, ürün opsiyonu pariteleri.
> ⚠️ "Tüm ayarları aç" balonlaşabilir → ticket yoğunluğuna göre öncelikli özelliklerle başla.

## ✅ Neden Güçlü
- **En güçlü dahili kanıt:** 6-7 L3 ticket doğrudan bu konuda (bkz. [[Sikayet-Product-Table]]).
- **Düşük teknik risk:** var olan backend'i açmak, sıfırdan sistem değil.
- **Felsefe uyumu:** "her şey forma bağlı" ile birebir.
- **Somut demo:** alışveriş akışı görsel ve net.

## ⚠️ Riskler
- ~~Frontend-vs-embedded-form mimari kararı~~ → ✅ **Karar verildi: app-native frontend** (yukarı).
- Kalan tek açık nokta: **öncelikli özellik seti** sabitlenmeli (kupon/kargo/sipariş e-postası ile başla).
- API yüzeyi: form Product List ayarlarının tamamı app-native UI'dan erişilebilir mi, yoksa bazıları form-builder'a gömülü mü? — implementasyon öncesi haritalanmalı.

## 📊 Skor
| Talep | Değer | Kapsam netliği | 1 ayda canlı |
|---|---|---|---|
| **Yüksek (6-7 L3 ticket)** | Yüksek | Orta-Yüksek | ✅ Yüksek |

İlgili: [[Oneri-1-Push-Scheduler]] · [[05-Tavsiye-ve-Sonraki-Adimlar]] · [[Sektor-Perakende]]
[[00-MOC|← MOC]]

#jotform/apps #proje #firsat
