---
tags: [jotform/apps, firsat]
status: olgun
updated: 2026-06-24
---

# 🗺️ Fırsat Haritası

> [!abstract] Amaç
> [[02-Bulgular|Bulgular]]'daki şikayetleri dört eksende (talep / değer / kapsam netliği / 1 ayda canlı) puanlayıp önceliklendirir. Bu tablo, [[04-Proje-Onerileri|proje önerilerinin]] gerekçesidir.

## Öncelik Matrisi

| Fırsat | Talep | Değer | Kapsam netliği | 1 ayda canlı |
|---|---|---|---|---|
| **Zamanlanmış/tekrarlayan push + bildirim merkezi** | Yüksek | Yüksek | Çok net | ✅ Yüksek |
| **App'lerde offline mod (PWA)** | Yüksek | Çok yüksek | Orta | ⚠️ Orta (teknik ağır) |
| **Kişiselleştirilmiş "Benim Verim" portal** | Orta-Yüksek | Yüksek | Orta | ✅ Orta-Yüksek |
| **Uygulama içi onay/iş akışı durumu** 🆕 | Orta-Yüksek | Yüksek | Orta | ✅ Orta-Yüksek |
| **Uygulama içi analitik/özet elementi** 🆕 | Orta | Orta-Yüksek | Orta | ✅ Orta |
| **Gelişmiş tasarım/CSS kontrolü** | Orta | Orta | Düşük | ❌ Düşük |

> 🆕 = Haziran 2026 ek araştırmasında eklendi (bkz. [[Ek-Arastirma-Haziran-2026]]).

> [!tip] Birleşik vizyon
> İlk iki satır ("push olgunluğu" + "offline mod") tek persona altında birleştirilebilir → [[Oneri-5-Saha-Modu]]. Teknik gerçeklik: push offline'ken inemez; *zamanlama* offline'ı atlatır, *teslim* bağlantı gelince olur.

## Satır → Not Eşlemesi

| Fırsat | İlgili Şikayet | İlgili Öneri |
|---|---|---|
| Push olgunluğu | [[Sikayet-Push]] | [[Oneri-1-Push-Scheduler]] ⭐ |
| Offline mod | [[Sikayet-Offline]] | [[Oneri-2-Offline-Mode]] |
| Portal görünümü | [[Sikayet-Portal]] | [[Oneri-3-Portal]] |
| Onay/iş akışı durumu 🆕 | [[Sikayet-Workflow]] | [[Oneri-3-Portal]] (besler) |
| Uygulama içi analitik 🆕 | [[Sikayet-Analitik]] | [[Oneri-4-In-App-Analytics]] |
| Tasarım/CSS | [[Sikayet-Tasarim]] | — (bkz. [[Kapsam-Disi]]) |

## Okuma

> [!success] En Dengeli Seçim
> **Push** satırı: yüksek talep + yüksek değer + **çok net kapsam** + canlıya çıkma şansı yüksek. Risk/getiri oranı en iyi. → [[Oneri-1-Push-Scheduler]]

> [!warning] En Yüksek Etki, Daha Yüksek Risk
> **Offline** satırı: değer "çok yüksek" ama teknik olarak ağır (service worker + sync + çakışma). Ancak agresif sınırlanmış MVP ile değerlendirilebilir → [[Oneri-2-Offline-Mode]].

> [!info] Düşük Öncelik
> **Tasarım/CSS** satırı: kapsam netliği ve canlıya çıkma düşük → ana proje değil.

## 🏭 Sektörel Doğrulama (Haziran 2026)
9 mevcut sektör ihtiyaçlarıyla incelendiğinde örüntü netleşti → [[00-Sektor-MOC]]:
- **Push** boşluğu **9 sektörün 7'sinde** ilk iki öncelikte (en geniş yankı).
- **Portal** 5/9; **Offline** & **Workflow** 3/9 ama kendi sektörlerinde *zorunlu*.
- Stratejik: tek boşluk yatırımı bir mevcut + bir yeni sektör kümesi açıyor → [[Erisilebilir-Yeni-Sektorler]].
- Sektörden doğan yeni fikir adayları (ör. **Durum Takip elementi**) → [[Sektorden-Dogan-Fikirler]].

[[00-MOC|← MOC]] · Devam: [[05-Tavsiye-ve-Sonraki-Adimlar]]

#jotform/apps #firsat
