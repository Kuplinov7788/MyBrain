---
name: MarsDC
description: Mars.core.uz davomat tekshirish va tuzatish skili. Bugungi guruxlarda qolib ketgan davomatlarni Telegram orqali Emirhan bilan kelishib to'ldiradi. Oyning oxirgi darsida coinlarni teng taqsimlaydi.
type: skill
tags: [mars, davomat, telegram, skill]
created: 2026-06-04
---

# MarsDC — Mars Davomat & Coin Skili

## Qachon ishlatiladi
- Telegram dan "MarsDC" yozilganda
- Bugungi guruxlarda davomat qolib ketgan bo'lsa

---

## QADAMLAR

### 1. Saytga kirish
- Playwright bilan `https://core.marsit.uz/` ga o'tish
- Login: `+998946188877` | Parol: `emir7788`
- `teacher-dashboard` ga kirish

---

### 2. Bugungi guruxlarni aniqlash
- Chap paneldagi barcha guruxlarni birma-bir bosib chiqish
- Har guruxda **Jun** oyini tanlash (joriy oy)
- Jadval header larini o'qish: `bugungi sana` ustunida **o'qituvchi ismi yo'q** bo'lsa → davomat qilinmagan

**Bugungi sana formati:** `DD.MM` (masalan: `04.06`)

**Gurux dars kuni tekshirish:**
- Agar bugungi sana jadvalda umuman yo'q → bu gurux bugun dars yo'q → o'tkazib yuborish
- Agar bugungi sana bor, lekin o'qituvchi ismi yo'q → davomat qilinmagan → TELEGRAM ga yozish

---

### 3. Telegram ga xabar yuborish (har gurux uchun alohida)

**Format:**
```
🏫 [GURUX_NOMI] guruhida [SANA] davomat qilinmagan.

O'quvchilar ro'yxati:
1. Familiya Ism
2. Familiya Ism
3. Familiya Ism
...

❓ Qaysi o'quvchi kelmadi?
Raqamlar bilan yozing (masalan: 2,3)
Agar hammasi kelgan bo'lsa: "hammasi"
```

**Kutish:** Foydalanuvchi javob berguncha keyingi guruxga o'tmaslik.

---

### 4. Javobni qayta ishlash

**Foydalanuvchi "2,3" yozsa:**
- 2 va 3-o'quvchilar → ❌ YO'Q (absent)
- Qolganlar → ✅ BOR (present)

**Foydalanuvchi "hammasi" yozsa:**
- Barcha o'quvchilar → ✅ BOR

**Foydalanuvchi "hech kim" yozsa:**
- Barcha o'quvchilar → ❌ YO'Q

---

### 5. Davomatni to'ldirish (Playwright)

**Dars boshlash (agar birinchi marta):**
1. Bugungi sana cellini bosish → mavzu modal chiqadi
2. Mavzular ro'yxatidan oxirgi "Darsni boshlash" tugmasini bosish
3. Modal yopiladi → hujayralar bosiladigan holga keladi

**Belgilash:**
- Har bir o'quvchi uchun `td.today-column` cellini bosish
  - BOR → ✅ yashil (bir marta bosish)
  - YO'Q → ☐ bo'sh qoldirish (bosmaslik)

**Muhim:** JS `.click()` ishlamaydi — faqat Playwright `[ref=eXXX]` orqali bosish

---

### 6. Natija xabarini yuborish

```
✅ [GURUX_NOMI] davomat saqlandi!

📊 [SANA] natijalar:
✅ BOR: Familiya1, Familiya2...
❌ YO'Q: Familiya3...
```

---

### 7. Barcha guruxlar tugaganda

```
🎉 Barcha guruxlar davomati to'ldirildi!

📋 Bugungi xulosa:
• [GURUX1]: X/Y keldi
• [GURUX2]: X/Y keldi
...
```

---

## OY OXIRI — COIN TAQSIMLASH

### Qachon ishlatiladi
- Foydalanuvchi "MarsDC coins" yozganda
- Yoki joriy oy oxirgi darsida avtomatik

### Coin taqsimlash algoritmi

1. Guruxni ochish
2. Har bir o'quvchining **Umumiy coin** ustunini o'qish
3. Guruxdagi **Coin havzasi** (sarlavhadagi coin soni, masalan `700`) ni o'qish
4. Formula:
   ```
   har_bir_o'quvchiga = havza_coin / aktiv_o'quvchilar_soni
   ```
5. Har o'quvchining Coin input maydoniga shu raqamni kiritib "Coin" tugmasini bosish

### Telegram xabari
```
💰 [GURUX_NOMI] coin taqsimlash:
Havza: [JAMI] coin
O'quvchilar: [SONI] kishi
Har biriga: [MIQDOR] coin

✅ Taqsimlash amalga oshirildi!
```

---

## TEXNIK MA'LUMOTLAR

### Login
- URL: `https://core.marsit.uz/`
- Tel: `+998946188877`
- Parol: `emir7788`

### CSS Selektorlar
- Bugungi ustun: `td.today-column`
- Davomat qutisi: `.attendance-box`
- O'quvchi ismi: `.student-row td:first-child`

### Guruxlar ro'yxati (2026-06-04 holatiga ko'ra)
| Gurux | Dars kunlari | Vaqt |
|-------|-------------|------|
| INPR-1954 | Toq kunlar | 18:40 |
| nBG-2999 | Juft kunlar | — |
| nF-2665 | Toq kunlar | — |
| nF-2719 | Juft kunlar | 11:20 |
| nF-460 | Toq kunlar | — |
| nFPro-422 | Juft kunlar | 15:10 |
| RCT-246 | — | — |
| RCT-299 | — | — |
| Tutor | — | — |

---

## XATOLAR VA YECHIMLAR

| Muammo | Yechim |
|--------|--------|
| Modal chiqmaydi | Sahifani yangilash, qaytadan urinish |
| JS click ishlamaydi | Playwright ref orqali bosish |
| Brauzer kichrayib qolsa | `browser_resize(1400, 800)` |
| Login sessiya tugagan | Qaytadan login qilish |

---

*Skill: MarsDC | Mars Space | Yaratilgan: 2026-06-04*
