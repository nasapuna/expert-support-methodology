# Built Asset Design Principles Framework

> Доменный слой над FPF для управления разработкой проектных решений ОКС: от исходных данных и сценариев использования к концепциям, архитектурным вопросам, проектным решениям, доказательствам и проектной документации.

- **Framework family:** Domain Principle Framework
- **Package edition ref:** `BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4`
- **Public pattern prefix:** `BDPF.*`
- **Legacy aliases:** `DPF.1..DPF.11` в период draft migration
- **Статус:** draft v0.4-package-structure
- **Дата:** 2026-07-02
- **Контекст применения:** экспертное сопровождение проектирования зданий и сооружений
- **FPF-основание:** FPF Core Conceptual Specification, версия June 2026; ID сверены через FPF MCP и audit-рекомендации `work/00_inbox/DPF-building-design-FPF-DPF-audit-and-edit-recommendations.md`
- **Package adequacy status:** `locallyUsableWithVisibleLimits` / `pilot-ready for one bounded P2S decision scenario`; не `stable`
- **Основной рабочий вопрос:** как сделать ход разработки проектного решения явным, проверяемым и улучшаемым, а не сводить проектирование к выпуску разделов ПД.

---

## Table of Contents

1. Readme - First Practical Entries
2. Preface - Cross-Cutting Ideas And Principles
3. Package Carrier Structure-Account Note
4. Package Boundary And Owner Routing
5. Pattern Index
6. Pattern bodies `BDPF.1..BDPF.11`
7. Repository package guard
8. Pilot, checklists, maturity and lexicon
9. Name And Edition Route
10. DPF Relation Records
11. Source Use And Refresh Map
12. Acceptance Cases
13. Refresh Route
14. Package Quality Result

## Readme - First Practical Entries

Use this package when a project team needs to make the development of a built-asset design decision explicit, reviewable and improvable. The entity-of-concern is the physical ОКС and the state of design decisions about it; ПД, BIM/IFC, tables, comments, dashboards and statuses are carriers, descriptions, views or evidence carriers.

Non-use boundary: this package is not a нормативная база, BIM-standard, template for ПД, expert-review regulation, completeness checklist, work schedule, approval route or proof that the built asset is correct.

| Work trigger | First pattern entry | First written result |
|---|---|---|
| ПД есть, но непонятно, почему решения такие | `BDPF.7` | PAD с selected structures, accepted losses и трассировкой к основаниям. |
| Исходных данных много, но непонятно, что они поддерживают | `BDPF.3` | Реестр source signals, admissible use и source-return conditions. |
| Есть source signal, но непонятно, какую структуру ОКС он затрагивает | `BDPF.3A` | Карта перехода от problem-side материала к структурам ОКС. |
| Проектировщик работает по разделам ПД, а не по логике объекта | `BDPF.2` | Метод разработки проектного решения. |
| Неясно, что должен обеспечивать объект | `BDPF.4` | Концепция использования. |
| Неясно, как объект работает как система | `BDPF.5` | Концепция системы. |
| Есть спор по архитектурному / конструктивному / инженерному решению | `BDPF.6` | Архитектурный вопрос и выбранная структура. |
| Нужно сравнить варианты по характеристикам | `BDPF.6B` / `BDPF.6C` | Criteria/eval and comparison basis. |
| Экспертиза видит повторяющиеся замечания | `BDPF.11` | Feedback/repair record к методу проектирования. |

## Preface - Cross-Cutting Ideas And Principles

BDPF is deliberately P2S-oriented: source material creates problem pressure and structuring need, not a direct decision. The package protects the chain:

```text
source signal -> architectureStructuringNeed -> unknown/candidate structures
-> architecture characteristics / criteria / eval -> candidate configurations
-> comparison / selected set -> PAD -> evidence -> documentation projection
-> feedback / source return / repair
```

The package keeps these owner boundaries stable:

- source carrier is not source signal;
- source signal is not project decision;
- selected set is not PAD;
- ADR/card is not PAD;
- evidence supports a claim in scope, not "the decision generally";
- gate/readiness is not proof or performed work;
- ПД/BIM/views are projections and carriers, not ОКС or architecture itself;
- expert comment or impact trace does not prove the PAD true or false by itself.

## Package Carrier Structure-Account Note

```text
FrameworkCarrierStructureCapture@BuiltAssetDesignPrinciplesFramework:
  evaluatedCarrierRef: DPF-building-design.md@draft-v0.4
  declaredUse: help expert teams make the development of built-asset design decisions explicit, reviewable, and improvable
  selectedSourceStructureDenominator: built asset design as source-signal-to-structure-to-decision work, with FPF P2S, built-asset architecture description, project decision, evidence, gate, carrier, and feedback owners as source traditions
  foregroundedStructure:
    - source signals and source-return conditions
    - use concept and system concept
    - built asset structures and architecture questions
    - candidate configurations, criteria/eval, comparison, selected set
    - project architecture decision / PAD and ADR projection
    - claim-specific evidence and readiness gates
    - projection into PD/BIM/views
    - expert/design feedback and method repair
  intentionallyCoarsenedAbstractedOmittedOrDeferredStructure:
    - full regulatory content of СП/ГОСТ/technical regulations
    - detailed BIM/IFC implementation standards
    - complete templates for all project documentation sections
    - full source pack and SoTA bibliography
    - role enactment details for all project organizations
    - post-design operation lifecycle loop beyond design source-return
  qualitativeCarrierEpiplexityForDeclaredUse: 3
  whyNot4: strong P2S chain and pattern map exist, but source-pack payload, heterogeneous cases, E.21 pattern evidence, and refresh evidence remain incomplete
  sourceReturnCondition: return to FPF Core owners, SourceUseAndRefreshMap, PFAD/PFR records, and project-specific evidence whenever a carrier, source, regulation, BIM/PD view, expert comment, score, or gate is used beyond its BDPF boundary
```

---

## 0. Назначение DPF

DPF нужен, когда проектная организация, экспертная команда или заказчик хотят управлять не только комплектностью проектной документации, но и **самим способом разработки проектного решения**.

DPF главным образом задаёт не набор документов, а управляемый поток превращения исходных сигналов в выбранные, описанные и проверяемые проектные структуры ОКС. Документы, BIM/IFC, таблицы, статусы, замечания и отчёты являются carriers, descriptions, views или evidence carriers; они не заменяют ОКС и не являются проектным архитектурным решением сами по себе.

Обычная слабость проектирования ОКС:

```text
исходные данные есть,
документация выпускается,
замечания фиксируются,
но не видно инженерной цепочки:
зачем объект нужен → как он используется → как он устроен как система → почему выбрано именно это решение → где это доказано.
```

DPF задаёт доменную рамку, в которой проектное решение рассматривается как результат цепочки:

```text
Исходные данные
→ потребности / ограничения / ценность
→ концепция использования
→ концепция системы
→ архитектурные вопросы и выбранные структуры
→ проектные решения
→ доказательства / обоснования
→ представление в ПД
→ экспертное рассмотрение
→ корректировка способа проектирования
```

Для BA-P2S эта цепочка уточняется как P2S-спина:

```text
source signals / исходные данные
→ reviewable problem-side record
→ architecture structuring need
→ unknown structures
→ candidate structure kinds
→ architecture characteristics + criteria
→ candidate architecture configurations
→ comparison basis / protected trade-offs
→ selected set / retained alternatives
→ ArchitectureDecisionRelation@Project
→ ArchitectureDescription / BuiltAssetArchitectureDescriptionUseCard
→ ProjectDocumentationProjection
→ method / work plan / readiness
→ design work / project representation review
→ feedback / source return / repair
```

Минимальное правило P2S: исходные данные не выбирают проектное решение. Они создают структурирующую потребность, ограничения, условия возврата к источнику и требования к синтезу кандидатных структур.

## 0.1. Package Boundary And Owner Routing

`DPF-building-design.md` является publication carrier-ом текущей DPF-редакции, а не всей архитектурой DPF-пакета, не source pack, не quality result и не work authority.

FPF-owner: `E.4.DPF`, `E.4.DPF.DA`, `E.4.PFAD`, `E.4.PFR`.

```text
DPFPackageStewardshipRecord@BuiltAssetDesignPrinciplesFramework:
  frameworkEditionRef: BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4
  declaredDomainOrLocalContext: экспертное сопровождение проектирования зданий и сооружений / ОКС
  intendedReaderOrOperator:
    - руководитель проектирования
    - главный инженер проекта / главный архитектор проекта
    - эксперт сопровождения
    - координатор BIM/ПД as publication/projection user
    - заказчик или технический заказчик as decision-reader
  declaredUse: сделать ход разработки проектного решения явным, проверяемым и улучшаемым
  nonUseBoundary: не нормы, не BIM-стандарт, не шаблон ПД, не регламент экспертизы, не proof качества ОКС
  fpfCoreEditionRef: FPF Core Conceptual Specification@June2026
  sourceBasisRefs: SourceUseAndRefreshMap@BuiltAssetDesignDPF
  pfadDecisionRefs: PFAD-BDPF-001
  patternSetRefs: BDPF.1..BDPF.11
  relationRecordRefs: PFR-BDPF-*
  publicationCarrierRefs: DPF-building-design.md@draft-v0.4
  accessCarrierRefs: none in this edition
  qualityEvaluationRefs: E4DPFDA-BDPF-2026-07-02; E21-BDPF-patterns-* lower/not-yet-materialized
  refreshRefs: RefreshRoute@BuiltAssetDesignDPF
  currentnessOrEditionBoundary: valid for draft/pilot until FPF Core edition, source pack, or pilot evidence changes
  blockedOverread: carrier-as-framework; BDPF-as-normative-regulation; checklist-as-method; BIM-as-architecture; gate-as-proof

FrameworkEditionDependencyRecord@BuiltAssetDesignPrinciplesFramework:
  frameworkEditionRef: BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4
  dependsOnEditionRefs: FPFCorePatternSet@June2026
  dependencyReason: BDPF reuses FPF Core owners for holons, bounded contexts, role assignments, method/work, P2S, architecture, PAD/ADR, evidence, gates, publication/views/carriers, improvement, and refresh
  compatibilityBoundary: BDPF may specialize built-asset design work but may not redefine A.1, A.1.1, A.2.1, A.15, C.30, C.30.AD.BA, C.32.P2S, C.32.PAD, C.32.ADR, A.10, A.21, E.17, E.23, or G.11
  deprecationOrSupersessionRefs: none for this draft
  refreshConditionRefs: FPF Core edition change; source-pack change; pilot failure; repeated expert-review defect not handled by current pattern set; package quality evaluation below floor
  reverseDependencyBlocked: FPF Core and FPF-Spec do not depend on this BDPF; Core candidates return through Core amendment decision

PrincipleFrameworkArchitectureDecision@BuiltAssetDesignDPF:
  frameworkDecisionId: PFAD-BDPF-001
  decisionQuestion: Which first DPF pattern set should govern expert support of design decision development for built assets?
  selectedPatternSetRefs: BDPF.1..BDPF.11
  selectedSpine: source signal -> architectureStructuringNeed -> candidate structures -> comparison -> PAD -> evidence -> documentation projection -> feedback
  rejectedAlternatives:
    - package as regulatory checklist
    - package as BIM/IFC standard
    - package as PD completeness checklist
    - package as expert-review comments workflow only
  rationaleRefs:
    - recurring defect: documents exist but engineering chain is hidden
    - P2S recovery need
    - carrier/description/decision/evidence/gate separation
  consequences: pilot can reconstruct one decision scenario; package has source-pack and relation-record debt before stable use
  sourceReturnConditions: return to source pack when source signals or regulatory/source basis change
  refreshOrSupersessionConditions: refresh when FPF Core, source pack, or pilot evidence changes

LegacyAliasRecord@BuiltAssetDesignDPF:
  DPF.1 -> BDPF.1
  DPF.2 -> BDPF.2
  DPF.3 -> BDPF.3
  DPF.3A -> BDPF.3A
  DPF.4 -> BDPF.4
  DPF.5 -> BDPF.5
  DPF.6 -> BDPF.6
  DPF.6A -> BDPF.6A
  DPF.6B -> BDPF.6B
  DPF.6C -> BDPF.6C
  DPF.7 -> BDPF.7
  DPF.7A -> BDPF.7A
  DPF.7B -> BDPF.7B
  DPF.8 -> BDPF.8
  DPF.9 -> BDPF.9
  DPF.10 -> BDPF.10
  DPF.11 -> BDPF.11
```

