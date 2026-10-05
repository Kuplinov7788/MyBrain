# Uysot — 8 Sales savolining UI tekshiruvi

Sana: 2026-09-29. Manba: foydalanuvchi so‘rovi bilan mavjud Chrome tabidagi Uysot hisobini Computer Use orqali o‘qish. Hisob UI’da Venera / Супер администратор deb ko‘rindi. Bu browser sahifalari tekshiruvi; API response/schema tekshiruvi emas.

Bog‘liq: [[Dantes Sales bosqichma-bosqich reja 2026-09-29]] · [[Sales suhbat - muammolar va AI agent talablari]].

## 1. Shu oy sotilgan uylar qayerda ko‘rinadi?

- [tekshirildi: UI] `Статистика → Продажа` (`/boss/sale`): yil 2026, `Помесячные` tanlangan; oylik xonadon soni/maydoni grafigi va hudud kesimidagi kartalar bor. Kartalarda 5 ko‘rindi; bu tekshirilgan sotuv soni sifatida olinmadi. Karta davri va hisob qoidasi ushbu tekshiruvda tasdiqlanmadi; oldingi 4 raqamini Sales rad etgan.
- [tekshirildi: UI] `Договоры` (`/main/contract`): sana, holat, ЖК, to‘langan summa kabi ustunlar; filtrda `Дата` va `Дата внесения в систему` alohida. `Статус договора` va `Удалённые контракты` filtrlari mavjud.
- [ochiq] Oylik sotuv qaysi sana/status bilan sanaladi va Venera qaysi hisobotga tayanadi? Grafik mavjudligi uning raqami biznes bo‘yicha to‘g‘ri ekanini isbotlamaydi.

## 2. Har bir loyiha qaysi kompaniyaga tegishli?

- [tekshirildi: UI] `Настройки → Строитель` (`/main/setting/builder/builder-config`) ikkita tashkilotni ko‘rsatadi: GULISTON INTER FUTBOL MCHJ va Harorat Invest MCHJ. Shaxsiy telefon/manzil/direktor tafsilotlari qayd qilinmadi.
- [tekshirildi: UI] `Настройки → Создание и редактирование ЖК` (`/main/setting/house/house-config`) har bir loyihaning mavjud formasidagi `Ответственный за строительство` qiymati o‘qildi; hech narsa saqlanmadi:

| Loyiha | Uysot’da qurilish uchun mas’ul tashkilot |
|---|---|
| Boston Avenue | GULISTON INTER FUTBOL MCHJ |
| Sayqal Residence | GULISTON INTER FUTBOL MCHJ |
| Yangiyer | GULISTON INTER FUTBOL MCHJ |
| Harorat Invest | Harorat Invest MCHJ |

- [ochiq] Bu konfiguratsiya quruvchi/mas’ul maydoni. Sotuvchi yuridik shaxs, pulni oluvchi kompaniya va guruh konsolidatsiyasi uchun kompaniya aloqasi ham shunday ekanini hujjat egasi tasdiqlashi kerak. Uysot’dagi ikki tashkilot guruhdagi barcha kompaniyalar ro‘yxati emas.
- [Venera tuzatishi, 2026-09-29] Jadvaldagi Harorat Invest — loyiha nomi emas: shu kompaniya loyihasining to‘g‘ri nomi **Park Residence**. Venera kompaniyalar to‘g‘ri ko‘rsatilganini tasdiqladi.

## 3. To‘lov qanday tasdiqlanadi, chek saqlanadimi?

