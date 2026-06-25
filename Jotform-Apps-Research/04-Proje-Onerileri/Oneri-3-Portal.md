---
tags: [jotform/apps, proje, firsat]
status: olgun
updated: 2026-06-24
---

# 🟡 Öneri 3 — Kişiselleştirilmiş "Benim Verim" Portal Görünümü

> [!note] Dengeli seçenek — talep güçlü, altyapı hazır

> [!warning] Kapsam daraltma (Haz 2026 doğrulaması — [[Guncel-Durum-Dogrulama]])
> 2026'da **AI Portal Builder** çıktı → jenerik "portal kur" + rol-bazlı erişim **artık var**. Bu yüzden öneriyi "portal yapalım" diye sunmak **boşa kürek**. Hâlâ açık olan ve bu önerinin odaklanması gereken çekirdek: **otomatik per-gönderen veri filtresi + gönderen-yüzlü canlı durum** (16 Nisan 2026 itibarıyla *"not available"*). Pratikte bu, öneriyi [[Sektorden-Dogan-Fikirler|Fikir A (Durum Takip)]] ile **birleştirmeye** işaret ediyor.

## 🧩 Çözdüğü Şikayet
[[Sikayet-Portal]] — Son kullanıcının giriş yapıp yalnızca kendi gönderimlerini şık, filtrelenmiş bir ekranda göreceği gerçek bir portal eksik. (Jenerik portal artık var; eksik olan **otomatik per-kullanıcı filtre + canlı durum** — bkz. yukarıdaki uyarı.)
İlişkili yeni bulgu: [[Sikayet-Workflow]] — onay/iş akışı durumu uygulama içinde görünmüyor; durum rozetlerinin teknik temeli burada.

## 📐 Kapsam
Mevcut **kayıt/giriş + assignee** altyapısı üstüne:
- Kullanıcıya filtrelenmiş **"Benim Gönderimlerim / Durumum"** elementi.
- **Durum rozetleri** (onay akışıyla entegre): beklemede / onaylandı / reddedildi vb.
- **Düzenleme / yeniden gönderme** imkânı.

## 💡 Neden Değerli
- **Talep güçlü** — forumda birden çok thread'de tekrar ediyor.
- **Kimlik/erişim altyapısı zaten var** (kayıt, giriş, assignee) → sıfırdan kimlik kurmaya gerek yok.
- **Kapsam offline'dan daha öngörülebilir** — net bir element/görünüm işi.

## 🛠️ Teknik Uygunluk
- Mevcut "My Submissions" elementi referans alınabilir; üstüne kullanıcı-bazlı filtreleme + durum katmanı.
- **Durum rozetleri Workflows'un Flow Status'una bağlanabilir** (bkz. [[Sikayet-Workflow]]) → onay motorunu sıfırdan yazmaya gerek yok.
- Hem backend (yetki/filtre) hem front-end (element UI) dengeli iş.
- Mobil 3-nokta menüsü kaybı gibi mevcut UX sorunları da bu kapsamda düzeltilebilir.

## 🏭 Sektörel Talep
En güçlü eşleşmeler: [[Sektor-Egitim]] (veli/öğrenci), [[Sektor-Emlak]] (kişisel katalog), [[Sektor-IK]] (çalışan portalı), [[Sektor-Saglik]] (hasta). Yeni sektör açar: **üyelik dernekleri** + **HOA** → [[Erisilebilir-Yeni-Sektorler]]. İlgili yeni fikir: [[Sektorden-Dogan-Fikirler|Durum Takip + Üyelik modülü]].

## 📊 Skor (bkz. [[03-Firsat-Haritasi]])
| Talep | Değer | Kapsam netliği | 1 ayda canlı |
|---|---|---|---|
| Orta-Yüksek | Yüksek | Orta | ✅ Orta-Yüksek |

> [!tip] Konum
> Ana aday [[Oneri-1-Push-Scheduler]] kapsam netliğiyle önde; bu öneri **güçlü bir alternatif/yedek**. Tasarım cilası tarafında [[Sikayet-Tasarim]] taleplerine de kısmen dokunur.

İlgili öneriler: [[Oneri-1-Push-Scheduler]] ⭐ · [[Oneri-2-Offline-Mode]]
[[00-MOC|← MOC]]

#jotform/apps #proje #firsat
