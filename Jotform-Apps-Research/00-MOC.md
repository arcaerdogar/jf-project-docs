---
tags: [jotform/apps, moc]
status: olgun
updated: 2026-06-24
---

# 🗺️ Jotform Apps — Staj Projesi Araştırması (MOC)

> [!summary] Yönetici Özeti
> Jotform App Builder ekibinde stajım sırasında canlıya çıkma potansiyeli olan **gerçek bir ürün projesi** seçmek için bu bilgi tabanını hazırladım. Araştırma; mevcut ürün durumunu, forum/inceleme sitelerinden derlenen önceliklendirilmiş kullanıcı şikayetlerini ve bunlardan türetilmiş üç somut proje önerisini bir araya getiriyor. **Ana bulgu:** AI ve içerik elementleri tarafı yoğun yatırım almış; asıl boşluk "uygulama davranışı" katmanında (çevrimdışı çalışma, bildirim olgunluğu, kişiselleştirilmiş veri). **Ana öneri:** mevcut push altyapısı üstüne kurulan, kapsamı en net ve canlıya çıkma şansı en yüksek olan [[Oneri-1-Push-Scheduler|Zamanlanmış & Tekrarlayan Push + Bildirim Merkezi]].

## 📚 Notlara Giriş

### 01 — Bağlam
- [[Staj-ve-Hedef]] — Stajın amacı ve "canlıya çıkabilir gerçek proje" hedefi.
- [[Apps-Mevcut-Durum-2026]] — 2025–2026'da çıkan özellikler; yeniden icat edilmemesi gerekenler.
- [[Teknik-Bildirim-Mekanizmalari]] 🔧 🆕 — PWA'da push dışı bildirim yolları; neyin offline çalıştığı.

### 02 — Bulgular (önceliklendirilmiş şikayetler)
- [[Sikayet-Offline]] 🔴 — PWA uygulamalar internet yokken açılmıyor.
- [[Sikayet-Push]] 🔴 — Push var ama olgun değil (zamanlama/tetikleme/merkez yok).
- [[Sikayet-Portal]] 🟠 — Gerçek, kişiye filtrelenmiş müşteri/üye portalı eksik.
- [[Sikayet-Tasarim]] 🟡 — Daha fazla layout/CSS kontrolü talebi (geniş & öznel).
- [[Sikayet-Workflow]] 🟠 🆕 — Onay/iş akışı durumu uygulama içinde son kullanıcıya görünmüyor.
- [[Sikayet-Analitik]] 🟡 🆕 — Son kullanıcıya submission özeti/grafik gösteren element yok.
- [[Kapsam-Disi]] ⚪ — Proje kapsamı dışına alınan başlıklar ve gerekçeleri.
- [[Ek-Arastirma-Haziran-2026]] 🔬 — İkinci tur araştırmanın değişiklik günlüğü (yeni bulgular).
- [[Musteri-Hikayeleri]] 📖 🆕 — İsimli gerçek müşteri hikâyeleri + çıkarımlar.
- [[Talep-Kataloğu]] 🗂️ 🆕 — Birebir kullanıcı istekleri, boşluğa göre gruplu (kaynak linkli).
- [[Guncel-Durum-Dogrulama]] ✅ 🆕 — Boşluklar hâlâ açık mı? (Haz 2026 "boşa kürek" kontrolü + verdikt tablosu).

### 03 — Sentez
- [[03-Firsat-Haritasi]] — Talep / değer / kapsam netliği / 1 ayda canlı matrisi.

### 04 — Proje Önerileri
- [[Oneri-1-Push-Scheduler]] ⭐ — Zamanlanmış & tekrarlayan push + bildirim merkezi (ANA ÖNERİ).
- [[Oneri-2-Offline-Mode]] — App Builder uygulamaları için offline mod (en yüksek etki).
- [[Oneri-3-Portal]] — Kişiselleştirilmiş "Benim Verim" portal görünümü (dengeli).
- [[Oneri-4-In-App-Analytics]] 🆕 — Uygulama içi özet/durum analitik elementi (ek aday).
- [[Oneri-5-Saha-Modu]] 🛰️ 🆕 — Offline veri + zamanlanmış hatırlatma birleşik vizyonu (Oneri-1 + Oneri-2).

### 05–06 — Karar ve Kaynaklar
- [[05-Tavsiye-ve-Sonraki-Adimlar]] — Önerilen sıra, doğrulama adımları, sunum stratejisi.
- [[06-Kaynaklar]] — Tüm referanslar ve erişim notu.

### 07 — Sektör Analizi 🆕
- [[00-Sektor-MOC]] — Sektör alt-MOC: 9 mevcut sektör + beyaz alan + ana matris.
- [[Erisilebilir-Yeni-Sektorler]] — Kazanılabilir yeni sektörler (dernek, amatör spor, tarım…).
- [[Sektorden-Dogan-Fikirler]] — Sektörden doğan **tamamen yeni** proje fikirleri (Durum Takip, Omnichannel hatırlatma, RSVP, Üyelik).

---

## 🔗 Hızlı Eşleme: Şikayet → Öneri

| Şikayet | İlgili Öneri | Öncelik |
|---|---|---|
| [[Sikayet-Push]] | [[Oneri-1-Push-Scheduler]] ⭐ | 🔴 |
| [[Sikayet-Offline]] | [[Oneri-2-Offline-Mode]] | 🔴 |
| [[Sikayet-Portal]] | [[Oneri-3-Portal]] | 🟠 |
| [[Sikayet-Workflow]] 🆕 | [[Oneri-3-Portal]] (besler) | 🟠 |
| [[Sikayet-Analitik]] 🆕 | [[Oneri-4-In-App-Analytics]] | 🟡 |
| [[Sikayet-Tasarim]] | — (bkz. [[Kapsam-Disi]] tartışması) | 🟡 |

#jotform/apps
