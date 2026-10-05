# Dantes Sales — bosqichma-bosqich reja

Sana: 2026-09-29. Holat: taklif etilayotgan ish rejasi; agent yaratish yoki jonli integratsiyani ishga tushirish hali bu topshiriqning qismi emas. Savollar Emirhan ko‘rib chiqishi uchun; yuborilmagan.

Manbalar: [[Sales suhbat - muammolar va AI agent talablari]] · [[Dantes Biznes Agent Dashboard 2026-09-25]] · [[Uysot Sales javoblari va dashboard dalillari 2026-09-28]].

## Maqsad va mavjud faktlar

Maqsad — Uysot’dagi Sales ma’lumotlarini tekshirib, Dantes so‘ragan umumiy moliya hisobotiga ishonchli kirish ma’lumoti tayyorlash. Guruh moliyasining to‘liq qamrovi va jamoalar mas’uliyati alohida kelishiladi.

- [foydalanuvchi/Sales javobi] Sales’da faqat Venera ishlaydi; to‘lovlarni o‘zi tekshirib Uysotga kiritadi. Mijoz bilan korporativ raqamdan bog‘laniladi. Bir necha ogohlantirishdan keyin qarz masalasi direktor Jonibek Komiljonovichga chiqariladi.
- [video/UI kuzatuvi] Shartnoma tafsilotida xonadon ma’lumoti va to‘lov tarixi, to‘lov jadvalida shartnoma maydoni ko‘ringan. API’da bog‘lanish va maydonlar hali tekshirilishi kerak.
- [cheklov] Video audiosining o‘zbekcha izohi ishonchli transkripsiya qilinmagan. Ekranda ko‘rinmagan biznes qoidalarini o‘rganilgan fakt deb hisoblamaymiz.

## Bosqichlar va natijalar

| Bosqich | Nima qilamiz | Yakunlash uchun kerakli natija |
|---|---|---|
| 1. Sales jarayonini aniqlash | Veneraga quyidagi savollarni beramiz; mavjud javoblarni qayta so‘ramaymiz. Muammo, amaldagi yechim va mas’ulni qayd qilamiz. | Jarayon qadamlari, ishonchli jadval/sana/statuslar va ochiq savollar ro‘yxati. |
| 2. Ma’lumot xaritasini tuzish | Kompaniya, loyiha, xonadon, mijoz, shartnoma, to‘lov jadvali, haqiqiy to‘lov va qarzdorlikni bog‘laymiz. Har maydon uchun manba va biznes ta’rifini yozamiz. | Tekshiriladigan maydonlar/ID’lar xaritasi; kompaniya va loyiha alohida; valyuta va hisob sanasi aniq. |
| 3. API yoki eksportni tekshirish | O‘qishga ruxsat etilgan endpoint/eksportlarning parametr, filter, pagination, schema va yangilanishini tekshiramiz. Loginning mavjudligi integratsiya imkoniyati tasdiqlangani degani emas. | Ma’lumot olish usuli tasdiqlangan, hujjatlashtirilgan; mavjud bo‘lmagan maydonlar ochiq belgilangan. |
| 4. Bir loyiha va davrda solishtirish | Emirhan/Venera tanlagan loyihada Uysot shartnomalari, to‘lovlari va qarzdorligini bir xil sana/filter/valyutada solishtiramiz. Venera natijani o‘z hisobi bilan tekshiradi. | Farqlar va sabablari qayd etilgan; mos kelmagan raqamlar tasdiqlangan natija sifatida ko‘rsatilmaydi. |
| 5. Birinchi agent vazifasini tanlash | Tasdiqlangan muammoga qarab kunlik to‘lov/qarz jamlanmasi, yaqin badallar ro‘yxati yoki ichki follow-up vazifalari kabi bitta vazifani tanlaymiz. Natija va ko‘rish huquqini kelishamiz. | Agent uchun aniq topshiriq: manba, natija, kim ko‘radi, kim tasdiqlaydi, muvaffaqiyat mezoni. Ishlab chiqish alohida topshiriq bilan boshlanadi. |
| 6. Nazoratli pilot | Tanlangan vazifa bo‘yicha namuna hisobotni tayyorlaymiz; Venera ma’lumotni, Emirhan yoki tayinlangan egasi format va foydaliligini tekshiradi. | Raqamlarning manbasi bor; yangilanish vaqti ko‘rinadi; takroriy import ma’lumotni ikki marta sanamaydi; ruxsat va yetkazish tartibi tasdiqlangan. |
| 7. Umumiy moliyaga ulash | Sales natijasini kompaniya/loyiha/shartnoma bo‘yicha guruh moliyasi mas’uliga uzatish tartibini belgilaymiz. Keyin 1C/bank/boshqa kompaniyalar manbalari bilan birlashtirish rejalashtiriladi. | Sales ma’lumotining guruh hisobotiga kirish formati va egasi aniq; tushum/daromad/foyda ta’riflari kelishilgan. |

