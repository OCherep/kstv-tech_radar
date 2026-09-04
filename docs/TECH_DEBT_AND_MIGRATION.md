# Tech-debt / migration тікети (зріз Jira, вересень 2026)

Проєкт: **VID** · cloud: `vidmind-dev.atlassian.net`

## Активні / релевантні для Tech Radar

### Scala → Java (PWF) — HOLD → вихід з HOLD
| Key | Summary | Status |
|-----|---------|--------|
| [VID-41206](https://vidmind-dev.atlassian.net/browse/VID-41206) | Migrate Entities module Scala→Java Step 1 | Open |
| [VID-41216](https://vidmind-dev.atlassian.net/browse/VID-41216) | Migrate Series/Episode/Session entities | Code Review |
| [VID-41221](https://vidmind-dev.atlassian.net/browse/VID-41221) | Migrate strugglers Scala→Java | WIP |
| [VID-41667](https://vidmind-dev.atlassian.net/browse/VID-41667) … [VID-41669](https://vidmind-dev.atlassian.net/browse/VID-41669) | GalleryItem, MongoProperties, enums | Open |
| [VID-41351](https://vidmind-dev.atlassian.net/browse/VID-41351)–[VID-41358](https://vidmind-dev.atlassian.net/browse/VID-41358) | commons, salesforce, session layer | Open |
| [VID-41243](https://vidmind-dev.atlassian.net/browse/VID-41243) | Delete useless Scala code Step 0 | Accepted |

### Session / SSO / Auth
| Key | Summary |
|-----|---------|
| [VID-41320](https://vidmind-dev.atlassian.net/browse/VID-41320) | [KIP] Kyivstar TV session |
| [VID-41317](https://vidmind-dev.atlassian.net/browse/VID-41317) | [KIP] Callback + token exchange |
| [VID-40933](https://vidmind-dev.atlassian.net/browse/VID-40933) | authorization server shared session issue |
| [VID-40935](https://vidmind-dev.atlassian.net/browse/VID-40935) | Payment Session deserialization failure |
| [VID-37528](https://vidmind-dev.atlassian.net/browse/VID-37528) | [KIP] NFR/SLO for KID integration |

### Infra / DevOps debt
| Key | Summary |
|-----|---------|
| [VID-40879](https://vidmind-dev.atlassian.net/browse/VID-40879) | Cut and move Jenkins to separate instance |
| [VID-40031](https://vidmind-dev.atlassian.net/browse/VID-40031) | CloudFront endpoint caching |
| [VID-12766](https://vidmind-dev.atlassian.net/browse/VID-12766) | Migrate to NAT gateway |

### Client tech cleanup
| Key | Summary |
|-----|---------|
| [VID-41410](https://vidmind-dev.atlassian.net/browse/VID-41410) | Cleanup after Compose migration |
| [VID-41436](https://vidmind-dev.atlassian.net/browse/VID-41436) | FilterSharedLocalStore dead API |
| [VID-41484](https://vidmind-dev.atlassian.net/browse/VID-41484) | Remove Compose suffix |

### Confluence
- [Monolith to Microservices 2026](https://vidmind-dev.atlassian.net/wiki/spaces/KB/pages/3853090821)
- [Tech improvements 2025](https://vidmind-dev.atlassian.net/wiki/spaces/KB/pages/3026976779) · epic VID-27755
- [Sessions flow rework](https://vidmind-dev.atlassian.net/wiki/spaces/KB/pages/2538897427)
- [Prioritized Debt List](https://vidmind-dev.atlassian.net/wiki/spaces/~7120205cb0afe4120c424b91d0a13f812cd5c6/pages/4285628423)
- [ADR hub](https://vidmind-dev.atlassian.net/wiki/spaces/KB/pages/3469410306/ADR)

### JQL для пошуку далі
```
project = VID AND (summary ~ "Scala" OR summary ~ "migration" OR summary ~ "refactor" OR summary ~ "legacy" OR summary ~ "session" OR labels in (tech-debt, TECH))
ORDER BY updated DESC
```

> Label `tech-debt` майже не використовується — варто запровадити разом з `tech-radar`.
