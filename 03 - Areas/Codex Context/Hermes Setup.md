---
type: setup-audit
updated: 2026-09-13
status: configured-memory-active
---

# Hermes — sozlash va rivojlantirish xaritasi

## 2026-09-13 — Dashboard model kartalari

- Dashboarddagi ko‘p karta bir vaqtda ishlayotgan ko‘p model degani emas; ular
  `state.db`dagi sessionlarni model, provider va source metadata bo‘yicha guruhlaydi.
- Joriy default profil bitta: `openai-codex` + `gpt-5.5`.
- Tekshiruvda DB’da 1503 session va 3225 message bor edi. Asosiy guruhlar:
  `gpt-5.5/openai-codex/tool` — 1349, provider belgisi yo‘q `gpt-5.5/tool` —
  141, `gpt-5.5/openai-codex/cli` — 10 va tarixiy Nous free sessionlari.
- Provider belgisisiz `GPT-5.5` kartalari alohida model emas, eski yoki to‘liq
  billing/provider metadata yozilmagan sessionlar bo‘lishi ehtimoli yuqori.
- `sessions` — saqlangan suhbat/session soni, parallel ishlayotgan process soni
  emas. Eski sessionlarni backup/audit qilmasdan o‘chirmaslik kerak.
- Computer Control surface bu sessiyada yoqilmagan
  (`CUA_REPL_ENABLED_SURFACES is required`); tahlil screenshot, Hermes config va
  lokal SQLite metadata orqali bajarildi.

### Dashboard cleanup

- Emirhan qarori: dashboardda faqat asosiy `GPT-5.5/openai-codex` Beluga sessioni
  qolsin; tarixiy free modellar va texnik one-shot kartalar kerak emas.
- `state.db` cleanup oldidan
  `/Users/protochka/.hermes/state.db.backup-20260913-before-dashboard-cleanup`
  backup olindi. 1502 ta background/tool session va 13 ta boshqa tarixiy session
  o‘chirildi; `beluga-owner-v2` saqlandi.
- Beluga background analysis va intent classification sessionlari ishlashda davom
  etadi, ammo running paytidan boshlab `archived=1` qilinadi va dashboardni
  to‘ldirmaydi. Yakuniy tekshiruvda visible session soni `1`.
- Beluga LaunchAgent restartdan keyin `running`; 99 test, Python compile, Node
  syntax va `git diff --check` o‘tdi.

### Yagona model rejimi — gpt-5.6-terra

- Emirhan dashboardda GPT-5.5 `AUX · MCP` kartalari yana ko‘ringanini bildirdi.
  Sabab: main model Terra bo‘lsa ham auxiliary MCP/curator, MoA reference’lari va
  Beluga backend hali GPT-5.5ga biriktirilgan edi.
- Hermes main, auxiliary MCP, curator va Beluga endi `openai-codex/gpt-5.6-terra`.
  MoA o‘chirildi va GPT-5.5 hamda free DeepSeek reference ro‘yxatlari olib tashlandi.
- Eski 14 Hermes session cleanup qilindi; oldindan config va state DB backup olindi.
  Yangi Beluga session nomi `beluga-owner-v3`; u birinchi owner xabarida yaratiladi.
- Tekshiruv: profile va Beluga runtime Terra, config valid, LaunchAgent running,
  99 test/compile/Node/diff check o‘tdi. Background auxiliary session archived va
  visible session hozircha `0`.

## 2026-09-10 — optimization audit

- `hermes doctor`: config v41, Python 3.11, TCC anchor, OpenAI Codex OAuth,
  built-in memory, 59 enabled skills va Playwright Chromium holati tekshirildi;
- real one-shot smoke test `openai-codex/gpt-5.5` bilan o‘tdi: `HERMES_SMOKE_OK`;
- default `openai-codex` + `gpt-5.5`, reasoning `medium`, language `ru`, sudo
  o‘chiq, memory user-profile yoqilgan;
- Gateway `stopped`: bu hozircha ataylab qoldirildi, chunki Telegram transporti
  Beluga’da ishlaydi va duplicate worker xavfi bor;
- optimization talab qiladigan majburiy xato topilmadi. Faqat browser/web workspace
  npm dependency audit ogohlantirishlari va 284 commit ortda qolgan update mavjud;
  ular ishlayotgan config’ni buzmaslik uchun avtomatik qo‘llanmadi.

[tekshirildi: `hermes doctor`, `config check`, `auth status openai-codex`,
`prompt-size`, `skills list`, `gateway status`, `rag-status.sh`, real one-shot inference,
`git diff --check`]