- [tekshirildi: UI] `Платежи` (`/main/payment`): yozuv raqami, asos, mijoz, shartnoma, sana, summa, to‘lov turi, mas’ul va ЖК ustunlari bor.
- [tekshirildi: UI] Shartnoma tafsilotida `История платежей` mavjud. `Архив` ochilganda `Архив таблицы платежей` chiqdi va tekshirilgan bitta shartnomada `Нет данных` ko‘rindi. Bu chek/hujjat arxivi sifatida tasdiqlanmadi.
- [tekshirildi: UI] To‘lovlar sahifasidagi `Банк` → `/main/monetary` bank integratsiyasining tavsifi va bog‘lanish ma’lumotini ko‘rsatdi. Bank ko‘chirmasi yoki amalga oshayotgan reconciliation ushbu ekranda ko‘rinmadi; boshqa joyda integratsiya yo‘q deb xulosa qilinmadi.
- [ochiq] Venera to‘lovni qaysi hujjat bilan tekshiradi va dalilni qayerda saqlaydi? `Банк` turi yoki Uysot’da summa borligi bank tasdig‘i emas.

## 4. Kelajakdagi badal va kechikkan qarz qayerda?

- [tekshirildi: UI] `Договоры → shartnoma → График платежей`: `Дата платежа`, `Сумма`, `Сумма платежа (сум)` ustunlari bor. Shartnoma tafsilotida `Оплаченная сумма`, `Оставшаяся сумма`, `Долг текущего месяца` ham ko‘rinadi.
- [tekshirildi: UI] `Задолженность` (`/main/arrearage`): shartnoma, mijoz, qarz summasi, kechikish, sana, penya, mas’ul va maksimal kechikish ustunlari bor.
- [natija] Ekranlarning joylashuvi aniqlandi. Qoldiq, kelajakdagi badal va muddati o‘tgan qarzning hisob formulalari hamda jadval to‘liqligi alohida tekshiriladi. “Qayerdan ko‘rasiz?” savolini umumiy shaklda qayta berish zarur emas.

## 5. Eslatma va direktorga eskalatsiya tartibi?

- [tekshirildi: UI] `Настройки → SMS → Отправка сообщений` (`/main/setting/message/sending-message`): `Задолженность` guruhida `За день до дня оплаты` switch yoqilgan; `Сообщение о задолженности` switch o‘chiq. Toggle’lar o‘zgartirilmadi.
- [cheklov] Yoqilgan sozlama haqiqiy yuborish/yetkazish isboti emas. SMS provider ulanishi va yuborish jurnali ushbu tekshiruvda tasdiqlanmadi.
- [avvalgi Sales javobi] Bir necha ogohlantirishdan keyin direktor Jonibek Komiljonovichga eskalatsiya qilinadi.
- [ochiq] Qo‘ng‘iroq/eslatmalar soni, oralig‘i, qayerga yozilishi va eskalatsiya mezoni. SMS sozlamasi bu qo‘lda bajariladigan tartibning o‘rniga olinmaydi.

## 6. Suhbat natijasi va keyingi aloqa qayd qilinadimi?

- [tekshirildi: UI] `Система CRM` (`/main/crm`) voronkasi mavjud. Lead kartasida `Чат`, `Примечание`, `Задание` va sana/mas’ul bilan vazifa kiritish joyi bor. Tekshirilgan bitta eski kartada vazifa va o‘chirilgan vazifa tarixi ko‘rindi. Qayd/yuborish tugmasi bosilmadi.
- [tekshirildi: UI] Hozirgi `Задачи` (`/main/task`) ko‘rinishi umumiy 0; o‘tgan/bugungi/ertangi/rejadagi 0 ko‘rsatdi. Barcha tarix yoki barcha xodimlarning haqiqiy ish hajmi deb talqin qilinmadi.
- [ochiq] Venera amalda har qo‘ng‘iroq natijasi va keyingi sanani shu yerga yozadimi yoki boshqa joyda yuritadimi? Imkoniyat borligi barcha ma’lumot kiritilganini isbotlamaydi.

## 7. Xato to‘lov yoki bekor shartnoma qanday tuzatiladi?

