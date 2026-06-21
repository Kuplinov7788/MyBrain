---
type: zone-context
zone: MCPs
owner: Emirhan
updated: 2026-06-21
---

# MCPs — Zone Context

## Umumiy
Model Context Protocol (MCP) serverlari — Claude Code uchun tashqi vositalar.

## Faol MCP lar

| MCP | Vazifasi | Qachon ishlatiladi |
|-----|---------|---------------------|
| Obsidian | MyBrain/weWatch vault o'qish/yozish | Kontekst, memory, notalar |
| Playwright | Sayt ochish, screenshot, test | UI tekshirish, web test |
| MongoDB | Ma'lumotlar bazasi boshqarish | DB query, schema tekshirish |
| GitHub | Repo, PR, issue boshqarish | Kod review, PR yaratish |
| Memory | Persistent memory entities | Sessiyalar arasi xotira |
| Sequential Thinking | Murakkab fikrlash | Arxitektura qarorlari |

## Konfiguratsiya
MCP lar `.claude/` sozlamalarida konfiguratsiya qilingan.

## Obsidian MCP
- REST API: `https://127.0.0.1:27124`
- Vaultlar: MyBrain (shaxsiy), weWatch-obsidian (loyiha)
- Obsidian ochiq bo'lishi kerak!

## Tadqiqot (D-014 dan)
11 ta MCP plugin analiz qilindi (2026-05-18):
- P0: Expo MCP, GitHub MCP, Sequential Thinking, Fetch
- P1: React Native MCP (49 tools), MongoDB, Redis, Obsidian
- P2: Playwright, Figma, Memory

---

*Zone context | MCPs | 2026-06-21*
