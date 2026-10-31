---
type: audit
updated: 2026-10-31
status: audited-open-findings
---

# Obsidian audit — 2026-10-31

## Qanday ishlaydi

- Shaxsiy xotira: MyBrain. Preferences → Context MOC → Last Session orqali Codex lokal Markdown fayllarni o‘qiydi. Bu Obsidian MCP ulanishi emas.
- Dantes xotirasi: DantesBrain; kod esa alohida dantes reposida. Obsidian registry ikkala vaultni ko‘rsatadi; DantesBrain open=true. App jarayoni mavjud; UI render tekshirilmadi.
- Qaydlar qo‘lda/agent topshirig‘i bilan yoziladi. Har bir promptni avtomatik yig‘ish ushbu auditda tasdiqlanmadi.
- MyBrain community ro‘yxati: obsidian-git, obsidian-tasks-plugin. Git sozlamasida save/push/pull har 10 daqiqa; amalda so‘nggi sync bajarilgani alohida dalil talab qiladi.
- RAG MyBrain va DantesBrain Markdownini oladi, Dantes kanonik memorylariga ustuvorlik beradi; maxfiy/login/credentials/secrets nomli fayllarni chiqaradi. Bu nomga asoslangan filter, to‘liq maxfiylik tekshiruvi emas.

## Tekshirilgan natijalar

- MyBrain: 117 Markdown; DantesBrain: 144 Markdown (ushbu qayd yaratilishidan oldin).
- Har ikkala vaultda prose wikilink/embed tekshiruvida missing/ambiguous/outside = 0, exact duplicate = 0.
- MyBrain: 17 frontmattersiz, 11 kiruvchi wikilinksiz kandidat. DantesBrain: 121 frontmattersiz, 2 kiruvchi wikilinksiz kandidat. Bu avtomatik xato yoki o‘chirish uchun sabab emas.
- MyBrain HEAD va GitHub main bir xil: 63a9a86adffc28158fbf7ce3b5c8663e3ca442a4; so‘nggi commit 2026-10-29 14:40 +05. `git ls-remote` bilan remote qayta tekshirildi. Lokal modified/untracked qaydlar commit/push qilinmagan.
- DantesBrain ichida .git yo‘q; mustaqil Git backup tasdiqlanmadi.
- RAG /health: ok=true, 2745 chunk, model_loaded=true, reranker=true. Haqiqiy search javob berdi.
- Indeks fayli oxirgi yangilanishi: 2026-10-30 14:48:38 lokal vaqt. Yangi 11-bosqich so‘rovi eski 33-bosqich qaydlarini qaytardi; bu bitta qidiruv sinovi, umumiy sifat bahosi emas.
- launchd reindex interval=600 soniya. 2026-10-31 10:10 logida MPS out-of-memory xatosi bor. Server ishlashi indeks yangiligini kafolatlamaydi.

## Ochiq muammolar va navbat

1. RAG reindex RAM/MPS cheklovi sabab yiqilgan. Kichik batch/CPU varianti resurs va sifat bilan sinovdan o‘tkazilsin; memory limit bypass yoqilmasin.
2. embed-reindex.sh indexer exit kodini tekshirmaydi, xatodan keyin serverni restart qiladi va done/exit 0 beradi. Fail-fast, haqiqiy success/failure, freshness health va oxirgi muvaffaqiyatli indeks nazorati kerak.
3. MyBrain 10 daqiqalik Git sozlamasi mavjud, ammo yangi lokal ishlar remote’da yo‘q. Aktiv vault/plugin ishini aniqlash kerak; faqat process borligi MyBrain Git plaginining ishlashini isbotlamaydi.
4. DantesBrain backup siyosatini belgilash kerak. Repo yoki cloudga avtomatik yuborish yoqilmadi.
5. Metadata/daily tuzilishi bir xil emas: root daily va DAILY/Emirhan qaydlari bor. Nomlash/routing kelishilib keyin kerakli qismlargina tartiblansin.
6. Yangi Base/Canvas/Clipper uchun haqiqiy UI/import tekshiruvi qolgan.

## Chegaralar

Audit skripti Markdown-style link, heading/block anchor, YAML schema va Obsidian UI tezligini tekshirmaydi. Barcha fayllarning credential tarkibi yoki backup tiklanishi audit qilinmadi. Secret nomli Inbox qaydining mazmuni ochilmadi; git ls-files uni tracked deb ko‘rsatmadi. Global .gitignore’da maxfiy nomlar uchun umumiy qoida yo‘q; credentiallar vaultdan tashqarida saqlanishi kerak.

Audit davomida runtime, plugin, cron, index va Git remote o‘zgartirilmadi; faqat ushbu hisobot va navigatsiya/handoff qaydi yozildi. Commit/push bajarilmadi.

