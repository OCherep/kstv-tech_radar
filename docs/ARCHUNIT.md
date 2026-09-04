# ArchUnit для KSTV / Wildfire

[ArchUnit](https://www.archunit.org/) — бібліотека unit-тестів архітектури Java (bytecode analysis).

## Навіщо нам

Під час міграції Monolith → Microservices і Scala→Java:
- не допускати залежностей «вниз угору» (controller ← service ← repository);
- заборонити новим модулям тягнути HOLD-залежності (наприклад, прямий доступ до legacy session manager);
- фіксувати bounded contexts (slices без циклів);
- підкріпити ADR (ADR-000…004 по STB-WS) автоматичними перевірками.

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
@AnalyzeClasses(packages = "com.vidmind", importOptions = ImportOption.DoNotIncludeTests.class)
class ArchitectureTest {

  @ArchTest
  static final ArchRule no_cycles = slices()
      .matching("com.vidmind.(*)..")
      .should().beFreeOfCycles();

  @ArchTest
  static final ArchRule layered = layeredArchitecture().consideringAllDependencies()
      .layer("API").definedBy("..api..", "..controller..", "..ws..")
      .layer("Service").definedBy("..service..")
      .layer("Persistence").definedBy("..dao..", "..repository..", "..mongo..")
      .whereLayer("API").mayNotBeAccessedByAnyLayer()
      .whereLayer("Service").mayOnlyBeAccessedByLayers("API")
      .whereLayer("Persistence").mayOnlyBeAccessedByLayers("Service");

  @ArchTest
  static final ArchRule no_scala_in_new_code = noClasses()
      .that().resideInAPackage("..microservice..")
      .should().dependOnClassesThat().resideInAPackage("scala..");
}
```

## Зв’язок з Tech Radar

| Radar ring | ArchUnit role |
|------------|---------------|
| **ADOPT** | Правила «тільки так» (дозволені шари/пакети) |
| **HOLD** | `noClasses().should().dependOnClassesThat()…` на заборонені ліби |
| **TRIAL** | М’які правила / окремий модуль з винятками |

Рекомендація: почати з PWF/STB-WS після ADR-003/004, потім перенести правила в starters для нових мікросервісів.
