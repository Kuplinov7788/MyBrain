---
type: operating-model
updated: 2026-09-05
---

# Emirhan Codex + MyBrain ish tizimi

Desktopdagi ikki arxivdan foydali g‘oyalar MyBrain va Codex’ga moslashtirildi.

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
