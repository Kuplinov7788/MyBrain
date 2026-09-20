---
type: architecture-review
project: Dantes AI + Hermes Agent
observed: 2026-09-20
status: read-only analysis
---

# Dantes va Hermes Agent moslik tahlili

## Yakuniy ball

Bu tahlil uch xil narsani ajratadi:

| Savol | Ball | Ma'nosi |
|---|---:|---|
| Arxitektura g'oyasi bir-biriga mosmi? | **8.5/10** | Dantes Hermes'ni runtime sifatida ishlatadi, o'z biznes qoidalarini esa yadroda saqlaydi. Qatlamlar to'g'ri ajratilgan. |
| Kod va konfiguratsiya bilan real ulanish qanchalik tayyormi? | **5.8/10** | Profil va Kanban ulanishi yozilgan, lekin gateway, policy bridge, data va memory yo'li to'liq isbotlanmagan. |
| Hozir production'da mustaqil ishlashga tayyormi? | **3.8/10** | Dated holat bo'yicha gateway ishlamagan, sessiya va business data bo'sh, LLM quality eval yo'q. |
| **Umumiy hozirgi moslik** | **6.0/10** | Yaxshi tanlangan foundation, ammo Hermes va Dantes orasidagi runtime ko'prigi hali yakunlanmagan. |

Bu ball Hermes yomon yoki Dantes noto'g'ri degani emas. Hermes — umumiy agent engine; Dantes — Construction biznesi uchun domain/control layer. To'g'ri taqqoslash: Hermes mexanizmni beradi, Dantes unga ma'no, ruxsat, ma'lumot va javobgarlik beradi. [xulosa]

## Mezonlar bo'yicha moslik

| Mezon | Ball | Nega baland yoki past |
|---|---:|---|
| Mas'uliyatni ajratish | **9/10** | Hermes agent loop, provider va tool execution'ni boshqaradi. Dantes `core.py` registr, ruxsat va auditni o'zida qoldiradi. Bu eng to'g'ri qaror. |
| Profile va xodim modeli | **9/10** | Har Dantes xodimida `distribution.yaml`, `SOUL`, `config`, skill va manifest bor. Bu Hermes profile distribution formatiga juda yaqin. |
| Kanban orchestration | **8/10** | `digest_topshiriq.py` assignee, parent, skill, retry va idempotency key ishlatadi. Upstream Kanban ham durable parent-child task va worker lifecycle'ni shu modelda quradi. Jonli dispatcher o'tishi esa alohida isbot talab qiladi. |
| Tool va ish maydoni chegarasi | **5/10** | Config'larda terminal/file tool bor, lekin 13 profilning hech birida `terminal.cwd` yo'q deb qayd etilgan. Hermes profile'ning o'zi sandbox emas; `SOUL.md` ham filesystem chegarasini majburlamaydi. Demak Dantes qoidasi promptga bog'lanib qolishi mumkin. |
| Security va policy bridge | **6/10** | Dantes `ruxsat_bormi`, Telegram allowlist, audit va model trust qoidalariga ega. Lekin `core.model_tanla()` chaqiruvi Hermes'ning barcha real model/tool yo'liga ulanib turgani repo'dan isbotlanmadi. Bu eng muhim texnik bo'shliq. |
| Data, RAG va memory | **4/10** | Hermes session/memory mexanizmini beradi, Dantes esa o'z `xotira` va kutubxona qatlamini yozgan. Ammo 2026-09-13 o'lchovida Dantes xotirasi 0 yozuv, `home/memories` bo'sh, embedding/vector qidiruvi yo'q, haqiqiy ombor/1C ma'lumoti yo'q edi. |
| Version va deployment | **6/10** | Dantes deploy Hermes'ni `v0.20.4` commitiga pin qiladi. Rasmiy release sahifasida 2026-09-20 holatiga v0.21.3 mavjud. Pin reproducibility beradi, lekin upstream yangilanishlari bilan compatibility test kerak. |
| Evaluation va observability | **5/10** | Dantes audit, `trace_id`, guard va deterministic testlarga ega. Lekin unit test agentning manbaga sodiqligi, tool tanlovi, UZ/RU sifati, latency/cost yoki xato tiklanishini o'lchamaydi. |

O'rtacha mezonlar: **52/80 = 6.5/10**. Yuqoridagi umumiy **6.0** ball bunga runtime readiness jarimasini qo'shadi: gateway va real Kanban oqimi hali tasdiqlanmagan. [xulosa]

## Nima juda yaxshi moslangan

### 1. Hermes va Dantes vazifasi to'g'ri bo'lingan

Dantes arxitekturasidagi uch qatlam aniq:

```text
Hermes  = agent qanday fikrlaydi va tool chaqiradi
Kanban  = vazifa kimga, qachon va qaysi dependency bilan beriladi
Dantes core = kimga ruxsat bor, qaysi ma'lumot maxfiy, qanday audit qilinadi
```

