# Ring Change Proposal — шаблон Jira issue

**Issue Type:** Task (або Story)  
**Labels:** `tech-radar`, `tech-radar-proposal`  
**Component (опційно):** Tech Radar

## Summary (приклад)
```
[Tech Radar] Move «Kubernetes / EKS» from ASSESS → TRIAL
```

## Description (скопіюй у Jira)

### 1. Технологія
- **Назва:** …
- **Поточне кільце:** ADOPT | TRIAL | ASSESS | HOLD
- **Запропоноване кільце:** …
- **Квадрант:** Languages & Frameworks | Infrastructure & Cloud | Data & Storage | Techniques, Streaming & Clients

### 2. Обґрунтування
- Чому зараз?
- Який досвід уже є (команди, середовища, прод)?
- Ризики / обмеження
- Альтернативи, які розглядали

### 3. Докази
- Посилання на ADR / Confluence
- Посилання на Jira (trial, spike, migration epic)
- Метрики / інциденти (якщо є)

### 4. План після зміни кільця
- [ ] Оновити `config.json` у [kstv-tech_radar](https://github.com/OCherep/kstv-tech_radar) (`moved`: 1 або -1)
- [ ] PR + review
- [ ] Коментар у цьому issue з посиланням на commit/PR

### 5. Рішення
- **Approve / Reject / Defer** — після eng discussion
- Дата рішення: …
- Хто: …

---

**JQL filter для proposals:**
```
labels = tech-radar AND statusCategory != Done ORDER BY updated DESC
```
