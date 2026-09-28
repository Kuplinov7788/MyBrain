---
type: meeting-questions
project: Dantes AI + Hermes Agent
observed: 2026-09-21
status: preparation
---

# Dantes va Hermes: arxitektura va yuridik uchrashuv savollari

Bu hujjat uchrashuv uchun savollar ro'yxati. “Majburiy” degan joylar shartnoma va yurist tekshiruvida aniq bandga aylantiriladi. Savollar O'zbekiston qonunchiligi, Dantes repo hujjatlari va Hermes arxitekturasiga tayangan holda tuzildi; yakuniy yuridik xulosa emas.

## Uchrashuvda avval beriladigan 12 savol

1. Birinchi pilotda aniq qaysi ish ishlaydi: Telegram guruhini o'qish, digest, ombor hisobi yoki boshqa modulmi?
2. Qaysi natija “qabul qilindi” hisoblanadi va uni kim imzolaydi?
3. Hermes qaysi vazifani bajaradi, Dantes `core` qaysi qarorni majburiy nazorat qiladi?
4. Har bir model chaqiruvi va yozuvchi tool haqiqatan Dantes policy'sidan o'tadimi? Buni qanday log yoki test bilan ko'rsatamiz?
5. Har profile uchun `terminal.cwd`, sandbox va faylga kirish chegarasi qayerda belgilanadi?
6. Kanban dispatcher'ning yagona egasi qaysi gateway bo'ladi va gateway to'xtasa vazifa qanday tiklanadi?
7. Telegram guruhlarini o'qish uchun kimning yozma ruxsati bor? Bot guruhga yozadimi yoki faqat DM'ga yuboradimi?
8. Ma'lumotlarning source of truth'i qaysi: Telegram, 1C, Excel, GPS, ombor jurnali yoki odam tasdig'imi?
9. AI xato qilsa, oxirgi qarorni kim beradi? Moliyaviy, yuridik va xodimga oid qarorlar odam tasdig'isiz bajariladimi?
10. Xabar, hujjat, ovoz, GPS va xodim ma'lumotlari qayerda, qancha vaqt va qaysi provayderda saqlanadi?
11. Mijoz loyiha tugaganda ma'lumotlarni qaytarish, o'chirish va backup nusxalarini yo'q qilish tartibi qanday bo'ladi?
12. Birinchi pilotdan oldin qaysi hujjatlar imzolanadi: asosiy shartnoma, NDA, data-processing ilovasi, ruxsat xatlari va acceptance akti?

## A. Arxitektura savollari

### Hermes va Dantes chegarasi

1. Hermes faqat agent loop, profile, tool, session va gateway runtime sifatida qoladimi?
2. Dantes `core.py` ruxsat, audit, model trust va moliyaviy tasdiqning yagona majburiy eshigimi?
3. Hermes'ning profile yoki SOUL matni ruxsat bermasligi, ruxsat faqat `xodim.json` va registry'dan kelishi qanday tekshiriladi?
4. `core.model_tanla()` real provider chaqiruvidan oldin har safar ishlashini qaysi integration test isbotlaydi?
5. Open modelga restricted/confidential ma'lumot ketmasligini qanday bloklaymiz va rad qarori qayerda qayd qilinadi?

### Profile, tool va ish maydoni

6. 13 xodimning har birida explicit `terminal.cwd` bo'ladimi?
7. Local terminal o'rniga Docker, remote server yoki boshqa sandbox kerakmi?
8. Xodimning `terminal`, `file`, `memory`, `kanban` va Telegram tool'laridan qaysi biri read-only, qaysi biri write-capable?
9. Har bir write amaliga idempotency key, confirmation va rollback bormi?
10. Hermes profile update paytida `config.yaml`, SOUL, skills va cron qaysi tomon tomonidan boshqariladi? Config drift qanday oldi olinadi?

### Kanban va workflow

11. `yiguvchi → tekshiruvchi → hisobotchi` zanjirining har bosqichida input, output va acceptance schema nima?
12. Parent vazifa bajarilmasa child vazifa avtomatik bloklanadimi?
13. Worker yiqilsa retry soni, timeout, backoff va inson eskalatsiyasi qanday?
14. Bitta vazifa ikki marta bajarilib, ikki marta Telegram xabari ketmasligini qanday isbotlaymiz?
15. Kanban'da `trace_id` Telegram, model, tool, policy va audit yozuvlari bilan bir xil yuradimi?

### Data, memory va quality

16. Session memory, Dantes global xotirasi, RAG knowledge va xabarlar bazasi bir-biridan qanday ajratiladi?
17. RAG javobida hujjat, sana, xabar yoki bandga citation majburiymi?
18. O'zbekcha-ruscha aralash xabarlar uchun alohida acceptance dataset bormi?
19. Qaysi metrikalar release'ni to'xtatadi: source faithfulness, false positive, false negative, latency, cost yoki uptime?
20. Model yangilanganda regression eval kim tomonidan va qaysi approval bilan o'tkaziladi?

