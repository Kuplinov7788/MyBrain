---
title: AI kamera loyihasi — fazalar bo‘yicha hisobot
project: Hikvision AI Camera
status: Client-ready
updated: 2026-08-18
tags:
  - hikvision
  - ai-camera
  - attendance
  - analytics
  - client-report
---

# AI kamera loyihasi — fazalar bo‘yicha hisobot

Loyiha ikki asosiy fazada amalga oshiriladi. Birinchi faza o‘zgartirilmaydi. Ikkinchi faza xavfni kamaytirish va natijani bosqichma-bosqich tekshirish uchun **2A** va **2B** qismlarga bo‘linadi.

| Faza | Asosiy savol | Klient oladigan natija |
|---|---|---|
| 1-faza | Xodim qachon keldi va ketdi? | Davomat va ish joyida bo‘lgan vaqt hisoboti |
| 2A-faza | Xodim qayerda va qancha vaqt faol bo‘ldi? | Zona, ish formasi va faollik bo‘yicha analitika |
| 2B-faza | Xodim aynan qanday ish bajardi? | Oldindan belgilangan ishlarni AI orqali aniqlash |

## 1-faza — Davomat va kirish-chiqish tizimi

Bu fazada biz:

- kameralarni lokal serverga ulaymiz;
- videoni lokal xotiraga yozamiz;
- xodimlarning yuz bazasini shakllantiramiz;
- xodimlarni yuz orqali taniymiz;
- kirish va chiqish vaqtlarini aniqlaymiz;
- takroriy aniqlashlarni bitta hodisaga birlashtiramiz;
- xodimning birinchi kelgan va oxirgi ketgan vaqtini hisoblaymiz;
- kun davomida tashqariga chiqib qaytgan vaqtlarini hisoblaymiz;
- kunlik, haftalik va oylik davomat hisobotlarini tayyorlaymiz;
- hisobotlarni Telegram orqali yuboramiz;
- tanilmagan yuzlarni `UNKNOWN` sifatida saqlaymiz;
- noto‘g‘ri hodisalarni administrator tuzatishi uchun imkoniyat yaratamiz.

### 1-faza natijasi

Klient quyidagi ma’lumotlarni oladi:

> Xodim kim, qachon keldi, qachon ketdi, kun davomida qancha vaqt tashqarida bo‘ldi va ish joyida jami qancha vaqt qatnashdi.

**Muhim:** birinchi faza xodimning unumdorligini emas, faqat davomat va ish joyida bo‘lgan vaqtini hisoblaydi.

## 2A-faza — Tezkor AI nazorati

Bu faza birinchi faza barqaror ishlagandan keyin boshlanadi.

Bu fazada biz:

- yuzni surat yoki telefon videosi orqali aldashga qarshi himoyani tekshiramiz;
- xodimda belgilangan ish formasi mavjudligini nazorat qilamiz;
- oldindan kelishilgan kiyim yoki ranglarni tekshiramiz;
- ish joyini ish, mijozlar, ombor, dam olish va boshqa zonalarga ajratamiz;
- xodimning har bir zonada qancha vaqt bo‘lganini hisoblaymiz;
- kelishilgan qoidalar asosida faol, harakatsiz va tanaffus vaqtini chiqaramiz;
- shubhali natijalarni tekshirish uchun kadr yoki qisqa video saqlaymiz;
- natijalarni administrator paneli va Telegram hisobotiga qo‘shamiz.

### 2A-faza natijasi

Klient quyidagi ma’lumotlarni oladi:

> Xodim ish formasida bo‘lganmi, qaysi zonalarda yurgan va kelishilgan mezonlarga ko‘ra qancha vaqt faol, harakatsiz yoki tanaffusda bo‘lgan.

**Muhim:** bu haqiqiy unumdorlikka yakuniy baho emas. Natija kamera orqali ko‘rish va o‘lchash mumkin bo‘lgan, oldindan kelishilgan qoidalarga asoslanadi.

## 2B-faza — Xodim bajargan ishlarni aniqlash

Bu murakkab AI qismi bo‘lib, faqat 2A-faza natijasi foydali deb topilgandan keyin boshlanadi.

Bu fazada biz:

- xodimni bir nechta kamerada kuzatamiz;
- har bir xodim uchun kunlik faoliyat tarixini shakllantiramiz;
- klient bilan kelishilgan 3–5 ta aniq va kamerada ko‘rinadigan ish turini aniqlash modelini ishlab chiqamiz.

Aniqlanishi mumkin bo‘lgan ishlar misoli:

- mijozga xizmat ko‘rsatish;
- mahsulotlarni tokchaga joylashtirish;
- yuk olib yurish;
- tozalash;
- mahsulotlarni tartibga keltirish.

Buning uchun:

- real ish joyidan video namunalar yig‘iladi;
- kerakli harakatlar belgilanadi;
- maxsus AI modeli tayyorlanadi va sinovdan o‘tkaziladi;
- zarur bo‘lsa lokal GPU server ishlatiladi;
- natija kadr yoki qisqa video bilan tasdiqlanadi;
- AI ishonmagan holatlar alohida ko‘rsatiladi.

### 2B-faza natijasi

Klient quyidagiga yaqin hisobot oladi:

> Xodim bugun ma’lum vaqt mijozlarga xizmat ko‘rsatdi, mahsulot joylashtirdi, tozalash bilan shug‘ullandi va ma’lum vaqt davomida kelishilgan faoliyat kuzatilmadi.

## Loyiha chegaralari

- POS va ERP tizimlari ushbu loyiha tarkibiga kiritilmaydi.
- AI yuz foiz xatosiz ishlamaydi; shubhali natijalar inson tomonidan tekshiriladi.
- Kamera ko‘rmaydigan yoki boshqa harakatdan ajratib bo‘lmaydigan ishni tizim ishonchli aniqlay olmaydi.
- AI hisoboti ish haqi, jarima yoki intizomiy jazo uchun avtomatik yakuniy qaror bo‘lmaydi.
- 2B-fazaning aniq muddati va narxi pilot video hamda 2A-faza natijalaridan keyin belgilanadi.
- Xodimlarning yuz ma’lumotlari va videolari himoyalangan lokal tizimda saqlanadi; ulardan foydalanish uchun klient tegishli rozilik va ichki tartiblarni ta’minlaydi.

## Amalga oshirish ketma-ketligi

1. Kameralar va lokal serverni tayyorlash.
2. 1-faza davomat tizimini ishga tushirish.
3. Real sharoitda aniqlikni tekshirish va tizimni barqarorlashtirish.
4. 2A-faza bo‘yicha zona, forma va faollik pilotini o‘tkazish.
5. 2A natijasi foydali bo‘lsa, 2B-faza uchun 3–5 ta ish turini tanlash.
6. Video ma’lumot yig‘ish, AI modelini tayyorlash va sinash.
7. Yakuniy hisobotlar va Telegram integratsiyasini ishga tushirish.

## Qisqa xulosa

- **1-faza:** kim, qachon keldi, qachon ketdi va qancha vaqt ish joyida bo‘ldi.
- **2A-faza:** xodim qayerda bo‘ldi, ish formasiga rioya qildimi va qancha vaqt faol yoki harakatsiz ko‘rindi.
- **2B-faza:** xodim oldindan belgilangan qaysi ishlarni bajarganini AI yordamida aniqlash.

