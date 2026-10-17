---
type: integration-status
updated: 2026-10-06
---

# Beluga — Mem0 va RAG

- [foydalanuvchi ruxsati] Mem0 Beluga’ga o‘rnatilsin; foydali bo‘lsa Obsidian bilan moslashtirilsin va mavjud RAG tekshirilsin.
- [tekshirildi: CLI/kod] Mem0 OSS `2.2.1` Beluga `.venv-mem0` muhitida. Lokal Qdrant/history `Beluga/state/mem0/`da, telemetry o‘chirilgan. Mavjud RAG `/embed` endpointi va `multilingual-e5-base` 768-dimension modelidan foydalanadi. Yangi embedding model, cloud account yoki API key kerak bo‘lmadi.
- [tekshirildi: kod] Private owner chat va owner task uchun Mem0 qidiruvi promptga source/date/status bilan qo‘shiladi. Native `context.py` ham foydalanadi. Group/background oqimi bu owner Mem0 bazasini o‘qimaydi va yozmaydi.
- [tekshirildi: kod] Hermes `context_update.important_facts` orqali ajratgan qisqa faktlar `candidate` sifatida saqlanadi. Qo‘shimcha Mem0 LLM extraction `infer=False`; har xabar avtomatik indekslanmaydi. Summary, raw chat, draft va promise maydonlari import qilinmaydi. Credential pattern filtri oddiy secretlarni chetlaydi; bu barcha maxfiy ma’lumotlarni aniqlash kafolati emas.
- [tekshirildi: CLI] Preferences’dan bitta curated afzallik seed qilindi: o‘zbekcha, qisqa va amaliy javoblar. Mem0 orqali qayta topildi. Butun vault yoki private chatlar ko‘chirilmagan.

## Obsidian bilan munosabat

MyBrain — inson o‘qib/tahrir qiladigan kanonik qaydlar; RAG shu hujjatlardan passage topadi. Mem0 — agent suhbatining bounded faktlarini semantic qidiradi. Mem0 candidate yangi permission yoki confirmed operational lesson emas; muhim qarorda original qayd/API tekshiriladi. Eskirgan xotiradan ko‘ra yangi kanonik qayd ustun. Vaultni Mem0 bilan ikki tomonlama avtomatik mirror qilish yoqilmagan.

Dantes xotirasi alohida DantesBrain’da; hozirgi RAG ikkala vaultni qidiradi. Bu Mem0 integratsiyasi Dantes runtime/configiga yozmadi.

## Tekshiruv — 2026-10-06

- [tekshirildi: test] Beluga 153/153 unit test; production gate 32/32; Uzbek routing 40/40; Python compile, Node syntax, `pip check`, `git diff --check` o‘tdi.
- [tekshirildi: real lokal Mem0] Izolyatsiyalangan vaqtinchalik bazada add → yangi processdan search → retry dedup → delete → empty list o‘tdi. Candidate/source labels saqlandi. Production owner context real Mem0 va RAG source label’larini birga oldi.
- [tekshirildi: RAG] Health `ok`, 2434 chunk, model/reranker loaded. Live relevance 5/5, hit@5=1.0, MRR=0.9, o‘rtacha ~565 ms. Dantes vault haqidagi real query DantesBrain manbalarini ham qaytardi. Reindex LaunchAgent 600-soniyalik interval bilan sozlangan; bu har bir kelajakdagi indeks muvaffaqiyatiga kafolat emas.
- [tekshirildi: runtime] Idle queue’dan keyin worker restart qilindi. Telegram `true`, worker loaded, observer yangi PID/fresh; queue/running/review 0, 22 tarixiy failure. Mem0 health `ok`, count 1.
- [cheklov] Yangi Mem0 oqimi bilan jonli Telegram suhbat/model answer sifati hali sinalmagan. Retrieval natijasi javobning har safar to‘g‘riligini isbotlamaydi. Har Mem0 operatsiya 15 soniyagacha kutishi mumkin; uzilsa degraded label bilan RAG davom etadi. Automatic expiry yo‘q.

## Boshqarish

Beluga katalogida:

```bash
python3 status.py
python3 semantic_memory.py list
python3 semantic_memory.py search "savol"
python3 semantic_memory.py delete MEMORY_ID
```

Eski yoki xato fakt `list` orqali topilib ID bo‘yicha o‘chiriladi; tasdiqlangan durable qaror MyBrain kanonik qaydiga yoziladi. Lokal yozuv remote Git/cloud sync isboti emas; bu sessiyada commit/push qilinmadi.

Bog‘liq: [[Beluga Plan]], [[Preferences]], [[Last Session]].
Manba: https://github.com/mem0ai/mem0 va https://docs.mem0.ai/open-source/configuration.
