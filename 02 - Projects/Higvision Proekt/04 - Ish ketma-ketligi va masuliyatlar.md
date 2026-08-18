---
type: implementation-plan
project: Higvision Proekt
updated: 2026-08-14
---

# Ish ketma-ketligi va mas’uliyatlar

## 1. Klientdan boshlash uchun kerak

Klient tushunadigan shaklda:

1. Do‘konning kirish va chiqish joyidan qisqa video.
2. Hozir ishlayotgan kameralar rasmlari.
3. Kamera yozuvlarini saqlaydigan qurilmaning oldi-orqasidan rasm.
4. Tizim taniydigan xodimlarning ism-familiyasi.
5. Har bir xodim odatda soat nechada ish boshlashi va tugatishi.
6. Har bir xodimning yuzi old tomondan tiniq ko‘rinadigan 3–5 ta surati.
7. Hisobot boradigan Telegram chat.
8. Montaj va sinov uchun do‘konga kirish ruxsati.
9. Yuz ma’lumotlarini ishlatishga xodimlar roziligi.

## 2. Bizning vazifalar

1. Joy va mavjud uskunalarni tekshirish.
2. Kamera modeli, suffix va firmware’ni tasdiqlash.
3. Kamera joylashuvi va ko‘rish burchagini chizish.
4. RTSP/ONVIF/ISAPI testlari.
5. Lokal AI va davomat bazasi.
6. Yuzni ism bilan tanish.
7. Kelish, ketish va tanaffus qoidalari.
8. Telegram hisobotlari.
9. Kamera uzilish ogohlantirishi.
10. 7 kun test va kalibrovka.
11. Texnik hujjat va foydalanish yo‘riqnomasi.

## 3. Kamerachi/montajchi vazifasi

- kamera va kronshteyn;
- CAT6 kabel;
- PoE switch;
- elektr va UPS;
- montaj;
- suv/konditsioner oqishidan himoya;
- fizik burchak va fokus;
- kabel va elektr barqarorligi.

Bu chegaralar shartnomada yoziladi. Kabel yoki elektr muammosi dastur xatosi sifatida bizga qolmasligi kerak.

## 4. Ish muddati

- 1–2 kun: audit;
- 1 kun: yozma texnik topshiriq;
- 1–2 kun: montaj va tarmoq;
- 5–7 kun: AI, davomat va Telegram;
- 7 kun: real sinov.

Umumiy: taxminan **10 ish kuni + 7 kun test**.

## 5. Pilot qabul mezonlari

- kameralar barqaror 24/7 ishlashi;
- 20 ta test kirishining kamida 18 tasi to‘g‘ri qayd bo‘lishi;
- takroriy ko‘rinishlar yangi kelish sifatida yozilmasligi;
- kunlik hisobot vaqtida Telegramga kelishi;
- kamera uzilganda 2–5 daqiqada ogohlantirish;
- hodisada ism, vaqt, kamera va surat bo‘lishi;
- internet uzilganda hodisalar yo‘qolmasligi.

Kamera o‘rnatilgandan keyingi batafsil texnik ishlar: [[10 - Kamera o‘rnatilgandan keyingi lokal MVP rejasi]].

Bog‘liq: [[01 - Loyiha konteksti va talablar]], [[06 - Klientga yuboriladigan matnlar]]
