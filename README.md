# Jotform Apps — Bildirim & E-posta Gönderim Sistemi

Bu repo, **Jotform App Builder uygulamaları için çok-kanallı (push + e-posta) gönderim sistemi** projesine odaklıdır: anlık / cron / scheduled gönderim, koşullu tetikleme ve uygulama içi bildirim merkezi. Proje, birden çok aday arasından seçildi (Haziran 2026).

## 📂 Yapı

| Yol | İçerik |
|---|---|
| **`docs/`** | Odaklı çalışma seti — implementasyon için okunacak yer. |
| `docs/00-Proje-Ozeti.md` | Proje brifi: problem, kapsam, talep kanıtı, dilimleme, açık sorular. |
| `docs/01-Teknik-Notlar.md` | Bildirim mekanizmaları, push fiziği, elenen alternatifler. |
| `docs/02-Kaynaklar.md` | Bildirimle ilgili referanslar. |
| `docs/03-Gelistirme-Ortami.md` | Mimari kısıt: iki backend reposu (ana=salt-istek, intern API=düzenlenebilir/kısıtlı) + request akışları. |
| **`docs/Gelistirme-Asamalari/`** | **Yol haritası** — geliştirme aşamaları (01 Cron Motoru = aktif odak). Başlangıç: `00-Yol-Haritasi.md`. |
| `archive/` | Projeyi seçmeye götüren **tam araştırma vault'u** (37 not) + Obsidian artıkları. Implementasyon için **gerekli değil**; yalnızca derin bağlam için. |

## 🎯 Özet
Push var ama olgun değil; e-posta app özelinde düzenlenemiyor. **Kanal × Gönderim Türü × Tetikleme** ekseninde tek bir gönderim motoru kuruyoruz. **Kanallar asimetrik (Haz 2026 kısıtı):** push yalnızca ana repodan tetiklenir ve **herkese broadcast** (cron/scheduled var; transactional/kişi-bazlı **yok**); **e-posta tam kapsam** (anlık/cron/scheduled + transactional + koşullu + kişi-bazlı). Artı: gönderim geçmişi/durum takibi için bildirim merkezi. Detay: [docs/00-Proje-Ozeti.md](docs/00-Proje-Ozeti.md).

## ⏭️ Sonraki Adım
İmplementasyon planı ayrı bir oturumda işlenecek. Başlangıç noktası: `docs/00-Proje-Ozeti.md`. İmplementasyon kodu bu repoya eklenecek.

> **Not (context):** `archive/` klasörünü varsayılan olarak yüklemeyin — odak `docs/`'tedir.
