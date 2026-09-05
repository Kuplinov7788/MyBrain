---
type: integration-audit
updated: 2026-09-05
status: pending-user-credentials
---

# Telegram shaxsiy MCP — tekshiruv

Desktopdagi `emir-telegram-mcp.tar.gz` ichidagi `TELEGRAM-MCP.md` o‘qildi. Bu oddiy bot emas, Telethon orqali foydalanuvchining shaxsiy Telegram akkaunti nomidan ishlaydigan userbot MCP.

## Nima beradi

- akkaunt holatini tekshirish;
- dialoglar ro‘yxatini olish;
- chatdagi xabarlarni o‘qish va qidirish;
- recipientni nom bo‘yicha topish;
- faqat preview va `confirm=true` dan keyin xabar yuborish.

## Hozirgi holat

Hali ulanmagan. Sabab: `api_id`, `api_hash`, telefon va Telegram login kodi foydalanuvchining maxfiy ma’lumotlari. Ular chatga yozilmaydi va Obsidian’ga saqlanmaydi. Arxiv kodi `people_lint` modulini ixtiyoriy try/except ichida chaqiradi; shu sababli asosiy o‘qish funksiyalari uchun u majburiy emas.

## Codex scaffold

- Server: `/Users/protochka/.codex/telegram-personal/server.py`
- Login: `/Users/protochka/.codex/telegram-personal/login.py`
- Virtual muhit: `/Users/protochka/.codex/telegram-personal/venv` (`telethon==1.43.2`, `mcp==1.27.2`)
- Codex MCP nomi: `telegram_personal` (`/Users/protochka/.codex/config.toml`)
- Maxfiy fayl: `/Users/protochka/.codex/telegram-personal/credentials.json` — placeholder bilan tayyor; `.gitignore` session va credential fayllarini yopadi.

## Ulanish uchun kerak bo‘ladigan ishlar

1. `my.telegram.org` → API development tools’dan shaxsiy `api_id` va `api_hash` olish.
2. Lokal `credentials.json` fayliga qiymatlarni kiritish.
3. `login.py` ni lokal terminalda ishga tushirish; SMS kodi va 2FA parolini faqat foydalanuvchi o‘zi kiritadi.
4. Codex `config.toml` ga lokal stdio MCP serverini qo‘shish.
5. Yangi Codex sessiyasida server holatini tekshirish.

Hozir 1–3-qadamlarning xavfsiz qismi tayyorlandi; API qiymatlarini va telefonni lokal `credentials.json` fayliga kiritish, keyin `login.py` ni o‘zingiz ishga tushirish qolgan.

## Xavfsizlik

- `credentials.json` va `*.session` hech qachon Git yoki Obsidian’ga kiritilmaydi.
- Xabar yuborishdan oldin recipientni qayta topish va preview ko‘rish shart.
- Ommaviy tarqatma yuborilmaydi.
- Bu qo‘llanma Claude Code uchun yozilgan; Codex’ga ulash konfiguratsiyasi alohida moslanadi.

## Aloqador

- [[Context MOC|Kontekstlar xaritasi]]
- [[Comfort Setup|Codex qulay ish muhiti]]
- `Desktop/emir-telegram-mcp.tar.gz` — original arxiv

## 2026-09-05 — Shaxsiy akkaunt autentifikatsiyasi

- Telegram personal MCP uchun lokal sessiya muvaffaqiyatli yaratildi: `~/.codex/telegram-personal/emir_personal.session`
- `telegram_personal` MCP Codex konfiguratsiyasida yoqilgan.
- API ma’lumotlari va 2FA parol Obsidian/Git’ga yozilmadi.
- SMS/2FA ma’lumotlari chatda oshkor qilinganligi sababli keyinroq Telegram 2FA parolini yangilash tavsiya qilinadi.