---

## 1. Что DPF не делает

DPF **не является**:

- перечнем нормативных требований;
- заменой СП, ГОСТ, технических регламентов, специальных технических условий, задания на проектирование или требований заказчика;
- BIM-стандартом;
- шаблоном проектной документации;
- регламентом экспертизы;
- чек-листом комплектности ИК;
- планом-графиком проектных работ.

DPF задаёт **структуру проектного рассуждения**: какие промежуточные знания должны появиться, чтобы проектное решение было не просто оформлено, а инженерно выведено и проверяемо.

---

## 2. Главные различения DPF

| Не смешивать | Правильное различение |
|---|---|
| ОКС и проектная документация | ОКС — целевая создаваемая система; ПД — описание / представление проектных решений. |
| Исходные данные и доказательства | Исходные данные дают основание для рассуждения; доказательство показывает, почему выбранное решение допустимо и достаточно. |
| Состав ИК и метод проектирования | ИК поставляет материалы; метод проектирования задаёт ход формирования решений. |
| Концепция и проектное решение | Концепция задаёт рамку использования / системы; проектное решение фиксирует выбранный способ реализации. |
| Требование и решение | Требование ограничивает или задаёт целевое состояние; решение отвечает, каким образом это обеспечено. |
| Замечание эксперта и причина дефекта | Замечание фиксирует обнаруженный дефект; причина может лежать в слабом способе проектирования. |
| Согласование / статус и инженерная истинность | Статус фиксирует прохождение процедуры; он не заменяет обоснование решения. |
| Вид / схема / модель и архитектура | Вид или схема описывает выбранную структуру; сама архитектура — не картинка и не файл. |
| Source signal и проектное решение | Исходный сигнал создаёт `architectureStructuringNeed`; решение появляется только после candidate synthesis, comparison, selected set и PAD. |
| Candidate structure kind и candidate configuration | Structure kind - тип структуры, которую надо рассмотреть; configuration - конкретный вариант выбранных или кандидатных структур. |
| Architecture characteristic и цель / потребность | Потребность отвечает зачем; characteristic отвечает какое свойство какой структуры удерживать, измерять или оценивать. |
| PAD и ADR / карточка решения | PAD - commitment по выбранным структурам; ADR/card - публикационная проекция решения для чтения и трассировки. |
| Expected structure и проектное представление | Expected structure ожидается по решению; ПД/BIM/views показывают, как эта структура представлена в проектном carrier-е для проверки. |

---

## 3. Доменная мантра проектирования ОКС

Для целевого ОКС и для каждой существенной подсистемы повторять цикл:

1. **Договорить всех о создаваемой системе в окружении.**  
   Что создаём, для кого, в каком окружении, какую пользу и какие эффекты должен обеспечить объект.

2. **Договорить всех о сценариях использования.**  
   Кто, когда, как и в каких режимах использует объект; какие эксплуатационные, технологические, пользовательские, аварийные и обслуживающие сценарии существенны.

3. **Договорить всех о системной логике.**  
   Из чего объект состоит, как взаимодействуют подсистемы, какие функции, потоки, границы, интерфейсы, режимы и ограничения должны быть обеспечены.

4. **Договорить всех о выбранных архитектурных структурах.**  
   Какие структуры действительно меняют проектное решение: функциональная, пространственная, конструктивная, инженерная, технологическая, организационная, эксплуатационная, интерфейсная, потоковая, управляющая.

5. **Договорить всех о способе создания.**  
   Как объект может быть построен, введён, обслужен, изменён и проверен без разрушения выбранной системной логики.

6. **Выпустить проектные решения как следствие.**  
   Решения должны быть прослеживаемы к исходным данным, сценариям, системной структуре, ограничениям и доказательствам.

### 3.1. P2S-правило для исходных данных

Исходный сигнал, требование, ограничение, ТЗ, изыскание, ТУ, обследование, требование эксплуатации или замечание сначала превращаются в вопрос о структуре ОКС:

```text
source signal
→ architectureStructuringNeed
→ unknown / candidate structure
→ architecture characteristics
→ candidate configurations
→ comparison / selected set
→ PAD
```

В текущей практике не используется отдельный conceptual carrier для сценариев работы объекта. Если требуется говорить о будущей работе объекта, использовать практические источники: ТЗ, технологические задания, требования эксплуатации, замечания, исходные данные, обследования, ТУ, изыскания и явно описанные сценарии использования.

---

## 4. Первые практические входы

| Ситуация | Первый BDPF-вход | Первый письменный результат |
|---|---|---|
| ПД есть, но непонятно, почему решения такие | BDPF.7 ArchitectureDecisionRelation@Project | PAD с selected structures, accepted losses и трассировкой к основаниям. |
| Исходных данных много, но непонятно, что они поддерживают | BDPF.3 DesignSourceSignalUse | Реестр исходных сигналов, их admissible use и source-return conditions. |
| Есть исходный сигнал, но непонятно, какую структуру ОКС он затрагивает | BDPF.3A BuiltAssetProblemToStructureFlow | Карта перехода от problem-side материала к структурам ОКС. |
| Проектировщик работает по разделам ПД, а не по логике объекта | BDPF.2 DesignDevelopmentMethod | Метод разработки проектного решения. |
| Неясно, что должен обеспечивать объект | BDPF.4 UseConceptRecord | Концепция использования. |
| Неясно, как объект работает как система | BDPF.5 SystemConceptRecord | Концепция системы. |
| Есть спор по архитектурному / конструктивному / инженерному решению | BDPF.6 ArchitectureQuestionCard | Архитектурный вопрос и выбранная структура. |
| Есть несколько допустимых конфигураций структуры | BDPF.6A CandidateArchitecturePalette | Палитра кандидатных архитектурных конфигураций. |
| Нужно сравнить варианты по характеристикам | BDPF.6B/BDPF.6C Criteria and Comparison | Набор критериев, eval и basis сравнения. |
| Экспертиза видит повторяющиеся замечания | BDPF.11 DesignMethodFeedback | Карта обратной связи от замечаний к методу проектирования. |
| Нужно понять готовность к следующему этапу разработки | BDPF.9 DesignReadinessGate | Карта готовности проектного шага. |

---

## 5. Pattern Index

| ID | Паттерн | Когда применять | Основной рабочий продукт | FPF-якоря |
|---|---|---|---|---|
| BDPF.1 | ОКС как целевая система | Нужно удержать объект как систему в окружении | `BuiltAssetSystemCard` | A.1, A.1.1, C.30 |
| BDPF.2 | Способ разработки проектного решения | Нужно описать метод проектирования, а не только проверку ПД | `DesignDevelopmentMethodDescription` | A.3.2, A.15, E.18.1 |
| BDPF.3 | Исходные данные как source signals | Нужно понять, какой сигнал извлечён и какую структуру он затрагивает | `DesignSourceSignalUseRecord` | C.22.2, C.32.P2S, A.10, B.3 |
| BDPF.3A | Развитие проблемы в структуры ОКС | Нужно провести problem-side материал к unknown/candidate structures | `BuiltAssetProblemToStructureFlowCard` | C.32.P2S, C.30, C.30.ASV, C.32 |
| BDPF.4 | Концепция использования | Нужно вывести структурные требования из сценариев использования | `UseConceptRecord` | C.2.1, C.30, C.28 |
| BDPF.5 | Концепция системы | Нужно описать состав, работу, bearer structures и границы ОКС | `SystemConceptRecord` | A.1, A.22, C.30 |
| BDPF.6 | Архитектурный вопрос ОКС | Нужно понять, какая структура меняет решение | `ArchitectureQuestionCard` | C.30, C.30.ASV, A.22 |
| BDPF.6A | Кандидатные архитектурные конфигурации | Нужно синтезировать несколько допустимых вариантов структуры | `CandidateArchitecturePalette` | C.32, C.18, C.19 |
| BDPF.6B | Критерии и eval architecture characteristics | Нужно измерять или оценивать характеристики, не превращая eval в решение | `ArchitectureCharacteristicCriteriaSet`, `ArchitectureCharacteristicEvalProgram` | C.32.ACS, C.32.ACE, C.16, C.25 |
| BDPF.6C | Comparison / selected set | Нужно сравнить варианты и опубликовать retained/selected set | `ComparisonBasis`, `SelectedSetPublication` | A.19.CPM, A.19.SelectorMechanism, G.5 |
| BDPF.7 | Проектное архитектурное решение | Нужно зафиксировать commitment по выбранным структурам | `ArchitectureDecisionRelation@Project` | C.32.PAD, C.11, A.10 |
| BDPF.7A | ADR / record-проекция решения | Нужно сделать решение читаемым carrier без подмены PAD | `ArchitectureDecisionRecordProjection` | C.32.ADR, E.17, E.9 |
| BDPF.7B | Пакет чтения решения | Нужно компактно собрать PAD, ADR, evidence, projection и роли без создания нового root-решения | `MinimalDecisionUsePackage` | C.32.PAD, C.32.ADR, E.17, A.10 |
| BDPF.8 | Доказательство / обоснование решения | Нужно отделить решение от claim-specific evidence и eval | `DesignEvidenceTrace` | A.10, B.3, C.16, C.32.ACE |
| BDPF.9 | Готовность проектного шага | Нужно понять, можно ли переходить дальше | `DesignReadinessGate` | A.15.5, A.21 |
| BDPF.10 | Проекция решения в ПД / BIM / views | Нужно связать selected structures с carriers и descriptions | `BuiltAssetArchitectureDescriptionUseCard`, `ProjectDocumentationProjection`, `MachineReadableValidationProjection` | C.30.AD.BA, E.17, C.33 |
| BDPF.11 | Обратная связь к методу и архитектуре | Замечания, source changes или проектные несоответствия требуют repair/source return | `DesignMethodFeedbackRecord`, `DesignChangeImpactTrace` | C.32.FAIL, E.23, G.11, A.15, C.32.P2S |

