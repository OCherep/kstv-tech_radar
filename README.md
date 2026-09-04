# KSTV Tech Radar

Технологічний радар платформи **Kyivstar TV / Vidmind (KSTV)**.

> **Part of [DevOps Hub](https://github.com/OCherep/devops-hub)** — єдина точка входу до OnCall, Radar та наступних інструментів.

Візуалізація поточного стану технологій, які ми використовуємо, пробуємо або свідомо уникаємо.

## Жива версія

Після увімкнення GitHub Pages (або іншого static hosting) радар буде доступний за адресою репозиторію.

Локально:

```bash
# будь-який static server
python3 -m http.server 8000
# відкрити http://localhost:8000
```

## Структура

| Файл | Призначення |
|------|-------------|
| `index.html` | Сторінка радара + пояснення |
| `config.json` | Список технологій (entries) + дата |
| `radar.css` | Стилі |
| `docs/` | ArchUnit, DORA, metrics, automation, proposals |

## Квадранти

1. **Languages & Frameworks** — Java, Kotlin, Swift, Angular, Go, ArchUnit…
2. **Infrastructure & Cloud** — AWS, CloudFormation, Spotinst, Nginx, K8s…
3. **Data & Storage** — MongoDB, Redis, Solr, NATS, EDA…
4. **Techniques, Streaming & Clients** — HLS/SSAI, session model, microservices, StarAds…

## Кільця

- **ADOPT** — рекомендуємо для нових робіт
- **TRIAL** — вже є успішний досвід, можна розширювати
- **ASSESS** — варто досліджувати / прототипувати
- **HOLD** — не беремо в нові проєкти (борг / застаріле)

## Як оновлювати

1. Редагувати `config.json` (додавати/рухати entries).
2. Поле `moved`: `0` = без змін, `1` = підняли, `-1` = опустили, `2` = нове.
3. Зробити PR / commit у гілку `grok-0.0.1` (або main).
4. Обговорити з eng-командами зміни кілець.

## Пов’язані проєкти

| Проєкт | Роль |
|--------|------|
| [DevOps Hub](https://github.com/OCherep/devops-hub) | Центральний портал |
| [OnCall System](https://github.com/OCherep/oncall-system) | Чергування / звернення / дейлі |

## Походження

- Ідея: ThoughtWorks Technology Radar
- Візуалізація: open-source [zalando/tech-radar](https://github.com/zalando/tech-radar) (MIT)

---

**v0.0.3** — ArchUnit ADOPT, DORA docs, VidMind platform services (вересень 2026).
