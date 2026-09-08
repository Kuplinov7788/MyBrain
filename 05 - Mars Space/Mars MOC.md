---
type: MOC
updated: 2026-09-08
---

# Mars Space — Xarita

Joriy reja: [[05 - Mars Space/Academy Architecture|Academy arxitekturasi va auto-otchotlar]]. 2026-09-08: reja saqlandi, implementatsiya keyingi davom ettirishga qoldirildi.

Mars.core.uz bilan bog'liq barcha skilllar va ma'lumotlar shu yerda.

---

## Skilllar

| Skill | Vazifasi | Trigger |
|-------|---------|---------|
| [[MarsDC]] | Davomat tekshirish + Coin taqsimlash | `MarsDC` (Telegramdan) |

---

## Qo'shish rejalashtirilgan skilllar
- MarsGrades — dars baholari
- MarsReport — oylik hisobot

---

Tags: #MOC #mars

## 2026-09-07 — Dashboard auditi

### Tekshirilgan holat

- Emirhan Mars IT School’da Tutor sifatida ishlaydi. Dashboardga kirish va asosiy ko‘rinishlar brauzerda tekshirildi; login ma’lumotlari bu qaydga yozilmaydi. [tekshirildi: `https://core.marsit.uz/`]
- Tutor menyusida 8 ta biriktirilgan guruh ko‘rindi: `IK-496`, `IND-F-549`, `nBG-2999`, `nF-455`, `nF-460`, `nFPro-422`, `RCT-299`, `YB-3088`.
- Guruh sahifasidagi asosiy bo‘limlar: Davomat, Mavzular, Topshiriqlar, Uyga vazifalar. Guruh metama’lumotlarida yo‘nalish, vaqt, dars kunlari, filial, xona, muddat va darslar soni bor.
- Tutor → Darsga kelmagan o‘quvchilar bo‘limi sana oralig‘i bilan umumiy propusklarni ko‘rsatadi; audit paytida 22 ta propusk, 22 ta o‘quvchi va 11 ta guruh ko‘rsatildi.
- Tutor → Talabalar topshiriqlari bo‘limi topshiriq manbasi, propusk sanasi, berilgan sana va “tutorga yozilgan” holati bilan paginatsiyalangan navbatni ko‘rsatadi; audit paytida 4469 ta yozuv indikatori ko‘rindi.
- Qo‘shimcha darslar haftalik vaqt jadvali ko‘rinishida; audit paytida jadval bo‘sh edi. Ota-onalar guruhiga havola ayrim guruhlarda mavjud, o‘quvchilar guruhi esa ulanmagan holat ham uchradi.

### Agent bo‘yicha dastlabki taklif

1. **Mars Monitor (read-only):** bugungi darslar, davomat kiritilmagan guruhlar, umumiy propusklar va topshiriqlar navbatini Telegramga qisqa hisobot qiladi.
2. **Davomat yordamchisi:** guruh va o‘quvchilar ro‘yxatini chiqaradi, Emirhan javobini olgachgina belgilashni taklif qiladi; yozishdan oldin aniq preview va tasdiq shart.
3. **Topshiriq nazoratchisi:** kechikkan yoki tutorga yozilmagan topshiriqlarni guruh/o‘quvchi kesimida jamlaydi.
4. **Haftalik hisobot:** guruh, davomat, topshiriq bajarilishi va mavzu bo‘yicha agregat ko‘rsatkichlarni yuboradi; ism va shaxsiy ma’lumotni faqat kerak bo‘lganda chiqaradi.

### Chegaralar

- Birinchi bosqich faqat o‘qish va hisobot; davomat, coin, baho yoki boshqa yozish amallari avtomatik bajarilmaydi.
- Telegram agenti dashboardga brauzer sessiyasi orqali kirsa, sessiya tugashi, Mac uyqusi va sayt UI o‘zgarishi alohida kuzatiladi.
- Mavzular va ayrim topshiriqlar bo‘limlarida ma’lumot bo‘sh ko‘rinishi mumkin; bu “ma’lumot yo‘q” degani emas, alohida guruh/oy bilan qayta tekshirish kerak. [xulosa]

## 2026-09-07 — Profil va oylik auditi

### Tekshirilgan hisob modeli

- Profil sahifasida oy tanlash, Senior daraja, umumiy o‘rtacha reyting, eng past guruh va jarimalar ko‘rsatiladi. [tekshirildi: `https://core.marsit.uz/teacher-profile`]
- Hisob-kitob varaqasi tasdiqlangan/tasdiqlanmagan holatga ega. Umumiy hisoblangan summa, 7.5% daromad solig‘i, oylik netto va shu kungi kunlik miqdor alohida beriladi.
- Har bir guruhda reyting `Audit 50 + Natija 50` ko‘rinishida ajratilgan. Ayrim oylar yoki guruhlarda quiz xatolari uchun o‘quvchi natijasiga +20% kompensatsiya qo‘shiladi; bu guruh bonusiga ta’sir qiladi.
- Tekshirilgan nF-460 va nBG-2999 guruhlarida formula: fiks 100,000 so‘m + to‘liq bonus 110,000 so‘mning guruh reytingi foiziga mos qismi. Boshqa yo‘nalishlar stavkasi farq qiladi. Sayt izohiga ko‘ra stavka darslar soniga bo‘linib, har o‘quvchining TO‘LANGAN darslariga ko‘paytiriladi. Qatnashuv to‘lov bilan bir xil emas: kelmagan belgisida ham musbat summa, kelgan belgisida ham nol summa kuzatildi.
- Guruh tafsilotida har bir dars sanasi, qatnashuv belgisi va o‘sha dars uchun hisoblangan summa ko‘rinadi. `-`, qatnashgan va kelmagan holatlari alohida ajratilgan.
- O‘rinbosar (`Zamena`) guruhlari alohida belgilanadi va bonus 100% deb ko‘rsatiladi.