---

# BDPF.1 — ОКС как целевая система

## Problem frame

Используйте этот паттерн, когда объект капитального строительства обсуждается как набор разделов, чертежей, помещений, систем или замечаний, но не как целевая система в окружении.

## Что должно быть восстановлено

```text
BuiltAssetSystemCard:
  objectRef:
  objectName:
  objectKind:
  lifecyclePhase:
  environmentContext:
  beneficiaryStakeholders:
  operatingStakeholders:
  regulatoryAndSiteConstraints:
  valueStatement:
  primaryUseScenarios:
  systemBoundary:
  externalInterfaces:
  nonAdmissibleOverread:
```

## Минимальное правило

Пока не названы **объект**, **окружение**, **польза**, **сценарии использования**, **граница системы** и **внешние интерфейсы**, проектное рассуждение не должно переходить сразу к проектным решениям.

## Антипаттерны

| Антипаттерн | Симптом | Исправление |
|---|---|---|
| Объект как комплект ПД | Разговор идёт только о разделах и файлах | Вернуть `objectRef` и `valueStatement`. |
| Объект как пятно на участке | Есть посадка, но нет сценариев работы объекта | Описать `primaryUseScenarios`. |
| Объект как сумма систем | Есть АР, КР, ИОС, но нет целевой системной границы | Описать `systemBoundary` и `externalInterfaces`. |

---

# BDPF.2 — Способ разработки проектного решения

## Problem frame

Используйте этот паттерн, когда проектировщик выпускает документацию, но не предъявляет управляемый ход разработки решения.

## Рабочий продукт

```text
DesignDevelopmentMethodDescription:
  methodName:
  designScope:
  inputState:
  outputState:
  requiredIntermediateRecords:
    - BuiltAssetSystemCard
    - DesignSourceSignalUseRecord
    - BuiltAssetProblemToStructureFlowCard
    - UseConceptRecord
    - SystemConceptRecord
    - ArchitectureQuestionCard
    - CandidateArchitecturePalette
    - ComparisonBasis
    - ArchitectureDecisionRelation@Project
    - ArchitectureDecisionRecordProjection
    - DesignEvidenceTrace
    - BuiltAssetArchitectureDescriptionUseCard
    - ProjectDocumentationProjection
  roles:
  roleAssignmentPolicy:
    authoringRoleAssignmentRefs:
    reviewRoleAssignmentRefs:
    approvalRoleAssignmentRefs:
    publicationRoleAssignmentRefs:
    coordinationRoleAssignmentRefs:
    separationOfDutiesRefs:
    assignmentWindowPolicy:
    roleEvidenceOrSourceRefs:
    nonAdmissibleUse:
  workSteps:
  readinessChecks:
  evidenceRequirements:
  feedbackLoop:
  nonGoals:
```

## Минимальная цепочка метода

```text
1. Идентифицировать ОКС как систему в окружении.
2. Извлечь source signals из исходных данных, требований, ограничений, ТЗ, изысканий, ТУ, обследований, требований эксплуатации и замечаний.
3. Превратить source signals в `architectureStructuringNeed`.
4. Назвать unknown/candidate structures и минимальный набор relevant structure kinds.
5. Описать сценарии использования и системную концепцию.
6. Выделить архитектурные вопросы и candidate configurations.
7. Сформировать criteria/eval и comparison basis.
8. Зафиксировать selected set и PAD.
9. Опубликовать ADR/record-проекцию без подмены решения carrier-ом.
10. Приложить claim-specific evidence / eval.
11. Спроецировать selected structures в ПД/BIM/views.
12. Проверить readiness и передать в work plan / performed work.
13. Вернуть замечания, проектные несоответствия и потери представления в repair/source-return.
```

## Проверка

Метод считается достаточно описанным для пилота, если по одному типу решения можно восстановить:

- какие source signals извлечены из исходных данных;
- какую `architectureStructuringNeed` они создают;
- какая unknown/candidate structure возникла;
- какой сценарий использования формируют;
- какую системную структуру поддерживают;
- какие candidate configurations сравнивались;
- какой selected set или stop reason получен;
- какой PAD принят;
- чем оно обосновано;
- где selected structures отражены в ПД/BIM/views;
- как эксперт его проверяет.

Role name, должность, подпись, статус согласования или publication carrier не доказывают, что решение сформировано, проверено или принято. Для reliance-bearing claim нужен `RoleAssignment` с holder, role, bounded context и window либо явное lower/block состояние.

---

# BDPF.3 — Исходные данные как source signals

## Problem frame

Используйте этот паттерн, когда исходные данные, ТЗ, ИРД, ГПЗУ, изыскания, ТУ, требования эксплуатации, BIM/IFC, обследования, экспертные заключения или замечания переданы как материалы, но ещё не ясно:

- какой source signal из них извлечён;
- какую `architectureStructuringNeed` он создаёт;
- какую unknown/candidate/selected structure он затрагивает;
- где граница admissible use;
- когда нужен source return.

## Рабочий продукт

```text
DesignSourceSignalUseRecord:
  sourceSignalRef:
  sourceKind:
  sourceOwner:
  issueDateOrVersion:
  extractedSignal:
  needKind:
  affectedHolonOrScope:
  supportedQuestion:
  affectedStructureKindRefs:
  affectedArchitectureCharacteristics:
  admissibleUse:
  nonAdmissibleUse:
  freshnessBoundary:
  missingOrAmbiguousData:
  sourceReturnCondition:
  affectedDecisionRefs:
  affectedSelectedStructureRefs:
  affectedEvidenceTraceRefs:
  affectedDocumentationProjectionRefs:
  changeImpactRule:
  receivingPatternRef:
```

## Минимальное правило

Не запрашивать исходные данные и не ссылаться на них как на основание решения без ответа на вопросы:

```text
Какой source signal извлечён?
Какую структуру ОКС он делает неизвестной, спорной или ограниченной?
Какой следующий DPF/FPF-owner должен принять claim?
```

`DesignSourceSignalUseRecord` не является evidence решением. Он только показывает, что можно извлечь из carrier-а и куда этот сигнал допустимо передать дальше.

## Классификатор `needKind`

| `needKind` | Что даёт | Обычно затрагивает | Чего не решает само по себе |
|---|---|---|---|
| `regulatoryConstraintNeed` | Норматив, ТУ, запрет, допустимый диапазон. | Constraint, control, spatial, flow structures. | Не выбирает планировку или конструктивную схему. |
| `sitePlacementNeed` | Ограничения участка, ГПЗУ, посадка, сервитуты, ЗОУИТ. | Spatial, interface, external flow structures. | Не выбирает объёмно-планировочное решение. |
| `geotechnicalOrStructuralNeed` | Геология, нагрузки, основания, конструктивные ограничения. | Load-bearing, material, construction method structures. | Не выбирает архитектурную форму без comparison. |
| `engineeringCapacityNeed` | Мощности, подключения, режимы, трассы. | Engineering systems, interface, control structures. | Не доказывает достаточность инженерной схемы. |
| `useScenarioNeed` | Практический сценарий использования, эксплуатации, обслуживания или эвакуации. | Functional, flow, control, maintenance structures. | Не заменяет концепцию использования и не является самостоятельным проектным решением. |
| `constructionRealizationNeed` | Площадка, этапность, временные состояния, ограничения производства работ. | Construction method, temporary, logistics structures. | Не заменяет work plan. |
| `informationRelianceNeed` | BIM/IFC, обследование, реестр, цифровой двойник используется как источник. | Description/source relation, captured/lost structure. | Не делает модель ОКС, evidence, gate или decision. |
| `expertReviewNeed` | Замечание или вопрос рассмотрения указывает на дефект решения или метода. | Evidence, decision, method, feedback structures. | Не является критерием качества само по себе. |

## Пример

| Исходные данные | Неудачная трактовка | DPF-трактовка |
|---|---|---|
| ГПЗУ / градостроительные ограничения | Просто обязательный файл | Source signals для `sitePlacementNeed`, границ, допустимых параметров, внешних интерфейсов и архитектурных вопросов. |
| Технологическое задание | Просто приложение к заданию | Source signals для режимов использования, функционально-планировочных структур и системной концепции. |
| Инженерные изыскания | Просто исходный документ | Source signals для `geotechnicalOrStructuralNeed`, конструктивных, инженерных и организационно-строительных структур. |

---

# BDPF.3A — Развитие проблемы в структуры ОКС

## Problem frame

Используйте этот паттерн, когда по ОКС есть исходные данные, требования, ограничения, ТЗ, изыскания, ТУ, обследования, требования эксплуатации или замечания, но ещё не ясно:

- какая структура ОКС неизвестна или спорна;
- какие structure kinds надо рассматривать;
- какие architecture characteristics должны удерживаться;
- какие candidate configurations нужно синтезировать;
- какой следующий FPF-owner должен принять claim.

## Рабочий продукт

```text
BuiltAssetProblemToStructureFlowCard:
  flowId:
  describedHolonRef:
  boundedContextRef:
    holonScope:
    lifecycleSlice:
    nqdWorkState:
    closurePosture:
    sourceMaturity:
    decisionMaturity:
    publicationMaturity:
  architectureStructuringNeed:
    needKind:
    sourceSignalRefs:
    architectureConcernRefs:
    affectedHolonRefs:
    currentStopOrReturnReason:
    sourceReturnCondition:
  architectureContent:
    candidateStructureKindRefs:
    selectedStructureRefs:
    expectedStructureRefs:
    representedStructureRefs:
    architectureCharacteristicRefs:
    architectureCharacteristicCriteriaSetRef:
    qBundleRefs:
    candidateSynthesisRef:
  structuralInformation:
    unknownStructure:
    selectedStructure:
    expectedStructure:
    representedStructure:
    capturedInDescriptionsOrDecisions:
    handedToMethodsOrWork:
    latentOrHiddenStructure:
    lostStructure:
    sourceReturnCondition:
  decisionAndWorkDocking:
    candidateSetOrPaletteRef:
    comparisonBasisRef:
    selectedSetRef:
    architectureDecisionRef:
    methodDescriptionRefs:
    workPlanRefs:
    readinessRefs:
    performedWorkRefs:
  builtAssetDescriptionDocking:
    builtAssetArchitectureDescriptionUseCardRef:
    bimOrIFCRefs:
    assetInformationRefs:
    referenceDesignationRefs:
    digitalTwinViewRefs:
    publicationOrExchangeRefs:
  feedback:
    evalProgramRefs:
    evalResultRefs:
    measurementRefs:
    operationOrUseObservationRefs:
    designRepresentationRefs:
    ownerSpecificReturnOrRepair:
  neighboringOwnerForNextClaim:
```

## NQD-like состояния P2S

