---
type: setup-audit
updated: 2026-09-05
scope: shaxsiy kundalik qulaylik
---

# Codex — qulay ish muhiti

Maqsad: Emirhan har safar o‘zini tanishtirmasdan, o‘zbekcha topshiriq berib, qaydlar, brauzer, kompyuter va hujjatlar bilan ishlashi.

## 2026-09-05 tekshiruvi

Biznes arxitekturasi uchun o‘rnatilgan skilllar: `business-model`, `startup-canvas`, `monetization-strategy`, `org-design`, `drawio-bpmn`. Beshala `SKILL.md` fayli to‘liq o‘qildi va format validatsiyasidan o‘tdi. `drawio-bpmn` dagi validatorga mos kelmagan `version` frontmatter maydoni olib tashlandi. Saytdagi `business-model-designer` repo ichida skill emas, command bo‘lgani uchun unga yaqin ishlaydigan `business-model` tanlandi.

`codex plugin list` 18 ta pluginni `installed, enabled` deb qaytardi. Bu holat barcha akkauntlar avtorizatsiyasi yoki har bir funksiyaning sinovdan o‘tganini anglatmaydi.

| Plugin | Versiya | Vazifasi |
|---|---|---|
| browser | 26.901.41600 | Brauzer imkoniyatlari |
| unified-computer-use | 26.901.41600 | Brauzer/native app boshqaruvi |
| chrome | 26.901.41600 | Chrome integratsiyasi |
| computer-use | 1.0.1000926 | Kompyuter boshqaruvi paketi |
| codex-app-tools | 0.1.3 | App vositalari |
| visualize | 1.0.29 | Suhbatdagi vizualizatsiyalar |
| sites | 0.1.57 | Sayt yaratish va hosting |
| documents | 26.904.11930 | Word hujjatlari |
| pdf | 26.904.11930 | PDF |
| spreadsheets | 26.904.11930 | Jadvallar va Excel |
| presentations | 26.904.11930 | Slaydlar |
| template-creator | 26.904.11930 | Qayta ishlatiladigan shablonlar |
| openai-templates | 0.1.1 | Tayyor shablonlar |
| deep-research-work | 0.1.14 | Maxsus Deep research so‘rovlari |
| plugin-management | 0.1.0 | Plugin boshqaruvi |
| github | 0.1.12-5f7cd798dc99 | Repository/PR; akkaunt ulanishi sinovdan o‘tkazilmadi |
| expo | 1.0.2 | Dasturlash; kundalik qulaylik sozlamasi emas |
| test-android-apps | 0.1.2 | Android sinovlari; kundalik qulaylik sozlamasi emas |

GitHub, Expo va Test Android Apps oldingi bosqichda o‘rnatilgan. Foydalanuvchi keyin maqsad kundalik qulaylik ekanini aniqlashtirdi. Ularni o‘chirish so‘ralmagan, shuning uchun saqlandi. Bu bosqichda yangi plugin o‘rnatilmadi.

## Vault sinxronizatsiyasi

Obsidian Git sozlamalari o‘qildi: auto-save/commit `10` daqiqa, auto-push `10` daqiqa, pushdan oldin pull yoqilgan, push o‘chirilmagan. Remote: `https://github.com/Kuplinov7788/MyBrain.git`. Shu sababli Obsidian Git yangi o‘zgarishlarni davriy commit va push qiladi. Qaydlar `5decbfc` commitida saqlandi va `origin/main` ga push qilindi. Bu Codex har bir satr o‘zgarishida alohida commit qiladi degani emas.

## MCP va amaliy kirish

