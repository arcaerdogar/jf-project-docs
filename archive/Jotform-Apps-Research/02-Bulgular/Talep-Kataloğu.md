---
tags: [jotform/apps, kanit, talep]
status: olgun
updated: 2026-06-24
---

# 🗂️ Talep Kataloğu (Birebir Kullanıcı İstekleri)

> [!abstract] Amaç
> Forum/destek kaynaklarında bulunan **somut, çoğu birebir** kullanıcı istekleri — boşluğa göre gruplu, kaynak linkli. Sunumda "bunu biz değil, kullanıcılar istiyor" kanıtı. Sentez için: [[03-Firsat-Haritasi]] · isimli hikâyeler: [[Musteri-Hikayeleri]].

## 🔔 Push — Zamanlama & Tetikleme → [[Sikayet-Push]] / [[Oneri-1-Push-Scheduler]]
- "Her **Cuma 16:00 timesheet hatırlatması**", "**haftalık** öğrenci planlayıcı hatırlatması" (zamanlanmış + tekrarlayan).
- "Forma **submission gelince otomatik push**" (olaya dayalı tetikleme).
- iOS'ta bildirime dokununca **mesaj kayboluyor**, geçmiş yok (uygulama içi merkez talebi).

## 🎯 Push — Hedef Kitle → [[Sikayet-Push]] (madde 5)
- *"Is there a way to choose which people I want to send the push notification to, or must it be all at the same time?"* — [push yardım sayfası yorumları](https://www.jotform.com/help/how-to-create-and-send-push-notifications-for-jotform-apps/)
- "manage who can receive them" — [answers/11213771](https://www.jotform.com/answers/11213771)
  > 💡 Bugün gönderim **tüm abonelere** gidiyor; alıcı seçimi yok.

## 👤 Portal — Kişiye Filtrelenmiş Görünüm → [[Sikayet-Portal]] / [[Oneri-3-Portal]]
- "user-filtered submissions view" — [answers/4574374](https://www.jotform.com/answers/4574374-jotform-apps-user-filtered-submissions-view)
- "portal to allow users to login individually... see their prior submissions" — [answers/3836866](https://www.jotform.com/answers/3836866-portal-to-allow-users-to-login-individually-to-complete-web-forms-and-be-able-to-see-their-prior-submissions)
- "how to allow users to view **their own submissions only**" — [answers/16007921](https://www.jotform.com/answers/16007921-how-to-allow-users-to-view-their-own-submissions-only)
- "how to let users access **only their own submission**" — [answers/17543123](https://www.jotform.com/answers/17543123-how-to-let-users-to-access-only-their-own-submission)
  > 💡 Aynı talep en az 4 ayrı thread'de tekrar ediyor → güçlü, tutarlı sinyal.

## 🔄 Durum Takibi — Son Kullanıcının Onay Durumu → [[Sikayet-Workflow]] / [[Sektorden-Dogan-Fikirler|Fikir A]]
- Burs başvuru yöneticisi: başvuranların *"login to see the status of their application"* (Jotform hesabı gerektirmeden) — [answers/5052504](https://www.jotform.com/answers/5052504-approval-status-letting-the-user-check-their-approval-status-in-jotform)
  > Jotform cevabı: *"no currently possible way..."* — Enterprise'da bile yok, **geliştiricilere eskale**.
- *"there is no link available... to view their own submission's approval status"* — [answers/12518471](https://www.jotform.com/answers/12518471-how-will-my-form-responders-track-approval-status)

## 📴 Offline → [[Sikayet-Offline]] / [[Oneri-2-Offline-Mode]]
- "can I use the app I created offline" → resmî cevap **hayır** — [answers/23130091](https://www.jotform.com/answers/23130091-can-i-use-the-app-i-created-offline) · [answers/4955237](https://www.jotform.com/answers/4955237-does-jotform-app-work-offline)
  > 💡 Field Service şablon sayfası "offline accessibility" derken destek "Apps offline çalışmıyor" diyor → **pazarlama/ürün çelişkisi**.

## 📊 Analitik → [[Sikayet-Analitik]] / [[Oneri-4-In-App-Analytics]]
- "Jotform Apps: Analytics support" — [answers/34711541](https://www.jotform.com/answers/34711541-jotform-apps-analytics-support)
- Google Analytics widget'ı Apps'te desteklenmiyor, **eskale edilmiş** — [answers/21496651](https://www.jotform.com/answers/21496651-how-do-i-add-google-analytics-to-my-app)

---

## 📌 Katalogdan Çıkarımlar
- **Tekrar = öncelik:** Portal (≥4 thread) ve push-zamanlama en sık tekrar eden iki tema → [[03-Firsat-Haritasi]] sıralamasını destekliyor.
- **"Escalated to developers" = içsel doğrulama:** Durum takibi, analitik (GA), portal taleplerinin **geliştiricilere eskale** edilmiş olması, bunların Jotform içinde de tanınan boşluklar olduğunu gösteriyor → [[05-Tavsiye-ve-Sonraki-Adimlar|dahili ticket sayısı]] argümanını güçlendirir.
- **Çelişki kozu:** Offline'daki pazarlama-vs-ürün çelişkisi sunumda en keskin tek kanıt.

## 🔗 İlgili
[[Musteri-Hikayeleri]] · [[06-Kaynaklar]] · [[00-MOC|← MOC]]

#jotform/apps #sikayet
