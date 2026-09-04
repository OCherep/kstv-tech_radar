# ArchUnit для KSTV / VidMind

[ArchUnit](https://www.archunit.org/) — unit-тести архітектури Java (bytecode). Версія в нових сервісах: **1.4.x** (`archunit-junit5`).

## Статус у Tech Radar

| Ring | Рішення |
|------|---------|
| **ADOPT** | Нові Java-мікросервіси (Spring Boot 3.x) — обов’язкові fitness functions |
| **TRIAL → стандарт у commons** | Shared rules у `kstv-backend-commons` / platform starter |
| Wildfire (legacy) | Поступове впровадження + `FreezingArchRule` на існуючі порушення |

## Уже в org VidMind

| Repo | Артефакт |
|------|-----------|
| [authorization-server](https://github.com/VidMind/authorization-server) | Service / Packaging / Controllers fitness |
| [playback-sessions](https://github.com/VidMind/playback-sessions) | Service / Controllers / Packaging |
| [lastlocation](https://github.com/VidMind/lastlocation) | Packaging / Controllers |
| [application-gateway](https://github.com/VidMind/application-gateway) | Packaging |
| [user-activity-gateway](https://github.com/VidMind/user-activity-gateway) | dependency у pom |
| [wildfire](https://github.com/VidMind/wildfire) `stb-ws` | `RestControllerArchitectureRules` (junit4, 1.2.0) |

Нові сервіси — **еталон**; wildfire — міграційний борг.

## Навіщо

- Шари API → Service → Persistence без «дірок»
- Bounded contexts (slices) без циклів
- Заборона HOLD-залежностей у новому коді (Scala, tomcat-redis-session-manager, …)
- Підкріплення ADR (STB-WS ADR-000…004, microservices roadmap)

## Швидкий старт (JUnit 5)

```xml
<dependency>
  <groupId>com.tngtech.archunit</groupId>
  <artifactId>archunit-junit5</artifactId>
  <version>1.4.2</version>
  <scope>test</scope>
</dependency>
```

```java
@AnalyzeClasses(
    packages = "tv.ks", // або com.vidmind
    importOptions = ImportOption.DoNotIncludeTests.class)
class ArchitectureTest {

  @ArchTest
  static final ArchRule no_cycles = slices()
      .matching("tv.ks.(*)..")
      .should().beFreeOfCycles();

  @ArchTest
  static final ArchRule layered = layeredArchitecture()
      .consideringOnlyDependenciesInLayers()
      .layer("API").definedBy("..api..", "..controller..", "..web..")
      .layer("Service").definedBy("..service..")
      .layer("Persistence").definedBy("..dao..", "..repository..", "..mongo..")
      .whereLayer("API").mayNotBeAccessedByAnyLayer()
      .whereLayer("Service").mayOnlyBeAccessedByLayers("API")
      .whereLayer("Persistence").mayOnlyBeAccessedByLayers("Service");

  @ArchTest
  static final ArchRule no_scala_in_new_services = noClasses()
      .that().resideInAPackage("tv.ks..")
      .and().resideOutsideOfPackage("..legacy..")
      .should().dependOnClassesThat().resideInAPackage("scala..");
}
```

### Freeze для legacy

```java
@ArchTest
static final ArchRule frozen_cycles = FreezingArchRule.freeze(
    slices().matching("com.vidmind.(*)..").should().beFreeOfCycles());
```

Нові порушення fail-ять build; старі — у freeze store до поступового виправлення.

## Зв’язок з Tech Radar

| Radar | ArchUnit |
|-------|----------|
| **ADOPT** | Жорсткі правила в CI |
| **HOLD** | `noClasses().should().dependOn…` |
| **TRIAL** | Правила в окремому модулі / з exclude |
| Метрика | ArchUnit fail rate на PR = leading indicator якості |

## План впровадження

1. **Зараз** — скопіювати fitness functions з `authorization-server` / `playback-sessions` у checklist нового сервісу.
2. **Commons** — винести common rules у `kstv-backend-commons` (або `platform-arch-tests` jar).
3. **Wildfire** — оновити до junit5 + freeze; розширити після Scala→Java.
4. **CI** — ArchUnit у required check для `tv.ks.*` сервісів.