- [tekshirildi: UI] Shartnoma tafsilotida `Отменить` amali bor; shartnomalar ro‘yxatida `Отменено` holati mavjud. Bekor qilish amali bajarilmadi.
- [tekshirildi: UI] `Изменения` (`/main/changes`) oynasida `Данные клиента`, `Данные договора`, `Формирование графика`, `Добавить платёж` tablari bor. Mijoz tanlanmasdan shartnoma tabiga kirishda `Клиент не выбран` chiqdi; yozuv tanlab/o‘zgartirib ko‘rilmadi.
- [cheklov] `Список событий` sahifasi ochildi, lekin jadval loading holatidan chiqmagan; ishlaydigan to‘lov audit jurnali deb tasdiqlanmadi.
- [ochiq] Xato to‘lovni tuzatish tartibi, ruxsat/tasdiqlovchi, qaytarilgan pul, qarz va xonadon statusining yangilanishi. Menyu yoki tab borligi jarayon xavfsiz/to‘liq ekanini isbotlamaydi.

## 8. Eng ko‘p vaqt oladigan ish va AI yordamining ustuvorligi?

- [ochiq] Dashboarddan Veneraning sarflaydigan vaqti, kundalik og‘irligi yoki qaysi ishni afzal ko‘rishini aniqlab bo‘lmaydi. Bu savol o‘zidan so‘raladi.
- [taklif] Keyingi agent vazifasini uning javobi va tekshirilgan ma’lumotdan kelib chiqib tanlash. Qarz agenti yoki avtomatik mijoz xabari hali tanlangan yechim emas.

## Tekshiruvdan keyingi qisqa savollar — yuborilmagan draft

1. Oy bo‘yicha sotuv hisobida `Дата`mi yoki `Дата внесения в систему`mi olinadi? Qaysi statusdagi shartnomalarni sotuv deb sanaysiz?
2. Uysot’da Boston, Sayqal va Yangiyer uchun GULISTON INTER FUTBOL, Harorat loyihasi uchun Harorat Invest ko‘rsatilgan. Shartnomadagi sotuvchi kompaniya va pul tushadigan kompaniya ham shularmi?
3. To‘lovni bank ko‘chirmasi, chek yoki qaysi hujjat orqali tasdiqlaysiz? Hujjatni qayerda saqlaysiz?
4. To‘lovdan bir kun oldingi SMS sozlamasi yoqilgan ekan — amalda mijozga yetib boradimi? O‘zingiz necha marta/qanday oraliqda eslatib, keyin direktorga chiqarasiz?
5. CRM’da izoh va vazifa bor ekan. Siz har bir suhbat natijasi va keyingi qo‘ng‘iroq sanasini shu yerga yozasizmi yoki boshqa joyga?
6. Noto‘g‘ri kiritilgan to‘lov yoki bekor shartnomani kim, qanday tasdiq bilan tuzatadi? Qaytarilgan pulni qayerga yozasiz?
7. Qaysi ikkita ish eng ko‘p vaqt oladi yoki xato chiqadi? AI avval qaysi birida yordam bersin?

### Русский

1. Для подсчёта продаж за месяц вы используете `Дата` или `Дата внесения в систему`? Договоры с какими статусами считаете продажей?
2. В Uysot у Boston, Sayqal и Yangiyer указан GULISTON INTER FUTBOL, у проекта Harorat — Harorat Invest. Эти же компании указаны продавцами в договорах и получают оплату?
3. По какому документу вы подтверждаете оплату: выписке банка, чеку или другому? Где храните этот документ?
4. Настройка SMS за день до оплаты включена. Доходят ли эти сообщения клиентам? Сколько раз и с каким интервалом вы сами напоминаете об оплате до обращения к директору?
5. В CRM есть примечания и задачи. Записываете ли вы там результат каждого разговора и дату следующего звонка или ведёте это в другом месте?
6. Кто и с чьего подтверждения исправляет ошибочный платёж или отменённый договор? Где фиксируете возврат денег?
7. Какие две задачи занимают больше всего времени или чаще приводят к ошибкам? С какой из них ИИ должен помочь в первую очередь?

