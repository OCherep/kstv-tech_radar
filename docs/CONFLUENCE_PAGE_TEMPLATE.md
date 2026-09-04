# Шаблон Confluence-сторінки: KSTV Tech Radar

Скопіюй у KB (або VID) як нову сторінку.

---

## KSTV Tech Radar

**Status:** Draft / Active  
**Owner:** Principal Engineers / Tech Leads  
**Repo:** https://github.com/OCherep/kstv-tech_radar  
**Live:** _(GitHub Pages URL після увімкнення)_

### Що це
Візуалізація технологічних рішень платформи (ADOPT / TRIAL / ASSESS / HOLD).  
Базується на ThoughtWorks + Zalando visualization.

### Поточний volume
- Date: 2026.09
- Branch/PR: https://github.com/OCherep/kstv-tech_radar/pull/1

### Як змінити кільце
1. Створи Jira issue за шаблоном [Ring Change Proposal](https://github.com/OCherep/kstv-tech_radar/blob/grok-0.0.1/docs/RING_CHANGE_PROPOSAL.md)
2. Labels: `tech-radar`, `tech-radar-proposal`
3. Після approve — PR у `config.json`

### Корисні посилання
- [Monolith to Microservices 2026](https://vidmind-dev.atlassian.net/wiki/spaces/KB/pages/3853090821)
- [Tech improvements 2025](https://vidmind-dev.atlassian.net/wiki/spaces/KB/pages/3026976779)
- [ADR hub](https://vidmind-dev.atlassian.net/wiki/spaces/KB/pages/3469410306/ADR)
- [Tech-debt map (repo)](https://github.com/OCherep/kstv-tech_radar/blob/grok-0.0.1/docs/TECH_DEBT_AND_MIGRATION.md)
- JQL: `labels = tech-radar ORDER BY updated DESC`

### Макрос / embed
```
// після GitHub Pages:
<iframe src="https://ocherep.github.io/kstv-tech_radar/" width="100%" height="900"></iframe>
```
або просто smart link на repo.

### Ритуал оновлення
| Коли | Хто | Що |
|------|-----|-----|
| Щокварталу | Principals | Full re-score |
| По demand | Будь-хто | Change Proposal |
| Після epic Done | Assignee epic | Оновити пов’язані entries |