Bosqichning natijasi tayyor bo‘lmasa, keyingi bosqichdagi raqamni yakuniy deb ko‘rsatmaymiz. Bir nechta agent yaratish zarurati hali tasdiqlanmagan.

## Veneraga birinchi savollar — draft

1. Oyda sotilgan xonadonlarni qaysi jadval yoki hisobotdan sanaysiz? Sotuv sanasi sifatida qaysi sana olinadi?
2. Uysot’dagi har bir loyiha qaysi kompaniyaga tegishli? Shu bog‘lanishni ro‘yxat qilib bera olasizmi?
3. To‘lovni Uysot’ga kiritishda qaysi hujjatga tayanasiz: bank ko‘chirmasi, chek yoki boshqa hujjat? Shu hujjat Uysot’da saqlanadimi?
4. Hali muddati kelmagan to‘lovlar bilan muddati o‘tgan qarzlarni qaysi jadvaldan alohida ko‘rasiz?
5. Jonibek Komiljonovichga chiqarishdan oldin odatda nechta va qancha vaqt oralig‘ida ogohlantirish berasiz? Natijasini qayerga yozasiz?
6. Korporativ raqamdagi suhbat natijasi va keyingi qo‘ng‘iroq sanasi Uysot/CRM’ga yoziladimi yoki boshqa joyda yuritiladimi?
7. Shartnoma bekor bo‘lsa yoki to‘lov noto‘g‘ri kiritilsa, qanday tuzatasiz? Qaytarilgan pul va qolgan qarz qayerda aks etadi?
8. Kundalik ishda eng ko‘p vaqt oladigan yoki ko‘p xato chiqadigan ikkita ish qaysilar? Avval qaysi birini yengillashtirish foydali bo‘ladi?

Zarur bo‘lsa keyin aniqlashtiriladi: lead kelish kanallari va lead→bron→shartnoma qadamlari; bron/sotuv statusini o‘zgartirish; Sotuvchi Sitora akkauntidan amalda foydalanish; CRM’ning to‘liqligi.

## Emirhan/Dantes bilan kelishiladigan qarorlar

- Birinchi tekshirish uchun loyiha va davr; guruhga kiruvchi yuridik kompaniyalar ro‘yxati.
- Hisobotni kim ko‘radi, moliyaviy raqamlarning biznes ta’rifini kim tasdiqlaydi va ma’lumot olishga kim ruxsat beradi.
- Birinchi agent vazifasi va keyinchalik mijozga xabar yuborish uchun tasdiqlash tartibi. Hozirgi bosqichda mijozga avtomatik xabar yuborish rejalashtirilmaydi.

## Tekshiruv qoidalari

- Kompaniya ID’si loyiha ID’siga tenglashtirilmaydi; kompaniya bir nechta loyihaga ega bo‘lishi mumkin.
- To‘lov tushumi, shartnoma summasi, buxgalteriya daromadi va foyda alohida tushunchalar.
- Umumiy shartnoma qoldig‘i va muddati o‘tgan qarz alohida hisoblanadi. Kutilayotgan badal reja; kafolatlangan tushum emas.
- To‘lovlarni bog‘lashda API’dagi barqaror ID va shartnoma aloqasi tekshiriladi. Bir xil ism/summa/sana o‘zi takroriy to‘lov isboti emas.
- Bekor qilingan shartnomalar, qaytarishlar, chegirmalar, penya va valyutalar tasdiqlangan qoidalarga ko‘ra hisoblanadi.
- Har natijada manba, hisob sanasi, davr, filter va yangilanish vaqti ko‘rsatiladi; maxfiy login va mijoz PII loyiha qaydlariga ko‘chirilmaydi.

## Hozirgi keyingi qadam

Emirhan avval yuqoridagi 8 savolni ko‘rib chiqadi. Javoblar kelgach, ma’lumot xaritasini yakunlaymiz va Uysot’da mustaqil tekshiriladigan API/eksport qismini hujjatlashtiramiz. Savollarni yuborish uchun alohida aniq so‘rov kutiladi.