| `nqdWorkState` | Рабочий смысл для ОКС | Что допустимо | Что ещё нельзя |
|---|---|---|---|
| `SignalIntake` | Есть исходные сигналы, но problem-side ещё не сформирован. | Собирать source signals, формировать ProblemCard. | Нельзя принимать architecture decision. |
| `ProblemShaping` | Проблемная сторона стала reviewable. | Формировать `architectureStructuringNeed`. | Нельзя утверждать выбранную структуру. |
| `StructureKindTriage` | Понятны типы структур, которые надо рассмотреть. | Заполнять `candidateStructureKindRefs`, `unknownStructure`. | Нельзя считать это candidate solution. |
| `CriteriaShaping` | Появляются characteristics/criteria. | Делать ACS/Q-Bundle/measurement plan. | Нельзя оптимизировать без bearer/scale. |
| `CandidateGeneration` | Синтезируются candidate configurations. | Создавать candidate palette. | Нельзя выбирать победителя. |
| `FrontIllumination` | Варианты оценены; виден trade-off front. | Делать eval/comparison input. | Нельзя сворачивать всё в один score. |
| `RetainedSetPublication` | Публикуется shortlist / selected set. | Публиковать selected set. | Это ещё не PAD. |
| `ArchitectureCommitment` | Принимается PAD. | Фиксировать `ArchitectureDecisionRelation@Project`. | Нельзя путать с ADR, BIM или ПД. |
| `DescriptionPublication` | Публикуются BIM/ПД/views. | Использовать description/publication owners. | Описание не становится ОКС или решением. |
| `WorkPreparation` | Решение передаётся в метод/план/readiness. | Готовить work plan и readiness. | План не является выполненной работой. |
| `DesignRepresentationReview` | Проверяются ПД/BIM/views и проектные carriers. | Фиксировать потерянную, искажённую или не представленную selected/expected structure. | Нельзя считать carrier самим решением. |
| `FeedbackRepair` | Проектное несоответствие возвращает repair/source-return. | Назвать owner-specific repair route. | Нельзя латать только текст carrier-а без возврата к решению или источнику. |

## Минимальное правило

```text
Нельзя переходить от исходных данных сразу к проектному решению, пока не названо:
1. какой ОКС / подсистема является describedHolonRef;
2. в каком boundedContextRef ведётся архитектурная работа;
3. какая architectureStructuringNeed возникла из source signals;
4. какая structure unknown / candidate / selected / expected / represented;
5. какие architecture characteristics удерживаются;
6. какой следующий FPF-owner принимает claim.
```

---

# BDPF.4 — Концепция использования

## Problem frame

Используйте этот паттерн, когда проектное решение обсуждается без явной картины того, как объект будет использоваться.

## Рабочий продукт

```text
UseConceptRecord:
  objectRef:
  contextRef:
  sourceSignalRefs:
  userGroups:
  beneficiaryGroups:
  operatingRoles:
  primaryUseScenarios:
  secondaryUseScenarios:
  maintenanceScenarios:
  emergencyScenarios:
  logisticsAndAccessScenarios:
  scenarioConflicts:
  valueAndLossClaims:
  capabilityOrFunctionImplications:
  constraintImplications:
  architectureCharacteristicRefs:
  evidenceRefs:
  downstreamSystemConceptRefs:

UseScenarioSourceUseBoundary:
  scenarioSourceRefs: ТЗ | технологическое задание | требования эксплуатации | обследование | замечание | explicitly described use scenario
  useConceptRecordUse: organizes scenario claims for downstream system concept and architecture questions
  nonAdmissibleUse: UseConceptRecord is not source authority, not ConOps carrier, not proof of demand, and not project decision
```

## Проверка

Концепция использования достаточна для перехода к концепции системы, если видно:

- кто использует объект;
- какие режимы и сценарии существенны;
- какие сценарии конфликтуют;
- какие сценарии должны быть поддержаны системными структурами;
- какие функции, ограничения и architecture characteristics возникают из сценариев;
- какие исходные данные подтверждают или ограничивают эти сценарии.

## Антипаттерн

`Назначение объекта = концепция использования` — ошибка. Назначение объекта слишком грубое. Концепция использования должна описывать сценарии, роли, режимы, ограничения и конфликты использования.

---

# BDPF.5 — Концепция системы

## Problem frame

Используйте этот паттерн, когда есть сценарии использования, но не восстановлена системная логика: состав, функции, границы, интерфейсы, потоки, режимы и ограничения.

## Рабочий продукт

```text
SystemConceptRecord:
  objectRef:
  useConceptRefs:
  sourceSignalRefs:
  systemBoundary:
  subsystems:
  bearerStructures:
  functions:
  flows:
  interfaces:
  operatingModes:
  constraints:
  architectureCharacteristicRefs:
  unknownOrCandidateStructures:
  criticalDependencies:
  unresolvedSystemQuestions:
  downstreamArchitectureQuestionRefs:
```

## Типовые системные области для ОКС

| Область | Что фиксировать |
|---|---|
| Функционально-планировочная | Какие функции и сценарии должны быть размещены и связаны. |
| Пространственная | Как объект размещается на участке и в окружении. |
| Конструктивная | Какая несущая логика и ограничения формируют решения. |
| Инженерная | Какие инженерные системы обеспечивают режимы использования. |
| Технологическая | Как технологический процесс определяет объект. |
| Эксплуатационная | Как объект обслуживается, ремонтируется, управляется. |
| Пожарная и безопасностная | Какие сценарии опасности, эвакуации и ограничения управляют решениями. |
| Организационно-строительная | Как объект может быть создан с учётом площадки, этапности и ограничений. |

---

# BDPF.6 — Архитектурный вопрос ОКС

## Problem frame

Используйте этот паттерн, когда спор идёт не о локальной детали, а о структуре объекта, которая меняет несколько решений сразу.

## Рабочий продукт

```text
ArchitectureQuestionCard:
  objectRef:
  contextRef:
  sourceSignalRefs:
  architectureConcernCue:
  sourceMaterialRef:
  candidateStructureKinds:
  smallestUsefulStructureKinds:
  architectureCharacteristicRefs:
  candidateConfigurationRefs:
  selectedStructureRefs:
  expectedStructureRefs:
  representedStructureRefs:
  affectedUseScenarios:
  affectedSystemConceptRefs:
  candidateDesignMoves:
  firstArchitectureMove:
  nonArchitectureClaims:
  nonAdmissibleOverread:
```

## Классификатор структур для проектирования ОКС

| StructureKind | Когда выбирать |
|---|---|
| FunctionalPlanningStructure | Функции, помещения, связи, сценарии использования. |
| MaterialSpatialStructure | Объём, посадка, геометрия, пространственные ограничения. |
| StructuralLoadBearingStructure | Несущая схема, конструктивная логика, основания. |
| EngineeringSystemsStructure | Инженерные системы, трассы, мощности, режимы. |
| TransformationFlowStructure | Потоки людей, транспорта, материалов, энергии, информации, строительства. |
| ControlOperationStructure | Управление, диспетчеризация, режимы эксплуатации. |
| ModuleInterfaceStructure | Границы подсистем, интерфейсы, точки подключения. |
| ConstructionMethodStructure | Организация строительства, этапность, временные состояния. |
| EvidenceAssuranceStructure | Структура доказательств, проверок, подтверждений. |
| ScaleEvolutionStructure | Возможность расширения, очередность, изменение объекта во времени. |

Классификатор не является чек-листом полноты. В карточке указывать только `smallestUsefulStructureKinds`: минимальный набор структур, без которого следующий архитектурный ход будет неправильным, преждевременным или невосстановимым.

## Минимальное правило

Архитектурный вопрос допустим, если он указывает:

```text
какой ОКС / подсистема описывается,
какая структура действительно влияет на решение,
какой следующий архитектурный ход нужен:
inspect | split | relate | downgrade | assignGoverningPattern | stop.
```

---

# BDPF.6A — Кандидатные архитектурные конфигурации

## Problem frame

Используйте этот паттерн, когда структура ОКС уже названа как relevant structure kind, но ещё нельзя честно принять одно решение: нужно синтезировать несколько допустимых candidate configurations или зафиксировать stop reason.

## Рабочий продукт

```text
CandidateArchitecturePalette:
  paletteId:
  objectRef:
  boundedContextRef:
  architectureQuestionRefs:
  candidateStructureKindRefs:
  architectureCharacteristicRefs:
  candidateConfigurations:
    - configurationId:
      selectedStructureRefs:
      expectedLosses:
      sourceSignalRefs:
      nonAdmissibleReading:
  rejectedOrUnavailableConfigurations:
  stopReasonIfNoPlurality:
  nextComparisonOwner:
```

## Минимальное правило

Candidate palette не выбирает победителя. Она только делает пространство вариантов обозримым для comparison, selected set или PAD.

---

# BDPF.6B — Критерии и eval architecture characteristics

## Problem frame

Используйте этот паттерн, когда варианты надо оценить по свойствам структур, но ещё не ясно, какие characteristics имеют bearer, scale, evidence и границы admissible use.

## Рабочий продукт

```text
ArchitectureCharacteristicCriteriaSet:
  criteriaSetId:
  objectRef:
  boundedContextRef:
  architectureCharacteristicRows:
    - characteristicRef:
      bearerStructureRef:
      measureOrEvalRef:
      admissibleUse:
      protectedCounterCharacteristic:
      proxyRisk:
      missingEvidence:

ArchitectureCharacteristicEvalProgram:
  evalProgramId:
  criteriaSetRef:
  candidateConfigurationRefs:
  measurementRefs:
  evidenceRefs:
  evalResultRefs:
  comparisonInputRefs:
  nonAdmissibleUse:
```

## Минимальное правило

Eval, расчёт, simulation или экспертная оценка не выбирают решение. Они дают input для comparison/selection/PAD и должны сохранять границы применимости.

---

# BDPF.6C — Comparison / selected set

## Problem frame

Используйте этот паттерн, когда есть candidate configurations и criteria/eval, но нужно отделить сравнение, selected set и project architecture decision.

## Рабочий продукт

```text
ComparisonBasis:
  comparisonId:
  objectRef:
  boundedContextRef:
  candidateConfigurationRefs:
  criteriaSetRefs:
  evalResultRefs:
  protectedTradeOffs:
  unacceptableLosses:
  missingEvidence:
  comparisonMethodRef:
  nonAdmissibleUse:

SelectedSetPublication:
  selectedSetId:
  comparisonBasisRef:
  retainedConfigurationRefs:
  rejectedConfigurationRefs:
  abstainOrHoldReason:
  nextDecisionOwner:
```

## Минимальное правило

Selected set ещё не является PAD. Он показывает, какие варианты удержаны после сравнения, но commitment по selected structures, accepted losses и reopen conditions появляется только в BDPF.7.

---

# BDPF.7 — Проектное архитектурное решение

## Problem frame

Используйте этот паттерн, когда нужно принять project architecture decision после candidate synthesis, comparison и selected set.

## Рабочий продукт

