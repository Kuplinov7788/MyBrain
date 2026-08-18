---
type: implementation-plan
project: Higvision Proekt
status: planned
created: 2026-08-14
updated: 2026-08-14
tags: [local-server, video-archive, attendance, telegram, mvp]
---

# Kamera o‘rnatilgandan keyingi lokal MVP rejasi

## Hozirgi vazifa

Kamera ichidagi qo‘shimcha softga bog‘lanmasdan quyidagi tizimni qilish:

1. kameralar videosini lokal joyda saqlash;
2. xodimni yuzidan aniqlash;
3. qachon kelgani va qachon ketganini qayd qilish;
4. kun davomida chiqib-kirgan vaqtlarini hisoblash;
5. do‘konda bo‘lgan jami vaqtni hisoblash;
6. kunlik, haftalik va oylik hisobot tayyorlash;
7. hisobotni Telegramga avtomatik yuborish.

Bu bosqich xodimning **do‘konda bo‘lgan vaqtini** hisoblaydi. U hali samarali/bekor vaqt yoki bajargan ishlarni baholamaydi; ular [[09 - Xodim faoliyatini tahlil qilish moduli|keyingi alohida bosqich]].

## Ishlaydigan umumiy sxema

```text
Kirish kamerasi ─┐
                 ├─ RTSP video ─→ Lokal server/NVR ─→ Video arxiv
Chiqish kamerasi ┘                     │
                                      ├─ Yuzni aniqlash
                                      ├─ IN/OUT hodisalari
                                      ├─ Davomat hisoblash
                                      ├─ Ma’lumotlar bazasi
                                      └─ Telegram hisobot
```

## 1. Montajdan keyin darhol tekshirish

- kirayotgan odamning yuzi birinchi kamerada to‘liq va tiniq ko‘rinishi;
- chiqayotgan odamning yuzi ikkinchi kamerada to‘liq va tiniq ko‘rinishi;
- yuz juda yuqoridan, yon tomondan yoki orqadan tushmasligi;
- eshikdagi kuchli qarshi yorug‘lik sozlanishi;
- kechasi yuz sifati tekshirilishi;
- kamera fokus va zoomi odam eshikdan o‘tadigan nuqtaga moslanishi;
- kamida 20 ta kirish va 20 ta chiqish test videosi olinishi.

Natija: AI ishlashi uchun yaroqli real video namunalari.

## 2. Lokal tarmoq va vaqtni sozlash

- har kameraga doimiy lokal IP manzil;
- alohida kuchli parol;
- kameralar, server va yozuv qurilmasida bir xil NTP vaqt;
- PoE switch va UPS;
- serverdan har bir kameraning RTSP oqimini tekshirish;
- kameralarni internetga ochiq port orqali chiqarmaslik;
- kamera uzilganda aniqlash uchun doimiy health-check.

Vaqt sinxron bo‘lmasa, kelish-ketish hisoboti noto‘g‘ri chiqadi. Shu sababli NTP majburiy.

## 3. Lokal video arxivni ishga tushirish

### Tavsiya

- NVR yoki lokal server uzluksiz videoni saqlaydi;
- AI hodisa vaqtida alohida surat va 10–20 soniyalik qisqa video saqlaydi;
- bazada xodim, vaqt, yo‘nalish, kamera va arxiv fayliga havola bo‘ladi;
- saqlash muddati klient bilan kelishiladi, boshlanishiga 30 kun tavsiya.

### Disk hajmini hisoblash

Formula:

`1 Mbps ≈ 10.8 GB/kun`

Misol uchun bitta kamera 4 Mbps yozsa:

- 1 kamera: taxminan 43 GB/kun;
- 2 kamera: taxminan 86 GB/kun;
- 2 kamera, 30 kun: taxminan 2.6 TB.

Zaxira va fayl tizimi uchun joy qoldirib, bunday holatda kamida 4 TB surveillance disk ma’qul. Aniq disk hajmi real bitrate, kamera soni, FPS va saqlash kuniga qarab hisoblanadi.

## 4. Lokal server dasturining karkasi

Biz quyidagi xizmatlarni yaratamiz:

1. **Camera service** — RTSP oqimini oladi va kamera holatini kuzatadi.
2. **Recorder** — uzluksiz yoki jadval bo‘yicha videoni segmentlarga yozadi.
3. **Detection service** — odam/yuzni topadi va sifatli yuz kadrini tanlaydi.
4. **Recognition service** — yuzni xodimlar bazasi bilan solishtiradi.
5. **Event service** — `IN`, `OUT`, `UNKNOWN` hodisalarini yaratadi.
6. **Attendance engine** — kelish-ketish va jami vaqtni hisoblaydi.
7. **Database** — xodimlar, jadvallar, hodisalar va hisobotlarni saqlaydi.
8. **Report scheduler** — kunlik, haftalik va oylik hisobotlarni avtomatik yaratadi.
9. **Telegram service** — hisobot va texnik ogohlantirishlarni yuboradi.
10. **Admin panel** — xodim qo‘shish, jadval o‘zgartirish va xato hodisani tuzatish uchun.