Hermes macOS’da lokal AI agent sifatida o‘rnatilgan. Bu qayd joriy tekshirilgan
holatni, Emirhan uchun foydali minimal sozlamalarni va keyingi ixtiyoriy etaplarni
saqlaydi. Tokenlar, parollar va OAuth credentiallari bu vaultga yozilmaydi.

## 2026-09-09 — tekshirilgan holat

- Hermes Agent `v0.21.1`, install katalogi `/Users/protochka/.hermes/hermes-agent`;
- Desktop interfeys tili `display.language: ru` qilib o‘zgartirildi; ilova to‘liq
  qayta ishga tushirilgach ruscha menyular ko‘rinishi tekshirildi;
- Desktop ilova ochiladi, gateway UI’da `ready` ko‘rinadi;
- default inference: `openai-codex` → `gpt-5.5`;
- Nous Portal OAuth ulangan, ammo paid credit yo‘qligi sabab managed web, image,
  TTS/STT, browser va Modal Tool Gateway mavjud emas;
- `ChatGPT or Codex Subscription` OAuth ulangan; hozirgi config’da default provider/model `openai-codex` + `gpt-5.5`;
- Codex ulanishi `openai-codex` + `gpt-5.5` bilan real `CODEX_OK` inference testi
  orqali tekshirildi;
- OpenAI API key o‘rnatilmagan. Bu hozir majburiy emas: Codex subscription OAuth
  alohida ishlaydi; OpenAI API billing ChatGPT obunasidan alohida;
- terminal backend lokal, `sudo` o‘chiq;
- `cua-driver 0.25.0` o‘rnatilgan va yangilangan;
- Hermes MCP serverlari hozir sozlanmagan;
- gateway LaunchAgent sifatida ishlamayapti, scheduled job `0`, active session `0`;
- built-in skilllar mavjud va 57 tasi enabled; `mybrain-memory` local skill ham
  enabled;
- `config.yaml`da pluginlar ro‘yxati bo‘sh, bundled pluginlar opt-in holatda;
- fallback provider sozlanmagan;
- Telegram, Discord, Slack, Email va boshqa asosiy messaging platformalari Hermes
  core’da sozlanmagan.

## 2026-09-09 — MyBrain memory integratsiyasi

- Quick snapshot yaratildi: `20260909-084115-before-mybrain-memory`;
- `OBSIDIAN_VAULT_PATH=/Users/protochka/MyBrain` Hermes `.env` fayliga qo‘shildi;
- Hermes default working directory `/Users/protochka` qilib belgilandi;
- `~/.hermes/memories/USER.md` yaratildi: Emirhan profili, til, javob va ishlash
  afzalliklari;
- `~/.hermes/memories/MEMORY.md` yaratildi: MyBrain routing, RAG helper, loyiha va
  muhitning ixcham doimiy faktlari;
- `/Users/protochka/.hermes.md` yaratildi: owner qoidalari, MyBrain restore/save
  tartibi, tekshiruv va xavfsizlik chegaralari;
- `mybrain-memory` local skill yaratildi va skill indeksida `local · enabled`
  ko‘rindi; `--skills mybrain-memory` real testida vault yo‘li to‘g‘ri qaytdi;
- built-in memory va user profile enabled; prompt-size tekshiruvida memory 1,848 B,
  user profile 1,184 B va project context 2,348 B yuklangani ko‘rindi;
- real Codex inference testida Hermes MyBrain’dan AiCamera vazifasi va canonical
  `ZONES/AiCamera/AiCamera.md` yo‘lini to‘g‘ri qaytardi;
- eski MarsDC qaydidagi ochiq login qiymatlari jonli vaultdan olib tashlandi va
  lokal secret storage/interaktiv sessiya ko‘rsatmasi bilan almashtirildi;
- lokal RAG qayta indekslandi: `ok=true`, 299 chunk, model va reranker loaded.

Hermes external memory provider ulanmagan; bu konfiguratsiyada built-in
`USER.md/MEMORY.md` tezkor xotira, MyBrain esa filesystem-first katta bilim bazasi,
lokal RAG esa cross-note recall vazifasini bajaradi. Bu yechim yangi cloud API key
yoki ma’lumotlarni uchinchi tomonga sinxronlashni talab qilmaydi.

[tekshirildi: `hermes config check`, `hermes memory status`, `hermes prompt-size`,
`hermes skills list`, `hermes --skills mybrain-memory`, real MyBrain recall,
`rag-status.sh`, `git diff --check`]

[tekshirildi: Hermes Desktop UI, `hermes --version`, `hermes status`,
`hermes auth list`, `hermes doctor`, `hermes profile list`, `hermes fallback list`,
`hermes gateway status`, `hermes computer-use status`, `hermes mcp list`,
`hermes plugins list`, `hermes skills list`, real Codex inference]

## Emirhan uchun birinchi navbat

