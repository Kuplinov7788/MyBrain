# Web + iOS + Android Sync — Brainstorm natijasi

**Sana:** 2026-06-14
**Loyiha:** WeWatch

## Savol

Android + iOS mesh orqali sinxron ishlaydi. Web ni qo'shsak — uchala platform bitta xonada bitta video ko'ra oladimi?

## Javob: HA, mumkin. WebRTC Mesh KERAK EMAS.

Socket.io + drift correction = yetarli.
100-300ms farq kino ko'rishda sezilmaydi.
scheduledAt (500ms) barcha platformalarni bir vaqtga keltiradi.

## Hozirgi muammo

Web da heartbeat, drift correction, buffer event, scheduledAt — HECH BIRI yo'q.
Natija: 1 soatda web ~25 sekund orqada qoladi.

## Fix: 5 fayl, ~2 kun

1. Heartbeat listener + drift correction (web hook)
2. Buffer event + owner mode (VideoPlayer)
3. YouTube IFrame API adapter
4. Backend platform field

## Batafsil

→ WeWatch vault: `KNOWLEDGE/web-mesh-sync-analysis.md`

---
*Emirhan | 2026-06-14*