Xizmatlarni Docker orqali lokal serverda alohida konteynerlarda ishlatish tavsiya qilinadi. Kamera yoki internet uzilsa, tizim lokal ishlashda davom etadi.

## 5. Xodimlar bazasini tayyorlash

Har xodim uchun:

- ichki ID;
- ism-familiya;
- faol/nofaol holati;
- odatda ish boshlash va tugatish vaqti;
- dam olish kunlari;
- 3–5 ta old tomondan tiniq yuz rasmi;
- kerak bo‘lsa bir necha smena varianti.

Rasmlar lokal serverda himoyalangan holda saqlanadi. Xodim tizimdan chiqarilsa, uning holati nofaol qilinadi; tarixiy hisobot buzilmaydi.

## 6. Yuzni tanish va IN/OUT hodisasi

Jarayon:

1. Kamera odamni ko‘radi.
2. Server yuzni topadi.
3. Eng sifatli kadrni xodimlar bazasi bilan solishtiradi.
4. Qaysi kamera ko‘rganiga qarab `IN` yoki `OUT` hodisasi yaratiladi.
5. Bir necha soniya ichidagi takroriy kadrlar bitta hodisaga birlashtiriladi.
6. Ishonch yetarli bo‘lmasa `UNKNOWN` sifatida saqlanadi va majburan boshqa xodimga yozilmaydi.
7. Hodisa bilan birga vaqt, surat va qisqa video saqlanadi.

Eng ishonchli sxema:

- 1-kamera — kirayotgan yuzga qaraydi va `IN` beradi;
- 2-kamera — chiqayotgan yuzga qaraydi va `OUT` beradi.

## 7. Davomat hisoblash qoidasi

Har ish kuni uchun:

- birinchi to‘g‘ri `IN` — kelgan vaqt;
- oxirgi to‘g‘ri `OUT` — ketgan vaqt;
- oraliq `OUT → IN` — tashqarida bo‘lgan interval;
- `ketgan vaqt − kelgan vaqt` — umumiy oraliq;
- `umumiy oraliq − tashqarida bo‘lgan vaqt` — do‘konda bo‘lgan jami vaqt;
- jadvaldagi boshlanish bilan solishtirish — kechikish;
- umuman `IN` bo‘lmasa — kelmadi yoki tekshirish kerak;
- `IN` bor, lekin `OUT` yo‘q bo‘lsa — hisobotda “chiqish aniqlanmadi” deb belgilanadi.

Muhim holatlar:

- bir kunda bir necha marta chiqib-kirish;
- tun smenasi va kun almashishi;
- bir nechta smena;
- kamera uzilishi;
- yuz ko‘rinmay qolishi;
- takroriy hodisa;
- noma’lum odam;
- administrator tomonidan qo‘lda tuzatish.

## 8. Ma’lumotlar bazasi

Minimal jadvallar:

- `employees` — xodimlar;
- `shifts` — ish vaqtlari;
- `cameras` — kamera va yo‘nalish;
- `recognition_events` — barcha IN/OUT/UNKNOWN hodisalari;
- `attendance_days` — kunlik hisob;
- `report_deliveries` — qaysi hisobot qachon yuborilgani;
- `system_alerts` — kamera/server uzilishlari;
- `audit_log` — administrator tuzatishlari.

Tayyor hisoblarni bazada saqlash bilan birga, ular xom hodisalardan qayta hisoblanadigan bo‘lishi kerak. Bu xato hodisa tuzatilganda eski hisobotni yangilash imkonini beradi.

## 9. Hisobotlar

### Kunlik hisobot

Har bir xodim uchun:

- ish jadvali;
- birinchi kelgan vaqt;
- oxirgi ketgan vaqt;
- kechikish;
- necha marta tashqariga chiqqani;
- tashqarida jami qancha bo‘lgani;
- do‘konda jami qancha bo‘lgani;
- muammo yoki tekshirilishi kerak bo‘lgan hodisa.

Misol:

```text
14.08.2026 — Kunlik davomat

Ali Valiyev
Jadval: 09:00–19:00
Keldi: 08:57
Ketdi: 19:08
Tashqarida: 00:42
Do‘konda: 09:29
Holat: vaqtida
```

### Haftalik hisobot

- ishlagan va kelmagan kunlar;
- jami do‘konda bo‘lgan vaqt;
- jami tashqarida bo‘lgan vaqt;
- kechikishlar soni va jami kechikish;
- to‘liq bo‘lmagan/tekshiriladigan hodisalar.

