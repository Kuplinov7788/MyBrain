---
type: architecture
project: Higvision Proekt
updated: 2026-08-13
---

# Texnik arxitektura va qarorlar

## Tavsiya qilingan birinchi arxitektura

```text
Hikvision kameralar
  ├─ People Counting
  ├─ Face Capture
  ├─ RTSP video
  └─ ISAPI hodisalari
          ↓
Lokal server yoki mini-PC
  ├─ yuzni xodim bazasi bilan solishtirish
  ├─ kirish/chiqish holatini birlashtirish
  ├─ takroriy hodisalarni tozalash
  ├─ tashqarida va ishda bo‘lgan vaqtni hisoblash
  └─ hisobot bazasi
          ↓
Telegram bot
  ├─ kunlik hisobot
  ├─ haftalik/oylik hisobot
  └─ kamera uzilishi haqida ogohlantirish
```

## Nega birinchi versiyada HEOP ichiga yozilmaydi?

HEOP kamera ichida custom C/C++ va AI ilova ishlatishga imkon beradi. Lekin buning uchun Hikvision Technology Partner Portal’da kompaniya sifatida ro‘yxatdan o‘tish, tasdiq, HEOP Agreement, SDK, model optimizatsiyasi va firmware testlari kerak.

Tez pilot uchun tashqi lokal server:

- tezroq ishlab chiqiladi;
- xatoni tuzatish oson;
- algoritmni yangilash oson;
- kamera almashtirilsa tizimni noldan yozish shart emas;
- keyinchalik stabil qismlarni HEOP ichiga ko‘chirish mumkin.

## Nega ikkita kamera?

Bitta kamera kirayotgan odamning yuzini ko‘rsa, chiqayotgan odam kameraga orqa o‘girgan bo‘lishi mumkin. People Counting yo‘nalishni biladi, ammo kim chiqayotganini aniq bilmasligi mumkin.

Eng ishonchli variant:

- 1-kamera — kirayotgan yuzga qaraydi;
- 2-kamera — chiqayotgan yuzga qaraydi;
- server hodisalarni birlashtiradi.

Agar ikkinchi kamera kassaga qo‘yilsa, xodimning ism bilan chiqish aniqligi cheklanishi texnik topshiriqda yoziladi.

## Uskunalar

- 1–2 dona tavsiya qilingan Hikvision kamera;
- Gigabit PoE switch;
- CAT6 kabel;
- kamera, switch va server uchun UPS;
- lokal mini-PC/server;
- NVR yoki microSD/video saqlash diski;
- vaqtni bir xil saqlash uchun NTP.

## Xavfsizlik

- kameraga kuchli alohida parol;
- default admin parolini qoldirmaslik;
- firmware yangilash;
- kameralarni alohida LAN/VLAN’da saqlash;
- internetga port ochmaslik;
- Telegram tokenlari va kamera parollarini Obsidian’ga yozmaslik;
- xodimlardan yuz ma’lumotini ishlatishga rozilik olish.

Bog‘liq: [[02 - Kamera modellari tahlili]], [[04 - Ish ketma-ketligi va masuliyatlar]]

