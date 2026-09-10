---
type: moc
updated: 2026-09-09
status: unified
---

# Hermes Hub — yagona bilim va ish oqimi

Bu sahifa Hermesga tegishli kurs, konfiguratsiya, Beluga transporti va tekshiruvlarni bitta kirish nuqtasiga birlashtiradi. Transcriptlar alohida fayl sifatida saqlanadi, lekin ularning indeks va amaliy ma’nosi shu hub orqali boshqariladi.

## Asosiy havolalar

- [[Hermes Course - TezCode Learning|Kurs xulosasi va amaliy xarita]]
- [[Hermes Setup|Joriy Hermes sozlamalari va audit]]
- [[Beluga Plan|Beluga ↔ Hermes reja va media oqimi]]
- [[Last Session|Oxirgi sessiya va davom ettirish nuqtasi]]
- [[Context MOC|MyBrain umumiy xaritasi]]

## Transcriptlar

Manba: Beluga pending Telegram media. To‘liq ro‘yxat va lokal fayl mapping: `Hermes Course Transcripts/manifest.json`. Har bir darsning `.md` faylida timestamp, audio matni va `.segments.json` segmentlar bor.

### Guruhlar

- 11–15: [[Hermes Course Transcripts/11 - dars-11-Hermes fayllari joylashuvi|Files]], [[Hermes Course Transcripts/13 - dars-13-Pluginlar- imkoniyatlarni kengaytirish|Plugins]], [[Hermes Course Transcripts/14 - dars-14-Pluginlarni boshqarish|Plugin boshqaruvi]], [[Hermes Course Transcripts/15 - dars-15-Kanban- vazifalarni boshqarish|Kanban]]
- 16–20: profile, MCP va tools transcriptlari — `Hermes Course Transcripts/16 ...` dan `20 ...` gacha
- 21–25: Git, memory, curator, sub-agent va browser transcriptlari — `Hermes Course Transcripts/21 ...` dan `25 ...` gacha
- 26–30: webhooks, pairing, auth, ops va analytics — `Hermes Course Transcripts/26 ...` dan `30 ...` gacha
- 31–35: automation transcriptlari — `Hermes Course Transcripts/31 ...` dan `35 ...` gacha
- 36–40: skill yaratish, tekshirish va xavfsizlik — `Hermes Course Transcripts/36 ...` dan `40 ...` gacha
- 41–45: Telegram, group, voice, media va mobile — `Hermes Course Transcripts/41 ...` dan `45 ...` gacha
- 46–50: model, local/cloud, context, cost va fallback — kurs xaritasida; transcript mavjud bo‘lsa shu papkadan tekshiriladi
- 51–55: debugging, gateway, update, backup va config — `Hermes Course Transcripts/51 ...` dan `55 ...` gacha
- 56–60: unified workflow, g‘oyalar, security va exam — `Hermes Course Transcripts/56 ...` dan `60 ...` gacha

## Ishlash tartibi

1. So‘rovni shu hub va [[Hermes Course - TezCode Learning|kurs xaritasi]] bilan bog‘la.
2. Tegishli transcriptni o‘qi; keyin live Hermes/Beluga holatini tekshir.
3. O‘zgarish bo‘lsa config/kodga yoz, health check qil, so‘ng shu hub yoki tegishli note’ga qisqa qaror yoz.
4. Telegram media yuborish faqat aniq recipient + action buyrug‘i bilan; o‘qish/transkripsiya yuborish ruxsati emas.
5. Skill va memory — qayta ishlatiladigan qoidalar; model weight retraining yoki o‘z-o‘zidan ruxsat kengayishi emas.

## Bog‘langan runtime artefaktlar

- Skill: `/Users/protochka/.hermes/skills/hermes-course/SKILL.md`
- Transcriber: `/Users/protochka/Beluga/scripts/transcribe_hermes_course.py`
- Transcript manifest: `/Users/protochka/MyBrain/03 - Areas/Codex Context/Hermes Course Transcripts/manifest.json`
