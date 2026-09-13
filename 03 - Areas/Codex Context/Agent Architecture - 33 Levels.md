---
type: architecture-guide
updated: 2026-09-14
status: active
---

# Agent arxitekturasi — 33 bosqich

Bu xarita AI agentni oddiy model chaqiruvidan boshqariladigan raqamli tashkilotgacha
rivojlantirish tushunchalarini beradi. Muhim tuzatish: 33 bandning barchasi har bir agent
uchun majburiy emas. Agentning darajasi komponentlar soni bilan emas, vazifani ishonchli,
xavfsiz, kuzatiladigan va o‘lchanadigan bajarishi bilan belgilanadi.

## 1–8: poydevor va agent runtime

| № | Tushuncha | Nima va nima uchun | Qachon kerak |
|---|---|---|---|
| 1 | TypeScript + Backend Systems | API, validation, DB, queue, test va deploy poydevori. TypeScript foydali, lekin shart emas — Python ham to‘g‘ri backend bo‘lishi mumkin. | JS/TS mahsulot qurilganda |
| 2 | LLM API | Modelning til va reasoning imkoniyatiga dasturiy kirish. Timeout, retry, limit va xarajat nazorati kerak. | Deterministik kod yetmaganda |
| 3 | Structured Output | Model javobini JSON Schema kabi contractga soladi. Parsingni ishonchli qiladi, ammo mazmun haqiqatligini kafolatlamaydi. | Javobni kod ishlatsa |
| 4 | Tool Calling | Model toolni va typed argumentlarni tanlaydi, host tekshirib bajaradi. Tool mavjudligi ruxsat degani emas. | Tashqi ma’lumot yoki action kerak bo‘lsa |
| 5 | Single Agent | Bitta model + instructions + context + tools + goal. Eng sodda va boshqariladigan boshlanish. | Deyarli har agentning bazasi |
| 6 | Agent Loop | Observe → decide → act → result → stop/continue. Turn, vaqt, token, cancellation va loop limiti bo‘ladi. | Ko‘p qadamli vazifalarda |
| 7 | Tool Engineering | Kichik, aniq, testlangan, idempotent va permissionli tool contractlari. Ko‘p hardcoded script yig‘ish emas. | Real integratsiya/invariantda |
| 8 | MCP | Agentni portable tool, resource va prompt serverlariga ulovchi standart. | Bir integratsiya bir nechta hostda kerak bo‘lsa |

## 9–16: state, bilim va xavfsizlik

| № | Tushuncha | Nima va nima uchun | Qachon kerak |
|---|---|---|---|
| 9 | State | Joriy ishning phase, recipient, natija va pending actionlari. | Multi-turn yoki resumable vazifada |
| 10 | Persistence | Restartdan keyin qoladigan session, job, checkpoint va delivery attempt. Atomic write, migration, backup va retention talab qiladi. | Ish yo‘qolmasligi kerak bo‘lsa |
| 11 | RAG | Kerakli source bo‘laklarini topib modelga kontekst beradi. Retrieval relevance va grounded answer alohida o‘lchanadi. | Katta/o‘zgaruvchan bilim bazasida |
| 12 | Memory | Tasdiqlangan preference, fakt, lesson va xulosalar. Provenance, correction, delete va approval bo‘lishi kerak. | Uzoq muddatli davomiylikda |
| 13 | Guardrails | Input/output/action scope, schema, secret, budget va approval tekshiruvlari. Xavfni kamaytiradi, nol qilmaydi. | Consequential actionlarda |
| 14 | Identity | User, agent, service va recipient kimligini ishonchli tasdiqlash. Matndagi “men ownerman” authority bermaydi. | Har qanday write/actionda |
| 15 | RBAC / ABAC | RBAC role orqali, ABAC subject/resource/action/environment atributlari orqali ruxsat beradi. Modeldan tashqarida enforce qilinadi. | Bir nechta rol yoki contextual scope’da |
| 16 | Policy Engine | Markaziy, versioned allow/deny/approval qarori va audit sababi. | Ko‘p tool/channel/tenant bo‘lsa |

## 17–24: production va murakkab orchestration

| № | Tushuncha | Nima va nima uchun | Qachon kerak |
|---|---|---|---|
| 17 | Single Agent Production | SLO, queue, retry, idempotency, cancellation, security, cost, incident va rollbackli real xizmat. | Multi-agentdan oldingi asosiy target |
| 18 | Multi-Agent | Alohida mas’uliyatli specialist agentlar. Koordinatsiya, latency va cost oshadi. | Eval single agent bottleneck ekanini ko‘rsatsa |
| 19 | A2A | Mustaqil agentlarning discovery va task almashish protokoli. MCP agent→tool, A2A agent→agent. | Turli framework/vendor agentlari bog‘lansa |
| 20 | Graph Orchestration | Node, edge, branch, join va checkpointli aniq workflow. | Takroriy conditional flow murakkab bo‘lsa |
| 21 | Temporal / Durable Execution | Uzoq workflow crash, kutish va retrydan keyin history/replay bilan davom etadi. | Soat/kun davom etuvchi muhim jarayonda |
| 22 | Event-Driven Architecture | Producer event chiqaradi, consumer async ishlaydi. Schema, dedup, ordering, DLQ va replay kerak. | Komponentlar mustaqil scale qilsa |
| 23 | Observability | Model/tool/policy/queue oqimiga bog‘langan traces, metrics va structured logs. | Production claimdan oldin |
| 24 | Evaluation | Task success, safety, grounding, tool choice, latency va cost dataset/metriclari. Unit test agent sifatini to‘liq o‘lchamaydi. | Har release va architecture qarorida |