| Vosita | Kuzatilgan holat | Dalil/cheklov |
|---|---|---|
| cua_repl | enabled; sessiyada javob berdi | `cua.getState()` Chrome va native app ro‘yxatini qaytardi; Obsidian ochiq |
| node_repl | enabled; vosita katalogida bor | Alohida amaliy hisoblash sinovi qilinmadi |
| eski computer-use server | disabled | Plugin enabled bo‘lishi server enabled degani emas; o‘zgartirilmadi |
| Sites/app vositalari | sessiyada mavjud | Har bir xizmat bo‘yicha amaliy ish sinovdan o‘tkazilmadi |
| MyBrain lokal fayllari | o‘qish va yozish ishladi | Profil o‘qildi, ushbu qayd yaratildi; MCP emas |
| Obsidian REST/MCP | konfiguratsiyada yo‘q | Vault community plugin ro‘yxatida Git va Tasks bor, REST API yo‘q |
| MongoDB / Context7 | sessiya va MCP ro‘yxatida yo‘q | Kundalik maqsad uchun hozir zarur emas |
| Kalendar / email connector | bu sessiyada ko‘rinmadi | Xizmat tanlanmagan, akkaunt ulanishi qilinmagan |

Alohida Obsidian yoki filesystem MCP yaratilmadi: lokal vault bilan kerakli ishlar mavjud fayl vositalari orqali bajariladi. Telegram desktop ochiq ekani Telegram MCP yoki bot ulanganini bildirmaydi.

## Skilllar

Mavjud yo‘nalishlar tekshirildi: imagegen, OpenAI Docs, skill/plugin yaratish va o‘rnatish, plugin boshqaruvi, Deep research, Word/PDF/jadval/slaydlar, shablonlar, Sites, vizualizatsiya. Yangi o‘rnatilgan Expo va Android paketlarida ham skilllar bor; bu suhbat boshidagi avtomatik skill katalogida ular hali ko‘rsatilmagan.

Yangi shaxsiy skilllar:

- `/Users/protochka/.codex/skills/emirhan-obsidian/SKILL.md` — kontekstni tiklash, xotira, sessiya qaydi va mavjud vazifalardan kunlik reja.
- `/Users/protochka/.codex/skills/comfort-tools-check/SKILL.md` — plugin/MCP/skill inventari, holatlarni ajratish va ushbu qaydni yangilash.

Global ko‘rsatma: `/Users/protochka/.codex/AGENTS.md`. Yangi suhbatda [[03 - Areas/Codex Context/Preferences|Preferences]] ni o‘qishni belgilaydi. Ushbu sessiyada fayl yaratildi; yangi sessiyadagi avtomatik yuklanish alohida tekshirilishi kerak. Bu fon xizmati yoki avtomatik eslatma emas.

Tekshiruv: ikkala yangi skill `quick_validate.py` orqali `Skill is valid!` natijasini berdi. Validator uchun PyYAML vaqtinchalik `/private/tmp/emirhan-skill-validation-20260905` muhitiga o‘rnatildi. Yaratilgan fayllar qayta o‘qildi, yangi Obsidian havolalari va Git diff formati tekshirildi.

## Qanday so‘rash mumkin

- “Kontekstni tikla, oxirgi safar qayerda qolgandik?”
- “Eslab qol: javobni avval qisqa ber, keyin kerak bo‘lsa tushuntir.”
- “Bugungi vazifalarimni Obsidian’dan olib reja tuz.”
- “Mana bu fikrni Inbox’ga saqla.”
- “Sessiyani Obsidian’ga yozib qo‘y.”
- “Plugin, MCP va skilllarim holatini tekshir.”
- “Shu PDFni o‘qib, qisqa xulosa ber.”

## Keyingi haqiqiy ehtiyoj bo‘lsa

- Kalendar/email integratsiyasi: foydalanuvchi ishlatadigan xizmatni tanlash va ulanish holatini tekshirish.
- Eslatma: aniq vaqt/takrorlanish bilan alohida sozlash; hozir yaratilmagan.
- Fayl tartiblash: aniq papka va vazifa bo‘yicha; umumiy tozalash bajarilmagan.
- Git/cloud sync: bu ishda commit/push qilinmadi; lokal qaydlar saqlandi.

## Sozlash manbalari

- [Global AGENTS.md tartibi](https://learn.chatgpt.com/docs/agent-configuration/agents-md.md)
- [Skilllar](https://developers.openai.com/plugins/concepts/skills.md)
- [MCP](https://learn.chatgpt.com/docs/extend/mcp.md)
- Lokal `codex plugin list`, `codex mcp list`, sessiya vositalari va skill fayllari.
