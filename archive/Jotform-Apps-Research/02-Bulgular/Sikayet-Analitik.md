---
tags: [jotform/apps, sikayet, firsat]
status: taslak
updated: 2026-06-24
---

# 🟡 Şikayet: Uygulama İçi Analitik / Veri Görselleştirme Boşluğu

> [!info] Kaynak: Haziran 2026 ek araştırması (bkz. [[Ek-Arastirma-Haziran-2026]])
> Öncelik: Orta (yeni bulgu — doğrulama gerekiyor)

## Problem
App Builder ile yapılan bir uygulamanın **son kullanıcısına**, toplanan verinin özetini (gönderim sayısı, basit grafik, ilerleme/sayı kartları) uygulama içinde göstermek **zayıf/eksik.** Bugünkü "analitik" elementleri esas olarak dekoratif: **Day Countdown, Fancy Timer, Math Graphs** — gerçek submission verisini görselleştirmiyorlar.

## İki Ayrı Eksik

### 1. Son kullanıcıya yönelik özet/dashboard elementi yok
- Builder, "şu ana kadar 142 başvuru / bugün 12" gibi canlı bir sayaç ya da basit grafik kartını uygulamaya **gömemiyor**.
- Topluluk talebi mevcut: *Jotform Apps: Analytics support* thread'i.

### 2. Builder'a yönelik kullanım analitiği parçalı
- **Google Analytics widget'ı Jotform Apps için desteklenmiyor** — talep geliştiricilere **eskale edilmiş** ama henüz yok.
- Enterprise tarafında **Insights** paneli var (trafik, indirme, aktif ziyaretçi, etkileşim oranı) — ama bu ayrı/Enterprise katmanı; uygulamanın *içine* gömülen, son kullanıcının gördüğü bir şey değil.

## Neden Önemli
- "Benim Verim" portalı ([[Sikayet-Portal]]) ile doğal komşu: kullanıcı kendi verisini görüyorsa, bir adım sonrası **özet/durum kartı**.
- Demosu görsel ve net; element bazlı, sınırlanabilir kapsam.

## Değerlendirme (ön)
| Boyut | Durum |
|---|---|
| Talep | Orta (sinyal var, forum/Insights talebi) |
| Değer | Orta-Yüksek |
| Kapsam netliği | Orta |
| 1 ayda canlı | ✅ Orta |

> [!note] Bağlantı
> Bu bulgu → [[Oneri-4-In-App-Analytics]] (ek aday öneri) ile ele alınıyor. [[Sikayet-Portal]] ile birlikte düşünülebilir.

[[03-Firsat-Haritasi]] · [[00-MOC|← MOC]]

#jotform/apps #sikayet #firsat
