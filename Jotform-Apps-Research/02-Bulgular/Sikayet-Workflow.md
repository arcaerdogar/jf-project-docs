---
tags: [jotform/apps, sikayet, firsat]
status: taslak
updated: 2026-06-24
---

# 🟠 Şikayet: İş Akışı/Onay Durumu Uygulama İçinde Görünmüyor

> [!info] Kaynak: Haziran 2026 ek araştırması (bkz. [[Ek-Arastirma-Haziran-2026]])
> Öncelik: Orta-Yüksek (yeni bulgu — [[Sikayet-Portal]]'ı güçlendiriyor)

## Problem
Jotform'un **ayrı ve güçlü bir Workflows/Approvals ürünü** var:
- Çok adımlı + paralel onay, **Group Approval**, özel sonuçlar (Approve/Deny + özel).
- **Assignee** (atama), yeniden atama, görev yorumları, dosya yükleme.
- **Flow Status** sütunu Jotform Tables'da görünüyor; durum değişim tarihi/sorumlusu kaydediliyor.

**Ama bu zenginlik App Builder'a yansımıyor.** Son kullanıcı, kendi uygulaması içinde başvurusunun **onay durumunu canlı göremiyor.** Workflow ile App arasında köprü zayıf.

## Kanıt / Sinyal
- **Resmî doğrulama (Haziran 2026):** Jotform, son kullanıcının kendi onay durumunu görmesinin *"no currently possible way..."* olduğunu söylüyor — Enterprise'da bile yok, **geliştiricilere eskale edilmiş**. Paylaşılabilir bir durum linki de yok. Flow Status yalnızca **builder-tarafı** (Tables/Inbox). Kaynaklar: [answers/5052504](https://www.jotform.com/answers/5052504-approval-status-letting-the-user-check-their-approval-status-in-jotform) · [answers/12518471](https://www.jotform.com/answers/12518471-how-will-my-form-responders-track-approval-status) · [help/1466](https://www.jotform.com/help/1466-how-do-you-track-the-approval-process-in-jotform-tables/)
- Mevcut workaround'lar (statik PDF, e-posta) **anlık güncellenmiyor.**
- İlgili: onay durumunun başka yüzeylere yansımaması tekrar eden tema — *"Approval status'u Google Sheet entegrasyonuna dahil et"* feature-request'i de aynı kopukluğu gösteriyor.
- **Fizibilite:** Workflow durumu **API ile çekilebiliyor** → app içi element için veri hazır ([API thread](https://www.jotform.com/answers/32922491-api-how-to-get-submissions-workflow-status)). Detaylı kapsama analizi: [[Sektorden-Dogan-Fikirler#🆕 Fikir A — "Durum Takip" (Status Tracker) Elementi ⭐|Fikir A doğrulaması]].

## 🔗 App ↔ Workflow İlişkisi (3 katman)
> [!info] "Appler Workflow'larla birlikte çalışıyor mu?" sorusunun net cevabı (Haz 2026 doğrulaması)

1. **Tetikleme — ✅ var (dolaylı):** Workflow, bağlı **form gönderilince** başlar; App form gömdüğü için App içi gönderim de workflow'u tetikler. Bağlantı App↔Workflow değil, **ortak form** üzerinden — form köprü. ([workflow tetikleme](https://www.jotform.com/help/guide-jotform-workflows/) · [API ile tetikleme](https://www.jotform.com/answers/3889144-how-can-i-trigger-the-approval-workflow-automatically-after-submitting-new-form-via-api))
2. **Durum geri-beslemesi — ❌ yok:** App, workflow durumunu son kullanıcıya gösteremiyor; tek geri besleme **e-posta**. (Bu notun ana boşluğu.)
3. **AI App Builder "workflows" — ⚠️ belirsiz:** AI App Builder (23 Haz 2026) "workflows üretiyor" diyor ama bunun **Approvals ürünü mü** yoksa app-içi akış mı olduğu net değil → izlenecek. ([AI App Builder](https://www.prnewswire.com/news-releases/jotform-introduces-ai-app-builder-turning-ideas-into-fully-functional-apps-in-minutes-302808099.html))

> [!success] Çıkarım: boru tesisatı hazır
> Katman 1 (tetikleme) + API'den durum verisi **zaten var**; eksik olan yalnızca **katman 2** (ekranda gösterme). [[Sektorden-Dogan-Fikirler|Fikir A]] tam bu boşlukta oturuyor.

## Neden Önemli
- Mevcut **Workflows altyapısı zaten var** — sıfırdan onay motoru yazmaya gerek yok. İş, durumu **App içinde göstermek**.
- [[Sikayet-Portal]]'daki "durum rozetleri (onay akışıyla)" talebinin **teknik temelini** oluşturuyor: portal + workflow durumu = tam çözüm.

## Değerlendirme (ön)
| Boyut | Durum |
|---|---|
| Talep | Orta-Yüksek |
| Değer | Yüksek |
| Kapsam netliği | Orta |
| 1 ayda canlı | ✅ Orta-Yüksek |

> [!note] Bağlantı
> Bu bulgu, [[Sikayet-Portal]] + [[Oneri-3-Portal]]'ı doğrudan besliyor: portal görünümünün durum rozetleri, Workflows'un Flow Status'una bağlanırsa "geçici çözüm" hissi gerçek bir ürün deneyimine döner.

[[03-Firsat-Haritasi]] · [[00-MOC|← MOC]]

#jotform/apps #sikayet #firsat
