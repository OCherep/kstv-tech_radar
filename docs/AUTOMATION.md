# Automation: Jira + GitHub для Tech Radar

## A. Jira Automation (UI: Project settings → Automation)

### Rule 1 — New proposal
- **When:** Issue created
- **If:** labels contain `tech-radar-proposal` OR summary contains `[Tech Radar]`
- **Then:**
  1. Add label `tech-radar`
  2. Comment з посиланням на процес (див. RING_CHANGE_PROPOSAL.md)

### Rule 2 — Done → нагадування оновити radar
- **When:** Issue transitioned to Done
- **If:** label = `tech-radar`
- **Then:** Comment:
  > Оновіть config.json у https://github.com/OCherep/kstv-tech_radar і додайте link на PR.

### Rule 3 — Weekly digest
- **When:** Scheduled (Mon 09:00 Europe/Kyiv)
- **Then:** Lookup issues JQL `labels = tech-radar AND statusCategory != Done`
- Send email/Slack summary

### Rule 4 — Incoming webhook (GitHub PR merged)
1. Create rule with **Incoming webhook** trigger → copy URL
2. GitHub repo → Settings → Webhooks → PR events → payload URL = Jira webhook
3. Action: if PR body/title contains `VID-XXXX` → comment on that issue

## B. GitHub Action (синхронізація / валідація)

Файл `.github/workflows/radar-validate.yml` (приклад):

```yaml
name: radar-validate
on:
  pull_request:
    paths: ['config.json']
  push:
    branches: [main]
    paths: ['config.json']

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Validate config.json
        run: |
          python3 - <<'PY'
          import json, sys
          data = json.load(open("config.json"))
          assert "entries" in data and "date" in data
          for e in data["entries"]:
              assert 0 <= e["quadrant"] <= 3
              assert 0 <= e["ring"] <= 3
              assert "label" in e
          labels = [e["label"] for e in data["entries"]]
          assert len(labels) == len(set(labels)), "duplicate labels"
          print(f"OK: {len(data['entries'])} entries, date={data['date']}")
          PY
```

Опційно: action, який раз на тиждень через Jira API збирає open `tech-radar` issues і відкриває issue/discussion, якщо config застарів.
