---
type: product-architecture-direction
project: Dantes AI
observed: 2026-09-25
status: user direction; concept only
---

# Dantes uchun biznes agentlar dashboardi

## Foydalanuvchi yo'nalishi

- [foydalanuvchi yo'nalishi] AI agentlar biznesni avtomatlashtirishga xizmat qilishi kerak; misollar sifatida CEO, HR va boshqa xodim rollari aytildi.
- [foydalanuvchi yo'nalishi] Julian Goldie ko'rsatgan Agent OS dashboardiga o'xshash, lekin Dantes loyihasiga mos boshqaruv paneli kerak.
- [ochiq] Panel Dantes Construction mijozining ishiga moslanadimi yoki TezCode/AiSolution'ning o'z biznes jarayonlarimi — aniqlanmagan. Bu qaror HR ma'lumoti, KPI va ruxsat chegaralarini belgilaydi.

## Dantes'da tekshirilgan tayanch

- [tekshirildi: CLI, 2026-09-25] `/Users/protochka/dantes` Git ishchi daraxti `main...origin/main` holatida toza.
- [tekshirildi: `xodimlar/*/xodim.json`, 2026-09-25] 13 ta xodim manifesti bor: 5 `faol`, 8 `rejalashtirilgan`. `rahbar` — faol AI orkestrator; CEO va HR alohida manifest sifatida topilmadi.
- [tekshirildi: `scripts/dantes_dashboard.cmd`] Mavjud launcher Hermes dashboard'i 8791-portda ishga tushiradi. Bu Hermes operator paneli; Dantes biznes KPI va tasdiq jarayonlariga alohida moslashtirilgan custom panel borligi koddan topilmadi.
- [tekshirildi: `ARXITEKTURA.md`] Hermes agent/profilni yuritadi, Kanban vazifani kim va qachon bajarishini boshqaradi, Dantes `core.py` esa ruxsat, audit va biznes siyosatini ushlab turadi. VPS'da dashboard porti ochilmasligi, kerak bo'lsa SSH tunnel ishlatilishi yozilgan.
- [tarixiy kuzatuv: 2026-09-20 Dantes Audit] O'sha kuni Hermes UI'da Profiles, Sessions, Chat, Logs, Config va Kanban kabi operator bo'limlari ko'rilgan; `Gateway stopped`, 0 faol sessiya va 3 eski `Done` karta qayd etilgan. Bu 2026-09-25 dagi jonli runtime holati emas.

## Julian Agent OS bilan farqi

- [tekshirildi: public GitHub] `nilhemdot/agent-os` o'zini Hermes/Claude/OpenClaw va boshqa komponentlarni bitta lokal command center'da jamlaydigan Agent OS pack deb ta'riflaydi; README pack sanasi 2026-07-03. Julian Goldie yoki Boardroom'ning kanonik rasmiy repo'si ekanini public sahifadan tasdiqlab bo'lmadi. Uni tayyor Dantes yechimi emas, UI/ish oqimi namunasi sifatida ko'rish kerak.
- [aniqlashtirildi: Julian Agent OS] `gdotbat/Hermes-agentic-os` README o'zini Julian Goldie qurgan deb ataydi, ammo repo `quoctuancqt/agentic-os` fork'i; clone uchun JulianGoldie repo'siga collaborator access kerakligini va AIPB a'zolari uchunligini yozadi. Public Agent OS packning `nilhemdot/agent-os` README'si esa butun agent jamoasi/org-chart uchun **Paperclip**ni alohida ixtiyoriy modul deb ko'rsatadi. Demak Agent OS — yagona kompaniya boshqaruv backend'i emas.
- [tekshirildi: Hermes rasmiy docs] Hermes dashboard profil, konfiguratsiya, skill/tool, sessiya va runtime boshqaruvi uchun machine-level panel. Hermes Kanban plugin esa xodim profillari o'rtasidagi topshiriqlarni ko'rsatadi. Rasmiy Kanban qo'llanmasida org-chart, biznes KPI va governance gate'lari plugin doirasidan tashqarida deb ko'rsatilgan.
- [cheklov] Onlayn Hermes docs Dantes deploy qiladigan versiyadan yangiroq bo'lishi mumkin: `ARXITEKTURA.md` VPS Hermes'ni `74f99af` (`v0.20.4`) commitiga pin qiladi. Plugin va API imkoniyatlarini tanlashdan oldin aynan shu pin bilan mosligini tekshirish kerak.

## GitHub repo'lar taqqoslanishi

Baholar — repo tavsifi va Dantes arxitekturasiga tayangan Codex xulosasi; kodni klonlab ishga tushirish yoki adapter integratsiya testi qilinmagan.

| Repo | Dantes biznes paneliga mosligi | Kuchli tomoni | Dantes bilan asosiy farq |
|---|---:|---|---|
| [`paperclipai/paperclip`](https://github.com/paperclipai/paperclip) | **9/10 biznes maqsadi; 6/10 Dantes'ga tayyor ulanish** | AI kompaniya/org chart, rollar, maqsadlar, task, budget, approvals, audit; MIT. Rasmiy Paperclip docs `hermes_local` (lokal CLI) va `hermes_gateway` (HTTP/SSE) built-in adapterlarini tasdiqlaydi. | Dantes'ning 13 profili, maxsus `HERMES_HOME`, Kanban va `core.py` siyosatini Paperclip agent/task modeliga map qilish tekshirilmagan. Custom `HERMES_HOME` skills inventory bug'i upstream issue'da qayd etilgan. Ruxsat va audit authority Dantes `core`da qolishi kerak. |
| [`gdotbat/Hermes-agentic-os`](https://github.com/gdotbat/Hermes-agentic-os) | **4/10** | Hermes CLI, chat, voice, Obsidian journal/goals uchun lokal command center. | Biznes org-chart/bo'lim KPI/approval control-plane emas; README foydalanishni AIPB a'zolariga cheklaydi va resale/redistribution'ni man qiladi. |
| [`nilhemdot/agent-os`](https://github.com/nilhemdot/agent-os) | **4/10 biznes panel; 7/10 UX namuna** | Claude, Hermes, OpenClaw va boshqa lokal vositalarni bitta dashboard'da jamlaydi; optional Paperclip module bor. | Personal/local command center va pack yo'riqnomasi; HR, Dantes ruxsat va biznes data modelini almashtirmaydi. README pack sanasi 2026-07-03. |
| [`benjaminLedel/covey`](https://github.com/benjaminLedel/covey) | **5/10 hozirgi integratsiya** | AI agentlar uchun identity/HR, org-chart, izolatsiya, credential broker va markaziy approval g'oyasi juda mos. | Hozirgi runtime adapter Claude Code; Hermes ko'rsatilmagan. Go + Postgres va alohida platforma sifatida Dantes'ga og'irroq; AGPL-3.0 sharti mijozga tarmoq orqali xizmat ko'rsatishda alohida ko'rib chiqiladi. |
| [`fab-agent/agentic-organization`](https://github.com/fab-agent/agentic-organization) | **5/10** | Org chart, department/personnel, policies, autonomous flows va A2A delegation uchun approval paneli bor; MIT. | O'z provider, registry, chat, flow va A2A platformasini olib keladi; Dantes/Hermes tayyor ko'prigi README'da yo'q, natijada ikki xil agent/control-plane paydo bo'lishi mumkin. |

### Tanlov

- [xulosa] Eng mos public repo — **[`paperclipai/paperclip`](https://github.com/paperclipai/paperclip)**. Julian Agent OS README'sining o'zi Paperclip'ni AI xodimlar jamoasini kompaniya kabi boshqarish uchun alohida modul sifatida ko'rsatadi.
- [baholash] Paperclip'ning biznes boshqaruv konsepsiyasi **9/10**, Hermes runtime bilan native mosligi hujjat bo'yicha **9/10**, aynan Dantes profil/`HERMES_HOME`/policy mapping'i **6/10** (hali sinovsiz). Dantes'ga moslashtiriladigan asos sifatida umumiy xulosa **8/10**, tayyor o'rnatib ishlatish emas.
- [tekshirildi: rasmiy Paperclip docs] `hermes_local` Hermes CLI'ni child process sifatida ishga tushiradi; `hermes_gateway` esa Hermes REST/SSE API serveriga ulanadi. `hermes_gateway` uchun Hermes API server alohida yoqilgan va ruxsati kalit bilan himoyalangan bo'lishi kerak.
- [cheklov: upstream issue, 2026-08-20; 2026-09-25 da Open] Paperclip adapterida non-default `HERMES_HOME` bo'lsa Hermes skill inventory noto'g'ri papkadan o'qilishi qayd etilgan; issue runtime ishlashiga emas, skills ko'rinishiga ta'sir qilishini aytadi. Dantes'ning maxsus Hermes home'i sabab bu alohida acceptance tekshiruvi bo'ladi.
- [cheklov: upstream issue, 2026-08-11; 2026-09-25 da Open] Paperclip v2026.722.0 dagi Hermes Gateway adapterida per-agent model/provider tanlovi yo'q deb qayd etilgan. Dantes xodimlarida alohida model/trust talabi borligi sabab gateway'ni tanlashdan oldin masala yechilganini yoki boshqa konfiguratsiya yo'lini tasdiqlash zarur.
- [xulosa: Dantes Hermes mosligi] Rasmiy adapter sahifasida Dantes'ning har bir Hermes profilini tanlaydigan aniq `profile` parametri ko'rsatilmagan. Shu sabab Paperclip 13 Dantes profilini to'g'ri tanlashi va Dantes `core.py` ruxsat/audit yo'lini chetlab o'tmasligi isbotlanmagan.
- [taklif] Paperclip biznes cockpit/orchestrator UI bo'lsin, Hermes agent runtime'ni bajarsin, Dantes `core.py` biznes amallarining yagona policy/audit eshigi bo'lib qolsin. Avval read-only agent holati va tasdiqlangan task ko'rinishi; write amallar faqat Dantes core'dan o'tadigan bog'lov bilan.
- [asosiy risk] Paperclip boshqaruv qatlamiga ega, Dantes'da esa xodim manifesti, Hermes Kanban va o'z `core`i bor. Bitta vazifa yoki agent uchun ikki tizimning parallel source-of-truth bo'lishiga yo'l qo'ymaslik kerak.
- [tuzatish: avvalgi xulosa] README'dagi runtime ro'yxatiga qarab Hermes adapteri yo'q deb yozilgan edi. Joriy rasmiy Paperclip adapter docs va `v2026.626.0` release notes `hermes_local` + `hermes_gateway` built-in ekanini tasdiqladi; Paperclip Hermes runtime integratsiyasiga oid ball yuqoriga tuzatildi. Dantes maxsus profillari bilan ishlashi hali tekshirilmagan.

## Dantes uchun dastlabki mahsulot xulosasi

- [xulosa] Hermes dashboard'ini operator/texnik panel sifatida qoldirib, uning ustiga Dantes'ning alohida **Biznes agentlar cockpit'i** kerak bo'ladi. U agent runtime holatini biznes natijasi va inson javobgarligi bilan bog'laydi.
- [taklif] Birinchi versiyada o'qish rejimidagi: kompaniya ko'rsatkichlari va manba yangiligi; agentlar ro'yxati (rol, egasi, ruxsat, KPI, holat); mavjud Hermes Kanban vazifalari; tekshiruv/tasdiq kutayotgan ishlar; audit va ogohlantirishlar bo'lishi mumkin.
- [taklif] Har KPI va ogohlantirish manba, vaqt va ishonchlilik holatini ko'rsatsin. Agentda real ma'lumot yoki tasdiqlangan ulanish bo'lmasa, raqam o'ylab topmasin — "ma'lumot yo'q" yoki "eskirgan" deb ko'rsatsin.
- [taklif] CEO agentini boshqaruvga hisobot va variantlar beradigan yordamchi sifatida chegaralash; yakuniy pul, shartnoma, ishga olish/bo'shatish va intizomiy qarorlar odamda qolsin. HR agentiga xodim ma'lumotini faqat yozma ruxsat, maqsad va cheklangan ruxsat aniqlangandan keyin ulash.
- [taklif] Agent harakati kerak bo'lsa, UI to'g'ridan-to'g'ri Hermes yoki bazaga vakolat bermasin: ruxsat va auditni Dantes `core`/aniq API orqali o'tkazsin. Mijoz Telegram guruhiga yuborish sinov taqiqi saqlansin.
- [taklif] Hermes dashboard'ini internetga bevosita ochmaslik; Dantes arxitekturasidagi localhost + SSH tunnel chegarasini saqlash.

## Keyingi qaror

Panel maketini yoki kodini boshlashdan avval maqsadli biznesni aniqlash: Dantes Construction mijozimi yoki TezCode/AiSolution'ning o'z operatsiyalarimi? Keyin CEO/HR va boshqa rollarning vazifalari, ma'lumot manbalari, KPI va odam tasdig'i talab qiladigan amallarni belgilash.

## Vizual xarita, Kanban, Hermes va Obsidian mezonlari (2026-09-25)

- [foydalanuvchi talabi] Dashboard agentlarni galaktika/xarita ko'rinishida ko'rsatsin, Trello'ga o'xshash vazifa taxtasi bo'lsin, Hermes agentlarini boshqarsin va Obsidian bilan bilim ulashsin; Dantes'ga moslashtirish afzal.
- [xulosa: eng mos UI asosi] Shu aniq mezonlar bo'yicha **[`Fruxano/fruvisi`](https://github.com/Fruxano/fruvisi)** Paperclip'dan yaxshiroq boshlang'ich UI: Hermes dashboard plugin'i, React Flow asosidagi 2D org chart, bo'lim/guruh ranglari, qidiruv, layout, jamoa presetlari va native Hermes Kanban vazifasini agentga drag/drop bilan biriktirish mavjud. Alohida task bazasi ochmaydi.
- [cheklov: galaktika] Hozirgi FruVisi — 2D tashkiliy xarita; 2.5D/3D spatial ko'rinish roadmap'da. Agent kartalarida live ishlash holati ham roadmap'da; UI inglizcha. Shuning uchun hozirgi talabning “galaktika” qismi vizual org-chart darajasida, haqiqiy 3D galaxy emas.
- [qulaylik bahosi] README'dagi oqim bo'yicha guruh spotlight/search, avtomatik joylashuv, agent kartasidan profil ko'rish, bo'sh task'ni sudrab tayinlash, tez task yaratish va Hermes gateway'dan tabiiy tilda preset almashtirish qulay. Biznes KPI, bo'lim natijasi, approval navbati, audit va xarajat overview'i FruVisi'da yo'q.
- [maturity/versiya] Public repo sahifasida 1 commit va 4 star ko'rinadi; README Hermes >=0.15 talab qiladi, ammo faqat 0.18.2 bilan sinaganini yozadi. Dantes arxitekturasida server Hermes 0.20.4'ga pin qilingan. 0.20.4 bilan ishlaydi deb taxmin qilmay, aynan shu versiyada compatibility tekshiruvi zarur.
- [Dantes mapping xavfi] Dantes agenti = Hermes profil + `xodim.json` manifesti + yadro ruxsati. FruVisi yangi profil yaratish wizard'i, Hermes profile description'iga org/preset belgilarini yozish va per-agent OpenRouter fallback'ini taklif qiladi. Dantes'da wizard'ni o'chirib/cheklab, xodim nomi/rol/status/ruxsatni `xodim.json`dan o'qitish; assignment'ni Hermes Kanban bilan saqlash; metadata yozishni Dantes sinxronlash bilan konfliktga tekshirish kerak. Fallback modelni esa `core.py` ishonch siyosatiga bog'lamaguncha yoqmaslik kerak.
- [Obsidian ulanishi] Hermes rasmiy MCP qo'llanmasi local/remote MCP serverlarni qo'llaydi. [`Vasallo94/obsidian-mcp-server`](https://github.com/Vasallo94/obsidian-mcp-server) Hermes uchun read/search/link inspection'ni, ixtiyoriy va standartda o'chirilgan write pack'ni taqdim etadi. Bu FruVisi ichidagi tayyor Obsidian integratsiya emas; MCP orqali alohida agent capability.
- [maxfiylik/joylashuv] `MyBrain` Emirhanning shaxsiy vault'i; Dantes runtime esa VPS'da. Mijoz agentlariga butun MyBrain'ni ochish mos emas va VPS lokal Mac vault'iga bevosita kira olmaydi. Kerak bo'lsa, Dantes uchun alohida, tanlangan va VPS'da ruxsatlangan vault/context papkasini avval read-only ulash; yozish huquqini keyin aniq yo'l va audit bilan qo'shish.
- [taqqoslash] **Paperclip** kompaniya holati, live agent status, tasklar, sarf va approval'lar uchun kuchliroq, Hermes adapteri bor, lekin “galaktika” xaritasi emas va Dantes uchun ikkinchi agent/task control plane yaratishi mumkin. **`mojomast/hermesdashboard`** session/file/tool/model/skill grafigi va live subagent drawer'ini beradi, ammo README'da Kanban va org-chart yo'q — uning grafigi xodimlar ierarxiyasi emas, runtime aloqalari.
- [joriy tanlov] Agar bir repo asosidan boshlash kerak bo'lsa, **FruVisi'ni Hermes dashboard ichidagi 2D org-chart + Kanban UI prototipi sifatida olish (UI-asos 8/10; Dantes'ga tayyor holati 5/10)**; Paperclip'dan esa KPI/approval/cost overview g'oyalarini olish. Haqiqiy biznes cockpit uchun ularni Dantes `xodim.json`/`core.py`/DB bilan bitta manbali qatlamga moslashtirish lozim.
- [tekshiruv chegarasi] Ushbu baho public README/docs va lokal Dantes hujjatlariga asoslangan. FruVisi klonlanmadi, o'rnatilmadi yoki Hermes 0.20.4'da ishga tushirilmadi; moslik va xavfsiz mapping hali isbotlanmagan.

## 2026-09-28 — Uysot Sales dashboard kuzatuvi

- [tekshirildi: Uysot UI] Menejer akkauntlari, loyiha xonadonlari, 2026-yil sotuv statistikasi, CRM voronkasi, sentabr qarzdorlik va to‘lov grafigi ko‘rildi; sanasi, qiymatlari va cheklovlari Dantes repo’dagi `docs/UYSOT-SALES-DASHBOARD-KUZATUVLARI-2026-09-28.md`da.
- [xulosa] Uysotda qarzdorlik mas’uli va to‘lov turi/summasi ko‘rinsa ham, agentning vazifasi/vakolati aniqlanmagan. Sales jarayonini tasdiqlashi kerak; alohida Finance bo‘limi tasdiqlanmagan.
- [qaror] Yangi mazmunli, tekshirilgan Uysot/Sales ma’lumotlari MyBrain Sales qaydi va Dantes loyihasidagi tegishli hujjatda saqlanadi. Salesga o‘zidan-o‘zi xabar yuborilmaydi.
- [Sales javobi: 2026-09-28] Bitta sotuvchi barcha loyihalarni yuritadi; qarz mas’uli mijozga bir necha ogohlantirish beradi, keyin direktorga eskalatsiya qiladi. Suhbatdosh to‘lovlarni tekshirib Uysotga kiritadi; mijozlarga korporativ raqamdan qo‘ng‘iroq qiladi. Tafsilotlar Dantes Uysot kuzatuv hujjatida.
- [tuzatish] `Продажа` sahifasidagi 4 raqamini Sales noto‘g‘ri deb aytdi; tasdiqlangan sotuv soni emas. “Finance” avvalgi savolda asossiz qo‘llangan.

## Manbalar

- [Dantes repo](/Users/protochka/dantes/README.md), [arxitektura](/Users/protochka/dantes/ARXITEKTURA.md), [xodimlar standarti](/Users/protochka/dantes/xodimlar/README.md), [dashboard launcher](/Users/protochka/dantes/scripts/dantes_dashboard.cmd).
- [[Dantes Audit 2026-09-20]], [[Dantes-Hermes Moslik Tahlili 2026-09-20]], [[AI Profit Boardroom Analysis 2026-09-25]].
- [Paperclip upstream](https://github.com/paperclipai/paperclip), [Hermes adapter](https://docs.paperclip.ing/reference/adapters/hermes/), [Hermes Gateway adapter](https://docs.paperclip.ing/reference/adapters/hermes-gateway/), [non-default HERMES_HOME issue](https://github.com/paperclipai/paperclip/issues/11760), [gateway model selection issue](https://github.com/paperclipai/paperclip/issues/11219), [Covey](https://github.com/benjaminLedel/covey), [Agentic Organization](https://github.com/fab-agent/agentic-organization).
- [Julian Goldie Agent OS public candidate](https://github.com/nilhemdot/agent-os).
- [Hermes Web Dashboard](https://hermes-agent.nousresearch.com/docs/user-guide/features/web-dashboard), [Hermes Kanban](https://hermes-agent.nousresearch.com/docs/user-guide/features/kanban).
- [FruVisi](https://github.com/Fruxano/fruvisi), [Hermes MCP](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp), [Obsidian MCP server](https://github.com/Vasallo94/obsidian-mcp-server), [Hermes Dashboard graph candidate](https://github.com/mojomast/hermesdashboard).
