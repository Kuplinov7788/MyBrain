---
type: project-review
project: Dantes AI
observed: 2026-09-20
status: read-only review
---

# Dantes AI — loyiha va Hermes dashboard ko‘rigi

## So‘rov va chegara

- [foydalanuvchi talabi] Emirhan `/Users/protochka/dantes` papkasini o‘qib, loyiha nima ekanini, nimalar borligini va nimalar qilish mumkinligini tushuntirishni hamda `https://bekzod-asosiy.tailb558fb.ts.net/profiles` Hermes dashboardiga kirishni so‘radi.
- [foydalanuvchi qarori] 2026-09-20: hozir hech qanday loyiha ishini boshlamaslik; faqat shu ko‘rikni Obsidian vaultga batafsil saqlash. Kelgusi ishlar quyida **taklif**, bajarilgan vazifa yoki ish boshlashga ruxsat emas.
- [tekshirildi: lokal CLI/browser] Ko‘rikda Dantes kodi va dashboard faqat o‘qildi. Gateway restart, bot ishga tushirish, vazifa yaratish yoki Telegramga xabar yuborish bajarilmadi.

## Loyiha nimaga xizmat qiladi

- [tekshirildi: `dantes/README.md`, `AGENTS.md`, `ARXITEKTURA.md`] Dantes Construction uchun AI xodimlar tizimi. Telegram guruh xabarlarini yig‘ish, xodimlar registri, ruxsat tekshiruvi, audit izi va boshqaruv hisobotlari uning asosiy qismlari. Hermes profillar, suhbat va Kanban ishlarini boshqaradi; biznes hisoblari Dantes Python kodida.
- [tekshirildi: `scripts/digest_topshiriq.py`] Mo‘ljallangan kunlik zanjir: yig‘uvchi → tekshiruvchi → hisobotchi. Vazifa Kanban’da oldingi qadamga bog‘langan, takror yaratishni cheklash uchun sana bo‘yicha idempotency key ishlatiladi.
- [tekshirildi: `scripts/core.py`, `baza.py`, `collector.py`, `xotira.py`] Registr/ruxsat/audit yadrosi, SQLite yoki PostgreSQL bazasi, Telegram xabar yig‘uvchi va strukturali ish xotirasi kodi mavjud. Kodning mavjudligi jonli servis ishlayotganini isbotlamaydi.
- [tekshirildi: `dantes/AGENTS.md`] Sinov davrida mijoz guruhlariga xabar yuborish taqiqlangan; u yerda bot faqat o‘qiydi. Yuborish yo‘li alohida oq ro‘yxat bilan chegaralanadi. Lokal kollektor/gatewayni qo‘shimcha nusxa qilib ko‘tarish bir tokenli Telegram jarayoni bilan to‘qnashishi mumkin.

## Papkalar va 13 xodim

| Qism | Hozirgi ma’nosi |
|---|---|
| `scripts/` | Yadro, baza, kollektor, guard, testlar, Kanban digest, Telegram yuborish qulfi va yordamchi jarayonlar. |
| `xodimlar/` | Har xodim uchun manifest (`xodim.json`), rol matni, Hermes profil tarqatmasi, skill va ayrimlarida mustaqil Python kodi/testlari. |
| `docs/` | Standartlar, quruvchi qo‘llanmalari va sanali sinov/audit hisobotlari. |
| `deploy/` | Serverga o‘rnatish va yangilash skriptlari. |
| `HOLAT.md` / `TASKS.md` | Tarixiy o‘lchovlar, bajarilgan va ochiq vazifalar; o‘zgaruvchan raqamni qayta tekshirish kerak. |

| Xodim | Rol | `xodim.json` holati |
|---|---|---|
| rahbar | Orkestrator va rahbariyatga javob | faol |
| yiguvchi | Guruh xabarlarini yig‘ish va tasniflash | faol |
| tekshiruvchi | Sifat va manbani tekshirish | faol |
| hisobotchi | Kunlik digest, savol-javob va eskalatsiya | faol |
| omborchi | Uch ombor bo‘yicha qoldiq, sarf va tugash bashorati | faol |
| integrator1c | 1C eksport/OData o‘qish va moslash | rejalashtirilgan |
| kutubxonachi | Hujjatlarni indekslash va manbali qidirish | rejalashtirilgan |
| moliyachi | Pul oqimi, byudjet chetlanishi, qarzdorlik | rejalashtirilgan |
| quruvchi | Obyekt hisobotlari va muddat kuzatuvi | rejalashtirilgan |
| sinovchi | Qabul sinovlari, tezlik, RBAC va audit | rejalashtirilgan |
| sotuvchi | Katalog asosida variant va tijorat taklifi loyihasi | rejalashtirilgan |
| transportchi | Avtopark, GPS, yoqilg‘i, ta’mir | rejalashtirilgan |
| yurist | Shartnoma xavfi, muddat va xat loyihasi | rejalashtirilgan |

- [tekshirildi: `xodimlar/*/xodim.json` va `kod/`] 13 papka bor; 5 ta manifestda `faol`, 8 tasida `rejalashtirilgan`. To‘qqizta rolning alohida Python ish kodi va testi bor. Manifestdagi `faol` — dashboard gateway ayni paytda ishlayotganining dalili emas.
- [tekshirildi: `omborchi.py`, `moliyachi.py`, `integrator1c.py`, `kutubxona.py`, `yurist.py`] Omborchi CSV harakatlaridan qoldiq, tugash xavfi, hujjatsiz harakat va haftalik hisobotni hisoblaydi; moliyachi hisob-kitob qiladi, to‘lov yubormaydi; 1C integratori ma’lumotni o‘qish yo‘liga mo‘ljallangan; kutubxonachi SQLite FTS5 bilan manbali qidiradi; yurist hujjat tahlili va xat loyihasi yaratadi. Ularning real mijoz ma’lumotida ishlashi bu ko‘rikda sinalmadi.

