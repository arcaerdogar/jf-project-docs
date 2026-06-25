---
tags: [jotform/apps, baglam, kaynak]
status: olgun
updated: 2026-06-24
---

# 🔬 Ek Araştırma — Haziran 2026 (Değişiklik Günlüğü)

> [!abstract] Amaç
> İlk vault kurulduktan sonra, [[06-Kaynaklar|doğrulanmış kaynaklar]] üzerinden yapılan ikinci tur araştırmanın çıktıları. Burada yalnızca **yeni / farklı** bulgular kayıtlı; mevcut şikayetleri yalnızca doğrulayan sonuçlar ilgili notlarda işaretlendi.

## ✅ Mevcut Bulguları Doğrulayan Sonuçlar
- **Push'ta zamanlama yok** — resmî yardım sayfası bunu netleştiriyor; yorumlarda zamanlama soruları yanıtsız. → [[Sikayet-Push]] teyit.
- **Submission-tetikli push** Form Builder tarafında zaten mümkün; App push'unda olgun tetikleme akışı hâlâ zayıf. → [[Oneri-1-Push-Scheduler]] kapsamını rafine etti.
- **Push personalizasyonu** (form alanlarını mesaja gömme) zaten var → scheduler'ı bunun üstüne kurmak mantıklı.

## 🆕 Yeni Bulgular

### 1. Push hedef-kitle segmentasyonu yok
Resmî dokümana göre bildirim **tüm abonelere aynı anda** gidiyor; "kime göndereyim?" seçimi yok. Bu, [[Oneri-1-Push-Scheduler]] için **opsiyonel 4. dilim** (basit segment/etiket) olabilir.

### 2. Uygulama içi analitik/veri görselleştirme boşluğu
- Son kullanıcıya submission özeti gösteren element yok; mevcut "analitik" elementleri dekoratif.
- **Google Analytics widget'ı Apps'te desteklenmiyor** (geliştiricilere eskale).
- Enterprise **Insights** var ama ayrı/builder-tarafı.
→ Yeni not: [[Sikayet-Analitik]] · Yeni öneri: [[Oneri-4-In-App-Analytics]]

### 3. Workflows ↔ Apps köprüsü zayıf
- Güçlü Workflows/Approvals ürünü (çok adımlı/paralel onay, Group Approval, assignee, Flow Status) var.
- Ama onay durumu **App içinde son kullanıcıya yansımıyor**; onay-sonrası güncellemenin başka yüzeylere taşınmaması tekrar eden tema.
→ Yeni not: [[Sikayet-Workflow]] — [[Oneri-3-Portal]]'ı teknik olarak güçlendiriyor.

## 🟦 Açık Uçlu İpuçları (doğrulanmamış — fikir aşaması)
> [!warning] Bunlar bulgu değil, **kovalanacak ipucu**. Sunumda kanıt olarak kullanma; önce teyit et.

### a. Uygulama içi koşullu görünürlük (conditional logic)
- Forms tarafında koşullu göster/gizle güçlü ve olgun. **Ancak App Builder element düzeyinde**, kullanıcıya/duruma göre element gösterip gizleme net biçimde **doğrulanamadı** — arama sonuçları çoğunlukla Form koşullarına işaret etti.
- Eğer App elementlerinde per-user/koşullu görünürlük yoksa, bu [[Sikayet-Portal]] ve [[Oneri-4-In-App-Analytics]] ile birleşebilecek **potansiyel bir boşluk**. → Forum + builder içi deneyle teyit edilmeli.
- Yan not: Forms koşullarında bile yalnızca **OR** mantığı var, **AND** talebi açık (Haziran 2025 sinyali) — App tarafına da yansıyabilir.

## ⚠️ Mevcut Araştırmanın Sınırları
- **İnceleme siteleri çekilemedi:** G2 (403) ve research.com (403) erişim engeli verdi; Capterra/Trustpilot/GetApp henüz taranmadı. İnceleme-sitesi kaynaklı somut "cons" listesi **hâlâ boş** — ikincil kanıt olarak sonra madenlenebilir (bkz. [[06-Kaynaklar]]).
- En güçlü kanıt yine **forum feature-request thread'leri** (birincil); inceleme siteleri yalnızca destekleyici olacak.

## ⏭️ Sonraki Doğrulama
Bu üç yeni bulgu için de [[05-Tavsiye-ve-Sonraki-Adimlar]]'daki doğrulama adımları geçerli: dahili ticket sayısı + roadmap/sahiplik teyidi. Yukarıdaki açık uçlu ipuçları için ek olarak: builder içinde hızlı deney + forum teyidi.

[[00-MOC|← MOC]] · [[06-Kaynaklar]]

#jotform/apps #kaynak
