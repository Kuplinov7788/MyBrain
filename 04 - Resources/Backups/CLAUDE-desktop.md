# CLAUDE.md — Desktop (Global)

---

## TIL — QOIDA

**Claude DOIMO O'ZBEK tilida javob beradi.** Qaysi tilda so'ralsa ham — o'zbek tilida javob.
Kod, kommentariyalar, texnik terminlar — inglizcha.

---

## KIM — Emirhan

- Mobile + Frontend dasturchi (React Native, React, Node.js)
- Kompaniya: TezCode (7 kishilik jamoa)
- Loyihalar: WeWatch, HamshiraGo, Raos
- Self-taught, Claude bilan birga o'sgan

---

## BIRINCHI QADAM (HAR SESSIYADA)

1. **Memory o'qi:** `MEMORY.md` avtomatik yuklanadi
2. **Obsidian kontekst:** kerak bo'lsa MyBrain vault dan o'qi (REST API: 127.0.0.1:27124)
3. **Loyiha konteksti:** agar Rave papkasida bo'lsa — `CLAUDE.md`, `CLAUDE_MOBILE.md`, `CLAUDE_EMIRHAN.md` o'qi

---

## OBSIDIAN TIZIMI

### MyBrain vault (shaxsiy)
- Profil: `03 - Areas/Claude Context/Profile.md`
- Loyihalar: `03 - Areas/Claude Context/Projects.md`
- Qo'llanma: `03 - Areas/Claude Context/How-To-Use-Claude.md`

### WeWatch vault (loyiha)
- Yo'l: `C:/Users/User/OneDrive/Рабочий стол/weWatch-obsidian/`
- Arxitektura, buglar, qarorlar, tasklar shu yerda

### Obsidian ga yozish (REST API)
```bash
curl -s -k -X PUT \
  -H "Authorization: Bearer $OBSIDIAN_API_KEY" \
  -H "Content-Type: text/markdown" \
  --data-binary @- \
  "https://127.0.0.1:27124/vault/PATH/TO/NOTE.md" << 'EOF'
content here
EOF
```

---

## GLOBAL MCP LAR

| MCP | Vazifasi | Qachon ishlatish |
|-----|---------|-----------------|
| Obsidian | MyBrain vault o'qish/yozish | Kontekst, memory, notalar |
| Playwright | Sayt ochish, screenshot, test | UI tekshirish, web test |
| Filesystem | Fayl/papka boshqarish | Loyiha tuzilmasi |

---

## ISHLASH USLUBI

### Emirhan bilan ishlash qoidalari:
- **Aralash rejim:** ba'zan tez natija, ba'zan tushuntirish
- **O'zbek tilida** gaplash
- **Kod yozishdan oldin** mavjud kodni o'qi
- **Xato qilma** — fayl, endpoint, funksiya to'qib chiqarma
- **Oddiy qil** — ortiqcha murakkablashtirma

### Rejim tanlash:
- 1-2 fayl → oddiy ishlash
- 3+ fayl → plan mode
- 5+ fayl → multi-agent (agar Rave da bo'lsa)

---

## MEMORY QOIDALARI

### Nima yoziladi:
- Yangi loyiha yoki texnologiya haqida ma'lumot
- Emirhan ning yangi preference lari
- Muhim qarorlar va sabablari
- Takroriy xatolar va yechimlari

### Qayerga yoziladi:
- Tez ma'lumot → `MEMORY.md` (har sessiyada o'qiladi)
- Chuqur ma'lumot → Obsidian MyBrain vault
- Loyiha specifik → WeWatch Obsidian vault

---

## XAVFSIZLIK

```
❌ .env ni commitga qo'shma
❌ API key larni kodga yozma
❌ Production DB ga qo'l tegizma
❌ Boshqaning zonasiga ruxsatsiz kirma
```

---

## LOYIHALAR XARITASI

| Loyiha | Papka | Tech |
|--------|-------|------|
| WeWatch (Rave) | `C:/Users/User/OneDrive/Рабочий стол/Rave/` | React Native + Node.js monorepo |
| MyBrain | `C:/Users/User/OneDrive/Рабочий стол/MyBrain/` | Obsidian vault (shaxsiy) |
| WeWatch Obsidian | `C:/Users/User/OneDrive/Рабочий стол/weWatch-obsidian/` | Obsidian vault (loyiha) |

---
*CLAUDE.md | Desktop Global | v1.0 | 2026-06-04*
