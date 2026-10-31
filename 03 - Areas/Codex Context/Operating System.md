---
type: operating-model
updated: 2026-10-30
---

# Emirhan Codex + MyBrain ish tizimi

## 2026-10-30 — joriy arxitektura yo'nalishi

[foydalanuvchi qarori] 11 bosqichli arxitektura Codexga moslashtirildi:
[[Codex ish arxitekturasi - 11 bosqich]]. Shu hujjat katta tizim ishida
kanonik reja: audit/brief, qoidalar, memory, skill/MCP, retrieval,
agent loop, automation va o'lchanadigan yaxshilanish sikli.

Bu yangilanish hujjat va routing darajasida; global config, yangi cron/MCP
va self-improvement daemon yoqilmadi. Quyidagi 2026-09-05 paket holati tarixiy;
RAG/Telegram/sync haqidagi eski bandlar bugungi health isboti emas.


Desktopdagi ikki arxivdan foydali g‘oyalar MyBrain va Codex’ga moslashtirildi.

## 2026-10-30 — Obsidian qatlamining amaliy kengayishi

5 yangi Codex skill va mavjud context skillining routing/log yangilanishi:
[[AITMPL Obsidian - Codex moslashtirish 2026-10-30]]. Markdown, Bases, Canvas, Clipper va scoped vault audit
uchun lokal vositalar tayyor. Bu Obsidian MCP yoki background memory servisi
emas; manbaga mos asosiy vosita hali lokal fayl o'qish/yozish.

## Birlashtirilgan qatlamlar

1. **Kontekst:** `Context MOC → Preferences → Last Session → tegishli Zone _context`.
2. **Ishonchlilik:** da’voni amaldagi fayl, CLI yoki test bilan tekshirish; eski qaydni joriy fakt deb olmaslik.
3. **Qayd:** qarorlar, sessiya handoff’i va muhim o‘rganilgan narsalarni mos Obsidian qaydiga yozish.
4. **Sinxronizatsiya:** Obsidian Git 10 daqiqalik auto-commit/auto-push; zarur bo‘lsa qo‘lda commit + push.
5. **Qulaylik:** mavjud browser/computer-use, hujjat vositalari, pluginlar va shaxsiy skilllardan foydalanish.

## Desktop paketidan olinmagan qismlar

- Claude Code’ga xos hook konfiguratsiyasi Codex’ga ko‘chirilmagan.
- `dangerously-skip-permissions` aliasi qo‘shilmagan.
- RAG modeli va Telegram userbot maxfiy login talab qilgani uchun ulanmagan.
- Desktopdagi eski Windows yo‘llari, parollar va tarixiy buyruqlar joriy ruxsat hisoblanmaydi.

## Ishlatish buyruqlari

- “Kontekstni tikla” → markaziy xarita va oxirgi sessiya.
- “Qayerda qolgandik?” → `Last Session` + tegishli loyiha `_context` + amaldagi kod.
- “Eslab qol…” → `Preferences` yoki tegishli context.
- “Sessiyani saqla” → `Last Session` va kerak bo‘lsa daily note.
- “Vositalarni tekshir” → `Comfort Setup`.
