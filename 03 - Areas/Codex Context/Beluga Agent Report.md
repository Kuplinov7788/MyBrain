---
type: agent-report
updated: 2026-09-13
status: natural-task-live-validated
---

# Beluga Agent — imkoniyat va o‘zgarishlar hisoboti

## Natija

Beluga conversation-first agent yo‘nalishiga o‘tkazildi: oddiy owner so‘rovi suhbat,
Telegram action yoki restricted technical work ekanini agent tanlaydi. `/task` va
`/status` shortcut bo‘lib qoladi, kundalik majburiy interfeys emas.

## Agent nimani tushunadi

- Oddiy suhbat, follow-up va MyBrain/RAG kontekstli savollar.
- “Beluga testlarini tekshir”, “shu scriptni tuzat” kabi tabiiy technical work niyati;
  owner private chatida u restricted task oqimiga yo‘naltiriladi.
- Named recipientga draft/send, tanlangan suhbatni davom ettirish, pending media forward
  va ruxsatli group reply contractlari. Delivery’ni agent emas, policy host bajaradi.
- “Bas qil”, “endi u bilan gaplashma”, “shu suhbatni yop” kabi tabiiy stop iboralari.

## Nima o‘zgardi

- `experience.py`: atomik, private learning store. Lesson `candidate`dan boshlanadi;
  takroriy dalil yoki verified yozuv bilan `confirmed`ga o‘tadi. Faqat confirmed lesson
  relevant agent promptiga beriladi.
- `hermes_agent.py`: `task` action va relevant confirmed lessons qo‘shildi. Tabiiy
  technical request restricted high-reasoning task oqimiga o‘tishi mumkin.
- `bot.py`: tabiiy task routing; failure’da raw traceback yoki “/statusni ko‘ring” o‘rniga
  xato turi, noaniq natijani takrorlamaslik sababi va xavfsiz keyingi qadam beriladi.
- `conversation_intent.py`: tabiiy stop variantlari modelsiz deterministik ishlaydi.
- `status.py`: Telegram/RAG tarmoq xatosida traceback bilan yiqilmaydi, degraded JSON beradi.
- `AGENTS.md` va `README.md`: conversation-first, learning va permission chegaralari yozildi.

## Scriptlar bo‘yicha qaror

- Agent reasoning: niyat, savol, tashxis, taklif va javob mazmuni.
- Reusable skill: qayta ishlatiladigan soha bilimi/workflow.
- Zarur script/tool: Telegram transport, recipient/policy, durable queue/lock, media,
  observer, health va regression test.
- Legacy/duplicate entrypointlar topildi, lekin Git bo‘lmagan ishchi papkada jonli
  bog‘liqlikni isbotlamasdan o‘chirilmadi. Keyingi cleanup alohida dependency/live testdan keyin.

## Tekshiruv holati

### Tekshirilgan va ishlaydi

- 97/97 unit test; barcha Python compile; Node syntax.
- Natural stop inference bypass testi.
- Natural technical request → restricted task routing testi.
- Candidate → confirmed → relevant lesson recall testi.
- Status network failure → degraded JSON testi.
- LaunchAgent restartdan keyin worker `running`; observer `connected/fresh`; queue 0.
- Ikki owner-confirmed lesson live private store’da relevant recall bilan tekshirildi.
- Telegram owner private chatida slashsiz `Beluga testlarini tekshir va muammo bo‘lsa
  sababi bilan ayt` so‘rovi job `678230960` sifatida `done`, `error=null` yakunlandi.
  Agent 97 test, Python compile va Node syntax natijasini qaytardi; `/task` yoki `/status`
  talab qilmadi va fayl o‘zgartirmaganini aniq aytdi.
- Ikkinchi jonli diagnosis testi job `678230961`, `done`, `error=null`: agent Telegram,
  LaunchAgent, Hermes, observer, RAG, queue va testlarni o‘zi tekshirdi; joriy va tarixiy
  holatni ajratdi, isbotlanmagan sababni to‘qimadi va redacted error detail taklif qildi.
- Taklif implementatsiya qilindi: yangi failed joblarda `error`, `error_stage` va
  maxfiy raw matnsiz `error_detail` saqlanadi. Eski 10 failed job o‘zgartirilmadi.
- Error-detail schema migratsiyasi, explicit-column insert regressioni va barcha tekshiruv:
  98/98 test; worker restartdan keyin `running`, queue 0.

### Tayyor, lekin jonli sinalmagan

- Haqiqiy yangi failure yuz berganda redacted `error_stage/error_detail` yozilishi;
  sun’iy regression testda tekshirilgan, production failure ataylab chaqirilmadi.
- Confirmed lessonning real Hermes javob sifatiga ta’siri.

### Ochiq cheklovlar

- Ushbu sandbox CLI tekshiruvida Bot API DNS/network va RAG health `false`; workerning
  personal observer’i alohida processda connected. To‘liq Telegram inference testi owner
  xabari bilan tasdiqlanadi.
- Job store’da 10 ta tarixiy failed job bor; joriy queue/running/needs_review 0.
- `/Users/protochka/Beluga` Git repo emas. Rollback snapshot:
  `state/backup-20260913-conversation-agent/`.
- 32 root Python faylning legacy/compatibility qismini olib tashlash hali bajarilmadi.

## Git va yangi qurilmaga ko‘chirish

- Private code repo: <https://github.com/Kuplinov7788/Beluga>.
- Initial remote commit: `9d56fbf`; `main == origin/main`. [tekshirildi: Git/gh]
- MyBrain alohida private repo bo‘lib qoladi. Beluga `MYBRAIN_PATH` yoki `~/MyBrain`
  orqali lokal yangilangan vaultni o‘qiydi; RAG reindex yangi Obsidian mazmunini qidiruvga qo‘shadi.
- Token, Telegram session, chat context, job DB, media, private experience va loglar
  Gitga kirmaydi. Yangi laptopda credentials/login alohida tiklanadi.
- Full different-username bootstrap hali ochiq: installer va qolgan helper pathlari
  portable configga ko‘chirilishi kerak.

## Jonli qabul testi

Owner Beluga private chatiga slashsiz: `Beluga testlarini tekshir va muammo bo‘lsa sababi bilan ayt`
deb yozadi. Qabul mezoni: agent technical work’ni o‘zi tanlaydi, test dalilini qaytaradi,
`/task` yoki `/status` talab qilmaydi va tashqi xabar yubormaydi.

Natija: **o‘tdi**. [tekshirildi: `jobs.sqlite`, job `678230960`]

[[Beluga Plan]] · [[Beluga Runtime]] · [[Preferences]]