Во время проверки данные не сохранялись в Uysot, сообщения не отправлялись. В заметку не перенесены имена, телефоны и суммы отдельных клиентов, а также секреты.

## Javoblar

- [Venera tasdiqladi, 2026-09-29] Oylik sotuvlar shartnoma tuzilgan sana (`Дата`) bo‘yicha hisoblanadi; barcha shartnoma statuslari sotuvga kiradi.
- [Venera tasdiqladi, 2026-09-29] Kompaniyalar to‘g‘ri ko‘rsatilgan. Harorat Invest MCHJ bo‘yicha loyiha nomi **Park Residence** (oldingi savolda loyiha nomi Harorat Invest deb noto‘g‘ri berilgan).
- [Venera tasdiqladi, 2026-09-29] SMS xabarlari abonent tarmoq qamrovidan tashqarida bo‘lgandagina yetib bormaydi. To‘lov kelishilgan kunda tushmasa, mijozlarga haftasiga 1–2 marta qo‘ng‘iroq qilinadi; bir necha marta qo‘ng‘iroq qilingandan keyin masala direktorga uzatiladi.
- [UI kuzatuvi va javob orasidagi ochiq farq] Uysot’dagi `Сообщение о задолженности` SMS sozlamasi o‘chiq ko‘rindi; Venera esa SMSlar odatda yetib borishini aytdi. Xabarlar qaysi sozlamadan/tizimdan yuborilishi tasdiqlanmagan.

## 2026-09-30 — Javob kutayotgan savollar

### 3. Подтверждение оплаты

