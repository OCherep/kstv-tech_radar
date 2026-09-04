# Метрики Tech Radar (KSTV)

Мета радара — не «гарна картинка», а **керований tech portfolio**. Метрики показують, чи процес працює.

## 1. Процесні (легко зібрати)

| Метрика | Як рахувати | Ціль (старт) |
|---------|-------------|--------------|
| Кількість entries по кільцях | `config.json` | HOLD не росте без proposals |
| Ring movements / квартал | diff `moved` між релізами | ≥ 3 осмислених зміни |
| Open Change Proposals | JQL `labels = tech-radar AND statusCategory != Done` | < 10, SLA review ≤ 2 тижні |
| Час від proposal → update config | Jira created → PR merge | ≤ 14 днів |
| % entries з `link` | config | ≥ 80% |

## 2. Adoption (складніше, цінніше)

| Метрика | Джерело |
|---------|---------|
| Нові сервіси на ADOPT-стеку vs HOLD | CF / deploy pipeline |
| Частка PR, що чіпають HOLD-залежності | code search / ArchUnit fail rate |
| Trial → Adopt conversion | історія radar volumes |
| Інциденти, пов’язані з HOLD-технологіями | PagerDuty / Jira |

## 3. Бізнес / delivery (зв’язок з roadmap)

- Time-to-market фіч у bounded contexts після M1/M2
- Незалежні релізи мікросервісів (Deployment Frequency, DORA)
- Зменшення «блокувань» через спільний моноліт ( qualitatively + lead time)

## 4. Ритуал

1. **Щокварталу** — re-score radar (eng leads + principals).
2. **Щомісяця** — digest open proposals + HOLD без owner.
3. **Після кожного major migration epic** — оновити кільця (Scala, session, Security Server).

## 5. Анти-метрики

- Кількість entries «для галочки» без link і owner
- HOLD, який ніхто не чіпає роками (мертвий борг)
- Adopt без production usage culture
