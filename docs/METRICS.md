# Метрики Tech Radar (KSTV)

Мета радара — не «гарна картинка», а **керований tech portfolio**. Метрики показують, чи процес працює.

Детально по delivery: **[DORA.md](./DORA.md)**.  
Архітектурні guardrails: **[ARCHUNIT.md](./ARCHUNIT.md)**.

## 1. Процесні (легко зібрати)

| Метрика | Як рахувати | Ціль (старт) |
|---------|-------------|--------------|
| Кількість entries по кільцях | `config.json` | HOLD не росте без proposals |
| Ring movements / квартал | diff `moved` між релізами | ≥ 3 осмислених зміни |
| Open Change Proposals | JQL `labels = tech-radar AND statusCategory != Done` | < 10, SLA review ≤ 2 тижні |
| Час від proposal → update config | Jira created → PR merge | ≤ 14 днів |
| % entries з `link` | config | ≥ 80% |

## 2. Adoption

| Метрика | Джерело |
|---------|---------|
| Нові сервіси на ADOPT-стеку vs HOLD | CF / deploy pipeline / org VidMind |
| Частка PR, що чіпають HOLD-залежності | code search / **ArchUnit fail rate** |
| Trial → Adopt conversion | історія radar volumes |
| Інциденти, пов’язані з HOLD-технологіями | PagerDuty / Jira |

## 3. Delivery — DORA (шар поверх process)

| Метрика | Сенс для радара |
|---------|------------------|
| **Deployment Frequency** | Чи дає мікросервісна міграція частіші незалежні релізи |
| **Lead Time for Changes** | Чи HOLD-інфра (Jenkins, AMI bootstrap) гальмує path to prod |
| **Change Failure Rate** | Чи ADOPT-практики (тести, ArchUnit) зменшують поломки |
| **Recovery time** | Операційна зрілість після failed deploy |

Мінімум: щомісяця DF + lead time по 3–5 сервісах (див. [DORA.md](./DORA.md)).

## 4. Бізнес / roadmap

- Time-to-market фіч у bounded contexts після M1/M2
- Незалежні релізи мікросервісів vs monolith train
- Зменшення блокувань через спільний пул ресурсів WF

## 5. Ритуал

1. **Щокварталу** — re-score radar + огляд DORA-трендів (eng leads + principals).
2. **Щомісяця** — digest open proposals + HOLD без owner + DF snapshot.
3. **Після major migration epic** — оновити кільця (Scala, session, Security Server, K8s).

## 6. Анти-метрики

- Entries «для галочки» без link і owner
- HOLD без плану виходу роками
- Adopt без production usage
- DORA лише org-wide average (ховає прогрес нових сервісів)