В разделе [«Платежи» Uysot](https://app.uysot.uz/main/payment) я вижу внесённые платежи, но не нашёл прикреплённых чеков или банковских выписок.

**По какому документу или источнику я могу проверить, что деньги действительно поступили? Где хранятся подтверждающие документы?**

*Для агента:* чтобы агент сверял платёж с надёжным подтверждением, а не считал запись в Uysot достаточным доказательством поступления денег.

### 5. Записи о звонках

В [CRM Uysot](https://app.uysot.uz/main/crm) я увидел возможность оставлять примечания и ставить задачи.

**Могу ли я посмотреть там результат разговора с клиентом и дату следующего звонка или эти данные ведутся в другом месте?**

*Для агента:* чтобы агент знал историю общения и мог подсказать, кому и когда нужно позвонить.

### 6. Исправления и возвраты

Я посмотрел разделы [«Изменения»](https://app.uysot.uz/main/changes) и [«Договоры»](https://app.uysot.uz/main/contract).

**Кто исправляет ошибочную запись об оплате или отменяет договор? Чьё подтверждение для этого нужно? Где фиксируется возврат денег?**

*Для агента:* чтобы агент знал, кому передавать такие случаи, мог проследить историю изменений и не менял финансовые данные без нужного подтверждения.

### 7. Приоритет для ИИ

**Какие две задачи в вашей работе занимают больше всего времени или чаще приводят к ошибкам? С какой задачи мне лучше начать автоматизацию с помощью ИИ?**

*Для агента:* чтобы начать автоматизацию с самой полезной для Sales задачи.

## Eslatma

- [x] 2026-10-02: Emirhan Veneraning javoblarini yubordi; 3, 5 va 6-savollarga taqsimlandi. Qolgan aniqliklar va javobsiz 7-savol quyidagi bo‘limda.
- Bu Obsidian’dagi vazifa qaydi; alohida bildirishnoma yoki kalendar eslatmasi yaratilmagan.

## 2026-10-02 — Venera javoblari: 3, 5 va 6-savollar

Manba: Emirhan ushbu suhbatda Veneraning javobini yubordi. Quyidagilar suhbatdosh ma’lumoti; bank hujjatlari yoki Uysot audit yozuvlari bu bosqichda mustaqil tekshirilmagan.

### 3. To‘lovni tasdiqlash — qisman javob olindi

- [Venera javobi, Emirhan yubordi] Cheklar Uysot’ga yuklanmaydi. Mijozlar turli banklar va bank ilovalari orqali to‘laydi; Venera bank ko‘chirmalari asosida to‘lov ma’lumotini Uysot’ga kiritadi.
- [Venera javobi, Emirhan yubordi] Kompaniyaning hisob-kitob hisobvarag‘i bo‘yicha bank ko‘chirmasi pulning haqiqatda tushganini tasdiqlovchi manbadir.
- [ochiq] Ko‘chirmalar qayerda saqlanishi, ularni olish tartibi va agent uchun ruxsatlangan format/kirish aniqlanmagan.
- [xulosa: agent talabi] Uysot yozuvi va bank ko‘chirmasi bilan solishtirilgan to‘lov holati alohida ko‘rsatilishi kerak; bank manbasi bo‘lmasa mustaqil bank tasdig‘i bor deb aytilmaydi.

### 5. CRM va qo‘ng‘iroqlar qaydi — savdo ofisidan aniqlanadi

- [Venera javobi, Emirhan yubordi] CRM masalasini savdo ofisida aniqlashtirish kerak: mijozlar bilan asosan ular ishlaydi.
- [ochiq] Suhbat natijasi va keyingi qo‘ng‘iroq sanasi qayerda yuritilishi hali javobsiz. Ushbu savol savdo ofisiga yo‘naltiriladi; CRM’da to‘liq tarix bor deb qabul qilinmaydi.
- [aniqlashtirish] Oldingi «Sales’da faqat Venera ishlaydi» qaydi bilan mijozlar bilan ishlaydigan savdo ofisining roli farqi ochiq; yangi javobdan xodimlar soni chiqarilmaydi.

### 6. O‘zgartirishlar, mas’ul va audit — qisman javob olindi

- [Venera javobi, Emirhan yubordi] Har bir mijoz anketasida uning shartnomasiga oid ma’lumotlar ko‘rinadi. O‘zgarishlar, to‘lov qo‘shish yoki o‘chirish tizimda sana va amalni bajargan shaxs bilan qayd etiladi.
- [Venera javobi, Emirhan yubordi] Excel konstruktor orqali ham jadval tuzish mumkin, ammo undagi hisobotda ma’lumot kamroq bo‘ladi.
- [Venera javobi, Emirhan yubordi] Shartnomalar bilan bog‘liq barcha amallar, ma’lumot kiritish va tuzatishlarni Venera bajaradi.
- [ochiq] Alohida kimning tasdig‘i kerakligi, shartnomani bekor qilish tartibi va qaytarilgan pul (refund) qayerda qayd qilinishi aniq bayon qilinmagan.
- [xulosa: agent talabi] Audit uchun mijoz/shartnoma kartasidagi tarixni tekshirish kerak; Excel eksporti barcha audit maydonlarini qamraydi deb hisoblanmaydi. Veneraning amaliy roli agentga yozish vakolati bermaydi.

### 7. AI ustuvorligi — javob olinmagan

- [ochiq] Eng ko‘p vaqt oladigan yoki xato keltiradigan ikki vazifa va birinchi avtomatlashtirish vazifasi ushbu javobda ko‘rsatilmagan.

Qolgan aniqliklar: bank ko‘chirmasi saqlash/kirish tartibi; savdo ofisining CRM qaydlari; tuzatish/bekor qilish tasdig‘i va refund qaydi; AI ustuvorligi. SMS yuborish manbasi bo‘yicha oldingi ochiq farq ham saqlanadi.

## 2026-10-03 — Javoblardan kelib chiqqan savollar

[taklif: aniqlashtirish savollari] Bank ko‘chirmasi saqlanishi va solishtirish, cheklarning Uysot tashqarisida saqlanishi, CRM/ofis rollari, tuzatish tasdig‘i, refund va audit tafsilotlari hamda AI ustuvorligi uchun 10 savol tayyorlandi.

Venera javobidan keyingi aniqlashtirish savollari. Quyidagi ruscha matn Venera va savdo ofisi uchun draft; boshqa chatlarga yuborilmasin.

Спасибо за ответы. Остались следующие уточнения.

3. Подтверждение оплаты
1) Где хранятся банковские выписки и как можно получить их для сверки с Uysot: файл, банковский кабинет или другой источник?
2) Как вы связываете поступление в выписке с конкретным клиентом и договором в Uysot? Что делаете, если платит другой человек или назначение платежа непонятно?
3) Как обнаруживаете и разбираете случаи, когда деньги уже поступили, но запись ещё не внесена в Uysot, либо сумма или дата не совпадают?
4) Если клиент присылает чек, сохраняется ли он где-либо вне Uysot или после проверки по выписке не хранится?

