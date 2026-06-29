---
tags: [jotform/apps, proje, firsat]
status: taslak
updated: 2026-06-24
---

# 🛰️ Öneri 5 — "Saha Modu": Offline Veri + Zamanlanmış Hatırlatma (BİRLEŞİK VİZYON)

> [!info] Kaynak: kullanıcı fikri (Haziran 2026) — [[Oneri-1-Push-Scheduler]] + [[Oneri-2-Offline-Mode]] sentezi.
> Statü: Vizyon/kuzey yıldızı. MVP olarak **tek yarıya** sabitlenmeli.

## 💡 Fikir
Tek persona — **saha/etkinlik çalışanı** — altında iki en yüksek-değerli bulguyu birleştir:
*"Sinyalsiz alanda form doldur (offline kuyruk); kapsama girince hem verin sync olur hem de kaçırdığın zamanlanmış hatırlatmalar iner."*

## 🧩 Çözdüğü Şikayetler
- [[Sikayet-Offline]] — veri *toplama* tarafı.
- [[Sikayet-Push]] — zamanlanmış *hatırlatma* tarafı.

## ⚠️ Teknik Gerçeklik (sunumda önce bunu bil)
Push **doğası gereği sunucu-tetikli**: sunucu → push servisi (FCM/APNs) → cihaz. Bildirimin *teslimi* için bağlantı gerekir. Telefon tamamen offline'ken ağ üzerinden bildirim inemez.

| Yorum | Çalışır mı? | Mekanizma |
|---|---|---|
| **A. Zamanlama sunucuda; teslim bağlantı gelince** | ✅ Evet | Schedule sunucuda; tetiklenince push servisi **TTL ile kuyruğa alır**, cihaz online olunca teslim eder. |
| **B. Telefon tamamen offline, uygulama yerel bildirim fırlatır** | ❌ Güvenilir değil | PWA'da cross-platform güvenilir "zamanlanmış yerel bildirim" API'si yok; `TimestampTrigger` standartlaşmadı, **iOS PWA desteklemiyor.** |

> [!danger] Yanlış anlaşılma riski
> "Telefon uçak modundayken hatırlatma çıkar" cümlesi **PWA'da, özellikle iOS'ta inşa edilemez.** Doğru çerçeve: *zamanlama offline'ı atlatır* (kaçmaz), bildirim ise *bağlantı gelince* iner.

> [!note] Push dışı bildirim yolları
> Bildirimi push dışında tetiklemenin sınırları ve **offline çalışan tek yol (uygulama içi merkez)** için ayrıntı: [[Teknik-Bildirim-Mekanizmalari]]. Alternatif kanal: sunucu scheduler → e-posta/SMS (Jotform altyapısı hazır).

## ✅ Buildable Versiyon (dürüst kapsam)
Tek feature değil, tek persona altında iki tamamlayıcı parça:
- **Offline (veri):** service worker + IndexedDB kuyruk + online'da otomatik sync. (bkz. [[Oneri-2-Offline-Mode]] MVP sınırı)
- **Push (hatırlatma):** sunucuda scheduler + tekrarlama; çalışan sinyalsizken schedule kaçmaz, bağlantı gelince hatırlatma iner. (bkz. [[Oneri-1-Push-Scheduler]])

## 🔶 Risk & Tavsiye
- Offline **tek başına** bile bir ay için riskli ([[Oneri-2-Offline-Mode]]); ikisini birleştirmek riski **artırır**.
- **Birleşik fikri "vizyon" olarak sun, MVP'yi tek yarıya sabitle.** Gerçekçi sıra: önce [[Oneri-1-Push-Scheduler]] (kapsamı en net) → offline'ı faz 2'de bağla.
- Sunum gücü: "neden ikisi birlikte?" hikâyesi tek tek önerilerden daha akılda kalıcı; ama teknik gerçekliği önden söyle → güven kazandırır.

## 📊 Skor (ön)
| Talep | Değer | Kapsam netliği | 1 ayda canlı |
|---|---|---|---|
| Yüksek | Çok yüksek | Düşük-Orta (birleşik) | ⚠️ Düşük-Orta — tek yarıya sabitlenirse ✅ |

İlgili: [[Oneri-1-Push-Scheduler]] ⭐ · [[Oneri-2-Offline-Mode]] · [[03-Firsat-Haritasi]]
[[00-MOC|← MOC]]

#jotform/apps #proje #firsat