1. **Hermesning rolini belgilash.** Hozir Beluga Telegram + native Codex + MyBrain
   oqimi mavjud. Hermes uni darhol almashtirmaydi. Dastlab Hermes desktop/terminal
   yordamchisi sifatida alohida sinov qilinadi; keyin Beluga bilan birlashtirish yoki
   migratsiya qilish qarori dalil asosida olinadi.
2. **Default model.** Codex obunasidan foydalanish uchun Hermes config’da provider
   `openai-codex`, model `gpt-5.5` qilib qo‘yilgan. Nous free model avvalgi fallback
   sifatida qaydda qolgan, lekin hozir default emas.
3. **Shaxsiy kontekst.** Hermes uchun qisqa owner qoidalari yozildi: o‘zbekcha javob, kod va
   texnik terminlar inglizcha, avval mavjud faylni o‘qish, natijani test bilan
   tekshirish, tarixiy qaydni joriy fakt deb bermaslik. MyBrain’dan avval
   `Context MOC → Preferences → Last Session → tegishli Zone` tartibida foydalanish.
4. **MyBrain read testi.** Hermes lokal file/terminal vositasi orqali vaultdagi
   AiCamera qaydini topib, manba bilan qisqa javob qaytardi. Har promptga butun vault
   yuborilmaydi; mavjud lokal RAG cross-note recall uchun ulandi.
5. **Xavfsizlik.** Secret redaction yoqilgan holda qoladi; `sudo` va `--yolo`
   yoqilmaydi. Eski [[../../05 - Mars Space/Skills/MarsDC|MarsDC]] qaydida ochiq
   credential bor edi; jonli qayddan olib tashlandi va RAG qayta indekslandi. Eski
   qiymat Git tarixida qolishi mumkin.
6. **Smoke test.** Codex modelida: oddiy chat, lokal fayl o‘qish, kichik reversible
   edit, browser/computer-use va restartdan keyingi auth holati alohida tekshiriladi.

## Agentning asosiy qatlamlari

| Qatlam | Vazifasi | Hermesdagi joyi | Joriy holat |
|---|---|---|---|
| `SOUL.md` | Agent kimligi, ohangi va doimiy muloqot uslubi | `~/.hermes/SOUL.md` | Mavjud; o‘zbekcha, qisqa va tekshiruvli ishlash qoidalari bor |
| `USER.md` | Emirhan profili, afzalliklari va kutilmalari | `~/.hermes/memories/USER.md` | Yaratildi va promptga yuklandi |
| `MEMORY.md` | Muhit, loyihalar va agent o‘rgangan foydali faktlar | `~/.hermes/memories/MEMORY.md` | Yaratildi va promptga yuklandi |
| `.hermes.md` / `HERMES.md` | Hermesga xos loyiha qoidalari; project context ichida eng yuqori priority | loyiha root’i | `/Users/protochka/.hermes.md` yaratildi va promptga yuklandi |
| `AGENTS.md` | Repo arxitekturasi, buyruqlar, testlar va ishlash qoidalari | loyiha root’i va ichki papkalar | `/Users/protochka` root’da yo‘q; alohida loyihada bo‘lishi mumkin |
| `config.yaml` | Model, reasoning, tools, approvals, memory limiti, delegation va UI | `~/.hermes/config.yaml` | Mavjud |
| Skills | Vazifaga mos ish protokollari | `~/.hermes/skills/` va built-in katalog | 57 built-in va 1 local `mybrain-memory` enabled |
| Tools | File, terminal, browser, computer-use, memory va boshqa amallar | toolsets/config | Asosiy vositalar mavjud; real smoke testlar to‘liq emas |
| Approvals/guardrails | Xavfli terminal va tashqi amallarni nazorat qilish | `config.yaml` va policy | Maxsus Emirhan policy hali yozilmagan |
| Sessions | Suhbat tarixi va resume | `state.db` | Hali active session 0 |
| Profiles | Alohida agent/home, xotira, persona va tool ruxsatlari | `hermes profile` | Faqat `default` |
| Gateway | Telegram/WhatsApp va boshqa messaging transporti | LaunchAgent/gateway config | Stopped; core messaging sozlanmagan |
| Cron/scheduler | Vaqtli vazifalar va hisobotlar | Hermes cron | Job 0 |
| MCP/plugins | Tashqi servis va qo‘shimcha capability | Hermes MCP/plugin config | MCP 0, pluginlar opt-in va enabled ro‘yxati bo‘sh |
| Logs/monitoring | Xato, tool va runtime kuzatuvi | `~/.hermes/logs/`, monitoring | Mavjud; maxsus audit oqimi hali tanlanmagan |
| Checkpoints/backup | Xavfli o‘zgarishdan oldin tiklash | Hermes checkpoints/backup | Etap oldidan sozlash tavsiya qilingan |