```text
ArchitectureDecisionRelation@Project:
  decisionId:
  objectRef:
  boundedContextRef:
  decisionQuestion:
  selectedArchitectureOption:
  affectedSelectedStructures:
  affectedExpectedStructures:
  acceptedLosses:
  rejectedAlternatives:
  retainedAlternatives:
  basis:
    sourceSignalRefs:
    useConceptRefs:
    systemConceptRefs:
    architectureQuestionRefs:
    candidatePaletteRefs:
    comparisonBasisRefs:
    selectedSetRefs:
    requirementRefs:
  evidenceRefs:
  methodUseInstructions:
  decisionAuthorRoleAssignmentRef:
  decisionReviewerRoleAssignmentRefs:
  decisionApproverRoleAssignmentRef:
  publisherRoleAssignmentRef:
  coordinationRoleAssignmentRefs:
  roleSeparationNotes:
  stakeholderConcernCoverage:
    - concernRef:
      stakeholderRoleOrGroupRef:
      viewpointRef:
      affectedStructureRefs:
      coveredByEvidenceOrAssuranceRefs:
      acceptedLossOrResidualRiskRef:
      unresolvedConcernOrSourceReturnCondition:
  protectionRiskAndComplianceRows:
    - concernRef:
      protectionNeedRef:
      riskAssumptionRef:
      regulatoryAssumptionRef:
      complianceRuleRef:
      affectedStructureRefs:
      evidenceOrAssuranceRefs:
      gateOrReviewRefs:
      accessOrConfidentialityBoundary:
      acceptedRiskOrLoss:
      unresolvedGap:
      receivingOwnerForNextClaim:
      nonAdmissibleUse:
  affectedDocumentationRefs:
  residualRisksOrOpenIssues:
  decisionStatus:
  reopenOrSupersessionCondition:
  sourceReturnCondition:
```

## Минимальное правило

Проектное архитектурное решение не считается достаточно зафиксированным, если указано только “что принято”, но не указано:

- какой вопрос решался;
- какие альтернативы рассматривались или почему они не требуются;
- какие selected structures и expected structures затронуты;
- какие trade-offs и accepted losses приняты;
- на какие source signals, концепции, candidate palette и comparison basis решение опирается;
- какие доказательства подтверждают допустимость;
- где решение отражено в ПД;
- какие concern/viewpoint покрыты, какие потери или residual risks приняты;
- кто сформировал, проверил, принял и опубликовал решение как `RoleAssignment`;
- какие method/work consequences появляются;
- при каком изменении решение надо пересмотреть, заменить или вернуть к источнику.

Concern/viewpoint не выбирает решение и не доказывает его допустимость. Он задаёт рамку чтения, проверки и source-return, в которой selected structures, evidence и projection должны быть представлены без потерь, существенных для этого concern.

Protection/security/compliance row фиксирует concern, assumption, affected structures и next owner. Она не доказывает безопасность, соответствие нормам, правомерность публикации или готовность к экспертизе без соответствующего evidence/assurance/gate owner.

---

# BDPF.7A — ADR / record-проекция решения

## Problem frame

Используйте этот паттерн, когда PAD уже принят и его нужно сделать читаемым для участников проекта, экспертизы или downstream work без подмены самого решения записью.

## Рабочий продукт

```text
ArchitectureDecisionRecordProjection:
  recordId:
  architectureDecisionRef:
  sectionFunction:
  contextSummary:
  decisionOutcome:
  selectedStructureRefs:
  rationale:
  consequences:
  acceptedLosses:
  evidenceRefs:
  methodUseInstructions:
  supersessionOrUpdateCondition:
  publicationCarrierRefs:
  nonAdmissibleUse:
```

## Минимальное правило

ADR, карточка решения, журнал или фрагмент ПД являются publication carriers. Они помогают читать PAD, но не заменяют `ArchitectureDecisionRelation@Project`.

---

# BDPF.7B — Minimal decision use package / пакет чтения решения

## Problem frame

Используйте этот паттерн, когда участнику проекта, экспертизы или downstream work нужен компактный пакет чтения уже принятого PAD без подмены PAD, evidence, gate или ПД.

## Рабочий продукт

```text
MinimalDecisionUsePackage:
  packageId:
  architectureDecisionRelationRef:
  architectureDecisionRecordProjectionRef:
  evidenceTraceRefs:
  documentationProjectionRefs:
  roleAssignmentRefs:
  readinessGateRefs:
  riskOrComplianceNoteRefs:
  publicationCarrierRefs:
  readerUse:
  admissibleUse:
  nonAdmissibleUse:
```

## Минимальное правило

`MinimalDecisionUsePackage` является navigation / publication package. Он не принимает решение, не доказывает claim, не проводит gate и не заменяет projection в ПД/BIM/views.

---

# BDPF.8 — Доказательство / обоснование решения

## Problem frame

Используйте этот паттерн, когда решение заявлено, но его допустимость, достаточность или надёжность не подтверждена.

## Рабочий продукт

```text
DesignEvidenceTrace:
  claimRef:
  claimText:
  claimScope:
  evidenceRefs:
  evidenceGraphPathRefs:
  evidenceCarrierRefs:
  evidenceProducingWorkRefs:
  evidenceInterpretingRoleAssignmentRefs:
  methodTraceRefs:
  measurementRefs:
  evalResultRefs:
  evidenceKind:
    calculation | model | normativeCheck | simulation | comparison | expertJudgement | sourceDocument | fieldData | issueRecord | reviewSessionResult | acceptedDeviation | other
  evidenceFreshness:
  timeOrFreshnessWindow:
  sourceCurrentnessRefs:
  rivalExplanationOrLimitation:
  reliabilityNotes:
  unresolvedEvidenceGap:
  admissibleUse:
  nonAdmissibleUse:
```

## Минимальное правило

Доказательство должно поддерживать конкретный claim, а не “решение вообще”.

Evidence graph path поддерживает только указанный claim в указанном scope. Он не является approval, gate passage, PAD, selected set или publication readiness.

Если расчёт, модель, simulation, BIM-clash, экспертная оценка или табличный score используются для сравнения вариантов, они остаются evidence/eval input. Они не становятся comparison, selected set или PAD без соответствующих BDPF.6C/BDPF.7 записей.

Плохая формула:

```text
Решение обосновано расчётом.
```

Рабочая формула:

```text
Claim: выбранная конструктивная схема обеспечивает требуемую несущую способность в данном расчётном случае.
Evidence: расчётная модель, нагрузки, сочетания, результаты, ограничения применимости.
AdmissibleUse: подтверждение выбранного решения в пределах указанной схемы и расчётных условий.
NonAdmissibleUse: не подтверждает технологичность, стоимость, пожарную безопасность или эксплуатационную пригодность.
```

---

# BDPF.9 — Готовность проектного шага

## Problem frame

Используйте этот паттерн, когда нужно понять, можно ли переходить к следующему шагу проектирования или передавать материалы на экспертное рассмотрение.

## Рабочий продукт

```text
DesignReadinessGate:
  gateId:
  gateProfile:
    domainDecisionReadiness | publicationReadiness | workEntryReadiness | reviewReadiness
  designStep:
  objectScope:
  requiredRecords:
  requiredEvidence:
  requiredProjectionRefs:
  blockingGaps:
  acceptedDeviations:
  gateDecision:
    pass | passWithReservations | hold | reject | abstain
  decisionBasis:
  nextAllowedWork:
  nonAllowedWork:
  nonAdmissibleUse:
```

## Пример gate для перехода от концепции к проектному решению

| Проверка | Pass, если |
|---|---|
| Исходные данные | Данные не просто загружены, а привязаны к проектным вопросам. |
| Концепция использования | Существенные сценарии описаны и связаны с системными требованиями. |
| Концепция системы | Видно, какие подсистемы, функции, потоки и интерфейсы нужны. |
| Архитектурные вопросы | Выделены структуры, которые меняют решение. |
| Доказательства | Для выбранного решения указано, чем оно будет проверяться. |

Gate не выбирает проектное решение и не доказывает его допустимость. Он проверяет, собран ли достаточный проектный комплект для следующего шага работы или рассмотрения.

`domainDecisionReadiness` проходит, если source signals, use concept, system concept, architecture question, candidate basis, comparison и evidence plan достаточно предъявлены для PAD/review.

`publicationReadiness` проходит, если PAD уже принят; ADR/projection связаны с PAD; selected/expected structures представлены в carriers; representation loss и source-return condition указаны; publication carrier не подменяет proof, gate или decision.

---

# BDPF.10 — Проекция решения в ПД / BIM / views

## Problem frame

Используйте этот паттерн, когда PAD принят, но не ясно, где и как selected/expected structures представлены в ПД, BIM/IFC, схемах, таблицах, спецификациях или других project carriers.

## Рабочий продукт

```text
BuiltAssetArchitectureDescriptionUseCard:
  architectureClaimRef:
  describedHolonRef:
  boundedContextRef:
  selectedStructureRefs:
  expectedStructureRefs:
  structureKindRefs:
  architectureStructuralViewRefs:
  referenceDesignationRefs:
  assetInformationRefs:
  bimOrIFCRefs:
  publicationOrExchangeRefs:
  correspondenceRefs:
  sourceReturnCondition:
  admissibleUse:
  nonAdmissibleUse:
  firstNeighborPatternApplication:

ProjectDocumentationProjection:
  decisionRef:
  selectedStructureRefs:
  documentationSectionRefs:
  drawingRefs:
  modelRefs:
  explanatoryNoteRefs:
  calculationRefs:
  scheduleOrSpecificationRefs:
  crossReferences:
  representationLossNotes:
  viewpointRefs:
  concernCoverageNotes:
  unrepresentedConcernRefs:
  reviewerUse:
  reviewerViewpointUse:
  sourceReturnConditionForConcernLoss:
  nonAdmissibleUse:

MachineReadableValidationProjection:
  validationProjectionId:
  governingClaimRef:
  checkedCarrierRefs:
  machineReadableRuleSpecRefs:
  ruleSpecOwnerRef:
  checkRunWorkRefs:
  checkResultRefs:
  checkedStructureRefs:
  capturedStructureNotes:
  lostOrUnvalidatedStructureNotes:
  evidenceOrGateUse:
  admissibleUse:
  nonAdmissibleUse:
  sourceReturnCondition:
```

## Минимальное правило

ПД, BIM, IFC, схемы, таблицы и dashboard - это project carriers / descriptions / views. Они не являются ОКС, PAD, proof, gate passage или performed work.

Для экспертного сопровождения важно видеть, что при переносе в carriers не потеряны:

- границы применимости;
- исходные основания;
- системная логика;
- selected structures и expected structures;
- выбранные альтернативы, retained alternatives или причины отсутствия альтернатив;
- доказательства;
- связанные решения в других разделах.

Machine-readable check может подтвердить, что carrier соответствует объявленным rule specs в указанном scope. Он не становится PAD, evidence sufficiency, gate passage, regulatory compliance или proof без прямого владельца claim.

---

# BDPF.11 — Обратная связь к методу и архитектуре в проектном контуре

## Problem frame

Используйте этот паттерн, когда замечания экспертизы, внутренние проектные проверки, междисциплинарные коллизии, несогласованность ПД/BIM/views или повторяющиеся вопросы рассмотрения показывают, что проблема не в одном файле, а в способе разработки проектного решения.

## Рабочий продукт

