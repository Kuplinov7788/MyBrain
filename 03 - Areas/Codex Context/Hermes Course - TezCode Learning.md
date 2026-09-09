---
type: learning-note
updated: 2026-09-09
source: TezCode Learning topic + Beluga pending media
status: captured-from-captions-and-guide
---

# Hermes Course — TezCode Learning

Bu qayd TezCode’dagi Learning topicida topilgan Hermes kursi xabarlari, Beluga pending media ro‘yxati va yuborilgan `HERMES.md` qo‘llanmasi asosida yozildi. Video ichidagi audio/transkript alohida ko‘chirilmadi; xulosalar caption, file nomlari va qo‘llanma matniga tayangan.

## Manbalar

- Telegram search: `TEZCODE Team Managment` (`id=-1002640882371`) ichida `HERMES KURSI`, `Model tanlash`, `dastlabki 10 ta asos` so‘rovlari.
- Pending media: `HERMES.md` va darslik videolari `dars-11`–`dars-60` oralig‘ida.
- Local fayl: `/Users/protochka/Beluga/state/media/678230831-0.md` — `Hermes Agent — amaliy qo'llanma`.
- Joriy lokal holat uchun alohida manba: [[Hermes Setup]]. Kurs qo‘llanmasi Hermes v0.20.5 haqida; lokal auditda Hermes v0.21.1 tekshirilgan.

## Kurs xaritasi

### Dastlabki 10 ta asos

Telegram xabarlarida “dastlabki 10 ta asos” deb tilga olingan, lekin bu sessiyada ularning alohida nomlari to‘liq ko‘rinmadi. Keyingi darslar aynan shu asoslar ustiga qurilgan.

### 1-kun — fayllar, loglar, pluginlar

11. FILES — Hermes saqlagan fayllar
12. LOGS — xatoni qanday topish
13. PLUGINS nima va nega kerak
14. Plugin o‘rnatish va o‘chirish
15. KANBAN plugini — vazifa taxtasi

Amaliy ma’no: Hermes bilan ishlaganda konfiguratsiya, xotira, skill, log va plugin joylarini bilish birinchi shart. Xato bo‘lsa avval log va config tekshiriladi, keyin modeldan taxmin so‘raladi.

### 2-kun — profillar, MCP va tools

16. PROFILES — bir nechta alohida Hermes
17. Profil yaratish va almashtirish
18. MCP nima — chuqurroq
19. MCP server qo‘shish amalda
20. TOOLS — agentning asboblari

Amaliy ma’no: mijoz, loyiha yoki shaxsiy agentlar bir-birining xotirasi va ruxsatlarini aralashtirmasligi uchun alohida profile ishlatiladi. MCP tashqi servislarni agentga tool sifatida ulaydi, lekin har tool ruxsat va xavfsizlik bilan boshqarilishi kerak.

### 3-kun — Git, memory, curator, sub-agent, browser

21. GIT integratsiyasi — yangi imkoniyat
22. MEMORY — agent nimani eslab qoladi
23. CURATOR — xotirani tartibga soluvchi
24. Sub-agent — vazifani boshqaga topshirish
25. Brauzer asboblari — sayt bilan ishlash

Amaliy ma’no: Git agent ishini tekshiriladigan tarixga aylantiradi. Memory qonun va muhim faktlar uchun, kundalik chat dump uchun emas. Curator xotirani tozalaydi/tartiblaydi. Sub-agent katta vazifani bo‘lishga yordam beradi. Browser tools real sayt/App UI bilan ishlashda foydali.

### 4-kun — webhooks, pairing, auth, ops, analytics

26. WEBHOOKS — tashqi tizim chaqirsa
27. PAIRING — kim ulanishi mumkin
28. AUTH — panelni parol bilan yopish
29. OPS — texnik xizmat buyruqlari
30. ANALYTICS — sarf va statistika

Amaliy ma’no: agentni Telegram, dashboard yoki tashqi tizimga ochishda pairing/auth qatlamlari majburiy. Ops buyruqlari monitoring va restart uchun kerak. Analytics token, xarajat va ishlash ko‘rsatkichlarini nazorat qiladi.

### 5-kun — avtomatlashtirish

31. Avtomatlashtirish 1: kunlik hisobot
32. Avtomatlashtirish 2: pochta saralash
33. Avtomatlashtirish 3: sayt kuzatuvi
34. Avtomatlashtirish 4: fayl tartibi
35. Avtomatlashtirish 5: eslatma yuborish

Amaliy ma’no: Hermesning kuchli tomoni — jadval va fon ishlar. Lekin qo‘llanmadagi muhim tuzoq: cron faqat gateway ishlaganda otadi; jadvalga ishonishdan oldin qo‘lda `cron run` va `gateway status` bilan tekshirish kerak.

### 6-kun — skilllar

36. Skill yozish — birinchi qadam
37. Skill ichida nima bo‘ladi
38. Skill hub — tayyorini olish
39. Skillni sinash va tuzatish
40. Xavfli skilldan qanday saqlanish

Amaliy ma’no: skill — takrorlanadigan workflow va qoidalarni saqlash joyi. Skillga log emas, qayta ishlatiladigan protsedura yoziladi. Xavfli skill ruxsat, credential va side-effect jihatdan tekshiriladi.

