---
type: phase-plan
project: Higvision Proekt
phase: 2A
status: proposed
created: 2026-08-18
updated: 2026-08-18
tags: [camera-ai, phase-2a, anti-spoofing, uniform, zones]
---

# Faza 2A — Tezkor va o‘lchanadigan AI kengaytmalari

## Maqsad

1-fazani o‘zgartirmasdan, uning event va davomat bazasi ustiga tezroq tekshiriladigan,
huquqiy va texnik riski boshqariladigan funksiyalarni qo‘shish.

## Scope

### 1. Anti-spoofing va ishonchli davomat

- kirishda dual-lens/IR Face Access Terminal variantini baholash;
- foto yoki telefon videosi bilan aldash xavfini kamaytirish;
- kerak bo‘lsa `Face + karta/PIN` kombinatsiyasi;
- terminal eventini 1-fazadagi xodim va davomat bazasi bilan bog‘lash;
- terminal ishlamasa 1-fazadagi kamera davomatini fallback sifatida saqlash.

Tavsiya: maxsus face terminal ishlatish. Oddiy CCTV oqimida faqat dasturiy passive
liveness’ga tayanish tavsiya etilmaydi.

### 2. Forma nazorati

Erkin “nima kiygan?” matni emas, oldindan tasdiqlangan belgilar tekshiriladi:

- forma bor/yo‘q;
- oq ko‘ylak;
- qora fartuk;
- kepka yoki kaska;
- klient tanlagan rang va kiyim qismi.

Natija: `mos`, `mos emas`, `aniqlanmadi`. Har bir nomuvofiqlik uchun vaqt, kamera,
ishonch darajasi va tasdiqlovchi kadr saqlanadi.

### 3. Zona va vaqt analitikasi

Kamera tasvirida klient bilan birga quyidagi zonalar belgilanadi:

- asosiy ish joyi;
- mijozga xizmat ko‘rsatish joyi;
- ombor;
- tanaffus/dam olish joyi;
- kirish/chiqish;
- kamera ko‘rmaydigan yoki noma’lum zona.

Tizim har bir xodim bo‘yicha zonaga kirish, chiqish va zonada bo‘lgan vaqtni saqlaydi.

### 4. Qoida asosidagi faol/harakatsiz vaqt

- kelishilgan vaqt davomida harakat bo‘lmasa `harakatsiz` segment;
- ish zonasidagi harakat `faol` segment;
- tanaffus zonasidagi vaqt `tanaffus`;
- ko‘rinish yo‘qolsa `aniqlanmadi`;
- tashqarida bo‘lsa 1-faza eventlari bilan `tashqarida`.

Bu “samaradorlik bahosi” emas. Hisobotda aynan `qoida asosidagi faol/harakatsiz vaqt`
deb yoziladi.

### 5. Admin tasdig‘i va hisobot

- vaqt chizig‘ini ko‘rish;
- xato segmentni tahrirlash;
- forma hodisasini tasdiqlash/rad etish;
- nima sabab tuzatilganini audit logda saqlash;
- kunlik Telegram xulosasi;
- haftalik trend va aniqlanmagan vaqt ulushi.

## Arxitektura

```text
1-faza eventlari ----------------------|
Face terminal / liveness --------------|
Ichki kamera sub-stream → odam/tracking|→ 2A Rules Engine
Forma modeli --------------------------|       |
Zona konfiguratsiyasi -----------------|       v
                                         Timeline DB
                                              |
                               Admin panel + Telegram
```

AI server uchun avval sub-stream va past tahlil FPS ishlatiladi. Kamera/terminal tayyor
event bersa GPU xaridi pilotdan oldin majburiy emas; real yuk o‘lchanib keyin tanlanadi.

## Biz qiladigan tasklar

- [ ] 2A.1 — 1-faza API/event sxemasini muzlatish.
- [ ] 2A.2 — Face terminal va mavjud kamera bilan 100 ta nazoratli kirish testi.
- [ ] 2A.3 — Liveness va fallback event integratsiyasi.
- [ ] 2A.4 — Ish hududi zonalarini chizish va versiyalash.
- [ ] 2A.5 — Xodim tracking va zona eventlari.
- [ ] 2A.6 — 2–4 ta forma belgisi uchun dataset va detektor.
- [ ] 2A.7 — Faol/harakatsiz/tanaffus/aniqlanmadi qoidalari.
- [ ] 2A.8 — Timeline DB va deduplikatsiya.
- [ ] 2A.9 — Admin tuzatish va audit log.
- [ ] 2A.10 — Telegram kunlik/haftalik hisobot.
- [ ] 2A.11 — Yorug‘lik, to‘siq va bir nechta odam bilan real test.
- [ ] 2A.12 — Klient qabul testi va 2B uchun Go/No-Go hisoboti.

## Klientdan kerak

1. Forma qoidasi va har bir holat uchun namunaviy rasmlar.
2. Ish, ombor, tanaffus va noma’lum zonalarni tasdiqlash.
3. “Harakatsiz” deb hisoblash uchun vaqt chegarasi.
4. Bir xodimning roziligi va pilot ishtiroki.
5. Turli yorug‘likdagi namunaviy videolar.
6. Face terminal olish yoki vaqtincha test qurilmasi berish bo‘yicha qaror.
7. Hisobotni kim ko‘rishi va saqlash muddati.

## Qabul mezonlari

- har bir funksiya uchun oldindan belgilangan test to‘plami;
- false accept, false reject va `aniqlanmadi` ulushi alohida o‘lchanadi;
- forma bo‘yicha xato hodisa tasdiqlovchi kadr bilan chiqadi;
- zona vaqtlarining yig‘indisi kunlik timeline bilan mos keladi;
- admin tuzatishlari yo‘qolmaydi va audit logda qoladi;
- internet bo‘lmasa lokal ishlaydi, keyin Telegram navbati yuboriladi;
- klient natijani real kuzatuv bilan taqqoslab yozma qabul qiladi.

Aniq foiz pilot videosi ko‘rilmasdan va boshlang‘ich benchmark olinmasdan va’da qilinmaydi.

## Taxminiy muddat

- audit va qoidalar: 3–5 ish kuni;
- integratsiya va modellar: 10–15 ish kuni;
- real pilot va sozlash: 7–10 kun;
- umumiy: **3–5 hafta**.

## 2A tarkibiga kirmaydi

- aynan qaysi ish bajarilganini erkin matn bilan yozish;
- ko‘p kamera orasida to‘liq ReID;
- AcuSeek NVR xaridi;
- HEOP uchun production ilova;
- xodimga avtomatik intizomiy yoki moliyaviy baho;
- POS va ERP.

Bog‘liq: [[09 - Xodim faoliyatini tahlil qilish moduli]] · [[13 - Faza 2B ilgor faoliyat analitikasi]]