Hermes prompt tartibida `SOUL.md` global identity sifatida alohida yuklanadi.
Project context uchun birinchi topilgan tur ishlaydi: `.hermes.md` →
`AGENTS.override.md` → `AGENTS.md` → `CLAUDE.md` → `.cursorrules`.
`USER.md` va `MEMORY.md` yangi sessiya boshida frozen snapshot sifatida promptga
kiradi; sessiya ichida yozilgan yangi memory keyingi sessiyada to‘liq yuklanadi.

Joriy `config.yaml` memory limitlari: `MEMORY.md` uchun 2,200 belgi va `USER.md`
uchun 1,375 belgi. Shu sabab MyBrain’ning hammasini memoryga ko‘chirish kerak emas:
memoryda faqat ixcham indeks va doimiy faktlar, batafsil bilim MyBrain/RAGda qoladi.

### Tavsiya qilingan prompt arxitekturasi

1. `SOUL.md`: ohang, xarakter, javob sifati va halollik.
2. `USER.md`: Emirhan kimligi, til, tajriba va shaxsiy afzalliklar.
3. `MEMORY.md`: Mac/MyBrain yo‘llari, faol tizimlar, tekshirilgan integratsiyalar
   va eskirishi mumkin bo‘lgan holatlarni qayta tekshirish qoidasi.
4. `/Users/protochka/.hermes.md`: kundalik owner qoidalari va MyBrain context
   routing. Project-specific qoidalar har repo ichidagi `AGENTS.md`da qoladi.
5. `config.yaml`: Codex default model, reasoning, memory approval, toolset,
   approvals, context limit va fallback.
6. Skills: Obsidian/MyBrain, sessiya handoff, loyiha auditlari va maxsus workflowlar.
7. Guardrails: credential chiqarmaslik, yuborish/o‘chirish/publish kabi amallarda
   aniq ruxsat va destructive command deny qoidalari.

## Keyin kerak bo‘lsa

- **Fallback:** Codex ishlamasa Nous yoki boshqa tasdiqlangan providerga o‘tish;
- **Gateway:** Hermes’ni Telegram/WhatsApp kabi messaging bilan ishlatish qarori
  bo‘lsa ishga tushirish. Avval Beluga bilan duplicate reply va bitta bot tokenini
  ikki worker ishlatish xavfi tekshiriladi;
- **Scheduler:** aniq eslatma yoki Academy auto-otchot talabi tasdiqlangandan keyin;
- **MCP:** faqat mavjud local file/computer-use yetmaydigan aniq integratsiya uchun;
- **Pluginlar:** vazifa chiqqanda bittadan yoqish va health test qilish;
- **Profil ajratish:** Emirhan va Mokhinur uchun alohida profil kerak bo‘lsa,
  credential, xotira, workspace va messaging ruxsatlari aralashmasligi tekshiriladi;
- **Backup:** katta Hermes sozlamasidan oldin `~/.hermes` backup va restore testi.

## Hozir kerak emas

- OpenAI API key sotib olish: Codex OAuth ishlayotgani uchun majburiy emas;
- barcha API key va pluginlarni birdan yoqish;
- yangi RAG modelini takroran o‘rnatish: avval mavjud MyBrain RAGdan foydalanish
  imkoniyati tekshiriladi;
- Hermes Telegram gateway’ini Beluga bilan yonma-yon productionda ishga tushirish;
- Nous paid credit olish: faqat managed Tool Gateway vositalari haqiqatan kerak bo‘lsa.

## Qabul mezonlari

- yangi Hermes sessiyasi o‘zbekcha va qisqa javob beradi;
- tanlangan default model UI va CLI’da bir xil ko‘rinadi;
- MyBrain’dan kerakli qaydni topadi, lekin maxfiy credentialni javobga chiqarmaydi;
- lokal fayl amali qayta o‘qish va mos test bilan tekshiriladi;
- messaging yoqilsa faqat owner allowlisti, duplicate himoyasi va bitta jonli owner
  testi o‘tadi;
- restartdan keyin auth, model va kerakli xizmatlarning holati qayta tekshiriladi.

## Aloqador

- [[Context MOC|Kontekstlar xaritasi]]
- [[Preferences|Emirhan afzalliklari]]
- [[Comfort Setup|Codex qulay ish muhiti]]
- [[Beluga Usage|Beluga foydalanish qo‘llanmasi]]
- [[Last Session|Oxirgi sessiya]]
> Yagona kirish nuqtasi: [[Hermes Hub]]. Kurs transcriptlari, Beluga oqimi va skill qoidalari shu hub orqali ulanadi.
