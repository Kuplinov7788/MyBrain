---
type: user-guide
updated: 2026-09-07
status: verified-core
---

# Beluga — qanday ishlataman?

Beluga — Telegram va haqiqiy Codex terminalidan foydalaniladigan bitta saqlangan
suhbat. MyBrain va lokal RAG xotira manbalari bo‘lib qoladi.

## 1. Kompyuterda ochish

Terminalga `beluga` yozing. Bu endi eski oddiy Python chatini emas, fondagi
Codex app-serverga ulangan haqiqiy Codex terminalini ochadi.

Oddiy `codex` buyrug‘i o‘z-o‘zidan Beluga suhbatini tanlamaydi. Beluga bilan
umumiy suhbat uchun aynan `beluga`dan foydalaning. Shu sozlashni qilgan alohida
Codex desktop chat avtomatik birlashtirilmagan.

Terminaldan chiqish: Ctrl+D. Remote Codex “Any running work continues” deb
xabarlaydi. Terminalni yopish suhbatni o‘chirmaydi. Ishni ataylab to‘xtatish
uchun Telegramda `/stop`; terminaldagi interrupt ham joriy ishni to‘xtatishi mumkin.

## 2. Telefonda davom ettirish

Telegramda `@BelugaCat_Asisstent_bot`ga o‘z akkauntingizdan yozing:

- “Hozir qayerda qoldik?”
- “Terminalda boshlagan ishimiz natijasini ayt.”
- “WeWatch haqida Obsidian qaydlarimdan topib ber.”
- “Bugungi ishlarim bo‘yicha reja tuz.” — mavjud qaydlar va bergan topshiriqlaringiz asosida.

Boshqa chat/guruh a’zolari bu owner-only workerga topshiriq bera olmaydi.
Terminaldagi ish faol bo‘lsa, yangi Telegram topshirig‘i navbatda kutadi.
Bir vaqtda ikki joydan boshqa-boshqa katta ish yubormaslik ma’qul: terminaldagi
matn faol umumiy ishga qo‘shimcha ko‘rsatma sifatida tushishi mumkin.

## 3. Buyruqlar

| Buyruq | Vazifasi |
| --- | --- |
| `/status` | Agent, RAG va navbat holati; AI chaqirilmaydi |
| `/usage` | Oxirgi qayd etilgan model input/output/cached tokenlari; pul narxi emas |
| `/stop` | Navbatni bekor qilish va faol umumiy ishga to‘xtatish so‘rovi |
| `/task README ni tekshir` | Beluga/MyBrain doirasidagi texnik ish |

Oddiy suhbat yoki aniq yuborish topshirig‘iga `/task` shart emas. Terminalga tabiiy
matn yozish kifoya. `beluga --once` eski matn adapteridir, yuborish uchun ishlatmang.

## 4. RAG va xotira

“Oldin nima degandim?”, “Loyiham haqida nima bilasan?” kabi so‘rovlarda tegishli
MyBrain qismlari RAG orqali olinadi. Qaror uchun muhim ma’lumot asl fayl bilan
solishtiriladi. Telegram so‘rovlariga qisqa kontekst beriladi; Codex terminali
`python3 /Users/protochka/Beluga/context.py "savol"` yordamchisidan foydalanadi.

“Buni eslab qol” yoki “Obsidian’ga yoz” desangiz, muhim fakt qaydga saqlanishi
kerak; suhbat tarixining o‘zi cheksiz va xatosiz xotira emas. Uzoq tarixni native
Codex terminalida `/compact` bilan ixchamlashtirish mumkin. RAG ishlamasa, agent
asosiy qaydlar bilan davom etib, cheklovni aytishi kerak.

