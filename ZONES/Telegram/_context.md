---
type: zone-context
zone: Telegram
owner: Saidazim + Emirhan
updated: 2026-06-21
---

# Telegram — Zone Context

## Umumiy
Telegram botlar, bildirishnomalar va integratsiyalar.

## Komponentlar

### 1. WeWatch Telegram Bot
- **Service:** notification (port 3007)
- **Endpoint:** `POST /telegram/webhook`
- **Vazifa:** Foydalanuvchilarga bildirishnoma, share link

### 2. Telegram Auth
- **Service:** auth (port 3001)
- **Endpoint:** `POST /telegram/login`, `POST /telegram/init`
- **Vazifa:** Telegram orqali login

### 3. Task Notification Bot
- **Script:** `.claude/scripts/tg-notify.sh`
- **Vazifa:** Jamoa ichida task status bildirishnomalar
- **Actions:** new, claim, done, update, blocked

## Tegishli agentlar
- `.claude/agents/telegram-agent.md`

## Holat
Task notification bot ishlaydi. WeWatch Telegram bot — asosiy funksionallik tayyor.

---

*Zone context | Telegram | 2026-06-21*
