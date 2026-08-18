---
type: phase-plan
project: Higvision Proekt
phase: 2B
status: gated
created: 2026-08-18
updated: 2026-08-18
tags: [camera-ai, phase-2b, action-recognition, reid, acuseek, heop]
---

# Faza 2B — Ilg‘or faoliyat analitikasi

## Boshlanish sharti

Bu faza faqat [[12 - Faza 2A tezkor AI kengaytmalari|2A]] real foyda bergani va klient
qo‘shimcha investitsiyani tasdiqlagandan keyin boshlanadi. Hozirgi status: **gated**.

## Maqsad

Kamerada aniq ko‘rinadigan, klient oldindan tanlagan ish turlarini aniqlash, xodimni
bir nechta kamerada kuzatish va ishonch darajasi bilan faoliyat timeline’ini yaratish.

## Scope

### 1. Kameralararo kuzatish

- har bir kamerada tracking ID;
- yuz va tashqi ko‘rinish belgilaridan ReID;
- kamera A dan yo‘qolib, kamera B da paydo bo‘lishni bog‘lash;
- ishonch past bo‘lsa avtomatik birlashtirmaslik;
- admin tomonidan tracklarni birlashtirish/ajratish.

### 2. Oldindan belgilangan ishlarni tanish

Dastlab faqat 3–5 ta aniq ish turi:

- mijozga xizmat ko‘rsatish;
- mahsulotni polkaga joylash;
- yuk ko‘tarish/tashish;
- tozalash;
- ish joyini tartibga keltirish.

Har bir ish uchun boshlanish/tugash qoidasi, minimal davomiylik, kerakli kamera burchagi
va qabul mezoni alohida yoziladi.

### 3. Dataset va model

- real ish jarayonidan rozilik bilan videolar yig‘ish;
- yuz va maxfiy hududlarni kerak bo‘lsa maskalash;
- ish segmentlarini administrator bilan belgilash;
- train/validation/test to‘plamlarini alohida saqlash;
- baseline model va xato turlarini o‘lchash;
- yangi uniforma, joylashuv yoki kamera o‘zgarsa model drift nazorati.

### 4. AcuSeek — qo‘shimcha qidiruv qatlami

Yangi Hikvision AcuSeek NVR/HikCentral orqali tabiiy tilda:

- “qora kiyimdagi odam”;
- “quti ko‘targan xodim”;
- “falon vaqt va joydagi odam”

kabi video qidiruvni alohida demo qilish mumkin. Bu davomat yoki ish klassifikatorining
o‘rnini bosmaydi; incident tekshirish vaqtini kamaytiradigan optional modul.

Rasmiy manba:
[Hikvision AcuSeek](https://display.hikvision.com/mena-en/products/IP-Products/Network-Video-Recorders/)

### 5. HEOP — edge deployment

Serverdagi model barqarorlashgach, yengil qismini kamera ichida ishlatish baholanadi:

- server va tarmoq yukini kamaytirish;
- kamera ichida event yaratish;
- faqat metadata va kerakli kadrni yuborish;
- internet/server uzilganda lokal aniqlashni davom ettirish.

HEOP uchun kamera modeli/suffix/firmware mosligi, TPP tasdig‘i, agreement, SDK, litsenziya
va kamera resurslari tekshiriladi. 1.5 TOPS kamerada barcha og‘ir modelni ishlatish mumkin
deb oldindan va’da qilinmaydi.

Rasmiy manba: [Hikvision HEOP 2.0](https://tpp.hikvision.com/tpp/HEOP)

## Arxitektura

```text
Ichki kameralar → lokal GPU inference → tracking / ReID
                              |             |
                              v             v
                         Action models → Activity events
                                               |
2A timeline + davomat -------------------------|
                                               v
                                    Activity Timeline DB
                                               |
                              Admin review + Telegram report

Optional: AcuSeek NVR → matn bilan video qidirish
Optional: HEOP → stabil yengil modelni kamera ichiga ko‘chirish
```

## Biz qiladigan tasklar

- [ ] 2B.1 — Klient bilan 3–5 ta ish turini muzlatish.
- [ ] 2B.2 — Har bir ish uchun kamera ko‘rinishi va test protokoli.
- [ ] 2B.3 — Biometrik/video dataset siyosati va rozilik hujjati.
- [ ] 2B.4 — Dataset yig‘ish, anonimlashtirish va labeling.
- [ ] 2B.5 — Lokal GPU/server benchmark va smeta.
- [ ] 2B.6 — Multi-camera tracking/ReID baseline.
- [ ] 2B.7 — Har bir ish turi uchun baseline model/qoidalar.
- [ ] 2B.8 — Ish segmentlari deduplikatsiyasi va timeline.
- [ ] 2B.9 — Confidence, UNKNOWN va admin review.
- [ ] 2B.10 — Kunlik faoliyat hisoboti va tasdiqlovchi kliplar.
- [ ] 2B.11 — Turli yorug‘lik, to‘siq va ko‘p odamli load test.
- [ ] 2B.12 — AcuSeek demo va iqtisodiy baho.
- [ ] 2B.13 — HEOP feasibility/TPP/licensing tekshiruvi.
- [ ] 2B.14 — Klient qabul testi va kengaytirish smetasi.

## Klientdan kerak

1. Har bir ish turining aniq ta’rifi va video misollari.
2. Kameralar ko‘rmaydigan ishlar ro‘yxati.
3. Dataset yig‘ishga ruxsat va xodim roziligi.
4. Noto‘g‘ri AI xulosasini kim tekshirishi.
5. GPU/NVR/qo‘shimcha kamera budjeti.
6. Video, yuz embedding, event va kliplarni saqlash muddatlari.
7. AcuSeek qidiruvi kerak bo‘ladigan real biznes ssenariylari.

## Qabul mezonlari

- aniqlik har bir ish turi bo‘yicha alohida o‘lchanadi;
- precision, recall, false event va UNKNOWN ko‘rsatiladi;
- bir faoliyat boshqa faoliyat bilan adashishi confusion matrix’da ko‘rsatiladi;
- natija yangi kun/yangi xodim videolarida tekshiriladi;
- xulosa tasdiqlovchi klip bilan bog‘lanadi;
- AI natijasini admin tuzatishi mumkin;
- tizim noaniq holatda fakt uydirmaydi.

## Taxminiy muddat

- talab/dataset dizayni: 1 hafta;
- dataset yig‘ish va labeling: 2–4+ hafta;
- model va integratsiya: 3–6+ hafta;
- real pilot: 2 hafta;
- umumiy: **6–10+ hafta**, dataset va ish turlariga qarab uzayishi mumkin.

## 2B tarkibiga kirmaydi

- xodimning niyati yoki kayfiyatini aniqlash;
- kamera ko‘rmagan kompyuter/telefon ichidagi ishni bilish;
- istalgan yangi ishni examplesiz avtomatik tanish;
- AI xulosasi asosida avtomatik jarima yoki ish haqi;
- 100% aniqlik;
- POS va ERP.

## Yakuniy natija

Klientga “AI hamma narsani biladi” degan va’da emas, balki oldindan tasdiqlangan ishlar
bo‘yicha o‘lchangan aniqlik, UNKNOWN holati va tasdiqlovchi video bilan audit qilinadigan
faoliyat hisoboti beriladi.

Bog‘liq: [[09 - Xodim faoliyatini tahlil qilish moduli]] · [[12 - Faza 2A tezkor AI kengaytmalari]]

