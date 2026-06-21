---
type: zone-context
zone: WeWatch-Backend
owner: Saidazim
updated: 2026-06-21
---

# WeWatch Backend — Zone Context

## Umumiy
7 ta Node.js + Express microservice. MongoDB + Redis + Elasticsearch.

## Papka
`services/auth,user,content,watch-party,battle,notification,admin/` — Saidazim zonasi.

## Servislar

| Service | Port | Vazifasi |
|---------|------|----------|
| auth | 3001 | JWT RS256, OAuth (Google/Apple/Telegram), registration |
| user | 3002 | Profil, do'stlar, DM, FCM tokenlar, heartbeat |
| content | 3003 | Video extraction (yt-dlp/Playwright), HLS proxy, search |
| watch-party | 3004 | Xonalar, Socket.io sync, playlist, voice (WebRTC) |
| battle | 3005 | Gamification, 1v1 (ishlab chiqilmoqda) |
| notification | 3007 | FCM push, email, in-app, Telegram bot, campaigns |
| admin | 3008 | Dashboard, moderation, analytics, support, error tracking |

## Pattern
- Controller = HTTP qatlam (request/response)
- Service = biznes logika
- Model = Mongoose schema
- Validator = Joi/Zod
- DB query faqat service da

## Xavfsizlik
- JWT: 15min access (RS256) + 30d refresh
- bcrypt 12 rounds
- Rate limiting (Redis)
- INTERNAL_SERVICE_SECRET (service-to-service)
- helmet + CORS whitelist

## Jami: 232 HTTP endpoint + 61 Socket.io event

---

*Zone context | WeWatch-Backend | 2026-06-21*