```text
DesignMethodFeedbackRecord:
  feedbackId:
  feedbackSourceKind:
    expertReview | designReview | interdisciplinaryCoordination | pdBimConsistencyCheck | sourceReturn | other
  reviewResultRefs:
  designCheckRefs:
  projectCarrierRefs:
  selectedStructureRefs:
  expectedStructureRefs:
  representedStructureRefs:
  measurementRefs:
  evalResultRefs:
  repeatedDefectPattern:
  affectedDesignMethodStep:
  suspectedRootCause:
  ownerSpecificReturnOrRepair:
    c32SynthesisRef:
    c32PadRepairOrSupersessionRef:
    c30DescriptionSourceReturnRef:
    a15WorkPlanRepairRef:
    e23MethodImprovementCycleRef:
    g11CurrentnessRefreshRef:
  proposedMethodChange:
  affectedTemplatesOrForms:
  validationCheck:
  decision:
    acceptChange | rejectChange | probeMore | hold
  reopenCondition:

DesignChangeImpactTrace:
  impactTraceId:
  changedSourceSignalRef:
  changedCondition:
  changedCarrierOrVersionRef:
  suspectDecisionRefs:
  suspectSelectedStructureRefs:
  suspectExpectedStructureRefs:
  suspectEvidenceTraceRefs:
  suspectDocumentationProjectionRefs:
  impactDisposition:
    noImpact | reviewNeeded | sourceReturn | padRepair | evidenceRefresh | publicationRepair | methodRepair | hold
  ownerSpecificReturnOrRepair:
    sourceReturnRef:
    c32PadRepairOrSupersessionRef:
    a10EvidenceRefreshRef:
    c30DescriptionSourceReturnRef:
    e23MethodImprovementCycleRef:
    g11CurrentnessRefreshRef:
  nonAdmissibleUse:
```

## Граница контекста

BDPF.11 в этой версии ограничен проектированием. Он не ведёт самостоятельный контур после проектирования. Внешние данные жизненного цикла, если они когда-нибудь понадобятся, должны входить как отдельный source-return к проектному методу, а не расширять текущий BDPF за пределы проектирования.

Impact trace не доказывает, что решение неверно. Он фиксирует suspectness и следующий owner-specific route для проверки, ремонта, source return или подтверждения `noImpact`.

## Пример

| Повторяющееся замечание | Возможная методическая причина | Изменение метода |
|---|---|---|
| Решения не обоснованы исходными данными | Нет `DesignSourceSignalUseRecord` | Ввести трассировку source signal → architectureStructuringNeed → structure → decision. |
| Разделы противоречат друг другу | Нет `SystemConceptRecord` и интерфейсных связей | Ввести системную концепцию до выпуска разделов. |
| Варианты сравниваются формально | Нет criteria/eval и comparison basis | Ввести `ArchitectureCharacteristicCriteriaSet`, `ComparisonBasis` и selected set до PAD. |
| Эксперт видит решение слишком поздно | Нет readiness gate перед детализацией | Ввести ранний gate после концепции системы. |

---

## 6. Минимальный комплект DPF-файлов для репозитория

Status guard: текущий файл остаётся монолитным draft-carrier-ом в `work/00_inbox/`. Ниже показана только целевая структура после стабилизации; эта версия не разбивается на отдельные файлы и не переносится в `pack/`.

```text
pack/dpf/building-design/
  BuiltAssetDesignPrinciplesFramework.md         # после стабилизации
  relation-records.md
  source-use-and-refresh-map.md
  acceptance-cases.md
  quality/
    E4DPFDA-BDPF-*.md
    E21-BDPF-patterns-*.md
  patterns/
    BDPF.1-built-asset-system-card.md
    BDPF.2-design-development-method.md
    BDPF.3-design-source-signal-use.md
    BDPF.3A-built-asset-problem-to-structure-flow.md
    BDPF.4-use-concept-record.md
    BDPF.5-system-concept-record.md
    BDPF.6-architecture-question-card.md
    BDPF.6A-candidate-architecture-configurations.md
    BDPF.6B-architecture-characteristic-criteria-and-eval.md
    BDPF.6C-comparison-and-selected-set.md
    BDPF.7-project-architecture-decision.md
    BDPF.7A-architecture-decision-record-projection.md
    BDPF.7B-minimal-decision-use-package.md
    BDPF.8-design-evidence-trace.md
    BDPF.9-design-readiness-gate.md
    BDPF.10-project-documentation-and-bim-projection.md
    BDPF.11-design-method-feedback.md

work/dpf/
  improvement-proposals/
  pfad/
  problem-cards/
  p2w/
  pilots/
    G0-G1-APL-P2S/
  drafts/

platform/
  signal-docs/
  templates/
```

Пока BDPF не стабилизирован, рабочее место лучше держать в `work/`. В `pack/` переносить только те паттерны, которые уже стали source-of-truth доменного знания после acceptance cases, source-use map, PFR records и quality evidence.

---

## 7. Первый пилот применения

Рекомендуемый пилот:

```text
Pilot-P2S-G0G1-APL-001
EntityOfConcern:
  физический ОКС / корпус / участок проектирования

Цель пилота:
  проверить, можно ли из текущих ИК G0/G1 восстановить трассу:
  source signal → architecture structuring need → unknown/candidate structures
  → candidate configurations → comparison → PAD → ПД/BIM projection.
```

Стартовое условие пилота: выбрать один конкретный decision scenario или спор, а не абстрактную полноту документации.

```text
CurrentStateMap:
  currentDecisionOrIssueRef:
  describedHolonRef:
  currentCarrierRefs:
  currentSourceRefs:
  currentRoleAssignmentRefs:
  currentEvidenceRefs:
  currentToolOrRepositoryRefs:
  currentDefectPatternRefs:
  currentRepresentationLossNotes:
  firstP2SQuestion:
  nonUseBoundary:
```

`CurrentStateMap` не является PAD, evidence, gate или work plan. Он фиксирует, из какого текущего carrier/source/role/evidence состояния начинается P2S-восстановление.

Порядок:

0. Создать `CurrentStateMap` для одного текущего decision scenario.
1. Создать `BuiltAssetSystemCard` для одного объекта.
2. Создать `DesignSourceSignalUseRecord` для 5-10 ключевых source signals из текущих ИК G0/G1.
3. Создать `BuiltAssetProblemToStructureFlowCard` и назвать `architectureStructuringNeed`.
4. Создать `UseConceptRecord` для 3-5 ключевых сценариев использования.
5. Создать `SystemConceptRecord` для объекта и существенных подсистем.
6. Создать 2-3 `ArchitectureQuestionCard` по структурам, реально меняющим решение.
7. Создать `CandidateArchitecturePalette` или stop reason, если plurality пока невозможна.
8. Создать `ComparisonBasis` и selected/retained set.
9. Создать `ArchitectureDecisionRelation@Project`.
10. Создать `ArchitectureDecisionRecordProjection` как readable carrier решения.
11. Создать `MinimalDecisionUsePackage`, если нужен компактный пакет чтения уже принятого PAD.
12. Связать selected structures с ПД/BIM/views через `BuiltAssetArchitectureDescriptionUseCard` и `ProjectDocumentationProjection`.
13. Проверить `DesignReadinessGate` с явным `gateProfile`.
14. По итогам экспертного рассмотрения, source change или проектных проверок создать `DesignMethodFeedbackRecord` / `DesignChangeImpactTrace`.

```text
BDPFPilotQualityFrame:
  objectUnderImprovementRef:
    DesignDevelopmentMethodDescription | DPFPatternSlice | PilotDecisionScenario | ProjectDocumentationProjectionPractice
  declaredUse:
  evaluationPurpose:
    floorEvaluation | pilotCalibration | adoptionTelemetry | methodRepair | publicationProjectionRepair
  metricRows:
    - metricId: chainCompleteness
      measuredQuestion: восстановлена ли цепочка source → use concept → system concept → decision → evidence → publication
      evidenceRefs:
      nonAdmissibleUse:
    - metricId: evidenceNotCarrierStatus
      measuredQuestion: evidence поддерживает claim, а не carrier/status
      evidenceRefs:
      nonAdmissibleUse:
    - metricId: roleAssignmentCompleteness
      measuredQuestion: author/reviewer/approver заданы как RoleAssignment refs
      evidenceRefs:
      nonAdmissibleUse:
    - metricId: sourceChangeImpactLatency
      measuredQuestion: как быстро найден suspect decision/projection после source change
      evidenceRefs:
      nonAdmissibleUse:
    - metricId: publicationLinkedToDecision
      measuredQuestion: publication carrier связан с architectureDecisionRef
      evidenceRefs:
      nonAdmissibleUse:
  localTargetValues:
  failureReasonDistribution:
  feedbackRoute:
    designMethodFeedbackRef:
    e23ImprovementCycleRef:
    g11RefreshRef:
```

Метрики DPF-пилота измеряют качество метода сопровождения и полноту предъявления хода. Они не доказывают качество ОКС, не подтверждают PAD, не проводят экспертизу и не заменяют evidence по конкретным claims.

---

## 8. DPF-checklist для проектного решения

Перед передачей проектного решения на экспертное рассмотрение проверить:

- [ ] ОКС назван как целевая система в окружении.
- [ ] Видно, какая польза / эффект ожидается от объекта.
- [ ] Существенные сценарии использования описаны.
- [ ] Системная концепция связана со сценариями.
- [ ] Source signals отделены от исходных carriers и имеют admissible use.
- [ ] Есть `architectureStructuringNeed`, а не прямой скачок от ИД к решению.
- [ ] Есть хотя бы одна unknown/candidate structure или честный stop reason.
- [ ] Архитектурные вопросы выделены до детализации решений.
- [ ] Candidate configurations, criteria/eval и comparison basis отделены от PAD.
- [ ] Выбранное решение оформлено как PAD с selected structures, accepted losses и reopen/source-return conditions.
- [ ] Author/reviewer/approver/publisher заданы через `RoleAssignment` refs или явно указан lower/block.
- [ ] Concerns/viewpoints, accepted losses, residual risks и unresolved source-return conditions отделены от доказательств.
- [ ] ADR/card/ПД/BIM являются projection/publication carriers, а не самим решением.
- [ ] Есть доказательства / обоснования по конкретным claim.
- [ ] Видно, где selected structures отражены в ПД/BIM/views.
- [ ] Gate/readiness имеет явный profile и не подменяет decision или proof.
- [ ] Замечания экспертизы и проектные несоответствия могут быть возвращены не только в правку файла, но и в улучшение метода проектирования.

## 8.1. P2S-checklist для проектного решения