Bu model Hermes'ning platform-agnostic `AIAgent`, central tool registry, session storage va gateway tuzilishiga mos keladi. Dantes biznes qarorini prompt ichiga yashirmasdan `core.py`ga chiqarishga harakat qilgan. [tekshirildi: [ARXITEKTURA.md](/Users/protochka/dantes/ARXITEKTURA.md), [core.py](/Users/protochka/dantes/scripts/core.py), [Hermes Architecture](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture)]

### 2. Dantes xodim papkalari Hermes distribution'iga mos

`distribution.yaml + SOUL.md + config.yaml + skills/` shakli upstream Hermes profile distribution'ining asosiy shakli. `xodimlar_sinxron.py` manifestni yadro registriga yozadi va profilni o'rnatishga urinadi. Bu Dantes'ni Hermes'ga qattiq fork qilmasdan, profile layer sifatida saqlash imkonini beradi. [tekshirildi: [xodimlar_sinxron.py](/Users/protochka/dantes/scripts/xodimlar_sinxron.py), [Profile Distributions](https://hermes-agent.nousresearch.com/docs/user-guide/profile-distributions)]

### 3. Kunlik zanjir upstream Kanban konsepsiyasiga mos

`yiguvchi → tekshiruvchi → hisobotchi` zanjirida keyingi karta oldingisiga parent sifatida bog'lanadi. Natijada yig'uvchi tugamasa tekshiruvchi, tekshiruvchi o'tmasa hisobotchi ishga tushmasligi kerak. Bu Hermes Kanban'dagi parent dependency va assignee modeliga mos. [tekshirildi: [digest_topshiriq.py](/Users/protochka/dantes/scripts/digest_topshiriq.py), [Hermes Kanban](https://hermes-agent.nousresearch.com/docs/user-guide/features/kanban)]

### 4. Deterministic biznes kodini modeldan tashqarida qoldirish to'g'ri

Ombor qoldig'i, pul amali, Telegram yuborish qulfi, audit va schema tekshiruvi Python'da bo'lishi kerak. Model faqat tasniflash, rejalash va izohlashga yordam beradi. Bu agent architecture qoidasiga mos: authorization, delivery, idempotency va destructive action free-form reasoning ichida qolmasligi kerak. [tekshirildi: [xodimlar/README.md](/Users/protochka/dantes/xodimlar/README.md), [agent-architecture levels](/Users/protochka/.codex/skills/agent-architecture/references/levels.md)]

## Nima uchun ball pasaydi

### 1. Eng katta muammo — ishlash holati bilan dizayn aralashib ketgan

Repo'da gateway, collector, guard va Kanban uchun service fayllari bor. Bu ularning ishlayotganini bildirmaydi. `HOLAT.md`ning 2026-09-13 qaydida gateway hech qachon ko'tarilmagani, Hermes sessiyalari 0 va Kanban amalda 0 ekani yozilgan. Dashboard ko'rigida esa 2026-09-20 kuni `Gateway stopped`, 0 active session va Dantes doskasida uchta eski `Done` karta ko'ringan. Shuning uchun “zanjir kodi bor”ni “agent zanjiri ishladi” deb hisoblamadim. [tekshirildi: [HOLAT.md](/Users/protochka/dantes/HOLAT.md), [[Dantes Audit 2026-09-20]]]

### 2. Dantes policy'si Hermes runtime'ga to'liq kiritilmagan

Dantes `core.ruxsat_bormi()` va `core.model_tanla()`ni markaziy himoya deb belgilagan. Telegram yuborish kodi `core` orqali o'tadi. Biroq `rg` tekshiruvida `model_tanla()` asosan core CLI va testlarda ko'rindi; Hermes'ning provider resolver va tool dispatch yo'lida Dantes policy adapteri ko'rinmadi. Bu — “policy mavjud” va “har model chaqiruvini policy bloklaydi” o'rtasidagi farq. [xulosa: lokal `rg` tekshiruvi]

### 3. Profile alohida bo'lishi filesystem sandbox degani emas

Upstream hujjatiga ko'ra profile o'z config, memory va session state'iga ega; terminal qayerdan boshlanishi `terminal.cwd` bilan belgilanadi; profile o'zi sandbox emas. Dantes config'larida `terminal.cwd` yo'q deb o'z auditi qayd etgan. Shuning uchun `AGENTS.md` zanjiri, ish papkasi va fayl ko'lami kutilganidek ishlayotganini alohida tekshirmasdan security ballini yuqori qo'ymadim. [tekshirildi: [XODIM-STANDARTI.md](/Users/protochka/dantes/docs/XODIM-STANDARTI.md), [Hermes Profiles](https://hermes-agent.nousresearch.com/docs/user-guide/profiles)]

### 4. Biznes ma'lumoti bo'lmasa, xodim faqat qobiq bo'lib qoladi

`omborchi`, `moliyachi`, `integrator1c` va `kutubxonachi` uchun kod bor. Lekin real ombor, 1C, transport va moliya papkalari bo'sh deb qayd qilingan. RAG'da FTS5 poydevori bor, ammo vector/embedding yo'q. Agentning “hisobot beradi” degan qobiliyati shu ma'lumot yo'li tasdiqlanmaguncha faqat design-level capability hisoblanadi. [tekshirildi: [XODIM-STANDARTI.md](/Users/protochka/dantes/docs/XODIM-STANDARTI.md), [HOLAT.md](/Users/protochka/dantes/HOLAT.md)]

### 5. Testlar agent sifatini hali o'lchamaydi

23/23 va 97/97 raqamlari 2026-09-13 dagi deterministic/security/system testlariga tegishli. Ular JSON schema, manifest, kod va invariantlarni tekshiradi. Lekin yig'uvchi manbani to'g'ri saqladimi, tekshiruvchi hallucination'ni topdimi, hisobotchi UZ/RU aralash matnni buzmadimi — bular uchun versioned LLM eval kerak. [tekshirildi: [HOLAT.md](/Users/protochka/dantes/HOLAT.md), [XODIM-STANDARTI.md](/Users/protochka/dantes/docs/XODIM-STANDARTI.md)]

## Hermes'ni Dantes uchun ishlatish qarori

**Tanlov to'g'ri: Hermes'ni almashtirish kerak emas.** Dantes o'z agent engine'ini noldan qurishi shart emas. Hermes agent loop, profiles, Kanban, gateway, session va tool runtime'ni beradi. Dantes esa core policy, domain code, data contracts, audit, business connectors va acceptance eval'ni beradi.

Lekin Dantes “Hermes ustiga 13 ta prompt yozildi” darajasida qolmasligi kerak. U production agent bo'lishi uchun quyidagi ko'priklar majburiy:

1. **Runtime policy bridge:** har model/provider va write-capable tool chaqiruvi `core` policy bilan tekshirilsin; faqat CLI testida emas.
2. **Workspace boundary:** har profile uchun explicit `terminal.cwd` yoki haqiqiy sandbox; `SOUL.md`ga ishonish yetarli emas.
3. **Bitta live acceptance flow:** synthetic Telegram input → collector → Kanban → worker → checker → digest → test DM; har bosqichda trace ID.
4. **Data grounding:** avval bitta vertikal — ombor; import schema, manba freshness, permission filter va citation tekshirilsin.
5. **Agent eval:** kamida 30–50 UZ/RU savol, tool choice, source faithfulness, refusal, retry, latency va cost; release shu natijaga bog'lansin.
6. **Version contract:** Dantes pinned Hermes commiti bilan CI'da test qilinsin; upstream v0.21.x ga o'tish alohida compatibility branch/eval orqali qilinsin.

## Yakuniy xulosa

Dantes va Hermes **arxitektura g'oyasi bo'yicha yaxshi mos**: **8.5/10**. Eng to'g'ri qismi — Hermes'ni almashtiriladigan runtime, Dantes `core`ini esa biznes va xavfsizlik yadro sifatida ajratish.

Hozirgi repo va runtime bo'yicha moslik **6.0/10**. Ballni tushirayotgan narsa profile soni yoki kod sifati emas; policy bridge, `terminal.cwd`/sandbox, real ma'lumot, gateway/dispatcher ishlashi va agent eval'larining isbotlanmagani.

Production'ga tayyorlik **3.8/10**. Avval bitta ombor verticalini va bitta kundalik digest zanjirini to'liq isbotlash kerak. Shundan keyin qolgan xodimlarni yoqish ma'noli bo'ladi. [xulosa]

## Manbalar

- Lokal: [ARXITEKTURA.md](/Users/protochka/dantes/ARXITEKTURA.md), [README.md](/Users/protochka/dantes/README.md), [core.py](/Users/protochka/dantes/scripts/core.py), [digest_topshiriq.py](/Users/protochka/dantes/scripts/digest_topshiriq.py), [HOLAT.md](/Users/protochka/dantes/HOLAT.md), [XODIM-STANDARTI.md](/Users/protochka/dantes/docs/XODIM-STANDARTI.md).
- Rasmiy Hermes: [Architecture](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture), [Profiles](https://hermes-agent.nousresearch.com/docs/user-guide/profiles), [Profile Distributions](https://hermes-agent.nousresearch.com/docs/user-guide/profile-distributions), [Kanban](https://hermes-agent.nousresearch.com/docs/user-guide/features/kanban), [Releases](https://github.com/NousResearch/hermes-agent/releases).
