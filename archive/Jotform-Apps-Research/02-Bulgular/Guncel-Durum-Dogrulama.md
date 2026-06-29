---
tags: [jotform/apps, kanit, baglam]
status: olgun
updated: 2026-06-24
---

# ✅ Güncel Durum Doğrulaması (Haziran 2026)

> [!abstract] Amaç
> "Jotform bu boşlukları 2025–2026'da kapatmış olabilir mi?" sorusunun cevabı — yani **boşa kürek çekmeyelim** kontrolü. Her boşluğun en güncel durumu ve en taze kanıt aşağıda. [[Erisilebilir-Yeni-Sektorler]]'deki "teyit edilmedi" uyarısını kapatır.

## 🧭 Verdikt Tablosu

| Boşluk | Durum (Haz 2026) | En güncel kanıt | Karar |
|---|---|---|---|
| **Zamanlanmış/tekrarlayan push** | 🟢 AÇIK | 2026 thread'leri "not available, escalated"; reminder yalnızca **e-posta** için | [[Oneri-1-Push-Scheduler]] **güvenli** |
| **Offline (App Builder)** | 🟢 AÇIK | Destek: *"this can't work offline"*; 2026'da PWA offline güncellemesi yok | [[Oneri-2-Offline-Mode]] **güvenli** |
| **Kişiye-filtreli portal + giriş + canlı durum** | 🟡 AÇIK (ama pazarlama bulanık) | **16 Nisan 2026** thread: *"we don't have an option to create a login portal for your clients"* | [[Oneri-3-Portal]] **DARALT** |
| **Submitter-yüzlü onay/iş akışı durumu** | 🟢 AÇIK | Aynı 16 Nisan 2026 thread: *"no live status tracking visible to individual submitters"* | [[Sektorden-Dogan-Fikirler|Fikir A]] **güvenli & keskin** |
| **In-app analitik (son-kullanıcı)** | ⚪ MUHTEMELEN AÇIK | GA widget eskale; 2026'da ayrıca teyit edilmedi | [[Oneri-4-In-App-Analytics]] *düşük güven* |

## ⚠️ En Önemli Bulgu: Portal "Boşa Kürek" Riski
2026'da Jotform **AI Portal Builder** çıkardı (no-code portal, PWA; "farklı kullanıcılara belirli veri/form/dashboard erişimi", rol-bazlı izinler). Ayrıca Client/Customer Portal şablonları ve "client portal nasıl yapılır" blogu (Mart 2026) var.

**Ama pazarlama ile gerçek çelişiyor.** En taze destek cevabı (**16 Nisan 2026**, [answers/37535031](https://www.jotform.com/answers/37535031-client-portal-how-to-create-a-dashboard-for-clients-to-log-in-and-track-application-status)) şunları **hâlâ yok** diyor:
- Bireysel istemci giriş kimliği
- Yalnızca kendi verisini gösteren istemci dashboard'u
- Gönderene görünen **canlı durum takibi**
- Manuel durum güncellemesinin istemci-yüzlü yansıması

Client-portal blogu (Mart 2026) da rol-bazlı izinleri **manuel** kuruyor; **otomatik per-kullanıcı submission filtresi yok**.

> [!danger] Sunum kozu (ama dikkat)
> Birisi "ama artık Portal Builder var" diyebilir. Doğru çerçeve: **Portal Builder = rol-bazlı erişim + form/tablo bağlama.** Çözmediği şey: *otomatik per-gönderen veri kapsamı + gönderen-yüzlü canlı durum* — ki bu tam olarak [[Oneri-3-Portal]] + [[Sektorden-Dogan-Fikirler|Fikir A]]'nın çekirdeği (16 Nisan 2026 itibarıyla hâlâ açık).

## 🤖 Bağlam: 2025–2026 Yatırımı = AI
Jotform'un son dönem ağırlığı net biçimde AI: AI Agents (Şub 2025), konuşma-tabanlı Jotform AI (Mart 2026), ChatGPT Marketplace (Mart 2026), **AI App Builder** (Haz 2026 — "pages, navigation, workflows, layouts, data connections" üretiyor), **AI Portal Builder**.
> 💡 Bu, [[Apps-Mevcut-Durum-2026|ana tezi]] **doğruluyor**: yatırım AI tarafında; "uygulama davranışı" boşlukları (offline, zamanlı push, per-kullanıcı portal/durum) **açık kalıyor**. Yeni AI-üretimli app/portal iskeletleri, bizim elementlerimizin **bağlanacağı zemini** büyütüyor — rakip değil, taşıyıcı.

## ⚠️ Belirsizlikler
- Offline için en taze **birebir** destek alıntısı 2023; 2026 aramaları çelişen bir güncelleme bulmadı ama "kesin hâlâ yok" için bir 2026 destek teyidi ideal olurdu.
- Zamanlanmış push için kanıt 2026 arama-derlemesi (birden çok thread aynı yönde); tek bir 2026 thread'i tam metniyle açılmadı (sayfa login'e yönlendi).
- In-app analitik 2026'da yeniden teyit edilmedi → düşük güven.
- AI Portal Builder'ın **lansman tarihi** sayfada belirtilmemiş; "2026" konumlandırması dolaylı.
- **AI App Builder "workflows" belirsizliği:** AI App Builder (23 Haz 2026) "workflows üretiyor" diyor; bunun Approvals ürününü mü yoksa app-içi akışı mı kastettiği teyit edilmedi → daha sıkı App↔Workflow entegrasyonu geliyorsa [[Sektorden-Dogan-Fikirler|Fikir A]]'yı etkileyebilir. İzlenecek. (bkz. [[Sikayet-Workflow]])

## 🔗 İlgili
[[Ek-Arastirma-Haziran-2026]] · [[Apps-Mevcut-Durum-2026]] · [[Oneri-3-Portal]] · [[06-Kaynaklar]] · [[00-MOC|← MOC]]

#jotform/apps #kanit
