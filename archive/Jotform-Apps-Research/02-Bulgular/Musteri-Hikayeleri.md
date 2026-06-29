---
tags: [jotform/apps, kanit, sektor]
status: olgun
updated: 2026-06-24
---

# 📖 Müşteri Hikâyeleri ve Senaryolar (+ Çıkarımlar)

> [!abstract] Amaç
> Araştırmada yüzeye çıkan **isimli gerçek müşteri hikâyeleri** ve somut kullanım senaryoları. Her birinin altında bir **çıkarım** var — boşluklarımızı ve fikirlerimizi gerçek dünyaya bağlar. Sunumda soyut iddiadan çok daha güçlü kanıt.

## 🏛️ Kamu / Yerel Yönetim
Kaynak: [5 ways government entities use Jotform](https://www.jotform.com/blog/ways-government-entities-use-jotform-enterprise/)

- **Three Rivers Park District** — Saha personeli için **iz/parkur denetimini OFFLINE yapan beyaz-etiketli mobil uygulama** kullanıyor.
  > 💡 **Çıkarım:** Markalı saha uygulaması istiyorlar ama offline ihtiyacı yüzünden **App Builder yerine Mobile Forms'a** itilmişler. Yani [[Sikayet-Offline|offline boşluğu]] müşteriyi başka bir ürüne kaydırıyor — [[Oneri-2-Offline-Mode]] tam da bu kaymayı durdurur.
- **County of Marin** — Saha anketini **tabletlerle** topluyor.
  > 💡 **Çıkarım:** Saha veri toplama gerçek ve aktif; cihaz hazır, eksik olan App Builder'ın offline davranışı.
- **Park County (MT)** — Fon/teçhizat **onay akışları + otomatik bildirim mektubu üretimi**.
  > 💡 **Çıkarım:** Durum iletişimini sağlamak için **manuel mektup üretimine** başvurmuşlar → [[Sikayet-Workflow|durum yansıması]] talebi, workaround inşa edecek kadar güçlü. [[Sektorden-Dogan-Fikirler|Durum Takip elementi]] bunu otomatikleştirir.
- **CiviLaw.Tech — Kansas Protection Order Portal** — Vatandaş portalı.
  > 💡 **Çıkarım:** Kişiselleştirilmiş vatandaş portalı talebi gerçek → [[Sikayet-Portal]] / [[Oneri-3-Portal]].
- **Tinley Park Public Library** ve **Miami-Dade okul yöneticisi** (personel devamı için bir **Jotform App**).
  > 💡 **Çıkarım:** Miami-Dade örneği eğitim + İK/operasyon kesişimi — App'ler şirket-içi araç olarak da kullanılıyor ([[Sektor-IK]]).

## 🤝 Nonprofit
Kaynaklar: [UK Charity](https://www.jotform.com/customer-stories/uk-charity/) · [Jotform customer stories](https://www.jotform.com/customer-stories/)

- **UK Charity** — Yılda **yüzlerce hibe başvurusu + ~4.000 oylama formu**, Salesforce entegrasyonu.
  > 💡 **Çıkarım:** Bu hacimde "başvurum ne durumda?" sorusu personele ağır yük bindirir → **başvuran-yüzlü self-service durum takibi** ([[Sektorden-Dogan-Fikirler|Fikir A]]) doğrudan operasyonel tasarruf. Segmentli/zamanlı bildirim ([[Oneri-1-Push-Scheduler]]) de buradan değer üretir.
- **TRIO Upward Bound**, **Scripture Union NI**, **Helping Hands Orillia** — program/gönüllü/etkinlik yönetimi.
  > 💡 **Çıkarım:** Nonprofit kullanımı program + gönüllü + etkinlik etrafında yoğunlaşıyor; hatırlatma/portal ihtiyaçları doğal.

## 🧱 Şablon-Temelli Senaryolar (ürünün kendi vaadi)
- **Eğitim:** School Parent App, School Management App — yoklama, ödev, veli iletişimi. → [[Sektor-Egitim]]
- **Emlak:** Open House App'te **"Start Check-In"** ile ziyaretçi check-in + taze geri bildirim. → [[Sektor-Emlak]]
- **Etkinlik:** Enterprise Event App — kayıt + gündem + konuşmacı profilleri tek app'te. → [[Sektor-Etkinlik]]
- **Saha:** Field Service App — Daily Reports, Task Logging, fotoğraf + dijital imza. → [[Sektor-Saha-Hizmetleri]]
- **İK:** Employee Portal — End of Day Report, **Leave Request**, **Employee Complaint**, Peer Performance Evaluation. → [[Sektor-IK]]
- **Perakende:** Store Apps — ürün sayfaları + 100+ ödeme. → [[Sektor-Perakende]]

---

## 🧭 Hikâyelerden Birleşik Çıkarımlar
1. **Boşluk = ürün kaybı:** En keskin örnek Three Rivers — müşteri markalı saha app'i istiyor ama offline yüzünden App Builder'ı bırakıp Mobile Forms'a geçiyor. Boşluklar yalnızca "eksik özellik" değil, **aktif kullanıcı kaybı**.
2. **Workaround = doğrulanmış talep:** Park County'nin manuel bildirim-mektubu üretmesi, durum iletişimi ihtiyacının emek harcatacak kadar güçlü olduğunu kanıtlıyor.
3. **Hacim = portal/durum ihtiyacı:** UK Charity'nin yüzlerce başvuru + 4.000 form hacmi, self-service durum/portal'ın "nice-to-have" değil **operasyonel zorunluluk** olduğunu gösteriyor.
4. **App'ler çok-amaçlı:** Kamu personel devamı, okul-içi operasyon → App'ler sadece dış-yüzlü değil, **şirket-içi araç** olarak da kullanılıyor; İK/operasyon senaryoları büyük.

## 🔗 İlgili
[[Talep-Kataloğu]] · [[00-Sektor-MOC]] · [[03-Firsat-Haritasi]] · [[00-MOC|← MOC]]

#jotform/apps #sikayet #sektor
