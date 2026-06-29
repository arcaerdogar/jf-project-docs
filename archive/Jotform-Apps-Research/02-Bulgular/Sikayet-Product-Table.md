---
tags: [jotform/apps, sikayet, firsat]
status: olgun
updated: 2026-06-24
---

# 🛒 Şikayet: App Ürün Tablosu, Form Tarafının Kısıtlı Bir Alt Kümesi

> [!info] Kaynak: Mentör toplantısı (Haz 2026) + L3 ticket yığını + web doğrulaması
> Öncelik: 🔴 Yüksek — **6-7 L3 ticket** doğrudan bu konuda (en güçlü dahili talep sinyali).

## Problem
App içindeki alışveriş/ürün tablosu komponenti **temel**: yalnızca ürün ekleme, fiyat belirleme, ödeme/sipariş alma. Form tarafındaki **Product List** elementinde çözülmüş birçok problem app komponentinde **açık değil**.

## Parite Boşluğu (form'da var → app'te yok)
| Özellik | Form Product List | App Store |
|---|---|---|
| Kupon / promo kodu (son kullanma, limit) | ✅ | ❌ |
| Kargo ücreti | ✅ | ❌ |
| Vergi (oran / konum bazlı) | ✅ | ❌ |
| Ürün opsiyonu & özel fiyatlandırma | ✅ | kısıtlı |
| Stok yönetimi (tükendi/düşük-stok e-postası) | ✅ | ❌ |
| **Sipariş/onay e-postasını özelleştirme** | ✅ | ❌ |

## 🔑 Kanıt Niteliğindeki Nokta
Jotform'un **kendi destek cevabı**: Store Builder'da kupon **"mümkün değil"**, workaround olarak *"bir **form** oluşturup **Product List Element** kullanın."*
→ Yani yetenek **backend'de zaten var**; app sadece UI'da kullanıcıya açmıyor.
- [Store Builder kupon → form workaround](https://www.jotform.com/answers/4766963-jotform-store-builder-ability-to-add-coupon-codes) · [App kupon talebi](https://www.jotform.com/answers/14267353-jotform-app-ability-to-add-a-coupon-code-to-a-product) · [promo code store builder](https://www.jotform.com/answers/4066981-promo-code-option-store-builder)
- Form tarafı yetenekler: [kupon](https://www.jotform.com/help/233-how-to-add-coupon-code-to-payment-forms/) · [kargo/vergi](https://www.jotform.com/help/323-mastering-payment-form-integrations-with-jotform/) · [Product List](https://www.jotform.com/blog/introducing-product-list-form-field/)

## Çıkarım
Bu bir "yeni özellik geliştirme" değil, **var olan form yeteneklerini app yüzeyine taşıma** problemi → düşük teknik risk + şirket felsefesiyle ("her şey forma bağlı") birebir uyumlu. Çözüm önerisi: [[Oneri-6-App-Commerce-Parity]].

[[03-Firsat-Haritasi]] · [[00-MOC|← MOC]]

#jotform/apps #sikayet #firsat