| ID | Проверка |
|---|---|
| `BDPF-P2S-1` | Назван физический ОКС / подсистема как `describedHolonRef`, а не BIM, ПД, чертёж, таблица или согласование. |
| `BDPF-P2S-2` | Назван `boundedContextRef` с lifecycle slice, scope, NQD work state и maturity-полями. |
| `BDPF-P2S-3` | Исходные данные разложены на `sourceSignalRefs`, constraints, `needKind` и source-return conditions. |
| `BDPF-P2S-4` | Есть хотя бы один `unknownStructure` или `candidateStructureKindRef`. |
| `BDPF-P2S-5` | Architecture characteristics отделены от целей, метрик, evidence, eval results и решений. |
| `BDPF-P2S-6` | Есть candidate configurations или явно указан stop reason, почему plurality пока невозможна. |
| `BDPF-P2S-7` | Comparison basis содержит characteristics, evidenceRefs, missingEvidence, protectedTradeOffs и unacceptableLosses. |
| `BDPF-P2S-8` | Project architecture decision оформлен как PAD с selected structures, trade-off, accepted losses и reopen/source-return conditions. |
| `BDPF-P2S-9` | BIM, IFC, ПД, схемы, спецификации и dashboards оформлены как descriptions/views/publications с admissible use. |
| `BDPF-P2S-10` | Work plan, readiness и performed work не подменены проектным решением. |
| `BDPF-P2S-11` | Feedback route ограничен проектированием: expert/design review, междисциплинарная проверка, ПД/BIM consistency, source return, method repair. |
| `BDPF-P2S-12` | Если используется score, расчёт, simulation или экспертное предпочтение, оно не становится решением без comparison/selection/PAD owner. |
| `BDPF-P2S-13` | Source change создаёт suspectness/impact trace, а не автоматический вывод, что PAD неверен или подтверждён. |

---

## 9. Статусы зрелости DPF-артефактов

| Статус | Значение |
|---|---|
| cue | Есть сигнал или рабочая формулировка, но объект ещё не стабилизирован. |
| draft | Есть черновая форма и пример применения. |
| pilot-ready | Можно применять на одном фрагменте проектирования. |
| reviewed | Проверено на реальном или имитированном кейсе. |
| pack-candidate | Содержит доменное знание и может быть перенесено в pack. |
| stable | Используется как source-of-truth. |
| deprecated | Сохранено для трассировки, но не рекомендуется к применению. |

Эти статусы относятся к DPF-артефактам. Они не равны `nqdWorkState`, `decisionMaturity`, готовности ПД, прохождению gate или состоянию проектного решения.

---

## 10. Терминологический минимум

| Термин | Рабочее значение в DPF |
|---|---|
| ОКС | Целевая создаваемая система в окружении, а не только объект в разрешительной документации. |
| Исходные данные | Материалы, которые должны поддерживать проектные вопросы и решения. |
| Source signal | Извлечённый из carrier-а проектно значимый сигнал, который создаёт вопрос, ограничение или структурирующую потребность. |
| Architecture structuring need | Потребность выбрать, уточнить, проверить или вернуть к источнику структуру ОКС. |
| Концепция использования | Описание сценариев, ролей, режимов и конфликтов использования объекта. |
| Концепция системы | Описание состава, функций, границ, интерфейсов, потоков и режимов ОКС. |
| Structure kind | Тип структуры, которую надо рассмотреть для следующего архитектурного хода. |
| Candidate configuration | Конкретный вариант архитектурной конфигурации, ещё не выбранный как PAD. |
| Architecture characteristic | Свойство структуры, которое надо удерживать, измерять или оценивать. |
| Архитектурный вопрос | Вопрос о выбранной структуре объекта, которая меняет несколько решений сразу. |
| PAD / project architecture decision | Commitment по selected structures, trade-offs, accepted losses и условиям пересмотра. |
| ADR / карточка решения | Публикационная проекция PAD, а не само проектное решение. |
| Обоснование | Доказательная связь между claim, evidence и допустимым использованием решения. |
| Проекция в ПД / BIM / views | Представление selected structures в разделах, чертежах, моделях, записках, расчётах и спецификациях. |
| Экспертное замечание | Зафиксированный дефект или вопрос рассмотрения, который может указывать на проблему решения или метода разработки. |

## 10.1. DPF reference and local semantics discipline

FPF-owner: `E.10`, `A.6.5`, `E.4.DPF.DA`.

```text
BDPFReferenceDiscipline:
  stableIdsRequiredFor:
    - sourceSignalRef
    - useConceptRef
    - systemConceptRef
    - architectureQuestionRef
    - candidateConfigurationRef
    - criteriaSetRef
    - comparisonBasisRef
    - selectedSetRef
    - architectureDecisionRef
    - architectureDecisionRecordProjectionRef
    - evidenceTraceRef
    - documentationProjectionRef
    - readinessGateRef
    - feedbackRecordRef
  idDoesNotMean:
    - approval
    - evidence
    - currentness
    - source authority
    - gate passage
    - decision truth
  versionOrEditionBoundary:
  localTermOwner:
  admissibleUse:
  nonAdmissibleUse:
```

ID / Ref нужен для трассировки и currentness-control. ID не доказывает существование, качество, актуальность, согласование, доказанность или допустимость проектного решения.

---

## 11. Минимальная P2W-запись для запуска DPF

```text
P2W-DPF-001

ProblemCardRef:
  PC-ES-DESIGN-METHOD-001

CarriedDistinction:
  Проблема не только в составе ПД или ИК, а в слабом способе разработки проектного решения.

NextFPFUseQuestion:
  Какой доменный метод проектирования ОКС нужен, чтобы экспертное сопровождение могло управлять ходом формирования решений?

RecoveredFPFKindOrRelation:
  U.MethodDescription для способа разработки проектного решения.
  A.2.1 для RoleAssignment в author/reviewer/approver/publisher ролях.
  C.32.P2S для problem-to-structure architecturing flow.
  C.30 / C.30.ASV для selected structures и structural views.
  C.32.PAD / C.32.ADR для проектного архитектурного решения и его projection.
  C.30.AD.BA / E.17 для ПД/BIM/views как descriptions/publications.
  A.10 для claim-specific evidence graph path.
  A.21 для gate profile и readiness decision.
  E.22 / E.23 / G.11 для pilot-quality feedback, improvement loop и currentness refresh.

SelectedBDPFApplication:
  BDPF.2 DesignDevelopmentMethodDescription
  BDPF.3 DesignSourceSignalUseRecord
  BDPF.3A BuiltAssetProblemToStructureFlowCard
  BDPF.4 UseConceptRecord
  BDPF.5 SystemConceptRecord
  BDPF.6 ArchitectureQuestionCard
  BDPF.6A CandidateArchitecturePalette
  BDPF.6B ArchitectureCharacteristicCriteriaSet
  BDPF.6C ComparisonBasis
  BDPF.7 ArchitectureDecisionRelation@Project
  BDPF.7A ArchitectureDecisionRecordProjection
  BDPF.7B MinimalDecisionUsePackage

FirstPilot:
  Pilot-P2S-G0G1-APL-001.

StopCondition:
  Не внедрять как обязательный сервисный регламент, пока не пройден один пилотный фрагмент и не проверена полезность рабочих продуктов.
```

---

## 12. Основное правило развития DPF

Каждое новое расширение DPF добавлять только если оно отвечает на один из вопросов:

1. Какой проектный дефект это предотвращает?
2. Какой ход проектного рассуждения становится видимым?
3. Какой рабочий продукт становится проверяемым?
4. Какой переход в цепочке проектирования становится управляемым?
5. Какое повторяющееся экспертное замечание возвращается в улучшение метода?

Если расширение не отвечает ни на один вопрос, оно не должно попадать в DPF.

---

## 13. Name And Edition Route

```text
NameAndEditionRoute@BuiltAssetDesignPrinciplesFramework:
  publicPackageName: Built Asset Design Principles Framework
  frameworkFamily: Domain Principle Framework
  editionRef: BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4
  localPatternPrefix: BDPF
  legacyAliasPolicy: DPF.* aliases are readable during draft migration but should not be minted for new package records
  editionState: draft v0.4-package-structure
  localUseStatus: locallyUsableWithVisibleLimits / pilot-ready for one bounded P2S decision scenario
  notYetStatus: stable; public/enterprise reliance-bearing DPF package
  currentnessWindow: until FPF Core edition, source pack, pilot evidence, package relation records, or repeated defect evidence changes
```

## 14. DPF Relation Records

```text
PatternFrameworkRelationRecord@BuiltAssetDesignDPF:
  relationId: PFR-BDPF-CORE-DEP-001
  sourceRef: BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4
  targetRef: FPFCorePatternSet@June2026
  relationFunction: Framework edition dependency
  governedUse: BDPF patterns rely on FPF Core holon, context, method/work, architecture, decision, evidence, publication, gate, improvement, and refresh owners
  directGoverningPatternRef: E.4.PFR
  dependencyOrEditionEffect: BDPF depends on Core; Core has no reverse dependency
  blockedStrongerReading: not permission to redefine FPF Core owners
  refreshOrSupersessionCondition: refresh when relevant FPF Core edition changes

PatternFrameworkRelationRecord@BuiltAssetDesignDPF:
  relationId: PFR-BDPF-P2S-SPEC-001
  sourceRef: BDPF.3A, BDPF.6A, BDPF.6B, BDPF.6C, BDPF.7
  targetRef: C.32.P2S, C.32, C.32.PAD
  relationFunction: Specialization and pattern-use support
  governedUse: BDPF narrows problem-to-structure architecturing for built-asset design decisions
  directGoverningPatternRef: C.32.P2S
  dependencyOrEditionEffect: BDPF inherits Core P2S obligations and adds built-asset records/checks
  blockedStrongerReading: source signal does not directly choose a project decision; BDPF does not redefine C.32.P2S
  sourceReturnCondition: return to Core P2S owner when BDPF row tries to govern general architecturing flow
  refreshOrSupersessionCondition: refresh when C.32.P2S slots or owner routes change

PatternFrameworkRelationRecord@BuiltAssetDesignDPF:
  relationId: PFR-BDPF-SOURCE-REUSE-001
  sourceRef: SourceUseAndRefreshMap@BuiltAssetDesignDPF
  targetRef: BDPF.3, BDPF.3A, BDPF.4, BDPF.5, BDPF.6, BDPF.7, BDPF.8, BDPF.11
  relationFunction: Source or decision reuse
  governedUse: source rows support source signals, source-return conditions, evidence limits, and change-impact routes
  directGoverningPatternRef: G.2; G.11 for currentness refresh
  blockedStrongerReading: source rows do not become project decisions, evidence sufficiency, gate passage, or regulatory compliance proof
  sourceReturnCondition: return to G.2 when source kind, source owner, currentness, admissible use, or exact source row is missing
  refreshOrSupersessionCondition: refresh when source basis, regulatory/source currentness, or pilot source defects change

PatternFrameworkRelationRecord@BuiltAssetDesignDPF:
  relationId: PFR-BDPF-AD-BA-PROJECTION-001
  sourceRef: BDPF.10
  targetRef: C.30.AD.BA, C.33, C.34, E.17
  relationFunction: Publication / architecture-description specialization
  governedUse: BDPF uses built-asset architecture descriptions, BIM/IFC/PD/views, and projection records without treating carriers as OKS, PAD, proof, gate, or work
  directGoverningPatternRef: C.30.AD.BA
  blockedStrongerReading: BIM/IFC/PD/dashboard is not the built asset, architecture decision, proof, gate passage, or performed work
  sourceReturnCondition: return to C.33/C.34 when represented structure, captured structure, lost structure, or correspondence is unclear
  refreshOrSupersessionCondition: refresh when C.30.AD.BA, representation practice, or project carrier assumptions change

PatternFrameworkRelationRecord@BuiltAssetDesignDPF:
  relationId: PFR-BDPF-EVIDENCE-GATE-001
  sourceRef: BDPF.8, BDPF.9
  targetRef: A.10, B.3, A.21, A.15.5
  relationFunction: Evidence, assurance, and gate boundary relation
  governedUse: keep claim-specific evidence, assurance, readiness, and work-entry/project-review gates separate from project decision and publication carriers
  directGoverningPatternRef: A.10 for evidence; A.21 for gate
  blockedStrongerReading: calculation, model, BIM-clash, score, gate pass, or expert preference is not PAD or proof of all claims
  sourceReturnCondition: return to A.10/B.3/A.21 when claim scope, evidence path, freshness, gate profile, or gate decision is missing
  refreshOrSupersessionCondition: refresh when evidence, source currentness, gate profile, or claim scope changes

PatternFrameworkRelationRecord@BuiltAssetDesignDPF:
  relationId: PFR-BDPF-FEEDBACK-IMPROVEMENT-001
  sourceRef: BDPF.11, DesignMethodFeedbackRecord, DesignChangeImpactTrace
  targetRef: E.22, E.23, G.11, C.32.FAIL, A.15
  relationFunction: Method improvement and source-return relation
  governedUse: recurring expert/design-review defects and source changes return to method, PAD repair, evidence refresh, description/source return, or package refresh
  directGoverningPatternRef: E.23; G.11 when currentness changes
  blockedStrongerReading: an expert comment or impact trace does not prove the PAD false or true by itself
  sourceReturnCondition: return to owner-specific repair route when suspect decisions, selected structures, evidence traces, or projections are not named
  refreshOrSupersessionCondition: refresh when repeated defect pattern or source-change impact cannot be handled by current BDPF records
```

