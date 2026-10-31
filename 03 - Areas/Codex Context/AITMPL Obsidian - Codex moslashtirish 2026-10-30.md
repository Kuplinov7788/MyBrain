---
type: integration-audit
created: 2026-10-30
updated: 2026-10-30
status: local-skills-installed
source: https://app.aitmpl.com/
---

# AITMPL Obsidian → Codex moslashtirish

## Talab va qamrov

[foydalanuvchi topshirig'i] app.aitmpl.com saytidan Obsidian bilan bog'liq
komponentlarni topish, Codexga moslashtirish va nima o'zgarganini ko'rsatish.

[tekshirildi: catalog API] 1 912 entry, generatedAt 2026-10-30T03:07:04Z.
Barcha tur metadata'sida obsidian/zettel/second-brain/PKM/note-taking/
knowledge-management hamda vault kalitlari qidirildi; false-positive Electron
va security/Google Vault componentlari chiqarildi. Bevosita 12 komponent:
4 format skill, 7 Obsidian ops agent, 1 orchestration/log command.
Yana agent-memory-mcp va swarmvault yaqin yechim sifatida o'qildi: jami
14 component full content. Bu metadata bo'yicha katalog qamrovi; har bir
aloqasiz komponentning ichki faylida Obsidian so'zini izlash auditi emas.

API: https://app.aitmpl.com/api/v1/catalog.json .
Catalog SHA256: `72cec9d5131d7f18f04e1b290ee9060badab9839aa3ffcf2566cfc50b0b22851`.
Kod manbasi pinned commit: `807d769ee00753ad7475f76193fa080d71805e17`.
4 skill helper installer orqali vaqtinchalik katalogga olindi, barcha
relevant fayllari o'qilgach lokal moslashtirilgan nusxalari o'rnatildi.
MIT attribution LICENSE fayllarida saqlandi. Saytdagi npx installer ishga
tushirilmadi, hech qanday unreviewed script/server/hook yoqilmadi.

## Komponentlar va qarorlar

| Komponent (manba) | Turi | Codexdagi natija |
| --- | --- | --- |
| [connection-agent](https://github.com/davila7/claude-code-templates/blob/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/agents/obsidian-ops-team/connection-agent.md) | agents | obsidian-vault-maintenance ichidagi tegishli rejim; alohida agent yoqilmadi |
| [content-curator](https://github.com/davila7/claude-code-templates/blob/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/agents/obsidian-ops-team/content-curator.md) | agents | obsidian-vault-maintenance ichidagi tegishli rejim; alohida agent yoqilmadi |
| [metadata-agent](https://github.com/davila7/claude-code-templates/blob/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/agents/obsidian-ops-team/metadata-agent.md) | agents | obsidian-vault-maintenance ichidagi tegishli rejim; alohida agent yoqilmadi |
| [moc-agent](https://github.com/davila7/claude-code-templates/blob/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/agents/obsidian-ops-team/moc-agent.md) | agents | obsidian-vault-maintenance ichidagi tegishli rejim; alohida agent yoqilmadi |
| [review-agent](https://github.com/davila7/claude-code-templates/blob/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/agents/obsidian-ops-team/review-agent.md) | agents | obsidian-vault-maintenance ichidagi tegishli rejim; alohida agent yoqilmadi |
| [tag-agent](https://github.com/davila7/claude-code-templates/blob/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/agents/obsidian-ops-team/tag-agent.md) | agents | obsidian-vault-maintenance ichidagi tegishli rejim; alohida agent yoqilmadi |
| [vault-optimizer](https://github.com/davila7/claude-code-templates/blob/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/agents/obsidian-ops-team/vault-optimizer.md) | agents | obsidian-vault-maintenance ichidagi tegishli rejim; alohida agent yoqilmadi |
| [log](https://github.com/davila7/claude-code-templates/blob/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/commands/orchestration/log.md) | commands | Ish jurnali usuli mavjud obsidyan-skillga qo'shildi; slash command emas |
| [agent-memory-mcp](https://github.com/davila7/claude-code-templates/tree/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/skills/ai-research/agent-memory-mcp) | skills | O'rnatilmadi: qo'shimcha server/source-of-truth zarurati aniqlanmadi |
| [json-canvas](https://github.com/davila7/claude-code-templates/tree/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/skills/document-processing/json-canvas) | skills | Codex skill sifatida moslashtirildi |
| [obsidian-bases](https://github.com/davila7/claude-code-templates/tree/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/skills/document-processing/obsidian-bases) | skills | Codex skill sifatida moslashtirildi |
| [obsidian-markdown](https://github.com/davila7/claude-code-templates/tree/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/skills/document-processing/obsidian-markdown) | skills | Codex skill sifatida moslashtirildi |
| [obsidian-clipper-template-creator](https://github.com/davila7/claude-code-templates/tree/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/skills/productivity/obsidian-clipper-template-creator) | skills | Codex skill sifatida moslashtirildi |
| [swarmvault](https://github.com/davila7/claude-code-templates/tree/807d769ee00753ad7475f76193fa080d71805e17/cli-tool/components/skills/development/swarmvault) | skills | O'rnatilmadi: MyBrain/DantesBrain o'rniga yangi vault platformasi hozir kerak emas |

## Lokal o'zgarishlar

`/Users/protochka/.codex/skills/` ichida 5 yangi skill:

- obsidian-markdown — wikilink/embed/callout va existing YAML properties.
- obsidian-bases — .base filter/formula/view; oddiy table ko'rinishidan boshlash.
- json-canvas — .canvas node/edge/file layout va structural validation.
- obsidian-clipper-template-creator — representative URLdan importable JSON;
  MyBrain 00 - Inbox uchun generic create-template asset.
- obsidian-vault-maintenance — connection, metadata, tags, MOC, curation,
  storage va review vazifalarini bitta scoped workflowga birlashtiradi.

Mavjud obsidyan-skill context routingini saqladi; kerak bo'lsa shu specialized
skilllarga yo'naltiradi. Orchestration/log'dan factual task/source/outcome/
artifact/test/open-item work-log tartibi olindi. Tasdiqlanmagan davomiylik,
coverage va completion foizi yozilmaydi; external issue posting yoqilmagan.

Yangi maintenance/scripts/audit_vault.py faqat o'qiydi. Wikilink/embed
nomzodlari, missing frontmatter, exact body duplicates, inline tags, MOC va
large-file inventory. Markdown links/anchor/alias va to'liq YAML/tag schema
tekshiruvi emas. Scope ichidagi unlinked holat vault bo'yicha orphan degani
emas. Standart: report, hech qanday write/delete/network/sync yo'q.

## Asl komponentlardan nima o'zgartirildi

- /Users/cam/VAULT01 yo'llari va mavjud bo'lmagan metadata_adder/link_suggester/
  tag_standardizer buyruqlari olib tashlandi; bizning vault routingimiz ishlatiladi.
- PROACTIVELY subagent spawn va model: sonnet kabi Claude deklaratsiyalari
  ko'chirilmadi. 7 role — procedural modes; fon agentlar emas.
- Har qaydga 100 so'z, 2 link, tags yoki modified kabi majburiy foreign schema
  yo'q. Mavjud updated/type/aliases saqlanadi; short task noto'g'ri note emas.
- Eski sanaga qarab arxivlash, orphan deb o'chirish, rasmni 85% compress yoki
  universal 1 MB hard limit qo'llanmadi. 1 MB audit read budget, delete mezoni emas.
- Templates/Bases mavjud degan taxmin olib tashlandi; actual .base/note tekshiriladi.
- Canvas ID formatining hex bo'lishi majburiy emasligi rasmiy spec bilan tuzatildi.
- Clipperdagi WebFetch maxsus tool taxmini Codexdagi mavjud browser/fetchga
  almashtirildi; append/daily mode fieldlari current export/docs bilan tekshiriladi.
- Skill fayllari runtime auth yoki Obsidian MCP ulanishi sifatida ko'rsatilmaydi.

## Tekshiruv dalili

6 skill (5 yangi + mavjud obsidyan-skill) quick_validate'dan o'tdi.
Read-only audit helperning 8 offline testi: content/mtime o'zgarmasligi,
scope escape, symlink private faylni o'qimaslik, fenced/inline misollar,
Unicode/embeds, ambiguous basename, relative paths va duplicate candidates.

O'zgarishlardan oldingi MyBrain Codex Context scope auditida 78 qayd o'qildi: prose wikilink tekshiruvida
missing/ambiguous/outside 0, duplicate 0, large 0, missing-frontmatter 4.
Bu 4 metadata nomzodi avtomatik tahrirlanmadi; to'liq vault health yoki
Obsidian UI performance tekshiruvi deb aytilmaydi.

Yangi .base YAML, .canvas node/edge/file targets va Clipper JSON parse bilan
tekshiriladi; Obsidian/Web Clipper UI import/render bu sessiyada tekshirilmagan.
Userning mavjud nomlanmagan .base/.canvas va .obsidian/graph.json fayllari
tegilmadi. Global AGENTS/config, MCP, cron, RAG, Mem0 va Telegram o'zgarmadi.

## Foydalanish uchun ko'rinishlar

![[03 - Areas/Codex Context/Codex qaydlari.base]]

![[03 - Areas/Codex Context/Codex Obsidian xaritasi.canvas]]

Skills keyingi turn'da discovery uchun mavjud bo'ladi. Bu qaydlarni avtomatik
qayta tuzuvchi daemon, yangi RAG yoki cloud sync o'rnatilgani emas.

## Qaytish va davom ettirish

Mavjud obsidyan-skill asl nusxasi va installation manifesti:
`/Users/protochka/.codex/skill-backups/aitmpl-obsidian-2026-10-30/`.
Yangi skilllar mustaqil kataloglarda; kerak bo'lmasa shu 5 qo'shimchani
chetlatib, oldingi routing skillini backupdan tiklash mumkin. Boshqa skill
va servislar almashtirilmadi. Lokal notes commit/push qilinmadi; auto-sync
holati alohida tekshirilmagan. Source cache vaqtinchalik audit katalogida.

Kanonik ish tizimi: [[Codex ish arxitekturasi - 11 bosqich]], [[Operating System]],
[[Comfort Setup]], [[Context MOC]].

Rasmiy format manbalari:
- https://help.obsidian.md/bases/syntax
- https://jsoncanvas.org/spec/1.0/
- https://help.obsidian.md/web-clipper/templates

## Ko'rib chiqilgan full content hashlar

| Component ID | SHA256 |
| --- | --- |
| `agents/obsidian-ops-team/connection-agent` | `cc370ca611cd0165c69ebaa19ecd16b812267c0a10076e152c6fe85b41e2b1a6` |
| `agents/obsidian-ops-team/content-curator` | `067710dbda0141a9ee66ea51e3757890b4f21ef5bbc461e6379b00c71f13be09` |
| `agents/obsidian-ops-team/metadata-agent` | `57c3dccd9ca66eb3dce0f71b69e4851f8ab8a5ff3bd59e6105fb4396ac9ba081` |
| `agents/obsidian-ops-team/moc-agent` | `9d0889740a682a7cd932d1788b3dbeb663c5ca5224873d5b902fc4847d015325` |
| `agents/obsidian-ops-team/review-agent` | `84ca3a4df676253072ca6a042fdf0da487e66ae6369b787cfe4565e54ab0f655` |
| `agents/obsidian-ops-team/tag-agent` | `32f564ad63954695ee34b64193bc78805b38add7ecca8cbbe67256a706fb85a8` |
| `agents/obsidian-ops-team/vault-optimizer` | `95df577e12b9b65d43fd834ae87b6291921cc8fa63bb7a3a055aab3345e61f9e` |
| `commands/orchestration/log` | `86bd4a4ca2ce74e72e8bf83cf80d5b4516905128a7364c75683f3d05ef761382` |
| `skills/ai-research/agent-memory-mcp` | `62e6254dc3d94b4e084a89a98c45262ccd9929fbf51d6cdb04fe686a53dcc3dc` |
| `skills/document-processing/json-canvas` | `10673ba00ef89a9bd329d0f5df5297fa4efc045adb47e221b3db4edc113f07a9` |
| `skills/document-processing/obsidian-bases` | `9d274859b7e7fce2a4c54291f94b9ea8969c381b1c3f62a74294726c84ab216b` |
| `skills/document-processing/obsidian-markdown` | `0af2f12742148c3775f13fe4d11862949d2ce765738f77297a18fdf1ccbe28b7` |
| `skills/productivity/obsidian-clipper-template-creator` | `f892e170955ae5a469e4ff204e9cdc7f710cf7489f1b971997dd4fe7a1ace4bf` |
| `skills/development/swarmvault` | `b2445b485540a36649f3eb207717e77d4925a4125ec15c2da757a02407030437` |


## Marketplace va yakuniy tekshiruv

Saytning Buildwithclaude marketplace sahifasidagi kepano `obsidian-skills`
paketi ham tekshirildi. GitHub marketplace manifesti va package skills
katalogi uchlikni tasdiqladi: obsidian-markdown, obsidian-bases, json-canvas.
Ular yuqoridagi moslashtirish bilan qamrab olingan; Claude marketplace
wrapperi ikkinchi nusxa sifatida o'rnatilmadi. Bu qo'shimcha katalog entry
soniga qo'shilmaydi, alohida distribution listing.

Manbalar:
- https://aitmpl.com/plugins/buildwithclaude/
- https://github.com/davepoon/buildwithclaude/tree/main/plugins/obsidian-skills

Yakuniy scoped auditda yangi hisobot bilan 79 qayd ko'rildi; prose wikilink
missing/ambiguous/outside 0, metadata nomzodlari 4 bo'lib qoldi. 6 skill
validation, helper 8 test, resource links, Base YAML, Canvas IDs/fields/file
targets/non-overlap, Clipper create JSON va o'zgargan note frontmatteri
tekshirildi. Mavjud user graph/base/canvas fayllari hash bo'yicha o'zgarmagan.
Obsidian/Web Clipper UI render/import sinalmagan. Git diff --check toza.
