---
type: task
status: pending
priority: P1
created: 2026-06-04
---

# Noutbuk + Telegram Bot sozlash

## Holat
- PC: to'liq sozlangan (memory, obsidian, MCP, CLAUDE.md)
- Noutbuk: ishda qoldirilgan, hali sozlanmagan
- Telegram bot: hali yaratilmagan

## Ma'lumotlar
- Claude account: beelugacat@gmail.com (PC va noutda bir xil)
- GitHub account: Kuplinov7788 (PC va noutda bir xil)
- Noutbuk faqat ishda ishlatiladi

---

## TASK 1: Noutbukni ulash

### 1.1 — MyBrain vault ni clone qilish
```bash
cd ~/Desktop   # yoki kerakli papka
git clone https://github.com/Kuplinov7788/MyBrain.git
```

### 1.2 — Obsidian o'rnatish va vault ochish
- Obsidian yuklab olish: https://obsidian.md
- "Open folder as vault" → MyBrain papkasini tanlash
- Settings → Community plugins → "Restricted mode" o'chirish
- obsidian-local-rest-api va obsidian-git pluginlar avtomatik yuklanadi
- REST API plugin yoqilganini tekshirish (Settings → Local REST API → Enable)

### 1.3 — Claude Code settings nusxalash
Noutbukda `~/.claude/settings.json` ga quyidagini yozish:
```json
{
  "model": "opus",
  "mcpServers": {
    "obsidian": {
      "command": "mcp-obsidian",
      "env": {
        "OBSIDIAN_API_KEY": "<NOUTBUKDAGI OBSIDIAN REST API KEY>",
        "OBSIDIAN_HOST": "127.0.0.1",
        "OBSIDIAN_PORT": "27124"
      }
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@latest"]
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@anthropic-ai/mcp-server-filesystem", "<NOUTBUK_DESKTOP_PATH>"]
    }
  },
  "skipDangerousModePermissionPrompt": true,
  "permissions": {
    "allow": [
      "Bash(*)", "Read(*)", "Write(*)", "Edit(*)",
      "Glob(*)", "Grep(*)", "WebFetch(*)", "WebSearch(*)",
      "Task(*)", "mcp__obsidian__*", "mcp__playwright__*",
      "mcp__filesystem__*"
    ]
  }
}
```
**Eslatma:** API KEY noutbukda boshqa bo'ladi — Obsidian → Settings → Local REST API → API Key dan olish kerak.

### 1.4 — Global CLAUDE.md nusxalash
```bash
# Noutbukda home papkaga CLAUDE.md yaratish
# PC dagi C:/Users/User/CLAUDE.md ni nusxalash
```

### 1.5 — Memory yaratish
Claude Code ni noutbukda ishga tushirish — u CLAUDE.md o'qiydi, Obsidian dan kontekst oladi, memory yaratadi. Status card chiqishi kerak:
```
-------------------------------------
Salom Emirhan! Men seni taniyman.
Kontekst: TIKLANDI
Memory: OK
Obsidian: ULANGAN
-------------------------------------
```

### 1.6 — Tekshirish
- [ ] Obsidian ochiq, REST API ishlayapti
- [ ] Claude Code `salom` desa — o'zbek tilida javob + status card
- [ ] MyBrain vault sinxron (git pull/push ishlayapti)

---

## TASK 2: Telegram Bot yaratish va ulash

### 2.1 — Bot yaratish
- Telegram da @BotFather ga yozish
- `/newbot` buyrug'i
- Bot nomi: `EmirhanClaudeBot` (yoki boshqa nom)
- Token ni saqlash

### 2.2 — Bot ni Claude MCP ga ulash
PC va noutbuk `settings.json` ga qo'shish:
```json
"telegram": {
  "command": "npx",
  "args": ["-y", "@anthropic-ai/mcp-server-telegram"],
  "env": {
    "TELEGRAM_BOT_TOKEN": "<BOT_TOKEN>"
  }
}
```

### 2.3 — Bot imkoniyatlari
- Telegram dan Claude ga vazifa berish
- Bildirishnoma olish (task yaratildi, bajarildi)
- WeWatch jamoasi bilan integratsiya

### 2.4 — Tekshirish
- [ ] Bot ga `/start` yozilsa javob beradi
- [ ] Claude MCP orqali Telegram ga yoza oladi
- [ ] PC va noutbukda bir xil ishlaydi

---

## Tartib
1. Noutbukni uyga olib kelish
2. Task 1 bajarish (30 daqiqa)
3. Task 2 bajarish (20 daqiqa)
4. Tekshirish

---
*Yaratilgan: 2026-06-04 | Emirhan uchun*
