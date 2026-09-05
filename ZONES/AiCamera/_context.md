---
type: zone-context
zone: AiCamera
owner: Kuplinov7788
updated: 2026-09-05
source_repository: https://github.com/Kuplinov7788/AiCamera-
---

# AiCamera — Zone Context

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
