---
type: zone-context
zone: WeWatch-Mobile
owner: Emirhan
updated: 2026-06-21
---

# WeWatch Mobile — Zone Context

## Umumiy
React Native + Expo + TypeScript mobile app. Birga video ko'rish platformasi.

## Papka
`apps/mobile/` — Emirhan ning asosiy ish zonasi.

## Tech Stack
- React Native + Expo SDK 54
- TypeScript
- Zustand (state management)
- React Navigation (navigatsiya)
- Socket.io-client (realtime)
- react-native-video (video player)
- Expo Notifications (push)

## Tuzilma
```
apps/mobile/src/
├── screens/        → Ekranlar (Home, Profile, Room, Messages, etc.)
├── components/     → Qayta ishlatiladigan komponentlar
├── hooks/          → Custom React hooklar
├── navigation/     → Stack/Tab navigatsiya
├── store/          → Zustand storelar
├── services/       → API client funksiyalari
├── utils/          → Yordamchi funksiyalar
├── types/          → TypeScript tiplar
├── constants/      → Ranglar, o'lchamlar, doimiylar
└── i18n/           → Tarjimalar (uz, ru, en)
```

## Qoidalar
- `__DEV__` bo'lganda console.log ruxsat
- Production da faqat logger
- shared/types dan import qilinadi
- Socket.io eventlarni QAYTA NOMLAMASLIK

## Keyingi ishlar
- Backend servicelarni to'liq ulash
- Watch party real-time sync
- Push notifications
- E2E testlar

---

*Zone context | WeWatch-Mobile | 2026-06-21*
