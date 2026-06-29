---
tags: [jotform/apps, bildirim, mimari]
status: olgun
updated: 2026-06-26
---

# 🏗️ Geliştirme Ortamı & Mimari Kısıtlar

> [!warning] İmplementasyon için belirleyici kısıt
> Sistem iki backend reposu üzerine kuruluyor ve **yalnızca biri düzenlenebilir**. Bu, request akışlarını ve nerede kod yazılacağını doğrudan belirler. Detaylar (intern API'nin tam imkânları) **erişim sağlanınca** netleşecek; bu not o zaman güncellenecek.

## Repo Topolojisi
| Repo | İstek atılabilir? | Düzenlenebilir? | Not |
|---|---|---|---|
| **Ana Jotform reposu** | ✅ | ❌ | Kara kutu — yalnızca çağırırız (mevcut push/e-posta/form altyapısı burada). |
| **Intern API** | ✅ | ✅ | Bizim yazdığımız yer. **İmkânları kısıtlı** (kapsam erişimle detaylandırılacak). |
| **Frontend (App)** | İkisine de erişir | ✅ | Akışı orkestre edebilir. |

→ **Tüm yeni backend kodumuz intern API'de yaşar.** Ana repodaki yetenekleri yalnızca **istek atarak** kullanırız.

## Request Akışları

### 🔧 Varsayılan workaround — frontend köprü
Intern API kısıtlı olduğundan, birçok iş için frontend köprü görevi görür:
```
Frontend ──request──▶ Ana Repo
Frontend ◀─response── Ana Repo
Frontend ──bilgiyi yaz──▶ Intern API
```
Yani frontend: ana repodan veriyi alır, intern API'ye geri yazar. (Intern API ana repoya kendisi ulaşamadığında/kuramadığında.)

### ⭐ Tercih edilen — doğrudan sunucu-sunucu (imkân olursa)
Frontend'i köprü yapmadan, intern API doğrudan ana repoya gider:
```
Intern API ──request──▶ Ana Repo
Intern API ◀─response── Ana Repo
```
Daha temiz, daha az tur, frontend'e iş bindirmez. **Mümkünse bu tercih edilir.**

## Tasarım İmaları (bu projeye)
- **Orkestrasyon bizde:** Gönderim kuralları, scheduler/cron, koşullu tetikleme, bildirim merkezi mantığı = intern API'de (düzenlenebilir).
- **✅ Teyitli kısıt — Push:** Push **yalnızca ana repodan** tetiklenebiliyor ve **kişi-bazlı değil, herkese broadcast**. Yani scheduler/cron zamanlaması intern API'de tutulur, ateşlenince **ana repoya broadcast isteği** atılır. Transactional/kişi-bazlı/segment push **mümkün değil** → bunlar e-postaya taşındı. (Bkz. [00-Proje-Ozeti](00-Proje-Ozeti.md) yetenek matrisi.)
- **E-posta:** Tam kapsam (transactional, kişi-bazlı, koşullu). *(Doğrulanacak: e-posta gönderimi/kişi-bazlı hedefleme intern API'den mi yapılabiliyor, yoksa ana repoya mı delege gerekiyor?)*
- **Akış kararı özellik bazlı:** Her özellik için "doğrudan intern→ana mı, yoksa frontend köprü mü?" tercihi, intern API'nin o uca erişip erişemediğine göre verilecek. *(Push tetikleme için bu akış zaten gerekli — intern API ana repoya ulaşabiliyorsa doğrudan, değilse frontend köprü.)*

## ❓ Erişim Sağlanınca Netleşecek
- Intern API'nin tam imkân/kapsamı (hangi endpoint'ler, hangi yetkiler).
- Intern API ana repoya **doğrudan** istek atabiliyor mu (sunucu-sunucu mümkün mü)?
- Ana reponun hangi endpoint'leri push/e-posta/form-event için kullanılabilir.
- Kimlik/yetki (auth) iki repo arası nasıl taşınıyor.

İlgili: [00-Proje-Ozeti](00-Proje-Ozeti.md) · [01-Teknik-Notlar](01-Teknik-Notlar.md)