Backgroundda Telegram xabarini kutish AI token sarflamaydi. Agentga so‘rov va
uning vosita/model davomlari sarflaydi. RAG konteksti 8,000 belgi bilan chegaralangan;
bu jami model input limiti emas. Eski tarix, tizim ko‘rsatmalari va vosita natijalari
ham inputga kiradi. `/usage` oxirgi kuzatilgan chaqiruvni ko‘rsatadi, native terminalning
keyingi sarfi hali qaydga tushmagan bo‘lishi mumkin.

## 5. Telegram xabar yuborish

Aniq topshiriq yozing: “@username ga «matn» deb yubor”. Ism noaniq bo‘lsa agent
aniqlik so‘raydi. “Javob loyihasini yoz” yuborish topshirig‘i emas. Tashabbusli
shaxsiy auto-reply yoqilmagan. Yangi app-server orqali boshqa odamga jonli yuborish
bu etapda sinalmagan; barcha live testlar ownerning Beluga private chatida bo‘ldi.

## 6. Uzilish bo‘lsa

Mac uyg‘oq, foydalanuvchi login qilgan va internetga ulangan bo‘lsin. Mac uyquda
va o‘chiq bo‘lsa bu lokal xizmat javob bermaydi. Terminalni yopish Mac’ni uxlatish emas.

`/status`da `needs_review`/tekshirish kerak chiqsa, qayta yuborishga shoshilmang:
oldingi yuborish natijasi noaniq bo‘lishi mumkin. `/stop` allaqachon yuborilgan xabarni
qaytarib olmaydi. To‘liq Mac sleep/reboot sinovi hali bajarilmagan.

## Tekshirilgan natijalar — 2026-09-06

- Native Codex terminali mavjud Beluga thread’iga ulandi.
- Terminal Ctrl+D bilan yopilgach, Telegram bot o‘sha sinov kontekstini to‘g‘ri esladi.
- RAG command agentning o‘zi tomonidan bajarildi va asl WeWatch manbasi qaytdi.
- Telegram worker faol task paytida restart qilindi: o‘sha turn ID saqlandi, bitta yakuniy javob keldi.
- Ish davomida `/status` Telegramga `active` va navbat holatini qaytardi.
- 36 test, Python compile, Node syntax tekshiruvlari o‘tdi.

## Keyingi etap

Avtomatik vaqtli eslatmalar, kunlik avtomatik hisobot, loyihalar bo‘yicha alohida
suhbatlar va topicga yuborish hali bu etapga kirmaydi. Reja yozish — vaqtli eslatma
yoqildi degani emas. App-server remote transporti Codex’da experimental.

## Aloqador

- [[03 - Areas/Codex Context/Beluga Plan|Talablar va etap jurnali]]
- [[03 - Areas/Codex Context/Last Session|Oxirgi sessiya]]
- [OpenAI app-server hujjati](https://learn.chatgpt.com/docs/app-server)

2026-09-07 yakuniy tekshiruv: app-server, Telegram worker va RAG LaunchAgentlari running. RAG qidiruvi ushbu qo‘llanmani indeksdan qaytardi; navbatda qolgan yoki tekshirish talab qiladigan job yo‘q edi. Git push bajarilmadi.

## 2026-09-07 — Terminal natijasi endi Telegramga keladi

Terminalda `beluga` bilan ish boshlang. Ctrl+D bilan chiqishingiz mumkin. Yangi
terminal javobi tayyor bo‘lgach, bot Telegramga «Emirhan, terminaldagi topshiriqqa
javob tayyor» va qisqa natijani yuboradi. Tekshiruv oralig‘i 8 soniya; tarmoq
kechikishi qo‘shilishi mumkin. Failed/interrupted ish muvaffaqiyat deb ko‘rsatilmaydi.
Eski tarix avtomatik yuborilmaydi, Telegramdan berilgan ish javobi takrorlanmaydi.
Bu kuzatish AI token sarflamaydi. Murojaat va jonli auto-notification sinaldi;
barcha testlar jami 47 ta o‘tdi. Mac uyg‘oq va internetda bo‘lishi kerak.