## B. Bizning yuridik va tashkiliy majburiyatlarimiz

Shartnomaga quyidagi savollarni biz o'z majburiyatimiz sifatida kiritishni taklif qilamiz:

1. Biz qaysi yuridik shaxs nomidan xizmat ko'rsatamiz va shartnomani kim imzolash vakolatiga ega?
2. Bizning xizmatimiz “software development”, “AI consulting”, “managed service” yoki bir necha turdagi xizmat sifatida belgilanadimi?
3. Biz Dantes ma'lumotlarini “operator/protsessor” sifatida qayta ishlaymizmi yoki boshqa huquqiy rol bormi?
4. Biz ishlatadigan Hermes, model provider, VPS, Telegram, STT/vision va boshqa subprocessor'lar ro'yxatini beramizmi?
5. Har bir subprocessor ma'lumotni qaysi davlatda qayta ishlaydi va mijozning oldindan yozma roziligi kerakmi?
6. Maxfiy va shaxsga doir ma'lumotlar uchun access matrix, encryption, log, backup va incident response siyosatini taqdim qilamizmi?
7. Ma'lumot sizib chiqsa, qancha vaqt ichida kimga xabar beramiz, zararni kim kamaytiradi va xarajat kimda bo'ladi?
8. AI javobi xato bo'lsa, bizning javobgarlik chegaramiz qanday? Tizim maslahat beradi, final qaror insonda qolishi shartmi?
9. Moliyaviy to'lov, shartnoma imzolash, xodimni jazolash yoki ishdan bo'shatish kabi amallarni AI bajarmasligi shartnomada yoziladimi?
10. Dantes'ning maxsus kodlari, promptlari, SOUL/skill fayllari, schema va integratsiya kodiga IP kimga tegishli bo'ladi?
11. Hermes va boshqa open-source komponentlar uchun license, attribution, source notice va yangilanish majburiyati kimda?
12. Model provider shartlari AI input/output'ni training uchun ishlatadimi? Buni taqiqlash yoki alohida rozilik olish mumkinmi?
13. Mijoz ma'lumotidan anonymized eval yoki bug report uchun foydalanish mumkinmi? Mumkin bo'lsa, qaysi darajada va qancha muddat?
14. Shartnoma tugaganda repo, profile, database, logs, backup, embeddings va model cache qanday qaytariladi yoki o'chiriladi?
15. SLA, support va warranty nimani qamrab oladi: uptime, response time, bug fix, model drift yoki provider outage?
16. Vaziyatga qarab suspend qilish, modelni almashtirish, credential'ni bekor qilish va xavfli tool'ni o'chirish huquqi kimda?

## C. Ulardan bizga kerak bo'ladigan hujjat va ruxsatlar

Mijoz/jamoa quyidagilarni yozma ko'rinishda berishi kerak:

1. Yuridik shaxs rekvizitlari, shartnoma imzolovchi va loyiha egasi.
2. Dantes AI uchun aniq business scope, pilot modullar va “scope'ga kirmaydi” ro'yxati.
3. Telegram guruhlari ro'yxati, bot admin vakolati va guruh a'zolariga berilgan xabardorlik/ruxsat asoslari.
4. 1C, Excel, GPS, ombor va hujjat manbalaridan foydalanishga yozma authorization.
5. Ma'lumotlar inventari: ism, telefon, username, ovoz, rasm, GPS, ishchi ma'lumoti, moliyaviy va tijorat siri qaysi toifaga kiradi?
6. Har bir ma'lumot toifasi uchun processing purpose, retention period, deletion owner va access roles.
7. O'zbekiston fuqarolari ma'lumotlarini saqlash, database registration va chet elga uzatish bo'yicha yuristning yozma pozitsiyasi.
8. Qaysi cloud model/provider'lar ma'qullangan yoki taqiqlanganligi, maxfiy ma'lumot qaysi modelga chiqmasligi.
9. VPS joylashuvi, server egasi, root/admin access, backup location va credential topshirish kanali.
10. AI xatosi yoki security incident bo'lsa, mas'ul shaxs, 24/7 aloqa va qaror eskalatsiyasi.
11. Ombor uchun boshlang'ich qoldiq, mahsulot nomlari lug'ati, birliklar, obyektlar va test dataset.
12. UZ/RU aralash xabarlar, rasm, audio va hujjatlardan tozalangan/synthetic acceptance namunalar.
13. Har agent uchun owner, KPI, qabul qiluvchi va “nima qilmaydi” chegarasi.
14. Real ma'lumot bilan testga rozilik yoki synthetic data bilan test qilish bo'yicha qaror.
15. Qabul mezonlari: aniqlik, citation, xato darajasi, javob vaqti, uptime, audit va rollback.
16. Mijozning tijorat siri, xodim maxfiyligi, IP va data deletion bo'yicha ichki siyosatlari.

