---
type: technical-analysis
project: Higvision Proekt
updated: 2026-08-13
---

# Kamera modellari tahlili

## Yakuniy tavsiya

### DS-2CD3746G2H-LIZSU/SL (PTRZ) — birinchi tanlov

Tavsiya etiladigan konfiguratsiya:

- 4 MP;
- 2.7–13.5 mm motorli varifocal obyektiv;
- PTRZ;
- PoE;
- Face Capture;
- People Counting;
- AcuSense;
- HEOP 2.0;
- RTSP, ONVIF va ISAPI.

Nega mos:

- katta 1/1.8" sensor va yaxshi tungi tasvir;
- yuzni aniqlash uchun 4 MP yetarli;
- 8 MP’ga qaraganda disk, tarmoq va server yuki pastroq;
- motorli zoom/fokus sabab montajdan keyin ham kadrni to‘g‘rilash mumkin;
- IP66 va IK10 himoya;
- HEOP kelajakdagi custom AI uchun imkoniyat qoldiradi.

## Taqqoslangan modellar

| Model | Kuchli tomoni | Kamchiligi | Qaror |
|---|---|---|---|
| DS-2CD3746G2H-LIZSU/SL | 4 MP, motorli zoom, katta sensor, Face Capture, People Counting, HEOP | Qimmatroq | Asosiy tavsiya |
| DS-2CD3786G2HT-LIZSU/SL | 8 MP, motorli zoom, Face Capture, People Counting, HEOP | Ko‘proq disk/server yuki; HEOP quvvati 4 MP bilan bir xil | Katta hudud/uzoq masofa bo‘lsa |
| DS-2CD3146G2-IMS | 4 MP, HEOP, Face Capture, People Counting, tejamkor | Fixed lens; joyni oldindan aniq o‘lchash kerak | Tejamkor pilot |
| DS-2CD3186G2-IMS | 8 MP, HEOP, Face Capture, People Counting | Fixed lens va ortiqcha 8 MP yuk | Narx farqi kichik bo‘lsagina |
| DS-2CD3086G2-IS | 8 MP bullet, HEOP, People Counting, Face Capture, IP67 | Fixed lens; ayrim bozorlarda EOL/discontinued | Tashqi hudud uchun |
| DS-2CD6825G0/C-IV(S) | Dual-lens 3D People Counting juda aniq | Yuzni ism bilan aniqlashga mos emas; tepadan qaraydi; EOL | Faqat anonim odam sanash uchun |

## Atamalar farqi

- **People Counting:** nechta odam kirdi/chiqdi.
- **Face Capture:** yuz rasmini ushlaydi.
- **Face Recognition:** yuzni bazadagi ism bilan solishtiradi.
- **Davomat dasturi:** kelish, ketish, tanaffus va jami ish vaqtini hisoblaydi.

People Counting borligi xodimni ism bilan tanish va davomat tayyor degani emas.

## DS-2CD6825G0/C-IV(S) bo‘yicha qaror

Ikki obyektiv va 3D ko‘rish tufayli anonim odam sanashda juda yaxshi. Shiftga 90° pastga qarab o‘rnatiladi va yuzni ko‘rmaydi. Shuning uchun klientning “Sardor qachon keldi/ketdi?” maqsadini yolg‘iz bajara olmaydi. Bundan tashqari model EOL sifatida ko‘rsatilgan.

## Xariddan oldingi real demo

- ikki odam yonma-yon kirishi;
- odam kirib darhol qaytib chiqishi;
- kepka va turli yoritishda yuz ushlanishi;
- Entered/Exited sonlari;
- Face Capture rasmi;
- ISAPI hodisasini tashqi server olish;
- Face Capture va People Counting bir vaqtda ishlashi;
- aynan sotilayotgan suffix va firmware’da HEOP mavjudligi.

Bog‘liq: [[03 - Texnik arxitektura va qarorlar]]

