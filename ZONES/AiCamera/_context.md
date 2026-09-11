---
type: zone-context
zone: AiCamera
owner: Kuplinov7788
updated: 2026-09-11
source_repository: https://github.com/Kuplinov7788/AiCamera-
---

# AiCamera — Zone Context

## 2026-09-11 — Desktop nusxasi auditi

- Emirhan `/Users/protochka/Desktop/ai-camera` papkasini to‘liq audit qilishni so‘radi: barcha vazifalar/scriptlar/struktura, odamni “Begona #1” sifatida saqlash, old/orqa ko‘rinishda tanishning uzilishi va yaxshilash tartibi.
- [tekshirildi: fayl/CLI] Audit nishoni commit `9e26413`; 18 Python modul, JS/shell/README/ignore va 13 data JSON ko‘rib chiqildi. Hozirgi nusxa Flask 5001, YOLOv8s-pose + YOLOv8m, ByteTrack, ArcFace va BoxMOT ReID ishlatadi. Quyidagi Windows/8787 qaydlari eski boshqa nusxa konteksti; Desktop nusxasining joriy holati deb olinmasin.
- [tekshirildi: CLI] Bir kadr yo‘qolishi identity keshini o‘chiradi; qarama-qarshi tana namunasi eski identity gallery’siga yozilib unbind’ni bekor qiladi; body-only yangi visitor raqami yaratishi mumkin; enrollment boshqa yuzni ham qabul qiladi; parallel Memory writer yozuvni bosadi; qaytishdan keyingi gallery/last diskka to‘liq flush qilinmaydi. Dashboard `lastScan` xatosi va SAHI reentrant lock muammosi ham offline ko‘rsatildi.
- [tekshirildi: fayl] GUI stranger nazorati default o‘chiq; NVR capture UI fokusiga bog‘liq. Eski SFace va active ArcFace bazalari alohida; avtomatik migratsiya yo‘q.
- [tekshirildi: CLI] Mavjud visitor testlari 16/16 o‘tdi; audit probe 12 kuzatuvni (syntax + 11 xato/cheklov yo‘li) tekshirdi. Root Python AST, JS syntax va shell syntax tekshirildi. Bu real model aniqligi o‘lchovi emas.
- Chegara: ushbu nusxada venv/modellar/.env/visitor runtime bazasi yo‘q; jonli NVR/Mars/Telegram va real old/orqa inference tekshirilmagan. Koddagi eski FPS/accuracy izohlari qayta o‘lchanmagan.
- Hisobot: `/Users/protochka/Desktop/ai-camera/audit/AUDIT-2026-09-11.md`; qayta tekshiruv: `audit/probe.py`, dalil: `audit/results.json`. Bu boshlang‘ich commit auditi; keyingi patch quyida. Probe ataylab boshlang‘ich commitni vaqtinchalik papkada qayta bajaradi.
- [taklif] Avval identity/xotira, enrollment, yagona writer/engine, diagnostics va UI’dan mustaqil capture; keyin belgilangan kamera videosida oldin/keyin benchmark. Orqadan 100% doimiy kimlik va’da qilinmaydi; local track, person identity va visit alohida bo‘lsin.
- Maxfiy qiymatlar, embeddinglar yoki real kadrlar MyBrain’ga ko‘chirilmagan. Quyidagi “Git’da saqlanmaydi” eski qoida amalda Desktop nusxada bajarilmagan: credential joyi va tracked yuz/davomat fayllari auditda qayd etildi, remote tarqalish tekshirilmagan.

### “Davom et ishni”dan keyingi lokal tuzatishlar

- [tekshirildi: fayl/CLI] Production ish daraxtiga 5 sekund identity grace, zid tana namunasini o‘rganmaslik, visible identity collision himoyasi, lost-to-new-track qayta bog‘lash, enrollment similarity gate va `storage.py` orqali jarayonlararo atomik JSON yozuvi kiritildi. Default `BODY_ONLY_REGISTER=0`: yuzsiz yangi visitor ochilmaydi; eski tana mos kelsa tanish davom etadi; dalil yetmasa UI “Aniqlanmoqda” ko‘rsatadi. Mavjud env=1 yangi defaultdan ustun.
- [tekshirildi: CLI] 30/30 yangi regression va 16/16 mavjud visitor testi o‘tdi; 21 Python fayl AST, JS/shell syntax, diff check va tracked data o‘zgarmagani tasdiqlandi. 3 alohida process 24 yozuvni yo‘qotmasdan saqladi. Dashboard, SAHI, uzilgan streak, filial key, sleeping attribution va invalid RPC yo‘llari ham tekshirildi. Offline model o‘rinbosarlari ishlatilgan; bu ML aniqligi yoki real API testi emas.
- Patch tafsiloti: `/Users/protochka/Desktop/ai-camera/audit/FIXES-2026-09-11.md`; dalil: `audit/regression-results.json`. Real model/kamera/Telegram ishga tushirilmagan, commit/push/deployment bajarilmagan.
- Keyingi etap uchun Emirhandan muammoli filial/kamera va ishlayotgan nusxa kompyuter/papka yo‘li so‘raldi; javob hali olinmagan. Jonli old/orqa benchmark, doimiy capture, global identity service, model provenance va eski bazani migratsiya qilish ochiq. File lock alohida jarayonlarning `match → add` qarorlarini yagona transaction qilmaydi; shaxs dublikatini to‘liq bartaraf etmaydi.

