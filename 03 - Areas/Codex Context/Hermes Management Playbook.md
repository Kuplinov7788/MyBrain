---
type: playbook
updated: 2026-09-09
source: Hermes course transcripts + HERMES.md guide
status: active-reference
---

# Hermes Management Playbook

Bu qayd Hermes’ni boshqarish bo‘yicha amaliy playbook. Asosiy manbalar:

- [[Hermes Course - TezCode Learning]] — kurs xaritasi va oldingi xulosa.
- [[Hermes Course Transcripts]] — 44 ta video transkripsiyasi saqlangan papka.
- [[Hermes Setup]] — Emirhan kompyuteridagi joriy tekshirilgan Hermes holati.
- `HERMES.md` qo‘llanmasi: `/Users/protochka/Beluga/state/media/678230831-0.md`.

Eslatma: kursdagi qo‘llanma Hermes v0.20.5 asosida tayyorlangan. Joriy lokal holat va rasmiy dokumentatsiya har doim qayta tekshiriladi.

## Asosiy qoida

Hermes boshqaruvida avval scope va xavfsizlik aniqlanadi, keyin real holat tekshiriladi, keyin o‘zgarish kiritiladi, oxirida status/test bilan tasdiqlanadi. Xotira yoki skillga faqat qayta ishlatiladigan qoida/protsedura yoziladi; chat dump, secret, token va private xabarlar saqlanmaydi.

## Ishlash tartibi

1. Vazifa turini aniqlash:
   - config/model/provider;
   - memory/user profile;
   - skill;
   - gateway/Telegram;
   - cron/automation;
   - MCP/plugin;
   - troubleshooting/update/backup.
2. Latest source tekshiruvi:
   - Hermes haqida savolda avval `hermes-agent` skill va rasmiy docs ishlatiladi;
   - lokal holat uchun `hermes status`, `hermes config check`, kerakli subcommand `--help` yoki mavjud note o‘qiladi.
3. Xavfsizlik chegarasi:
   - secret `.env`da, setting `config.yaml`da;
   - destructive yoki external send/publish faqat explicit owner ruxsati bilan;
   - Beluga Telegram transporti ishlayotgan bo‘lsa, Hermes gateway parallel yoqilmaydi.
4. O‘zgarish:
   - config uchun qo‘lda YAML tahrirlashdan ko‘ra `hermes config set` afzal;
   - skill uchun reusable workflow yoziladi, task log emas;
   - cron uchun dry-run va manual run shart.
5. Verification:
   - config: `hermes config check` va tegishli status;
   - gateway: duplicate worker va routing tekshiruvi;
   - cron: `cron list/status/run` va delivery holati;
   - file/note edit: qayta o‘qish va `git diff --check`.

## Kursdan olingan amaliy saboqlar

### Files/logs/plugins

Hermes home (`~/.hermes`) ichida config, secrets, memory, skills, profiles, cron, sessions va loglar bo‘ladi. Xato bo‘lsa avval log/status, keyin taxmin. Pluginlar imkoniyat qo‘shadi, lekin default hammasini yoqish xavfsiz emas; bittadan yoqib health check qilinadi.

### Profiles/MCP/tools

Har loyiha yoki mijoz uchun alohida profile ishlatish kerak. Bu memory, credential va ruxsat aralashishini kamaytiradi. MCP tashqi xizmatni tool sifatida ulaydi; read-only va write/send amallari alohida ruxsatga ega bo‘lishi kerak.

### Git/memory/curator/sub-agent/browser

Git agent ishini qaytariladigan tarixga aylantiradi. Memory qonun va barqaror faktlar uchun; agar xato takrorlansa faqat memory qoidasini ko‘paytirish emas, mexanizmni kodga ko‘chirish kerak. Sub-agent katta vazifani bo‘lishga, browser tools esa real UI/site tekshiruviga yordam beradi.

### Webhooks/pairing/auth/ops/analytics

Agent tashqi tizimdan chaqirilsa auth, pairing va allowlist muhim. Ops buyruqlari restart/status/debug uchun, analytics esa token/xarajat/ishlashni ko‘rish uchun ishlatiladi.

### Automation/cron

Cron va scheduler fon ishlar uchun foydali, lekin “note yozildi” degani timed reminder ishlayapti degani emas. Cron qo‘yilgach manual run, gateway status va delivery tekshiruvi bajariladi. Og‘ir cron ishlarida LLM kutib osilib qolmasligi uchun script-first yoki dry-run yo‘li tanlanadi.

### Telegram/media/voice

Telegramdan boshqarish qulay, lekin bot token, owner id, group/topic routing va duplicate worker xavfi bor. Media fayl kelishi yuborishga ruxsat emas; aniq recipient va send/forward buyrug‘i kerak. Voice/audio uchun transkripsiya sifati tekshiriladi, mazmun taxmin qilinmaydi.

### Model/context/cost/fallback

Bitta model hamma ishga mos emas. Oddiy saralash/xulosa arzon modelga, murakkab reasoning/kod kuchli modelga beriladi. Context uzunligi va cached token xarajatga ta’sir qiladi. Fallback model faqat real ehtiyoj va health check bilan sozlanadi.

### Troubleshooting/update/backup

“Ishlamayapti” holatida avval status, config, auth, queue, logs, gateway va kerakli service tekshiriladi. Update yoki katta configdan oldin backup/snapshot olinadi. Manual config o‘zgartirilsa, darhol validation va smoke test qilinadi.

### Final workflow

Ish oqimi: manba → scope → tool → guardrail → action → verification → qisqa report. Agentning kuchi faqat gapirishda emas, real tekshiriladigan natija chiqarishda.

## Beluga bilan qo‘llash

- Beluga hozir Telegram transportni boshqaryapti; Hermes gatewayni yonma-yon productionda yoqishdan oldin duplicate worker, bot token va reply routing tekshiriladi.
- Telegram read-only ruxsat va send ruxsat alohida; media/contact yuborishni host bajaradi.
- MyBrain — yagona durable knowledge base. Kurs xulosasi, transkript va playbook MyBrain’da; secret va private chat dump kiritilmaydi.
- Hermes boshqaruv ishida bu qayd bilan birga `hermes-agent` skill va rasmiy docs ishlatiladi.

## Transkripsiya holati

- 44 ta video uchun transcript markdown va `.segments.json` fayllari yaratildi.
- Transkripsiya `faster-whisper base int8` bilan bajarildi.
- Uzbek/Russian talaffuzlarda ayrim matnlar xato yozilgan; shuning uchun yakuniy qoidalar caption, HERMES.md, transcript va joriy lokal holatni solishtirib chiqarildi.

## Aloqador

- [[Hermes Course - TezCode Learning]]
- [[Hermes Setup]]
- [[Beluga Usage]]
- [[Operating System]]
- [[Context MOC]]
