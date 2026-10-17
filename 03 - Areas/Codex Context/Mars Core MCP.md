---
type: integration
updated: 2026-10-08
status: login-required
---

# Mars Core — Beluga MCP

- [foydalanuvchi talabi] Beluga agenti Mars Core akkauntida mavjud bo‘limlarga kirib, tabiiy tildagi so‘rovlar bo‘yicha ish bajarsin. Akkauntning serverdagi huquqlari chegarasi saqlanadi.
- [tekshirildi: UI] Emirxan Ertan teacher dashboardi ochildi; 09.10.2026 uchun nF-455 10:10/B1, nF-460 15:10/A5, RCT-299 17:30/B2 — Yunusabad. Guruh davomatidagi Fri 09.10 bilan solishtirildi. Ro‘yxat explicit topshiriq bo‘yicha BelugaCat botga yuborildi, Telegram MCP receipt olindi.
- [o‘zgartirildi: kod/config] Beluga `marscore.py`, `marscore_mcp.py`, `marscore_routes.json`, focused test va README. Hermes `config.yaml`ga local stdio MCP qo‘shildi; private owner/task toolsetiga `marscore` qo‘shildi, group/background toolsetiga qo‘shilmadi. Mavjud unrelated o‘zgarishlar saqlandi.
- [tekshirildi: public frontend] Official app bundle va 139 lazy chunkdan 591 method/version/path katalog entry chiqarildi (309 GET, 199 POST, 35 PATCH, 19 PUT, 29 DELETE). Bu OpenAPI/schema yoki barcha route/account huquqlari jonli tekshirildi degani emas.
- [tekshirildi: test/MCP] 10 yangi test, jami 163/163 unit test; py_compile, git diff --check. Hermes mcp test marscore 5 tool topdi. Real stdio account_status login-required, route discovery natija qaytardi.
- [yozish oqimi] Exact owner request → current-state read → preview → 10 daqiqalik single-use ticket → durable attempt before I/O → execute → read-back. Noaniq write qayta yuborilmaydi. Credential/permission o‘zgartirishlari va StaffLog bypass toolda cheklangan. To‘lov, doimiy o‘chirish va boshqa consequential amallar alohida review talab qiladi.
- [cheklov] Mars Core login hali yo‘q. Jonli MCP account read/write sinalmagan; binary download, multipart upload va katalogda yo‘q API yo‘llar qo‘llanmaydi. “Hamma vazifa bajariladi” deb tasdiqlanmagan.
- [keyingi qadam] Owner lokal helperda telefon va yashirin parol bilan kiradi; parol saqlanmaydi, faqat private ignored state/marscore cookie sessiyasi. So‘ng account, groups va schedule real read bilan tekshiriladi; hech bir real baho/davomat/coin o‘zboshimchalik bilan o‘zgartirilmaydi.

Login:

```sh
/Users/protochka/.codex/telegram-personal/venv/bin/python /Users/protochka/Beluga/marscore.py login
```

Manbalar: https://core.marsit.uz/teacher-dashboard; https://core.marsit.uz/js/app.4cba16fc.js. Bog‘liq: [[Beluga Plan]], [[Comfort Setup]], [[Last Session]]. Credentiallar yoki private student/chat dump qaydga ko‘chirilmagan. Commit/push bajarilmadi.
