---
type: decision-log
project: Higvision Proekt
updated: 2026-08-14
---

# Yozishmalar va qarorlar tarixi

## 2026-08-13 — audio va transkripsiya

- `Kamera suxrob aka.m4a` audio topildi.
- Davomiyligi 42:12.
- O‘zbekcha nutqqa mos lokal Whisper modeli bilan transkripsiya qilindi.
- 85 ta 30 soniyalik vaqtli bo‘lak tayyorlandi.
- TXT, SRT va JSON formatlari yaratildi.
- Audio kompyuterda lokal ishlangan.

## Uchrashuvdan asosiy xulosa

- Klient oddiy kamerani doim kuzatishni xohlamaydi.
- Asosiy ehtiyoj xodimlar kelib-ketishi va tashqarida bo‘lgan vaqtni bilish.
- Kunlik/haftalik/oylik tayyor hisobot kerak.
- Telegram orqali hisobot kerak.
- Avval ikki kamera bilan pilot, keyin etapma-etap kengaytirish ma’qullangan.
- Taxminiy dastlabki muddat sifatida 3–4 hafta tilga olingan; texnik reja 10 ish kuni + 7 kun testga aniqlashtirildi.

## NotebookLM bo‘yicha suhbat

- NotebookLM audio va matnni manba sifatida olib, savol-javob va xulosa qilish uchun foydali.
- Transkripsiya lokal bajarildi; tayyor matn keyinchalik NotebookLM’ga yuklanishi mumkin.

## Hikvision/AcuSeek rasmi bo‘yicha suhbat

- Rasm kamera modeli emas, Hikvision AcuSeek video-qidiruv funksiyasi edi.
- AcuSeek tabiiy tildagi so‘rov bilan yozuv ichidan odam, transport yoki hodisani topadi.
- U davomatni avtomatik hisoblamaydi va bizning Telegram/davomat dasturini almashtirmaydi.
- VPro NVR va mos AcuSense/AcuSearch qurilmalar talab qilishi mumkin.

## Kamera modellari muhokamasi

Taqqoslanganlar:

- DS-2CD3086G2-IS;
- DS-2CD3746G2H-LIZSU/SL;
- DS-2CD3786G2HT-LIZSU/SL;
- DS-2CD3146G2-IMS;
- DS-2CD3186G2-IMS;
- DS-2CD6825G0/C-IV(S).

Yakuniy tanlov: **DS-2CD3746G2H-LIZSU/SL (PTRZ), 4 MP, 2.7–13.5 mm**.

## Muhim tuzatish

Foydalanuvchi qat’iy ko‘rsatma berdi:

> POS bilan ERP’ni umuman aralashtirma.

Shuning uchun barcha keyingi tahlil va klient xabarlarida bu mavzular chiqarib tashlanadi va tilga olinmaydi.

## Telegram yozishmalari

- Birinchi uzun texnik taklif foydalanuvchi nomidan `Suxrob Kamera` chatiga yuborilgan.
- Keyin foydalanuvchi qisqa variantni faqat BelugaCat botiga yuborishni so‘ragan.
- Juda qisqa hisobot BelugaCat botiga yuborilgan.
- Texnik atamalar klient tushunadigan tilga o‘zgartirilgan va BelugaCat’ga qayta yuborilgan.
- Oxirgi tasdiqlangan matnda loyiha faqat kamera AI, odam sanash, xodim davomatini aniqlash va Telegram hisobotidan iborat.

## Maxfiylik

- Telegram tokenlari, API hash, user session va kamera parollari bu Obsidian papkasiga saqlanmaydi.
- Oldin chatda ko‘ringan tokenlar loyiha qaydlariga ko‘chirilmaydi.

## 2026-08-14 — yangi faoliyat tahlili talabi

- Klient xodimning bir kunlik ish jarayonini kelganidan ketgunigacha tahlil qilishni so‘radi.
- Yangi istaklar: kiyim yoki forma nazorati, samarali/bekor vaqt, bajarilgan ishlar va kunlik hisobot.
- Tekshiruvda bu talab avvalgi transkripsiyada umumiy “kim nima qildi” istagi sifatida tilga olingani, lekin tasdiqlangan birinchi taskga batafsil kirmagani aniqlandi.
- Talab alohida 2-bosqich AI moduli sifatida rejalashtirildi.
- Tavsiya: avval lokal GPU serverda bitta xodim, bitta hudud va 3–5 ta ish turi bilan 4–6 haftalik pilot; natijadan keyin kengaytirish.
- Klientga yuborishga tayyor yangi draft yozildi, lekin foydalanuvchining aniq yuborish buyrug‘isiz hech qayerga jo‘natilmaydi.

## 2026-08-14 — lokal davomat MVP qarori

- Kamera ichidagi qo‘shimcha soft hozircha chetga surildi.
- Birinchi amaliy versiya lokal video arxiv, yuzni aniqlash, IN/OUT hodisalari, davomat hisobi va Telegram hisobotidan iborat bo‘ladi.
- Video dalil/arxiv uchun saqlanadi; hisobot barcha videoni qayta ko‘rish orqali emas, real vaqtda yaratilgan hodisalar bazasidan hisoblanadi.
- Hisobotlar kunlik, haftalik va oylik bo‘ladi.
- Davomat “do‘konda bo‘lgan vaqt”ni hisoblaydi; samarali/bekor vaqt keyingi alohida modulda qoladi.
- Batafsil texnik reja: [[10 - Kamera o‘rnatilgandan keyingi lokal MVP rejasi]].

## 2026-08-14 — tomonlar, arxitektura va tasklar

- Klient va biz tomondagi barcha kerakli ishlar alohida ro‘yxatga ajratildi.
- Uskuna/montaj, lokal tarmoq, xodimlar ma’lumoti va hisobot talablari klient tomoni sifatida belgilandi.
- Lokal server, video integratsiya, AI, davomat, baza, admin panel, monitoring va Telegram biz tomondagi ishlar sifatida belgilandi.
- Obsidian uchun Mermaid arxitektura va ma’lumot oqimi sxemalari chizildi.
- Ish 8 ta EPIC va raqamlangan tasklarga bo‘lindi.
- Batafsil hujjat: [[11 - Tomonlar masuliyati arxitektura va tasklar]].

## 2026-08-14 — transkripsiya papkasi D diskka ko‘chirildi

- `Kamera AI transkripsiya` ishchi papkasi C diskdagi Desktop’dan `D:\Kamera AI transkripsiya` manziliga to‘liq ko‘chirildi.
- Ko‘chirishdan keyin 30 503 ta fayl va 1 035 096 500 bayt (taxminan 0.964 GB) tekshirildi.
- Eski C diskdagi manba papka qolmagan.
- Obsidian’dagi ishchi papka havolasi yangi D disk manziliga yangilandi.

Bog‘liq: [[06 - Klientga yuboriladigan matnlar]], [[07 - Keyingi sessiya uchun kontekst]], [[09 - Xodim faoliyatini tahlil qilish moduli]], [[10 - Kamera o‘rnatilgandan keyingi lokal MVP rejasi]], [[11 - Tomonlar masuliyati arxitektura va tasklar]]
