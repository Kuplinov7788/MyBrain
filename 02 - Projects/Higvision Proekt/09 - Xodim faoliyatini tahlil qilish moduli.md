---
type: feature-plan
project: Higvision Proekt
status: proposed
created: 2026-08-14
updated: 2026-08-18
tags: [camera-ai, phase-2, activity-analysis, roadmap]
---

# 2-faza — Xodim faoliyatini tahlil qilish

## Muhim qaror

**1-fazaga tegilmaydi.** Lokal video arxiv, xodimni aniqlash, IN/OUT, davomat va
Telegram hisobot bo‘yicha tasdiqlangan MVP rejasi o‘z holicha qoladi:

- [[10 - Kamera o‘rnatilgandan keyingi lokal MVP rejasi]]
- [[11 - Tomonlar masuliyati arxitektura va tasklar]]

2-faza 1-faza qabul testidan muvaffaqiyatli o‘tgandan keyin boshlanadi va risk hamda
xarajatni boshqarish uchun ikki mustaqil qismga bo‘linadi.

## Nega ikkiga bo‘lindi?

Klient xodimning kiyimi, samarali/bekor vaqti va bajargan ishlarini kamera orqali
aniqlashni xohlaydi. Bu talablar bir xil murakkablikda emas:

- forma va zona qoidalari tayyor detektorlar hamda sodda biznes qoidalari bilan tezroq
  bajariladi;
- “aynan qaysi ishni bajardi” degan xulosa maxsus video dataset, GPU, model o‘qitish va
  uzoq real sinov talab qiladi;
- birinchi guruh iqtisodiy natijani tez tekshiradi, ikkinchi guruh esa faqat shu natija
  foydali bo‘lsa investitsiya oladi.

## 2A — Nazorat qilinadigan tezkor AI

Batafsil: [[12 - Faza 2A tezkor AI kengaytmalari]]

Maqsad:

- kirishda liveness/anti-spoofing bilan davomatni mustahkamlash;
- oldindan kelishilgan forma belgilarini tekshirish;
- ish, xizmat, ombor, tanaffus va noma’lum zonalarda vaqtni hisoblash;
- harakat/faoliyatsizlik asosida qoida bo‘yicha vaqt segmentlarini chiqarish;
- xato hodisalarni administrator tuzatishi;
- Telegramga tasdiqlovchi kadrli hisobot yuborish.

Bu bosqich “xodim haqiqatan foydali ish qildi” deb hukm chiqarmaydi. U faqat kamera
ko‘rgan zona, harakat va kelishilgan belgilar bo‘yicha o‘lchanadigan faktlarni beradi.

Taxminiy pilot: **3–5 hafta**, 1 xodim + 1 ish hududi. Aniq muddat audit va real video
kelgandan keyin beriladi.

## 2B — Ilg‘or faoliyat analitikasi

Batafsil: [[13 - Faza 2B ilg‘or faoliyat analitikasi]]

Maqsad:

- kameralar orasida xodimni kuzatish (ReID/tracking);
- dastlab 3–5 ta aniq, kamerada ko‘rinadigan ish turini tanish;
- ishlar vaqt chizig‘i va ishonch ko‘rsatkichini chiqarish;
- AcuSeek yordamida matn bilan video qidirishni baholash;
- stabil algoritmlarni HEOP orqali kamera ichiga ko‘chirish imkoniyatini tekshirish;
- ko‘p xodim va ko‘p zonaga kengaytirish.

Bu bosqich lokal GPU server, belgilangan video dataset va har bir ish turi bo‘yicha alohida
qabul mezonini talab qiladi.

Taxminiy pilot: **6–10+ hafta**. Dataset sifati va ish turlarining murakkabligiga bog‘liq.

## Umumiy ketma-ketlik

```text
1-faza (o‘zgarmaydi)
Arxiv + yuz + IN/OUT + davomat + Telegram
                 |
                 v
Qabul testi va real aniqlik o‘lchovi
                 |
                 v
2A — forma + zona + liveness + qoida asosidagi faol/harakatsiz vaqt
                 |
                 v
Go / No-Go va iqtisodiy natija
                 |
                 v
2B — aniq ishlarni tanish + ReID + AcuSeek/HEOP + GPU
```

## 2A dan 2B ga o‘tish sharti

2B avtomatik boshlanmaydi. Quyidagilar bajarilgandagina alohida smeta qilinadi:

1. 1-faza davomat natijasi klient tomonidan qabul qilingan.
2. 2A zonalari va forma qoidalari real ishda foyda bergan.
3. Klient aniqlanishi kerak bo‘lgan 3–5 ta ish turini yozma tasdiqlagan.
4. Har bir ish turi kamera burchagida aniq ko‘rinishi isbotlangan.
5. Dataset yig‘ish va biometrik/video ma’lumotlarni saqlash tartibi kelishilgan.
6. GPU, disk va qo‘shimcha kamera xarajati iqtisodiy jihatdan tasdiqlangan.

## O‘zgarmas cheklovlar

- POS va ERP loyiha tarkibiga kirmaydi.
- 100% aniqlik va’da qilinmaydi.
- AI xodimning niyati yoki kamera ko‘rmaydigan ishini bilmaydi.
- “Samarali/bekor” faqat klient tasdiqlagan qoidalar asosida yoziladi.
- Ish haqi yoki intizomiy qaror faqat AI natijasiga tayanib avtomatik chiqarilmaydi.
- Hisobotda `aniqlanmadi` holati, ishonch darajasi va administrator tuzatishi bo‘ladi.
- Xodim roziligi, biometrik bazani ro‘yxatdan o‘tkazish, O‘zbekistonda saqlash va
  yo‘q qilish muddati huquqiy tartibga kiritiladi.

## Qaror

1-faza loyiha uchun barqaror asos bo‘lib qoladi. 2A tez iqtisodiy natijani tekshiradi;
2B esa faqat 2A natijasi o‘zini oqlasa, alohida AI investitsiyasi sifatida boshlanadi.

Bog‘liq: [[01 - Loyiha konteksti va talablar]] · [[08 - Rasmiy manbalar]]

