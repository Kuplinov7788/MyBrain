---
type: project
status: active
created: 2026-08-13
updated: 2026-08-18
tags: [project, hikvision, camera-ai, people-counting, attendance, telegram]
---

# Higvision Proekt

> To‘g‘ri brend yozilishi: **Hikvision**. Papka foydalanuvchi so‘ragan nom bilan `Higvision Proekt` deb ochildi.

## Eng muhim qoida

**Bu loyihaga POS va ERP umuman aralashtirilmaydi va klientga yuboriladigan matnlarda tilga olinmaydi.**

## Maqsad

Do‘kondagi Hikvision kameralarni AI dasturiga ulab:

- kirgan va chiqqan odamlarni sanash;
- xodimni yuzidan aniqlash;
- xodim qachon kelganini va ketganini qayd qilish;
- ish vaqtida tashqarida qancha bo‘lganini hisoblash;
- kunlik, haftalik va oylik hisobotlarni Telegram orqali yuborish;
- kamerani 24 soat qo‘lda kuzatish zaruratini kamaytirish.

## Hozirgi asosiy qaror

Pilot uchun asosiy tavsiya:

- **Hikvision DS-2CD3746G2H-LIZSU/SL (PTRZ)**;
- **4 MP**;
- **2.7–13.5 mm motorli obyektiv**;
- kirish va chiqishni ishonchli aniqlash uchun imkon qadar **2 ta qarama-qarshi kamera**;
- birinchi versiyada AI va biznes hisoblari lokal serverda ishlaydi;
- kamera bilan aloqa RTSP/ONVIF/ISAPI orqali;
- HEOP keyingi bosqich uchun saqlanadi.

## Loyiha qaydlari

- [[01 - Loyiha konteksti va talablar]]
- [[02 - Kamera modellari tahlili]]
- [[03 - Texnik arxitektura va qarorlar]]
- [[04 - Ish ketma-ketligi va masuliyatlar]]
- [[05 - Yozishmalar va qarorlar tarixi]]
- [[06 - Klientga yuboriladigan matnlar]]
- [[07 - Keyingi sessiya uchun kontekst]]
- [[08 - Rasmiy manbalar]]
- [[09 - Xodim faoliyatini tahlil qilish moduli]]
- [[10 - Kamera o‘rnatilgandan keyingi lokal MVP rejasi]]
- [[11 - Tomonlar masuliyati arxitektura va tasklar]]
- [[12 - Faza 2A tezkor AI kengaytmalari]]
- [[13 - Faza 2B ilgor faoliyat analitikasi]]
- [[Materiallar/Audio uchrashuv xulosasi]]
- [[Materiallar/Telegram uchun tasdiqlangan hisobot]]

## Manba materiallar

- To‘liq transkripsiya: [[Materiallar/Kamera suxrob aka - transkripsiya.txt]]
- Subtitr: [[Materiallar/Kamera suxrob aka - transkripsiya.srt]]
- Texnik JSON: [[Materiallar/Kamera suxrob aka - transkripsiya.json]]
- Audio original joyi: `C:\Users\ertan\Downloads\Telegram Desktop\Kamera suxrob aka.m4a`
- Transkripsiya ishchi papkasi: `D:\Kamera AI transkripsiya`

## Hozirgi holat

- [x] 42:12 audio transkripsiya qilindi
- [x] Uchrashuv talablari tahlil qilindi
- [x] Hikvision modellari rasmiy ma’lumotlar bilan taqqoslandi
- [x] Asosiy kamera modeli tanlandi
- [x] Klientga tushunarli qisqa hisobot tayyorlandi
- [x] Transkripsiya ishchi papkasi C diskdan `D:\Kamera AI transkripsiya` ga ko‘chirildi va tekshirildi
- [ ] Klientdan joy videosi va mavjud uskunalar rasmini olish
- [ ] Kamera modeli/firmware bo‘yicha real demo o‘tkazish
- [ ] Pilot uchun yakuniy sxema va smeta
- [ ] Ikki kamerali pilotni o‘rnatish
- [ ] Telegram hisoboti va 7 kunlik sinov
- [ ] Lokal video arxiv va davomat MVP’ni ishga tushirish
- [ ] Klient va biz tomondagi mas’uliyatlarni yozma tasdiqlash
- [ ] Bir xodim va bitta ish hududida faoliyat tahlili pilotini sinash
- [ ] 1-faza qabul qilingach 2A forma/zona/liveness pilotini boshlash
- [ ] 2A Go/No-Go natijasidan keyin 2B advanced AI smetasini tasdiqlash