5. CRM — вопросы для офиса продаж
5) Где фиксируете результат разговора, обещанную дату оплаты и дату следующего звонка? Кто обновляет эти записи?
6) Как распределены обязанности между офисом продаж и Венерой: кто работает с обращениями и звонками, а кто ведёт договоры и оплаты?

6. Изменения и возвраты
7) Для исправления или удаления оплаты и отмены договора нужно ли чьё-либо согласование? Если да, чьё и где фиксируется подтверждение?
8) Где отражается фактический возврат денег клиенту и как он связан с договором и банковской операцией?
9) В каком разделе карточки клиента можно посмотреть историю изменений? Сохраняются ли прежнее и новое значения, причина изменения, дата и исполнитель, включая удалённые оплаты?

7. Приоритет для ИИ
10) Какие две задачи занимают больше всего времени или чаще приводят к ошибкам? С какой задачи лучше начать помощь ИИ? По возможности приведите один недавний пример.

Эти вопросы не означают, что документы потеряны: место хранения и порядок сверки пока не уточнены.

[tekshirildi: Telegram MCP] Emirhan so‘roviga ko‘ra savollar @BelugaCat_Asisstent_bot (BelugaCat Assistent for Emirhan) botiga yuborildi; send_message muvaffaqiyat tasdig‘ini qaytardi. Venera yoki savdo ofisiga yuborilgani yo‘q.

## 2026-10-04 — CRM amaliyoti bo‘yicha foydalanuvchi tuzatishi

- [foydalanuvchi aniqlashtirdi: shu sessiya] CRM izohlariga suhbat natijalarini yozishmaydi. Bu haqda qayta savol berilmaydi.
- [ochiq] Qayta qo‘ng‘iroq va mijoz va’da qilgan to‘lov sanasi qayerda yuritilishi aniqlanmagan. Ma’lumot mavjud bo‘lsa havola so‘ralgan ruscha draft tayyorlandi; Veneraga yuborilgani tasdiqlanmagan.

## 2026-10-04 — Va’da sanasi Excel jadvalida yuritilishi

- [Venera javobi, Emirhan yubordi] Shartnomadagi oylik to‘lov sanasi Uysot’da nazorat uchun ishlatiladi. To‘lov tushmasa mas’ul xodim qo‘ng‘iroq qiladi. Mijoz aytgan yangi to‘lov sanasi keyingi nazorat uchun Excel jadvaliga yoziladi.
- [ochiq] Excel jadvali Uysot ichidagi konstruktor, yuklab olingan fayl yoki tashqi jadval ekanligi aytilmagan. Jadval manzili, shartnoma kaliti va kirish formati ochiq. Va’da sanasi shartnoma sanasini rasman o‘zgartirishi tasdiqlanmagan.
- [tekshirish urinish: 2026-10-04] Computer Use inventory’da browser tablari yo‘q; native Google Chrome access «Computer Use was not approved» bilan rad etildi. Jonli Uysot sahifalari tekshirilmadi. Lokal route katalogidagi Excel eksport yo‘llari va oldingi Excel konstruktor UI kuzatuvi aynan shu jadval joylashuvini isbotlamaydi.