### 7-kun — Telegram orqali boshqarish

41. Telegram orqali boshqarish
42. Guruhda ishlatish qoidalari
43. Ovoz bilan buyruq berish
44. Rasm va hujjat yuborish
45. Telefondan turib ishlash

Amaliy ma’no: Telegram agentni telefon orqali ishlatish uchun qulay, lekin guruhda ishlatish ruxsat, mention/reply, topic va auto-reply qoidalari bilan cheklanishi kerak. Media kelganda agent uni avtomatik yuborishga ruxsat deb qabul qilmasligi kerak.

### 8-kun — model va xarajat

46. Model tanlash: tez yoki aqlli
47. Lokal model vs bulutdagi model
48. Kontekst uzunligi nima
49. Xarajatni qanday kamaytirish
50. Zaxira model — biri ishlamasa

Amaliy ma’no: bitta model hamma ishga mos emas. Oddiy matn va saralash arzon modelga, murakkab kod/reasoning kuchli modelga beriladi. Context uzunligi, cached token va fallback reja xarajatni boshqarishning asosiy qismi.

### 9-kun — xato, gateway, update, backup, manual config

51. Xatolikni o‘zi topish yo‘li
52. Gateway o‘lganda nima qilish
53. Yangilash va uning tuzoqlari
54. Zaxira nusxa va tiklash
55. Sozlamalarni qo‘l bilan boshqarish

Amaliy ma’no: agentga “ishlamayapti” deyishdan oldin gateway, log, config, auth va queue tekshiriladi. Update oldidan backup/snapshot kerak. Manual config o‘zgartirilsa, keyin health check qilinadi.

### 10-kun — yakuniy workflow va imtihon

56. Hammasini birlashtirish: ish oqimi
57. Mars akademiya uchun 3 g‘oya
58. Tezcode uchun 3 g‘oya
59. Xavfsizlik yakuniy tekshiruv
60. Imtihonga tayyorgarlik

Amaliy ma’no: yakuniy maqsad — agentni shunchaki chat emas, tekshiriladigan workflowga aylantirish: manba → tool → ruxsat → natija → verification → qisqa hisobot. Mars/TezCode g‘oyalari alohida loyiha qarori sifatida ajratib yozilishi kerak.

## HERMES.md qo‘llanmasidan eng muhim saboqlar

1. Hermes — local AI assistant: terminali, memory, cron va gateway/channel qatlamlari bor. Bu uni 24/7 jadval va avtomatlashtirish uchun qulay qiladi.
2. Claude Code/Codex chuqur repo ishlari va reviewda kuchliroq; Hermes esa fon ishlar, cron, alohida profile va gateway oqimlarida foydali.
3. `~/.hermes/` asosiy home: config, `.env`, memories, skills, profiles, cron va sessions shu yerda. `.env` sir hisoblanadi va vaultga yozilmaydi.
4. Skript/worker ichida `hermes` PATH’da bo‘lmasligi mumkin; avtomatlashtirishda to‘liq path ishlatish kerak.
5. Loyiha papkasidan chaqirilsa project context agent kimligini o‘zgartirishi mumkin; neutral folder yoki aniq `--in` ishlatiladi.
6. `hermes tools` TTY talab qilishi mumkin; skriptbop buyruqlar uchun `chat -Q -q`, `cron list/run/status`, `sessions list`, `gateway status` ishlatiladi.
7. Cron gatewayga bog‘liq: gateway o‘chsa job jim qolishi mumkin. Cron qo‘yilgach qo‘lda run va status tekshiruvi shart.
8. Memory qonun/faktlar uchun; agar agent bir xatoni takrorlasa faqat memory qoidasini ko‘paytirish emas, mexanizmni kodga ko‘chirish kerak.
9. Mijoz ko‘radigan javob ichki path, traceback, secret yoki texnik dumpni chiqarmasligi kerak.
10. Mijoz/loyiha agentlari alohida profileda turishi kerak, shunda xotira va credential aralashmaydi.

## Emirhan/Beluga uchun qo‘llash

- Beluga Telegram transportni boshqaryapti; Hermes gatewayni parallel yoqishdan oldin duplicate worker va token routing tekshiriladi.
- MyBrain yagona bilim bazasi bo‘lib qoladi: Hermes, Beluga va boshqa agentlar kerakli qaydni o‘qiydi, lekin maxfiy credential saqlamaydi.
- TezCode/Learning materiallari avtomatik yuborish ruxsati emas; o‘qish va xulosa qilish alohida, yuborish esa ownerning aniq buyrug‘i bilan host orqali bo‘ladi.
- Har yangi automation uchun minimal qabul mezoni: scope → dry run → real check → log/status → qisqa hisobot.

## Ochiq joylar

- Dastlabki 1–10 dars nomlari bu sessiyada to‘liq topilmadi.
- Video ichki audio/transkript tahlili bajarilmadi; kerak bo‘lsa keyingi bosqichda fayllar bo‘yicha transkripsiya qilinadi.
- TezCode forum topic metadata tool natijasida alohida ko‘rinmadi; qidiruv group ichida bajarildi va Hermes kursi xabarlari topildi.

## Aloqador

- [[Hermes Setup]]
- [[Beluga Usage]]
- [[Operating System]]
- [[Context MOC]]
