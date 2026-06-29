---
tags: [jotform/apps, proje, firsat]
status: taslak
updated: 2026-06-24
---

# 💡 Sektörden Doğan Yeni Fikirler

> [!abstract] Amaç
> Sektör araştırmasının ham verisinden çıkan, **mevcut [[04-Proje-Onerileri|Oneri-1..5]]'e girmeyen** özgün proje fikirleri. Hepsi taslak/aday; biri seçilirse tam Oneri notuna terfi eder. Kaynak: [[00-Sektor-MOC]] + 3 sektör raporu (Haziran 2026).

---

## 🆕 Fikir A — "Durum Takip" (Status Tracker) Elementi ⭐
**Gözlem:** Sektörler arası tekrar eden tek bir ihtiyaç: son kullanıcının **kendi kaydının durumunu** görmesi.
- Perakende: "siparişiniz hazırlanıyor/kargoda"
- İK: "izin talebiniz onaylandı/reddedildi"
- Kamu: "izin/ruhsat başvurunuzun aşaması"
- Sağlık: "sevk/onam onaylandı"
- Saha: "iş emri atandı/tamamlandı"

**Fikir:** [[Sikayet-Workflow|Workflows Flow Status]]'una bağlanan, son kullanıcıya **adım adım durum çizgisi** (rozet + zaman damgası) gösteren bağımsız bir app elementi.
**Neden yeni:** [[Oneri-3-Portal]]'dan ayrı — portal "verimi listeler", bu element "verimin nerede olduğunu" gösterir. Tek başına, portal olmadan da değerli.
**Teknik:** Mevcut Workflows altyapısı var; iş, durumu app içinde render etmek. Demosu çok görsel. **5/9 sektöre dokunuyor.** Ayrıca **tetikleme zaten çalışıyor** — App içi form gönderimi forma bağlı workflow'u başlatıyor; eksik olan tek halka durumu App'e geri göstermek (bkz. [[Sikayet-Workflow#🔗 App ↔ Workflow İlişkisi (3 katman)|App↔Workflow 3 katman]]).

> [!check] Workflows kapsama doğrulaması (Haziran 2026)
> Fikri terfi etmeden önce "bunun ne kadarı Workflows'ta zaten var?" diye doğrulandı. Sonuç: **motor + veri + API var, eksik olan tek şey son-kullanıcı UX'i** → fikir net biçimde net-yeni ve kapsamı bir aya uygun.
>
> | Katman | Var mı? | Not |
> |---|---|---|
> | Onay motoru (çok adımlı/paralel, Group Approval, assignee) | ✅ | Yeniden yazma yok |
> | Builder-tarafı Flow Status (Tables/Inbox/sahibin mobil app'i) | ✅ | Yalnızca **sahip/onaylayan** görüyor |
> | Karar sonrası e-posta | ✅ | Statik, anlık değil |
> | Workflow durumunu API ile çekme | ✅ | Elementi besleyecek veri hazır |
> | **Son kullanıcının kendi durumunu canlı görmesi** | ❌ | **Fikrin çekirdeği — boşluk burada** |
>
> Jotform resmî cevabı: *"no currently possible way to let the user access their specific submission status"* — Enterprise'da bile yok, **geliştiricilere eskale**. *"no link available... to view their own submission's approval status."*
> Kaynaklar: [answers/5052504](https://www.jotform.com/answers/5052504-approval-status-letting-the-user-check-their-approval-status-in-jotform) · [answers/12518471](https://www.jotform.com/answers/12518471-how-will-my-form-responders-track-approval-status) · [help/1466](https://www.jotform.com/help/1466-how-do-you-track-the-approval-process-in-jotform-tables/) · [API: workflow status](https://www.jotform.com/answers/32922491-api-how-to-get-submissions-workflow-status)
> **En taze teyit (16 Nisan 2026):** *"no live status tracking visible to individual submitters"* — [answers/37535031](https://www.jotform.com/answers/37535031-client-portal-how-to-create-a-dashboard-for-clients-to-log-in-and-track-application-status). Güncel durum özeti: [[Guncel-Durum-Dogrulama]].
>
> **Kapsam sınırı:** *Yapma* → onay mantığı/atama/çok-adımlı akış (var). *Yap* → API'den durumu çekip app içinde canlı, gönderen-yüzlü durum çizgisi elementi (yok).

## 🆕 Fikir B — Çok-Kanallı Zamanlanmış Hatırlatma (Omnichannel Reminder)
**Gözlem (keskin içgörü):** Jotform randevu/hatırlatmayı bugün **zamanlanmış e-posta autoresponder** ile çözüyor — push ile değil. Yani "zamanlama" mantığı kurumda *zaten var*, ama push kanalına bağlı değil.
**Fikir:** Tek bir "zamanlanmış hatırlatma" kuralı tanımla → kanal seç (**push + e-posta + in-app merkez**). [[Oneri-1-Push-Scheduler]]'ın doğal üst-çerçevesi.
**Neden yeni:** Oneri-1 yalnızca push'u zamanlıyordu; bu, mevcut e-posta zamanlamasını ve push'u **tek arayüzde** birleştirir → hem daha güçlü hem mevcut yatırımı kullanır. Sağlıkta HIPAA-dostu (e-posta/SMS fallback) avantajı da var.

## 🆕 Fikir C — RSVP / Katılım Yoklaması Elementi
**Gözlem:** Amatör spor (maç yoklaması), etkinlik (oturum RSVP), eğitim (etkinlik katılımı), nonprofit (gönüllü vardiya) hepsi **hafif "geliyor musun?"** akışı istiyor. Rakipler (Spond, BenchApp) tam bunu SMS ile yapıyor.
**Fikir:** Zamanlanmış hatırlatma + tek dokunuş RSVP (Evet/Hayır/Belki) + organizatöre canlı katılım sayısı.
**Neden yeni:** Push + hafif workflow + sayım kesişimi; tek bir paketlenmiş element. [[Oneri-1-Push-Scheduler]] üstüne küçük ama yüksek-talepli ek. Beyaz alan **spor kulüplerini** doğrudan açar ([[Erisilebilir-Yeni-Sektorler]]).

## 🆕 Fikir D — Üyelik/Sadakat Modülü (Membership)
**Gözlem:** Dernekler, HOA, spor kulüpleri, restoran-sadakat hepsi **üye girişi + aidat/puan + üyeye-özel içerik** istiyor. Jotform'un ödeme+kayıt'ı hazır, eksik olan üyelik katmanı.
**Fikir:** [[Oneri-3-Portal]] üstüne üyelik kartı, aidat/yenileme durumu, member-only içerik kilidi, basit puan/sadakat.
**Neden yeni:** Genel portaldan daha dikey; bir **sektör paketleri** stratejisinin (dernek/HOA) çekirdeği. Wild Apricot gibi pahalı araçlara doğrudan alternatif.

---

## 🔢 Aday Önceliklendirme (ön)
| Fikir | Talep genişliği | Kapsam netliği | Mevcut altyapı | Not |
|---|---|---|---|---|
| **A. Durum Takip** ⭐ | 5/9 sektör | Yüksek | Workflows var | En güçlü yeni aday |
| **B. Omnichannel hatırlatma** | Çok geniş | Orta | Push+e-posta var | Oneri-1'i yükseltir |
| **C. RSVP elementi** | Orta (spor/etkinlik) | Yüksek | Push gerekli | Küçük, demolik |
| **D. Üyelik modülü** | Orta (dikey) | Düşük-Orta | Portal+ödeme | En geniş kapsam |

> [!tip] Tavsiye
> **Fikir A (Durum Takip)** en güçlü yeni aday: geniş sektör dokunuşu + mevcut Workflows altyapısı + görsel demo. [[Oneri-3-Portal]] ile birlikte güçlü bir "ürün hikâyesi" oluşturur. **Fikir B**, [[Oneri-1-Push-Scheduler]]'ı seçersek onun kapsamını büyütmenin doğal yolu.

[[00-Sektor-MOC]] · [[03-Firsat-Haritasi]] · [[00-MOC|← Ana MOC]]

#jotform/apps #proje #firsat
