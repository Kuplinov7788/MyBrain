---
type: ai-handoff
project: Higvision Proekt
status: active
updated: 2026-08-14
---

# Keyingi sessiya uchun kontekst

## Bir jumlada

Hikvision kameralar yordamida odamlarni sanash, xodimni yuzidan aniqlash, kelish-ketish/tanaffus vaqtini hisoblash va Telegram hisoboti beradigan ikki kamerali lokal AI pilot.

## O‘zgarmas qarorlar

1. POS va ERP loyiha tarkibida yo‘q va tilga olinmaydi.
2. Asosiy kamera: DS-2CD3746G2H-LIZSU/SL PTRZ, 4 MP, 2.7–13.5 mm.
3. Ism bilan to‘liq kirish/chiqish uchun ikki qarama-qarshi kamera afzal.
4. Birinchi versiyada AI lokal serverda; HEOP keyingi bosqich.
5. Hisobot Telegramga yuboriladi.
6. Klient uchun texnik atamalar sodda tilda yoziladi.
7. Foydalanuvchi aniq buyurmasa klientga xabar yuborilmaydi; draft BelugaCat orqali foydalanuvchiga yuboriladi.
8. Klient xodimning kiyimi, samarali/bekor vaqti va bajargan ishlarini ham tahlil qilishni xohlaydi. Bu alohida 2-bosqich AI moduli.
9. Hozirgi birinchi maqsad: kamera ichidagi qo‘shimcha softsiz, lokal video arxiv + davomat + Telegram hisobot MVP.
10. Tomonlar mas’uliyati, yakuniy arxitektura va tasklar [[11 - Tomonlar masuliyati arxitektura va tasklar]] sahifasida.

## Keyingi amaliy qadam

Klientdan quyidagilar kelishini kutish:

- kirish/chiqish videosi;
- mavjud kameralar rasmlari;
- yozuv saqlovchi qurilma oldi-orqa rasmlari;
- xodimlarning ism-familiyasi;
- ish boshlash/tugatish vaqtlari;
- har xodimning 3–5 ta tiniq yuzi rasmi.

Kelgach:

1. Kamera va qurilma modelini rasmdan aniqlash.
2. Joylashuv va obyektiv tanlash.
3. Aynan mavjud firmware’da Face Capture + People Counting parallel ishlashini tekshirish.
4. Pilot sxemasi va uskunalar ro‘yxatini tayyorlash.
5. Shundan keyingina aniq narx va muddatni yozish.

Faoliyat tahlili uchun qo‘shimcha ravishda klientdan ish hududlari videosi, forma talabi, “samarali” va “bekor” vaqt qoidalari hamda kamera orqali aniqlanishi kerak bo‘lgan ishlar ro‘yxati olinadi.

Kamera o‘rnatilgach birinchi bajariladigan texnik reja: [[10 - Kamera o‘rnatilgandan keyingi lokal MVP rejasi]].

## Manbalar

- [[02 - Kamera modellari tahlili]]
- [[03 - Texnik arxitektura va qarorlar]]
- [[04 - Ish ketma-ketligi va masuliyatlar]]
- [[05 - Yozishmalar va qarorlar tarixi]]
- [[09 - Xodim faoliyatini tahlil qilish moduli]]
- [[10 - Kamera o‘rnatilgandan keyingi lokal MVP rejasi]]
- [[11 - Tomonlar masuliyati arxitektura va tasklar]]
- [[Materiallar/Kamera suxrob aka - transkripsiya.txt]]
