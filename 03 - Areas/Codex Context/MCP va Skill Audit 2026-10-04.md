# MCP va skill audit — 2026-10-04

Qamrov: lokal MCP konfiguratsiyasi, sessiyada ochiq connectorlar, faol skill katalogi va xavfsiz smoke sinovlar. Har bir yozish/publish/send operatsiyasi sinalmagan. Barcha imkoniyatlar to‘liq ishlashi kafolatlanmaydi.

- [tekshirildi: CLI] 19 plugin installed/enabled; 8 lokal MCP yozuvi, 5 enabled va 3 disabled.
- [tekshirildi: fayl] 49 skill fayli o‘qildi; 49 tasida name/description va YAML frontmatter bor.
- [tekshirildi: validator] 34/49 strict validation o‘tdi; 13 Figma skillidagi disable-model-invocation va 2 vendor skillidagi katta harfli nom validator bilan mos kelmadi. Bu vendor skilllar sessiya katalogida mavjud; e’tirozlar runtime buzilganining isboti emas.

| Vosita | Sinov natijasi va chegarasi |
|---|---|
| Telegram personal | Account status muvaffaqiyatli; xabar yuborilmadi. |
| Remotion | 6 tool; health va JavaScript validation smoke passed. Render E2E bu auditda bajarilmadi. |
| RAG | Health ok, 1066 chunk, model/reranker loaded; Dantes qidiruvi manbalarni qaytardi. |
| Node REPL | MCP initialize/tools-list (4 tool) va real hisoblash sinovi o‘tdi. |
| CUA/browser | Inventory Chrome yangi browser ID 2 ni qaytardi. Eski ID 1 mavjud emas; oldingi browser bosish/yozish/screenshot sinovi o‘tgan. |
| Native Chrome | getApp: Computer Use was not approved to use Google Chrome. Hozir bloklangan. |
| Uysot MCP | Oddiy newline JSON MCP stdio initialize 20s timeout. Kod faqat Content-Length formatini kutadi; shu formatda initialize, 5 tool va katalog javob berdi. Standart transport bilan moslik muammosi. |
| Uysot live data | UYSOT_API_TOKEN configured emas; account request bajarilmadi. |
| GitHub connector | USER_NOT_LOGGED_IN; ulanmagan. Alohida gh CLI auth status o‘tdi. |
| Figma | Account plugin list muvaffaqiyatli, bo‘sh ro‘yxat. Design read/write E2E sinalmagan. |
| Sites | list_sites muvaffaqiyatli, bo‘sh ro‘yxat. Create/deploy sinalmagan. |
| Plugin Management | Figma permission read muvaffaqiyatli. |
| Work Pets | list_pets muvaffaqiyatli. Aktiv pet o‘zgartirilmadi. |
| Live document control | Server javob berdi; connected document session yo‘q. |
| PDF/DOCX/XLSX | Bundled Python bilan create/read assertion passed; LibreOffice va Poppler version check passed. Render QA va formula recalculation sinalmagan. |
| Presentations/artifact-tool | Bundled artifact-tool 2.8.84 import o‘tdi; slayd yaratish/render sinalmagan. |
| Android QA/performance | Joriy PATHda adb topilmadi; emulator flow sinalmagan. |
| code-review/codex_app/computer-use eski MCP | CLI configuration disabled. Plugin enabled holati server enabled bilan teng emas; sababi bu auditda tasdiqlanmadi. |

## Ochiq tekshiruvlar

- Uysot transportini MCP newline formatiga moslashtirish va rasmiy tokenni ulash.
- Native Chrome approval va GitHub connector login.
- Android target/adb sozlamasi.
- ImageGen, diagram/design yozish, video render, deploy/publish, template generation va barcha skill workflow’lari alohida vazifa bilan E2E sinaladi. Skill — yo‘riqnoma; fayl validatsiyasi amaliy natijaning o‘rnini bosmaydi.

## Skill fayllari

| Skill | Strict validator |
|---|---|
| imagegen | passed |
| openai-docs | passed |
| review-agent | passed |
| skill-creator | passed |
| skill-installer | passed |
| agent-architecture | passed |
| beluga-assistant | passed |
| business-model | passed |
| comfort-tools-check | passed |
| drawio-bpmn | passed |
| emirhan-workflow | passed |
| humanizer | passed |
| monetization-strategy | passed |
| obsidyan-skill | passed |
| org-design | passed |
| skill-permission | passed |
| startup-canvas | passed |
| uysot-sales | passed |
| visualize | passed |
| figma-code-connect | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-create-new-file | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-design-to-code | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-generate-design | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-generate-diagram | passed |
| figma-generate-library | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-generative-plugins | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-implement-motion | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-shaders | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-swiftui | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-use | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-use-figjam | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-use-motion | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| figma-use-slides | Unexpected key(s) in SKILL.md frontmatter: disable-model-invocation. Allowed properties are: allowed-tools, description, license, metadata, name |
| sites-building | passed |
| sites-hosting | passed |
| sites-mcp | passed |
| sites-preview-troubleshooting | passed |
| plugin-management | passed |
| android-emulator-qa | passed |
| android-performance | passed |
| create-pet | passed |
| pets | passed |
| update-pet | passed |
| documents | passed |
| pdf | passed |
| excel-live-control | passed |
| spreadsheets | Name 'Spreadsheets' should be hyphen-case (lowercase letters, digits, and hyphens only) |
| presentations | Name 'Presentations' should be hyphen-case (lowercase letters, digits, and hyphens only) |
| template-creator | passed |

## Installed/enabled pluginlar

- documents@openai-primary-runtime         installed, enabled  26.930.11008
- pdf@openai-primary-runtime               installed, enabled  26.930.11008
- spreadsheets@openai-primary-runtime      installed, enabled  26.930.11008
- presentations@openai-primary-runtime     installed, enabled  26.930.11008
- template-creator@openai-primary-runtime  installed, enabled  26.930.11008
- codex-app-tools@openai-bundled       installed, enabled  0.1.5
- browser@openai-bundled               installed, enabled  26.930.31730
- unified-computer-use@openai-bundled  installed, enabled  26.930.31730
- chrome@openai-bundled                installed, enabled  26.930.31730
- computer-use@openai-bundled          installed, enabled  1.0.1001365
- code-review@openai-bundled           installed, enabled  26.930.31730
- visualize@openai-bundled             installed, enabled  1.0.46
- github@openai-curated-remote                                      installed, enabled  0.1.12-5f7cd798dc99                                 plugin_connector_1p_1a69035c238881919c4190932b2df699
- figma@openai-curated-remote                                       installed, enabled  15.0.0                                              plugin_connector_68df038e0ba48191908c8434991bbac2
- test-android-apps@openai-curated-remote                           installed, enabled  0.1.2                                               plugins~Plugin_4efcdf475f9881919671c7eb6476b26b
- openai-templates@openai-curated-remote                            installed, enabled  0.1.1                                               plugin_connector_1p_2330815c823c8191941e5dc465bb899f
- sites@openai-curated-remote                                       installed, enabled  0.1.75                                              plugin_connector_1p_689987207de08191979cf68eca2941c6
- plugin-management@openai-curated-remote                           installed, enabled  0.1.0                                               plugin_connector_1p_b3438d6beb9081918fba3625bc988128
- work-pets@openai-curated-remote                                   installed, enabled  0.1.6                                               plugin_connector_1p_bccf6c8660c08191ae4470d9ae4877fa
