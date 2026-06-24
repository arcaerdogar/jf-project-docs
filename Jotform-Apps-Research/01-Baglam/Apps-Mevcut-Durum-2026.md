---
tags: [jotform/apps, baglam]
status: olgun
updated: 2026-06-24
---

# 📦 Apps — Mevcut Durum (2025–2026)

> [!warning] Amaç
> Bu not, **yeniden icat edilmemesi gereken** özellikleri listeler. Bir proje önerisi seçmeden önce, bunların zaten var olduğunu bilmek gerekir — boşluk bunların *arasında* kalan yerde.

## 2025–2026'da Çıkan / Olgunlaşan Özellikler

### 🤖 AI Tarafı (yoğun yatırım)
- **Copilot / AI App Generator:** Prompt'tan uygulama üretme. Doğal dilden tam bir uygulama iskeleti çıkarıyor.
- **AI Chatbot elementi:** Uygulamaya eklenebilen, gömülü sohbet elemanı.
- **ChatGPT App Marketplace entegrasyonu** (Mart 2026 duyurusu).

### 🔔 Push Notifications (beta'dan çıktı, yaygınlaştı)
- İzin modalı, gönderim geçmişi, temel metrikler: **subscriber, delivered, CTR**.
- ⚠️ **ANCAK hâlâ yalnızca anlık/manuel gönderim — zamanlama yok.** → boşluk için bkz. [[Sikayet-Push]] ve [[Oneri-1-Push-Scheduler]].

### 🧱 App Elements Kütüphanesi
List, Card, Image Gallery, Slideshow, Video, Table, Rich Text, Heading, Button, Divider, Spacer ve **"My Submissions"** arşivi.
- "My Submissions" var ama kişiye filtrelenmiş portal deneyimi kısıtlı → bkz. [[Sikayet-Portal]].

### 🛒 Ticaret
- **Store Builder & Donation Apps** — 40+ ödeme geçidi desteği.

### 📲 Dağıtım Modeli
- **PWA (Progressive Web App):** Ana ekrana eklenebiliyor, **ama App Store / Play Store'a yüklenemiyor.**
- Bu **bilinçli bir mimari tercih** — bir eksiklik değil. (Bu yüzden "store'a yayınlama" projesi [[Kapsam-Disi]].)

---

## 🧭 Çıkarım (Boşluk Analizi)

> [!important] Ana Tez
> **AI ve içerik elementleri tarafı yoğun yatırım almış.** Asıl boşluk **"uygulama davranışı"** katmanında:
> - **Çevrimdışı çalışma** → [[Sikayet-Offline]]
> - **Bildirim olgunluğu** (zamanlama, tetikleme, merkez) → [[Sikayet-Push]]
> - **Kişiselleştirilmiş veri** (kullanıcıya özel görünüm) → [[Sikayet-Portal]]

Bu üç eksen, [[03-Firsat-Haritasi|Fırsat Haritası]]'nın temelini oluşturuyor.

[[00-MOC|← MOC'a dön]] · İlgili: [[Staj-ve-Hedef]]

#jotform/apps