## Tarixiy kontekst — 2026-09-05

## Umumiy

Windows uchun lokal Hikvision A5 Room AI prototipi. Tizim kameraning read-only oqimidan odamlarni aniqlaydi, xona bandligini hisoblaydi va ixtiyoriy lokal yuz ro‘yxati orqali tanilgan profilni ko‘rsatadi.

## Kod va manbalar

- **Asl kod repositorysi:** <https://github.com/Kuplinov7788/AiCamera->
- **Asosiy branch:** `main`
- **Lokal kod papkasi:** `/Users/protochka/AiCamera-`
- **Ushbu vaultdagi vazifa:** loyiha konteksti, qarorlar va ish rejasini saqlash. Kod, modellar, kamera kadrlari va biometrik ma’lumotlar bu yerga ko‘chirilmaydi.

## Imkoniyatlar

- Hikvision SDK orqali read-only RealPlay oqimi yoki JPEG snapshot olish;
- YOLOv8n ONNX orqali `person` detection va occupancy count;
- YuNet + SFace orqali lokal face enrollment va recognition;
- tanilgan xodim uchun oxirgi ko‘rinish, taxminiy chiqish/qaytish hamda tashqarida bo‘lgan vaqtni lokal jurnal qilish;
- `http://127.0.0.1:8787` lokal dashboard va CSV hodisa jurnali.

## Texnik stack

- Python, OpenCV DNN, YOLOv8n ONNX;
- Hikvision HCNetSDK va PlayCtrl;
- YuNet face detection va SFace embedding;
- Windows + PowerShell.

## Tasdiqlangan natijalar

- A5 Room, NVR channel 9 da person detection sinovi muvaffaqiyatli o‘tgan;
- snapshot rejimida taxminan 4.8–6.1 AI FPS;
- tavsiya qilingan Hikvision RealPlay substream rejimida taxminan 8.5–8.6 AI FPS;
- 15–25 AI FPS uchun GPU yoki yengilroq/kvantlangan model kerak bo‘ladi.

## Cheklovlar va xavfsizlik

- Keng va baland A5 Room rakursida yuzlar kichik bo‘lishi mumkin; recognition natijasi yuqori ishonchli identifikatsiya sifatida qabul qilinmaydi.
- Kirish/chiqishni ishonchli aniqlash uchun eshikka qaragan kamera yoki line-crossing tracker kerak.
- Kamera credentiallari, real kadrlar, yuz embeddinglari, ONNX model binarlari Git yoki vaultga saqlanmaydi.
- Biometrik ma’lumot faqat xabardor rozilik bilan ishlatiladi va avtomatik natija mehnatga oid yakuniy qarorning yagona asosi bo‘lmaydi.
- Dashboard internetga chiqarilsa, autentifikatsiya bilan himoyalanishi shart.

## Keyingi ishlar

- [ ] Odam tracking ID qo‘shish va takroriy sanashni kamaytirish
- [ ] Xona zonasi, `entered/exited/current occupancy` holatlarini qo‘shish
- [ ] Esnikka qaragan kamera yoki line-crossing tracker bilan kirish/chiqishni tekshirish
- [ ] Dashboard uchun autentifikatsiya strategiyasini belgilash

## Asl repo hujjatlari

- `README.md` — umumiy ishga tushirish va arxitektura;
- `FACE-ENROLLMENT.md` — yuz ro‘yxatga olish tartibi;
- `A5-AI-STAGE1-REPORT.md` — 1-bosqich test hisoboti;
- `A5-FPS-REPORT.md` — FPS optimizatsiyasi;
- `models/README.md` — alohida yuklanadigan ONNX modellar.

---

*Zone context | AiCamera | 2026-09-05*
