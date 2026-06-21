---
type: zone-context
zone: WeWatch-Web
owner: Emirhan
updated: 2026-06-21
---

# WeWatch Web — Zone Context

## Oxirgi sessiya: 2026-06-21

### Holat: i18n to'liq tugallandi

**Commit:** `1901102` — fix(web): complete i18n
**Branch:** main (pushed)

---

## Nima qilindi (2026-06-14)

### 1. Web app kodi push qilindi (T-C016/C017/C018/C019)
- 82 ta yangi fayl — commit `29ce65a`
- Auth, Friends, Messages, Profile, Rooms, Watch Party — hammasi tayyor
- Next.js 14 + Tailwind CSS 4 + Zustand + React Query + next-intl + Socket.io

### 2. TSC xatolar tuzatildi
- WeWatchLogo `textSize` prop qo'shildi
- Shared types yo'q edi — IMovie, IBattle, IAchievement web da lokal yaratildi
- Test fayllar tsconfig exclude ga qo'shildi
- Commit `34d0b40`

### 3. Mobile UI bilan moslashtirish
- Avatar: 50x50px, violet rank border
- Input: h-[54px], rounded-2xl, bg-[#111118]
- Button: h-[54px], gradient, shadow
- Tabs: bg-style (underline emas)
- Online dot: 14px, emerald-400
- Commit `fd78532`

### 4. i18n to'liq tugallandi
- **15 fayl** o'zgartirildi
- Barcha hardcoded o'zbekcha matnlar `useTranslations()` ga o'tkazildi
- Komponentlar: HomeContent, ProfileContent, MessagesContent, ChatWindow, ConversationList, ProfileCard, CreateRoomDialog, JoinRoomDialog, VideoSearch
- 3 til: uz.json, ru.json, en.json — home, profile, dm, room bo'limlari
- Page metadata title: inglizcha (locale-neutral)
- Commit `1901102`

---

## Arxitektura

| Fayl/Papka | Vazifa |
|------------|--------|
| `apps/web/src/app/(app)/` | App sahifalari (auth kerak) |
| `apps/web/src/app/(auth)/` | Login/Register |
| `apps/web/src/app/(landing)/` | Landing, Features, Pricing |
| `apps/web/src/components/` | UI komponentlar |
| `apps/web/src/hooks/` | React Query hooks (use-auth-guard, use-dm, use-friends, use-rooms, use-socket, use-watch-party, use-profile) |
| `apps/web/src/lib/api/` | API client funksiyalari |
| `apps/web/src/store/` | Zustand stores (auth, watch-party, toast) |
| `apps/web/messages/` | i18n — uz.json, ru.json, en.json |

## Design System
- bgVoid: #060608, bgBase: #0A0A0F, bgElevated: #111118
- Primary: #7C3AED (violet-600)
- Input: h-[54px], rounded-2xl, border-white/[0.06]
- Avatar: 50x50, border-2 border-violet-500/30
- Font: system (landing da Bebas Neue)

## Keyingi qadam
- Backend servicelarni ulash (hozir mockda)
- Socket.io real-time chat va watch party sync
- Playwright E2E testlar yozish
