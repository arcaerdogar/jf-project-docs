---
tags: [jotform/apps, proje, firsat]
status: taslak
updated: 2026-06-24
---

# 🟡 Öneri 4 — Uygulama İçi "Özet/Durum" Analitik Elementi (EK ADAY)

> [!info] Haziran 2026 ek araştırmasından doğdu — bkz. [[Ek-Arastirma-Haziran-2026]]
> Statü: Ek aday. Ana üç öneriden sonra değerlendirilmeli.

## 🧩 Çözdüğü Şikayet
[[Sikayet-Analitik]] — Son kullanıcıya gerçek submission verisinin özetini gösteren bir element yok; mevcut "analitik" elementleri dekoratif (Day Countdown, Fancy Timer, Math Graphs).

## 📐 Kapsam
Builder'ın uygulamaya gömebileceği **veri-bağlı özet elementi**:
- **(a) Sayı kartları:** "Toplam başvuru", "Bu ay", "Onay bekleyen" gibi canlı sayaçlar (form/submission verisine bağlı).
- **(b) Basit grafik:** Zaman içinde başvuru (çubuk/çizgi) — tek form kapsamında.
- **(c) Filtre:** Kullanıcıya/duruma göre (Workflows Flow Status'una bağlanabilir → [[Sikayet-Workflow]]).

## 💡 Neden Değerli
- **Demosu çok görsel** — sunumda anında etki.
- [[Oneri-3-Portal]] ile **doğal komşu**: portal "benim verim"i gösterir, bu element "verinin özeti"ni.
- Veri zaten sistemde; iş, **görselleştirme elementi** yazmak.

## ⚠️ Dikkat
- "Genel analitik motoru" yazmaya kayarsa kapsam patlar → **tek form + sabit birkaç kart/grafik** ile sınırla.
- Enterprise **Insights** ile çakışmadığından emin ol (o builder-tarafı panel; bu son-kullanıcı tarafı element). Roadmap teyidi şart → [[05-Tavsiye-ve-Sonraki-Adimlar]].

## 📊 Skor (ön — bkz. [[03-Firsat-Haritasi]])
| Talep | Değer | Kapsam netliği | 1 ayda canlı |
|---|---|---|---|
| Orta | Orta-Yüksek | Orta | ✅ Orta |

İlgili öneriler: [[Oneri-1-Push-Scheduler]] ⭐ · [[Oneri-3-Portal]]
[[00-MOC|← MOC]]

#jotform/apps #proje #firsat