### Komfortli agent taklifi

1. **Oylik komanda:** “Oyligim”, “Bu oy nima ta’sir qildi?”, “Bugun qancha qo‘shildi?”, “O‘tgan oy bilan solishtir” kabi tabiiy savollarni tushunadi.
2. **Izohli hisob:** netto → soliq → gross → guruhlar bo‘yicha ulush → darslar bo‘yicha ulushni bitta ixcham hisobotga aylantiradi.
3. **Muammo detektori:** reytingi past guruh, audit/natija pasayishi, o‘tkazib yuborilgan dars, kutilgan summa bilan amaldagi summa farqini belgilaydi.
4. **Oy yakuni:** har oy yopilishidan oldin davomat, topshiriq va oylikni tekshiradigan checklist yuboradi; hisob-kitob varaqasi tasdiqlanmagan bo‘lsa ogohlantiradi.
5. **“Nima qilsam oyligim oshadi?”:** faqat dashboarddagi formulaga tayangan holda qaysi guruh reytingi yoki natija ko‘rsatkichi ko‘proq ta’sir qilishini hisoblab beradi; o‘zi baho yoki davomatni o‘zgartirmaydi.
6. **Tarixiy grafik:** oylar bo‘yicha netto, reyting, bonus, darslar va qatnashuvni saqlab, trend ko‘rsatadi.

### Aniqlangan ehtiyot nuqtasi

- 2026-Aug tanlanganda ma’lumotlar keyinroq yangilandi, ammo sarlavhada `Groups (сентябрь)` yozuvi bir muddat saqlanib qoldi. Agent oy tanlangandan keyin qiymat, sana va guruhlar bir xil davrga tegishli ekanini yoxlamasdan hisobot bermasligi kerak. [tekshirildi: brauzerda oy almashtirish]
- Oylik bo‘yicha birinchi agent versiyasi faqat o‘qish, hisoblash va tushuntirish rejimida bo‘lishi kerak. Dashboarddagi davomat, baho yoki boshqa yozish amallariga avtomatik tegilmaydi.

## 2026-09-07 — Arxitektura auditi va tavsiya (hali amalga oshirilmagan)

- Tavsiya: Beluga ichida Academy moduli; Mars skill — amallar yo‘riqnomasi, maxsus adapter — saytni o‘qish/tekshirish, scheduler — vaqtli ishlar, lokal bazada sanali ko‘rsatkichlar. Alohida Telegram bot keyinchalik boshqa foydalanuvchilar uchun kerak bo‘lsa qo‘shiladi.
- Kod auditi: Beluga README, bot.py, context.py va app_bridge.mjs’da umumiy thread, durable navbat va RAG bor; Mars uchun maxsus adapter, scheduler va loyiha threadlari hozircha yo‘q. Status tekshiruvida RAG ok, 240 chunk, navbat bo‘sh; runtime notLoaded (faol turn ko‘rinmadi). Bu Mars integratsiyasi ishlashining dalili emas.
- Interaktiv brauzerga kirish Beluga fon xizmatida ham aynan shu imkoniyat borligini isbotlamaydi. Birinchi integratsiya tekshiruvi: Telegram so‘rovi → Marsdan yangi read-only ma’lumot → davr/manba/vaqt bilan javob.
- Operativ raqamlar sanali bazadan yoki yangi dashboard o‘qishidan olinadi. RAG — qoidalar, guruh konteksti va qarorlarni eslash uchun; joriy oylik manbasi sifatida eski RAG parchasiga tayanilmaydi.
- Avvalgi “nF-460 eng katta moliyaviy imkoniyat” xulosasi tasdiqlanmagan. Buning uchun barcha guruhlarning bonus stavkasi va haq to‘lanadigan dars hajmi solishtirilishi kerak. Eng past reyting eng katta yo‘qotish degani emas.
- Ochiq savollar: audit ballari/jarima qoidalari; guruh jami va o‘quvchi qatorlari jamining mosligi; tasdiqlanmagan hisobning keyin o‘zgarishi; profil va dashboarddagi guruhlar farqi; fon brauzeri sessiyasini tiklash. Bular aniqlanmasdan oylik prognozi kafolat sifatida berilmaydi.
- Komfort: Bugun / Oylik / E’tibor kerak / Guruhlar tugmalari; ertalab qisqa reja, darsdan keyin qolgan ish, sayt yangilanishidan keyin kechki hisobot; faqat muhim o‘zgarishda ogohlantirish, pauza va ish jurnalini ko‘rish.
- Eski MarsDC — tarixiy yo‘riqnoma; undagi qotirilgan Iyun oyi va eski guruhlar joriy avtomatlashtirishga mos emas. Unda ochiq login ma’lumotlari borligi aniqlandi; ularni umumiy RAGga kiritmaslik uchun alohida tozalash va indeks tekshiruvi kerak. Bu auditda credential qiymatlari ko‘chirilmadi.