Dalillar: audit_vault.py read-only hisobotlari /tmp/mybrain-audit-2026-10-31.json va /tmp/dantesbrain-audit-2026-10-31.json; git status/log/ls-remote; .obsidian configs; .codex/rag scripts/health/search/log; launchd plist; Obsidian registry. /tmp fayllar doimiy backup emas.

## Ishlash jarayoni auditi — qo‘shimcha tekshiruv

Foydalanuvchi jarayonni skilllar bilan audit qilishni so‘radi. Qo‘llandi:
obsidyan-skill (xotira routing), obsidian-vault-maintenance (read-only
strukturaviy audit), emirhan-workflow (kontekst → ish → qayd → sync).
Skill mavjudligi alohida tekshirildi; ular Obsidian ichida ishlaydigan
plagin yoki avtomatik background job emas.

| Bosqich | Amaldagi yo‘l | Natija / ochiq joy |
| --- | --- | --- |
| Kontekstni tiklash | AGENTS va workflow → Context MOC, Preferences, Last Session | Yo‘riqnoma va fayllar mavjud; agent ularni har vazifada tegishli hajmda o‘qishi kerak. |
| Joriy holatni aniqlash | Note → amaldagi fayl/CLI | Ushbu auditda qo‘llandi; eski note runtime dalili o‘rnini bosmaydi. |
| Yozish | Preferences / Last Session / daily / loyiha vaulti | Hisobot yozildi, qayta o‘qildi va MOC orqali topiladi; bu avtomatik barcha-prompt collector emas. |
| Qayta topish | MOC va bevosita fayl; yordamchi RAG | Bevosita fayl yo‘li mavjud. RAG server javob beradi, lekin indeks eski; yangi hisobot retrievalga kirgani tasdiqlanmagan. |
| Sinxronlash | MyBrain Obsidian Git | Sozlama bor, lokal yangi o‘zgarishlar hali remote commitga kirmagan. |
| Qayta tiklash | Git backup yoki boshqa backup | MyBrain remote oldingi commitni saqlaydi. To‘liq restore testi yo‘q; DantesBrain backup yo‘li tekshirilmagan. |

### Kontekst hajmi va routing

- Last Session: 940 qator, 114448 bayt, 82 sanali sarlavha. Bu hajm
  fayl inventari; token xarajati yoki model sifati o‘lchovi emas.
- [xulosa] Joriy handoff va tarix bitta faylda o‘smoqda. Qisqa joriy
  maqsad / holat / to‘siq / keyingi qadam / manbalar bo‘limi, eski
  sessiyalarga alohida tarix havolasi tavsiya qilinadi. Auditda tarix ko‘chirilmadi.
- MyBrain core daily-notes/templates/bases/canvas/backlink/outgoing-link
  yoqilgan. daily-notes.json va templates.json yo‘q; maxsus folder/template
  yo‘li tekshirilgan configda belgilanmagan. Root’da 2026-10-29.md,
  DAILY/Emirhan’da 3 ta sanali qayd bor. UI’da yangi daily yaratish sinalmadi.
- [xulosa] Agentning DAILY/Emirhan routing qoidasi bilan native daily
  yaratish joyini bir xil qilish kerak; maxsus template hali tekshirilmagan.
- Operating System eski qatlamlar bo‘limida RAG “ulanmagan” deb tarixiy
  yozilgan, yangi qismda esa tarixiy ekaniga izoh bor. Bu izohga qaramay,
  joriy holatni alohida qisqa jadval qilish o‘qishdagi chalkashlikni kamaytiradi.
- Dantes Context yangi final push holatini yuqorida beradi, eski push yo‘q
  yozuvlarini tarixiy deb belgilaydi. Bu manba ustuvorligini saqlashga yordam beradi.

### Skill va ko‘rinishlar

obsidyan-skill, obsidian-vault-maintenance, obsidian-markdown,
obsidian-bases, json-canvas, obsidian-clipper-template-creator SKILL.md
fayllari mavjud. Codex qaydlari.base faqat Codex Context .md qaydlarini
ko‘rsatish uchun sozlangan; bu barcha vault qaydlarining umumiy katalogi emas.
Haqiqiy Base/Canvas UI render va Web Clipper import tekshiruvi bajarilmadi.

### Tavsiya etilgan tartib

1. RAG reindex xatosi, fail-fast va freshness holati.
2. Qisqa joriy handoff va sanali tarixni ajratish.
3. Daily papka/template qoidalarini Obsidian va agentda bir xil qilish.
4. MyBrain sync va DantesBrain backupni jonli tekshirish, keyin restore sinovi.
5. Yangi Base/Canvas/Clipper ko‘rinishlarini UI’da tekshirish.

Bu bandlar taklif; audit davomida runtime, plugin config yoki tarix tuzilishi
almashtirilmadi. Strukturaviy qayta auditda MyBrain 118 Markdown,
missing/ambiguous/outside wikilink = 0. Script Markdown-style havolalar,
anchorlar, YAML schema va haqiqiy UI ishlashini qamramaydi.