### Oylik hisobot

- ish kunlari bo‘yicha umumiy jadval;
- jami ishlagan kun va vaqt;
- kelmagan kunlar;
- kechikishlar;
- tashqarida bo‘lgan jami vaqt;
- tuzatilgan yoki tasdiqlanmagan hodisalar;
- Telegram matni va kerak bo‘lsa Excel/PDF fayli.

## 10. Telegram avtomatizatsiyasi

- kunlik hisobot — klient belgilagan vaqtda;
- haftalik hisobot — haftaning belgilangan kuni;
- oylik hisobot — oyning birinchi kuni oldingi oy uchun;
- kamera uzilishi — 2–5 daqiqada ogohlantirish;
- kamera tiklanishi — alohida xabar;
- noma’lum yuz yoki to‘liq bo‘lmagan kun — tekshirish uchun xabar;
- hisobot yuborilmasa qayta urinish va lokal navbatda saqlash.

Internet vaqtincha o‘chsa, kamera yozuvi, aniqlash va hisoblash lokal davom etadi. Telegram xabarlari internet qaytganda yuboriladi.

## 11. Ish bosqichlari va muddat

### A. Texnik topshiriq va qoidalar — 1 ish kuni

- xodimlar, smenalar, hisobot va saqlash muddatini tasdiqlash.

### B. Kamera/tarmoq/video arxiv — 1–2 ish kuni

- IP, NTP, RTSP, yozuv, disk va uzilish nazorati.

### C. Xodim bazasi va yuzni tanish — 2–3 ish kuni

- xodimlarni kiritish, yuzlarni ro‘yxatdan o‘tkazish va real kamera testlari.

### D. Davomat hisoblash — 2–3 ish kuni

- IN/OUT, oraliq chiqish, kechikish va istisno holatlari.

### E. Telegram va hisobotlar — 2–3 ish kuni

- kunlik/haftalik/oylik format va avtomatik yuborish.

### F. Real sinov — 7 kun

- haqiqiy hodisalar bilan solishtirish, xato sabablarini tuzatish va yakuniy qabul.

Umumiy: kamera montaji tayyor, videolar sifati yaxshi va ma’lumotlar to‘liq bo‘lsa **10–12 ish kuni + 7 kun real sinov**.

## 12. Boshlash uchun klientdan kerak

1. O‘rnatilgan kameralar IP manzili va lokal kirish ruxsati.
2. Kirish va chiqishdan test videolari.
3. Xodimlar ism-familiyasi.
4. Har xodimning 3–5 ta tiniq yuz rasmi.
5. Har xodim nechidan nechigacha ishlashi va dam olish kunlari.
6. Kechikishga ruxsat etilgan daqiqa, agar bo‘lsa.
7. Video necha kun saqlanishi.
8. Kunlik, haftalik va oylik hisobot yuboriladigan vaqt.
9. Hisobot boradigan Telegram chat.
10. Xodimlarni yuz orqali aniqlash bo‘yicha xabardor qilish va rozilik.

## 13. Qabul mezonlari

- ikkala kamera lokal serverga uzluksiz video beradi;
- video kerakli kunlar davomida lokal saqlanadi va vaqt bo‘yicha topiladi;
- test kirish/chiqishlari ism, yo‘nalish, vaqt va surat bilan qayd etiladi;
- takroriy kadrlar yangi kelish sifatida hisoblanmaydi;
- bir necha chiqib-kirish to‘g‘ri birlashtiriladi;
- kunlik, haftalik va oylik hisob xom hodisalar bilan mos keladi;
- kamera/internet uzilishi ma’lumot yo‘qotmasdan boshqariladi;
- Telegram hisobotlari belgilangan vaqtda boradi;
- xato hodisani administrator tuzatganda hisobot qayta hisoblanadi.

## Birinchi amaliy qadam

Kameralar o‘rnatilgach, darhol quyidagilar olinadi:

1. har kameradan RTSP test oqimi;
2. 20 ta kirish va 20 ta chiqish videosi;
3. kamera modeli, firmware, IP va yo‘nalish ro‘yxati;
4. birinchi pilot xodimlarining rasmi va ish vaqti;
5. video saqlash muddati va Telegram hisobot vaqti.

Shundan keyin avval **lokal yozuv + hodisa bazasi**, undan so‘ng **yuzni tanish + davomat**, oxirida **Telegram hisobotlari** ishga tushiriladi.

Bog‘liq: [[03 - Texnik arxitektura va qarorlar]] · [[04 - Ish ketma-ketligi va masuliyatlar]] · [[09 - Xodim faoliyatini tahlil qilish moduli]]