## 25–28: agent platformasi / AIOS

| № | Tushuncha | Nima va nima uchun | Qachon kerak |
|---|---|---|---|
| 25 | Agent Registry | Agent owner, capability, endpoint, auth, policy, version va health katalogi. | Ko‘p mustaqil agentni boshqarishda |
| 26 | Tool Registry | Tool contract, owner, scope, risk, version va health katalogi. Registry access bermaydi — policy hal qiladi. | Ko‘p tool va permission drift bo‘lsa |
| 27 | AIOS Control Plane | Registry, identity, policy, scheduling, budget, rollout va auditni boshqaradi. | Haqiqiy platform scale’da |
| 28 | AIOS Data Plane | Agent turn, RAG va toollar bajariladigan, izolatsiya va quota qo‘llanadigan runtime. | Multi-tenant/ko‘p workload bo‘lsa |

## 29–33: raqamli tashkilot

| № | Tushuncha | Nima va nima uchun | Qachon kerak |
|---|---|---|---|
| 29 | AI Employee | Chegaralangan vazifa, tool, KPI, escalation va javobgar human ownerga ega AI rol. Unlimited autonomy emas. | Bitta agent real ish rolini bajarsa |
| 30 | AI Department | Bir business function uchun bir nechta ishonchli AI rollar va handofflar. | Individual rollar allaqachon o‘lchangan bo‘lsa |
| 31 | AI Management | Priority, assignment, review, cost/capacity, incident va human escalation boshqaruvi. | Ko‘p AI worker ishlaganda |
| 32 | Digital Organization | Human va AI rollarni process, data, governance va KPI bilan birlashtirgan tashkilot dizayni. | Kompaniya darajasida transformatsiyada |
| 33 | Self-Improving Organization | Outcome → proposal → isolated eval → approval → versioned rollout → monitor → rollback. | Kuchli eval/governance tayyor bo‘lsa |

Self-improvement hech qachon production kod, identity, policy, permission yoki memory’ni
yashirin o‘zgartirish degani emas.

## Darajani qanday baholaymiz

- **1–8:** ishlaydigan prototype.
- **9–16:** boshqariladigan va xavfsiz agent poydevori.
- **17 + 23–24:** kuchli production single agent.
- **18–28:** ehtiyoj bo‘lsa platform scale; avtomatik ravishda aqlliroq degani emas.
- **29–33:** business va governance yetukligi; model IQ darajasi emas.

## Beluga/Hermes uchun hozirgi xulosa

| Qatlam | Holat | Izoh |
|---|---|---|
| 1–8 | Bor | Hermes model, structured JSON, agent loop, host tools va MCP mavjud |
| 9–12 | Bor/partial | SQLite state, session, MyBrain RAG va controlled lesson/memory mavjud |
| 13–16 | Partial | Host validation va recipient/channel qoidalari bor; formal identity/RBAC/ABAC policy service to‘liq emas |
| 17 | Partial | LaunchAgent, queue, dedup, restart va testlar bor; SLO/live acceptance to‘liq emas |
| 18–22 | Hozir kerak emas | Single-agent muammosi eval bilan isbotlanmasdan qo‘shilmaydi |
| 23 | Partial | Status/log/job metadata bor; end-to-end trace va SLO telemetry kuchsiz |
| 24 | Partial | Unit/integration test bor; quality/safety/latency/cost scenario evallarini kuchaytirish kerak |
| 25–28 | Hozir kerak emas | Single-owner/single-machine dizayn uchun ortiqcha |
| 29 | Maqsad | Emirhan uchun chegaralangan, javobgar Telegram AI employee |
| 30–33 | Keyin | Real business rollar va KPI paydo bo‘lgandan so‘ng |

[xulosa] Beluga uchun yaqin target “33/33” emas. To‘g‘ri target: kuchli **Level 17**,
tanlangan 9–16 security/state qatlamlari va yaxshi **Level 23–24 observability/evaluation**.
Shu holatning o‘zi yuqori darajadagi shaxsiy agent bo‘la oladi.

## Keyingi qurilish tartibi

1. Level 17: state transition, permission negative tests, recoverable job, privacy/retention,
   error explanation va rollbackni mustahkamlash.
2. Level 24: tabiiy intent, recipient safety, tool choice, RAG grounding, failure recovery,
   latency va cost bo‘yicha versioned eval suite.
3. Level 23: Telegram update’dan final deliverygacha bitta correlation ID, redacted structured
   logs va oddiy SLOlar.
4. Multi-agent yoki durable workflow faqat takroriy muammo va evaldagi aniq foydadan keyin.
5. Learning: candidate → dalil/test yoki Emirhan tasdig‘i → versioned lesson/skill → monitoring
   → correction/delete. Permission learning orqali kengaymaydi.

## Rasmiy tayanch manbalar

- [OpenAI API — Evals va structured model contracts](https://platform.openai.com/docs/api-reference/evals)
- [Model Context Protocol specification](https://modelcontextprotocol.io/specification/2025-11-25)
- [A2A Protocol specification](https://a2a-protocol.org/v0.3.0/specification/)
- [OpenTelemetry signals](https://opentelemetry.io/docs/concepts/signals/)
- [NIST SP 800-162 — ABAC](https://csrc.nist.gov/pubs/sp/800/162/upd2/final)
- [Kubernetes control-plane architecture analogy](https://kubernetes.io/docs/concepts/architecture/)

## Bog‘lanishlar

- [[Beluga Agent Report]]
- [[Beluga Plan]]
- [[Hermes Setup]]
- [[Operating System]]
- [[../../ZONES/AI-Agents/_context|AI Agents zone]]

