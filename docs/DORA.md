# DORA metrics для KSTV / VidMind

DORA (DevOps Research and Assessment) — стандарт вимірювання **software delivery performance**.  
Для Tech Radar це **delivery-шар**: чи ADOPT-стек і мікросервісна міграція реально прискорюють поставку.

Офіційний гід: [dora.dev/guides/dora-metrics](https://dora.dev/guides/dora-metrics/)

## Чотири ключові метрики

| # | Метрика | Питання | Elite (орієнтир) |
|---|---------|---------|------------------|
| 1 | **Deployment Frequency (DF)** | Як часто успішний deploy у production? | кілька разів на день |
| 2 | **Lead Time for Changes** | Скільки від commit (або merge) до prod? | < 1 дня |
| 3 | **Change Failure Rate (CFR)** | % deploy, після яких потрібен hotfix / rollback? | 0–15% |
| 4 | **Failed Deployment Recovery Time** | Скільки до відновлення сервісу після failed deploy? | < 1 год |

> У новіших звітах DORA акцент на *Failed Deployment Recovery Time* замість класичного MTTR інцидентів; на практиці обидва корисні.

### Рівні performance (спрощено)

| Рівень | DF | Lead time | CFR | Recovery |
|--------|-----|-----------|-----|----------|
| Elite | ≥ 1/день | < 1 день | ≤ 15% | < 1 год |
| High | 1/тиждень–1/день | 1 день–1 тиждень | ≤ 30% | < 1 день |
| Medium | 1/місяць–1/тиждень | 1 тиждень–1 місяць | ≤ 45% | < 1 тиждень |
| Low | рідше | > 1 місяць | > 45% | > 1 тиждень |

## Як міряти в нашому стеку

| Метрика | Джерела даних |
|---------|----------------|
| **DF** | Успішні prod deploy: GitHub Actions, Jenkins, Spotinst/CF events; рахувати per-service |
| **Lead time** | `merged_at` PR → timestamp prod deploy (SHA mapping) |
| **CFR** | Deploy + інцидент у вікні N годин (PagerDuty / Jira / ops channel) |
| **Recovery** | Incident open → resolved (моніторинг / PD) |

### Мінімальний старт (без ідеальної автоматизації)

1. Обрати 3–5 сервісів: `wildfire` (або gwildfire path), `playback-sessions`, `authorization-server`, один зі StarAds (`ads-kstv-*`), один rec (`hyperion` / rankmate).
2. Раз на місяць: кількість prod-релізів, медіана lead time (merge→prod), кількість hotfix після релізу.
3. Записати в Confluence / spreadsheet → тренд.

## Зв’язок з Tech Radar і міграцією

| Ініціатива | Очікуваний вплив на DORA |
|------------|---------------------------|
| Microservices M1–M2 | ↑ DF, ↓ lead time у bounded contexts |
| ArchUnit + tests у нових сервісах | ↓ CFR |
| Вихід з HOLD (AMI bootstrap, Jenkins-only, shared session) | ↓ lead time, ↑ DF |
| K8s / незалежні релізи | ↑ DF per service |
| Monolith-first (HOLD) | тримає DF низьким, lead time високим |

Radar **process metrics** (proposals, ring moves) показують *керованість портфеля*.  
DORA показує *чи портфель дає delivery outcome*.

## Анти-патерни

- Оптимізувати лише DF (часті крихкі релізи → CFR росте)
- Lead time «від першого коміту в feature-гілці» без merge (розмиває метрику)
- Одна цифра на всю org без розбиття по сервісах (моноліт маскує мікросервіси)

## Наступні кроки

1. Додати DF + lead time у квартальний radar review (`docs/METRICS.md`).
2. Для сервісів з ArchUnit fitness — відстежувати CFR окремо (гіпотеза: нижчий).
3. Після M2 Security Server / account services — порівняти DORA «до/після» винесення з моноліту.
