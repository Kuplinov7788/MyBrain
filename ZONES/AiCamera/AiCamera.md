---
type: project
project: AiCamera
updated: 2026-09-05
---

# AiCamera

Windows uchun lokal Hikvision A5 Room AI kamera prototipi.

## Nima qiladi

- Kameradan odamlarni aniqlaydi va xona bandligini hisoblaydi.
- Ixtiyoriy lokal yuz ro‘yxati orqali tanilgan profilni ko‘rsatadi.
- Lokal dashboard va CSV hodisa jurnalidan foydalanadi.

## Texnologiya

Python, OpenCV DNN, YOLOv8n ONNX, Hikvision HCNetSDK, YuNet va SFace.

## Hozirgi holat

- A5 Room, NVR channel 9 person detection sinovidan o‘tgan.
- Snapshot rejimi: taxminan 4.8–6.1 AI FPS.
- RealPlay substream: taxminan 8.5–8.6 AI FPS.

## Muhim cheklovlar

Keng rakursda yuzlar kichik bo‘lishi mumkin; tanish natijasi yakuniy identifikatsiya deb qabul qilinmaydi. Kirish/chiqishni ishonchli aniqlash uchun eshikka qaragan kamera yoki line-crossing tracker kerak.

## Batafsil kontekst

- [[_context|AiCamera — to‘liq loyiha konteksti]]
- Kod: `/Users/protochka/AiCamera-`
- Repository: [Kuplinov7788/AiCamera-](https://github.com/Kuplinov7788/AiCamera-)