## D. Shartnomaga qo'yilishi kerak bo'lgan aniq bandlar

1. **Scope:** qaysi agent, qaysi kanal, qaysi data source va qaysi modul topshiriladi.
2. **Human approval:** AI qarori yuridik, moliyaviy yoki intizomiy final qaror emas.
3. **Data processing:** tomonlarning roli, purpose, categories, location, retention, deletion va subprocessors.
4. **Security:** least privilege, MFA, secret storage, encryption, audit, backup, incident notice va access revocation.
5. **IP:** existing Dantes core, yangi custom code, profile/skill/prompt, client data, model output va open-source license.
6. **Acceptance:** test dataset, KPI, defect severity, retest, sign-off va production'ga o'tish sharti.
7. **Liability:** hallucination, data loss, provider outage, Telegram cheklovi, noto'g'ri input va mijoz ruxsati yetishmasligi uchun mas'uliyat.
8. **Change control:** yangi agent, yangi model, yangi data source yoki yangi write permission faqat change request bilan.
9. **Exit:** export, handover, deletion certificate, credentials rotation va support tugashi.
10. **Audit:** mijozning audit huquqi, bizning loglarni saqlash muddati va maxfiylik chegarasi.

## E. Yuristga alohida beriladigan tekshiruv savollari

1. Telegram guruh xabarlarini, ovozini va hujjat rasmini bot orqali o'qish uchun qaysi rozilik yoki huquqiy asos kerak?
2. O'zbekiston fuqarolari ma'lumotlarini chet eldagi model provider'ga yuborish mumkinmi; qaysi shartlar bilan?
3. Shaxsga doir ma'lumotlar bazasini davlat reyestrida ro'yxatdan o'tkazish bizga yoki mijozga tegishlimi?
4. Dantes ma'lumotlari tijorat siri sifatida belgilanishi uchun mijoz qanday ichki rejim, buyruq va access list yuritishi kerak?
5. Ovoz, yuz/rasm, GPS va xodim faoliyati ma'lumotlari alohida yuqori xavfli toifaga kiradimi?
6. Omborchi yoki moliyachi bergan AI xulosasi qaysi holatda professional advice yoki yuridik/moliya xizmati deb baholanishi mumkin?
7. AI chiqargan hisobot, prompt, skill va generated code'ning mualliflik va foydalanish huquqi kimda bo'ladi?
8. Hermes/open-source license va model provider terms mijozga topshiriladigan deployment bilan mosmi?
9. Kiberhodisa haqida xabar berish, tekshirish, loglarni saqlash va tiklash bo'yicha qaysi muddatlar shartnomaga kiritiladi?
10. Dantes Construction muhim axborot infratuzilmasi subyekti yoki boshqa maxsus tartibga kiradimi?
11. 1C/OData orqali read-only ulanish uchun alohida vendor yoki buxgalteriya authorization kerakmi?
12. Mijoz guruhidagi uchinchi shaxslar, xodimlar yoki kontragentlar uchun alohida notice/consent kerakmi?

## Qizil bayroqlar

Quyidagilardan biri javobsiz qolsa, pilotni production deb e'lon qilmaslik kerak:

- data egasi va processing roli noma'lum;
- Telegram yoki 1C uchun yozma ruxsat yo'q;
- confidential/restricted data qaysi modelga ketishi noaniq;
- AI final yuridik, moliyaviy yoki xodim qarorini o'zi qiladi;
- incident, deletion va backup tartibi yo'q;
- IP va open-source license bandi yo'q;
- acceptance KPI va imzolovchi shaxs belgilanmagan.

## Tayanch manbalar

- [Dantes arxitekturasi](/Users/protochka/dantes/ARXITEKTURA.md), [Dantes topshiriqlari](/Users/protochka/dantes/TASKS.md), [Hermes arxitekturasi](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture).
- [Shaxsga doir ma'lumotlar to'g'risida O'RQ-547](https://lex.uz/docs/-4396419) va 2026-yilgi o'zgartirishlar bo'yicha yurist tekshiruvi.
- [Kiberxavfsizlik to'g'risida O'RQ-764](https://lex.uz/docs/-5960604).
- [Tijorat siri to'g'risida O'RQ-374](https://lex.uz/docs/-2460801).
- [AI rivojlantirish strategiyasi PQ-358](https://lex.uz/docs/-7158604).