## 15. Source Use And Refresh Map

```text
SourceUseAndRefreshMap@BuiltAssetDesignDPF:
  mapUse: support DPF source-signal extraction, domain pattern selection, evidence boundaries, and refresh route
  sourceRows:
    - sourceFamily: FPF Core
      sourceUse: Core owners and pattern obligations for holons, P2S, architecture, PAD, evidence, gates, publication, improvement
      affectsPatterns: BDPF.1..BDPF.11
      nonAdmissibleUse: not domain regulation and not proof that built-asset design solution is correct
      refreshCondition: FPF Core edition changes
    - sourceFamily: project source documents and requirements
      examples: ТЗ, технологическое задание, требования эксплуатации, ТУ, изыскания, обследования, замечания, ГПЗУ, ИРД
      sourceUse: source signals and source-return conditions
      affectsPatterns: BDPF.3, BDPF.3A, BDPF.4, BDPF.5, BDPF.6, BDPF.11
      nonAdmissibleUse: source document does not choose project decision by itself
      refreshCondition: source edition, owner, or condition changes
    - sourceFamily: regulatory and compliance sources
      sourceUse: constraints, assumptions, compliance claim owners, evidence requirements
      affectsPatterns: BDPF.3, BDPF.6B, BDPF.7, BDPF.8, BDPF.9
      nonAdmissibleUse: BDPF does not replace regulations and source row is not compliance proof
      refreshCondition: source currentness or applicability changes
    - sourceFamily: PD/BIM/IFC/views/project carriers
      sourceUse: architecture description, representation, projection, captured/lost structure
      affectsPatterns: BDPF.10, BDPF.11
      nonAdmissibleUse: carrier is not OKS, PAD, proof, gate, or performed work
      refreshCondition: carrier edition, model scope, represented/lost structure, or checked rule spec changes
```

## 16. Acceptance Cases

```text
AcceptanceCase-BDPF-01-SitePlacement:
  sourcePressure: ГПЗУ / участок / посадка
  forcedDistinction: source signal constrains spatial/interface structures but does not choose the project decision
  expectedRoute: BDPF.3 -> BDPF.3A -> BDPF.6 -> BDPF.6C -> BDPF.7 -> BDPF.10

AcceptanceCase-BDPF-02-GeotechnicalStructural:
  sourcePressure: изыскания -> конструктивная схема
  forcedDistinction: geotechnical evidence constrains load-bearing structures and evidence scope, not architecture decision by itself
  expectedRoute: BDPF.3 -> BDPF.6B -> BDPF.6C -> BDPF.7 -> BDPF.8

AcceptanceCase-BDPF-03-MEPCapacity:
  sourcePressure: ТУ / инженерные мощности -> engineering systems structure
  forcedDistinction: capacity signal creates interface/control/engineering structure questions and source-return conditions
  expectedRoute: BDPF.3 -> BDPF.5 -> BDPF.6 -> BDPF.7 -> BDPF.10

AcceptanceCase-BDPF-04-FireEvacuation:
  sourcePressure: сценарии эвакуации -> flow/control structures
  forcedDistinction: scenario source is not proof; UseConceptRecord organizes scenario claims for system and architecture questions
  expectedRoute: BDPF.4 -> BDPF.5 -> BDPF.6B -> BDPF.8 -> BDPF.9

AcceptanceCase-BDPF-05-ConstructionPhasing:
  sourcePressure: ограничения стройплощадки -> construction method structure
  forcedDistinction: construction realization need affects candidate structures and work entry but does not replace project design decision
  expectedRoute: BDPF.3 -> BDPF.3A -> BDPF.6A -> BDPF.6C -> BDPF.9

AcceptanceCase-BDPF-06-ReconstructionExistingAsset:
  sourcePressure: обследование существующего ОКС -> unknown/current/expected structures
  forcedDistinction: обследование is carrier/evidence input; current structure and expected structure must be separated before PAD
  expectedRoute: BDPF.1 -> BDPF.3 -> BDPF.3A -> BDPF.5 -> BDPF.7 -> BDPF.10

AcceptanceCase-BDPF-07-SourceChangeImpact:
  sourcePressure: изменение source signal -> suspect decisions/projections/evidence
  forcedDistinction: impact trace creates suspectness and owner route, not automatic proof that PAD is false or true
  expectedRoute: BDPF.3 -> BDPF.11 -> BDPF.7/BDPF.8/BDPF.10 repair as needed
```

## 17. Refresh Route

Use this route when the BDPF package is already applied and one of its source, Core, pattern, pilot, or carrier assumptions changes.

1. Return to `G.2` when a load-bearing source line is absent, stale, too narrow, contradicted, or used beyond admissible use.
2. Return to `BDPF.3` / `BDPF.3A` when source signals, needKind, source-return conditions, or affected structures change.
3. Return to `BDPF.6A/6B/6C/7` when candidate palette, criteria/eval, comparison, selected set, accepted losses, or PAD reopen conditions change.
4. Return to `BDPF.8` when evidence freshness, claim scope, evidence path, rival explanation, or reliability notes change.
5. Return to `BDPF.10` when PD/BIM/views lose, distort, or fail to represent selected/expected structures.
6. Return to `BDPF.11` when expert/design review, interdisciplinary coordination, source return, or carrier consistency defects repeat.
7. Use `E.22` when the improvement question is underframed: purpose, floor, protected trade-offs, evidence basis, result form, cost/risk, and expected next move are not explicit.
8. Use `E.23` for exact changed package/pattern/method/projection versions with re-evaluation planned.
9. Use `G.11` refresh when FPF Core edition, source pack, source currentness, pilot evidence, or package relation records change.
10. Keep project carriers, checklists, dashboards, and generated summaries outside pattern bodies unless their owner relation is explicit.

## 18. Package Quality Result

```text
DPFPackageAdequacyEvaluation@BuildingDesignDPF:
  evaluationId: E4DPFDA-BDPF-2026-07-02
  evaluatedPackageRef: BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4
  packageKind: all-in-one-publication-carrier / domain-principle-framework seed
  declaredDomainOrLocalContext: экспертное сопровождение проектирования зданий и сооружений / ОКС
  declaredUse: сделать ход разработки проектного решения явным, проверяемым и улучшаемым
  status: repairBeforeDPFUse for public/enterprise package use
  localStatus: locallyUsableWithVisibleLimits for one bounded P2S pilot
```

| Coordinate | Value | Evidence locus | Repair / disposition |
|---|---:|---|---|
| `D1DomainScopeAndUseAdequacy` | 3 | Title/front matter, sections 0-1, package stewardship | Keep filled records current. |
| `D2DidacticEntryAndAdoptionAdequacy` | 3 | ToC, Readme, first practical entries, Pattern Index | Add worked examples after pilot evidence. |
| `D3ScalableFormalityAndAssurancePathAdequacy` | 4 | BDPF.2-11 typed records | No proposal for bounded pilot. |
| `D4CoreDependencyAndDomainBoundaryAdequacy` | 3 | FrameworkEditionDependencyRecord, PFR records | Refresh on FPF Core edition/source changes. |
| `D5PackageFormLayeringAndRelationAdequacy` | 3 | Stewardship, dependency, PFAD, six PFR records | E.21 pattern evidence still lower/not materialized. |
| `D6DomainLexiconAndKindSettlementAdequacy` | 4 | Main distinctions, term minimum, reference discipline, BDPF prefix | Keep legacy aliases temporary. |
| `D7PracticeUtilityAndProblemResolutionAdequacy` | 4 | BDPF.1-11 and acceptance cases | Add worked project examples before stable. |
| `D8HeterogeneousCaseAndTransferAdequacy` | 3 | Seven acceptance cases | Replace synthetic cases with pilot evidence. |
| `D9EditionStateAndCurrentnessAdequacy` | 3 | Name/edition route, maturity statuses, refresh route | Add supersession/deprecation record when edition changes. |
| `D10ImprovementAndRefreshAdequacy` | 3 | BDPF.11, pilot quality frame, Refresh Route | Use E.22/E.23 after first pilot. |
| `D11DomainSoTAAlignmentAdequacy` | 3 | SourceUseAndRefreshMap | Add source-use payload/adopted-rejected readings before pack-candidate. |

## 19. Closure Tests For Next Version

```text
CC-BDPF-PKG-1: ToC, Readme, Preface, Package Carrier Structure-Account, Boundary/Owner Routing, Pattern Index exist before pattern bodies.
CC-BDPF-PKG-2: DPFPackageStewardshipRecord, FrameworkEditionDependencyRecord, PFAD, and at least six PFR records are filled.
CC-BDPF-PKG-3: Pattern ids are package-local BDPF.*, with legacy alias table.
CC-BDPF-PKG-4: SourceUseAndRefreshMap exists and at least one source row affects each of BDPF.3, 3A, 4, 5, 6, 7, 8, 10, 11.
CC-BDPF-PKG-5: Refresh Route names G.2, G.11, E.22, E.23, and BDPF owner routes.
CC-BDPF-PKG-6: At least five heterogeneous acceptance cases exist and each forces a different source/structure/decision/projection/feedback issue.
CC-BDPF-PKG-7: E.4.DPF.DA table is present with values, evidence loci, and repairs for all D1..D11.
CC-BDPF-PKG-8: E.21-lite result remains lower/not-yet-materialized and must not be overclaimed.
CC-BDPF-PKG-9: No source, carrier, gate, score, dashboard, approval, or expert comment is allowed to become PAD/evidence/proof/work by wording.
```