## Hermes dashboardda 2026-09-20 ko‘ringani

- [tekshirildi: browser, `/profiles`] Login `dantes`, dashboard v0.21.0. 15 profil: `default`, `dantes` va 13 xodim. Profillar ro‘yxatida `default` active profile sifatida ko‘rindi; kartalarda `Gateway stopped`, panelda `Active Sessions: 0` yozilgan. Bu kuzatuv aynan ochilgan dashboard holati; barcha tashqi jarayonlar haqida umumiy xulosa emas.
- [tekshirildi: browser, `/kanban`] `Dantes AI` doskasida 3 ta vazifa `Done`: 2026-09-06 xabar yig‘ish (`@yiguvchi`), tekshirish (`@tekshiruvchi`), digest (`@hisobotchi`). `Ready` va `In Progress` 0. UI belgisi haqiqiy Telegram yetkazilishi yoki hisobot sifati isboti emas.
- [tekshirildi: browser] Panelda Chat, Sessions, Files, Models, Logs, Cron, Skills, Plugins, MCP, Channels, Webhooks, Pairing, Profiles, Config, Keys, System, Documentation va Kanban bo‘limlari bor. Ularning ichki ma’lumoti va sog‘ligi birma-bir audit qilinmadi.

## Tarixiy qaydlar va aniqlik chegarasi

- [tekshirildi: `HOLAT.md`] Oxirgi yangilanish 2026-09-13/15. O‘sha paytda 23/23 yadro va 97/97 tizim sinovi, 5 faol xodim, gateway ishga tushmagan, xotira 0, real bo‘lim ma’lumoti yo‘q deb yozilgan. Bu **hozirgi test yoki runtime natijasi emas**; ushbu suhbatda testlar yuritilmadi.
- [tekshirildi: `HOLAT.md` va dashboard] `HOLAT.md` Kanban vazifasi 0 deb yozadi, 2026-09-20 dashboard esa Dantes doskasida 3 ta eski `Done` vazifasini ko‘rsatdi. Farqni vaqt va manba bilan qayd qilish kerak.
- [tekshirildi: `TASKS.md`, `dantes-config.json`, Git log] `TASKS.md` T24 kollektor avtomatik qayta ko‘tarilishini o‘chiq deb qayd etgan; joriy configda `qorovul_collector_kotarish: true`, so‘nggi commitda ham T24 yoqilgani yozilgan. Ishlayotgan guard jarayoni aynan shu configdan foydalanyaptimi, tekshirilmadi.
- [tekshirildi: `xodimlar/rahbar/config.yaml`] Profil configida `terminal.cwd` yo‘q. `HOLAT.md` ham 13 configda bu qiymat yo‘qligini qayd qiladi. Bu Hermes AGENTS zanjiri qayerdan o‘qilishini tekshirishga arziydi; jonli profil sozlamasi alohida ko‘rilmadi.
- [tekshirildi: `.github/workflows/ci.yml`] CI Python 3.12 bilan test buyruqlarini belgilaydi, ammo `requirements-dev.txt` o‘rnatish qadami yo‘q. CI hozir ishlagan yoki yiqilganini bu ko‘rik isbotlamaydi.
- [tekshirildi: Git] Macdagi `dantes` checkout `67d84fb` commitda edi, `git status --short` bo‘sh chiqdi. Bu faqat lokal checkout holati; Windowsdagi Hermes profillari yoki server deploy shu commit bilan tengligi tekshirilmadi.

## Nimalar qilish mumkin — keyingi ish sifatida, boshlanmagan

1. [taklif] Avval gateway, kollektor, guard, sessiyalar, Kanban dispatcher va model ulanishining jonli holatini alohida tekshirish; dashboarddagi `stopped` sababini aniqlash. Servisni ko‘tarish shu qayd bilan buyurilmagan.
2. [taklif] Bitta ombor vertikalini sintetik ma’lumotdan boshlab, real import sxemasi va manbalar bilan tekshirish: qoldiq, sarf, tugash sanasi va hujjatsiz harakat. 1C versiyasi/eksport formati mijozdan aniqlanmaguncha real integratsiyani taxmin qilmaslik.
3. [taklif] Xabar → yig‘uvchi → tekshiruvchi → hisobotchi zanjirini xavfsiz sinov muhitida o‘lchash, biriktirmalar va yetkazishni alohida tasdiqlash. Mijoz guruhiga sinov xabari yubormaslik.
4. [taklif] `HOLAT.md` va `TASKS.md` ni yangi o‘lchovlarga mos yangilash; xususan Kanban soni, T24 va `terminal.cwd` masalasini ajratish.
5. [taklif] Keyin ovoz/rasm aniqligi, hujjat qidiruvi, moliya va boshqa xodimlarni manba ma’lumotiga qarab bosqichma-bosqich baholash. Media kodi borligi real aniqlik yoki tayyor mahsulotni anglatmaydi.

## Manbalar

- Lokal loyiha: `/Users/protochka/dantes/README.md`, `AGENTS.md`, `ARXITEKTURA.md`, `HOLAT.md`, `TASKS.md`, `dantes-config.json`; `scripts/` va `xodimlar/` ichidagi yuqorida nomlangan fayllar.
- 2026-09-20 o‘qilgan dashboard: [Profiles](https://bekzod-asosiy.tailb558fb.ts.net/profiles) va [Dantes AI Kanban](https://bekzod-asosiy.tailb558fb.ts.net/kanban).
- Bog‘liq MyBrain sahifalari: [[Hermes Hub]], [[Hermes Setup]], [[Last Session]].
