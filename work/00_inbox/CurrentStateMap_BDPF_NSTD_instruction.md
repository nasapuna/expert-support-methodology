# Инструкция: как собрать `CurrentStateMap` для BA-P2S-пилота по `DPF-building-design.md`

> **Назначение файла:** рабочая инструкция и форма носителя для первого шага BA-P2S-пилота: зафиксировать текущее состояние одного проектного decision scenario до восстановления цепочки `source signal → architectureStructuringNeed → unknown/candidate structures → candidate configurations → comparison → PAD → ПД/BIM projection`.
>
> **Основание:** `DPF-building-design.md@draft-v0.4`, `NarrativizationAndNarrativeStudiesPrinciplesFramework@2026-06-30`, `FPF Core@June2026`.
>
> **Статус носителя:** локальный рабочий carrier для пилота; не source-of-truth DPF-пакета.

---

## 0. Что такое `CurrentStateMap`

`CurrentStateMap` — это стартовая карта текущего состояния одного проектного вопроса, спора или решения. Она отвечает не на вопрос «какое решение правильно?», а на вопрос:

```text
Из какого текущего состояния carriers / sources / roles / evidence / tools / defects / representation losses
мы начинаем P2S-восстановление проектного решения?
```

Карта нужна до `BuiltAssetSystemCard`, `DesignSourceSignalUseRecord`, `BuiltAssetProblemToStructureFlowCard`, `ArchitectureQuestionCard`, `ComparisonBasis` и `ArchitectureDecisionRelation@Project`.

### Жёсткая граница

`CurrentStateMap` **не является**:

- PAD / `ArchitectureDecisionRelation@Project`;
- evidence / доказательством;
- gate / readiness decision;
- work plan / планом работ;
- approval / согласованием;
- proof качества ОКС;
- checklist комплектности ПД;
- BIM-стандартом или регламентом экспертизы.

Её задача — сделать текущий вход в P2S-переход проверяемым и воспроизводимым.

---

## 1. Как применять Narrativization DPF при сборке `CurrentStateMap`

`Narrativization-and-Narrative-Studies-Principles-Framework.md` здесь используется не для «красивого рассказа», а как дисциплина превращения разрозненной структуры источников в читаемый route:

```text
selected source structures
→ ordered reader route
→ preserved relations
→ lost / coarsened relations
→ source-return conditions
```

Для `CurrentStateMap` это значит:

1. **Сначала source structure, потом изложение.** Не начинайте с «ситуация плохая» или «надо принять решение». Сначала назовите carriers, sources, роли, evidence, инструменты, дефекты и потери представления.
2. **Один decision scenario.** Карта не описывает весь проект и не проверяет всю ПД. Она фиксирует один спор, одно решение, одну подсистему или один участок проектирования.
3. **Route family = architecture-mediated.** В большинстве случаев `CurrentStateMap` ведёт к архитектурной работе: структурам ОКС, структурным видам, кандидатным конфигурациям, PAD и проекциям в ПД/BIM.
4. **Ordering rule должен быть явным.** Порядок чтения карты не должен выглядеть как причинность, доказательство или порядок работ. Укажите, что это порядок восстановления: например `source-intake order`, `decision-memory order`, `representation-loss order`.
5. **Потери и source return обязательны.** Если BIM, ПД, замечание или таблица скрывают selected/expected structure, запишите это как `currentRepresentationLossNotes`, а не исправляйте молча стилем.
6. **Engagement не добавляет authority.** Убедительное описание текущей ситуации не доказывает решение, не подтверждает evidence и не проводит gate.

---

## 2. Когда создавать `CurrentStateMap`

Создавайте карту, когда выполняются все условия:

- есть текущий проектный спор, решение, замечание, несогласованность или участок неясности;
- есть carriers: ПД, BIM/IFC, таблицы, ТЗ, ИРД, ГПЗУ, ТУ, расчёты, замечания, issue tracker, CDE, dashboard, протоколы;
- ещё не восстановлена цепочка от source signals к архитектурной структуре и decision owner;
- команда рискует перескочить от исходных данных или замечания сразу к проектному решению.

Не создавайте карту на «весь проект» без decision scenario. Это даст архив материалов, но не P2S-вход.

---

## 3. Минимальная форма из DPF

Базовая форма `CurrentStateMap`:

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

Эти 11 полей можно заполнять в короткой форме. Для пилота лучше использовать расширенный carrier ниже.

---

## 4. Расширенная форма носителя `CurrentStateMapCarrier@Project`

Используйте эту форму как Markdown-носитель в `work/dpf/pilots/<pilot-id>/current-state-map-<scenario-id>.md`.

```text
CurrentStateMapCarrier@Project:
  carrierId:
  carrierKind: current-state-map-publication-carrier
  carrierVersion:
  createdAt:
  createdByRoleAssignmentRef:
  reviewedByRoleAssignmentRefs:
  pilotRef:
  projectRef:
  declaredUse:
  intendedReaderOrOperator:
  sourceDPFRefs:
    - DPF-building-design.md@draft-v0.4
    - NarrativizationAndNarrativeStudiesPrinciplesFramework@2026-06-30
    - FPFCore@June2026

  narrativeRouteDiscipline:
    routeFamily: architecture-mediated
    sourceTemporalPosture: current design-state reconstruction
    orderingRuleKind:
      source-intake | decision-memory | representation-loss | mixed
    orderRationale:
    preservedSourceRelations:
    foregroundedSourceRelations:
    coarsenedOrLostSourceRelations:
    sourceReturnCondition:
    blockedRouteOverread:

  currentStateMap:
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

  nextOwnerRouting:
    likelyNextBDPFPatternRef:
    neighboringFPFOwnerRefs:
    stopOrReturnReason:

  qualityCheck:
    oneScenarioOnly:
    describedHolonNotCarrier:
    sourceSignalsSeparatedFromCarriers:
    rolesAreAssignmentsNotTitles:
    evidenceIsClaimSpecific:
    representationLossVisible:
    firstP2SQuestionNamesStructure:
    nonUseBoundaryPresent:
    readyForNextP2SStep:

  appendices:
    carrierInventoryTableRef:
    sourceSignalCandidateTableRef:
    roleAssignmentTableRef:
    evidenceCandidateTableRef:
    representationLossTableRef:
```

### Что важно про форму

`CurrentStateMapCarrier@Project` — это **publication carrier**, а не новый FPF `U.*` kind. Он помогает собрать и прочитать стартовое состояние. Он не создаёт решение и не доказывает claim.

---

## 5. Пошаговая процедура сборки

### Шаг 1. Выберите один decision scenario

Заполните рабочую строку:

```text
ScenarioSelection:
  projectRef:
  scenarioId:
  shortIssueName:
  whyThisScenarioNow:
  affectedOKSOrSubsystem:
  currentDecisionPressure:
  excludedScope:
```

Хорошие формулировки:

- `ISSUE-GPZU-PLACEMENT-001`: спор о посадке корпуса в границах ГПЗУ и пожарных проездов.
- `ISSUE-MEP-CAPACITY-002`: неясно, достаточно ли существующих ТУ и инженерных мощностей для выбранной функциональной схемы.
- `ISSUE-TECH-FLOW-003`: технологическое задание задаёт потоки, но в ПД не видно, какая функционально-планировочная структура их поддерживает.

Плохие формулировки:

- `Проверить весь проект`.
- `Разобраться с BIM`.
- `Подготовиться к экспертизе`.
- `Понять, всё ли правильно`.

Плохие формулировки слишком широкие: они не указывают decision scenario и не задают первый P2S-вопрос.

---

### Шаг 2. Назовите `describedHolonRef`

`describedHolonRef` — это физический ОКС, корпус, зона, подсистема или участок проектирования, а не файл, модель, раздел ПД или замечание.

Форма:

```text
describedHolonRef:
  holonId:
  holonName:
  holonKind: builtAsset | building | facility | zone | subsystem | site-slice | other
  lifecycleSlice: concept | schematic-design | design-documentation | working-documentation | construction-prep | other
  boundedContextRef:
  holonScope:
  environmentContext:
  excludedHolonScope:
```

Хорошо:

```text
describedHolonRef:
  holonId: OKS-G1-CORPUS-A
  holonName: корпус G1 / участок А проектирования
  holonKind: building
  lifecycleSlice: design-documentation
  boundedContextRef: Project-G1.DesignSupport.2026-07
  holonScope: корпус, посадка на участке, внешние инженерные подключения и пожарные проезды
  environmentContext: участок, красные линии, ЗОУИТ, существующие сети, соседние корпуса
  excludedHolonScope: эксплуатация после ввода; смежный корпус G2
```

Плохо:

```text
describedHolonRef: BIM-модель G1.rvt
```

Почему плохо: BIM-модель — carrier/description, а не ОКС.

---

### Шаг 3. Соберите `currentCarrierRefs`

`currentCarrierRefs` — это carriers, descriptions, views или evidence carriers, через которые видна текущая ситуация.

Форма строки carrier inventory:

```text
CarrierInventoryRow:
  carrierRef:
  carrierKind:
    PDSection | BIMModel | IFC | Drawing | Table | CalculationFile |
    ExpertComment | IssueTrackerItem | Protocol | Dashboard | CDEFolder |
    Register | Email | MeetingNote | Other
  titleOrName:
  versionOrDate:
  ownerOrPublisher:
  locationOrRepositoryRef:
  whatItShows:
  whatItDoesNotShow:
  admissibleUseInCurrentStateMap:
  nonAdmissibleUse:
  sourceReturnCondition:
```

Минимально собрать 5–15 carriers. Для каждого carrier обязательно указать `whatItDoesNotShow` и `nonAdmissibleUse`.

Пример:

```text
CarrierInventoryRow:
  carrierRef: CARRIER-GPZU-2026-02-14-PDF
  carrierKind: SourceDocument
  titleOrName: ГПЗУ участка 77:...
  versionOrDate: 2026-02-14
  ownerOrPublisher: уполномоченный орган / technical customer copy
  locationOrRepositoryRef: CDE:/00_input/GPZU/...
  whatItShows: границы участка, допустимые параметры, красные линии, зоны ограничений
  whatItDoesNotShow: не выбирает объёмно-планировочное решение и не задаёт candidate configuration
  admissibleUseInCurrentStateMap: source carrier for `sitePlacementNeed`
  nonAdmissibleUse: not PAD, not proof of selected layout, not gate passage
  sourceReturnCondition: return to source owner if boundaries, issue date, or regulatory context are disputed
```

---

### Шаг 4. Соберите `currentSourceRefs` и отделите source carrier от source signal

`currentSourceRefs` должны показывать не только документы, но и извлечённые source signals.

Форма:

```text
SourceSignalCandidateRow:
  sourceRef:
  sourceCarrierRef:
  sourceKind:
    GPZU | TZ | TechnicalAssignment | EngineeringSurvey | TechnicalConnectionCondition |
    OperationRequirement | SurveyReport | ExistingAssetRegister | BIMorIFCSource |
    ExpertComment | NormativeReference | Other
  issueDateOrVersion:
  extractedSignal:
  candidateNeedKind:
    regulatoryConstraintNeed | sitePlacementNeed | geotechnicalOrStructuralNeed |
    engineeringCapacityNeed | useScenarioNeed | constructionRealizationNeed |
    informationRelianceNeed | expertReviewNeed | other
  affectedHolonOrScope:
  affectedStructureKindCandidates:
  supportedQuestion:
  admissibleUse:
  nonAdmissibleUse:
  freshnessBoundary:
  missingOrAmbiguousData:
  sourceReturnCondition:
  likelyReceivingPatternRef: BDPF.3 | BDPF.3A | BDPF.4 | BDPF.5 | BDPF.6 | BDPF.8 | BDPF.11 | other
```

Правило: source signal создаёт вопрос, ограничение или structuring need. Он не выбирает проектное решение.

Пример:

```text
SourceSignalCandidateRow:
  sourceRef: SIG-GPZU-FIRE-ACCESS-001
  sourceCarrierRef: CARRIER-GPZU-2026-02-14-PDF
  sourceKind: GPZU
  issueDateOrVersion: 2026-02-14
  extractedSignal: пожарный проезд должен сохранять нормативную ширину и разворотную геометрию в зоне посадки корпуса
  candidateNeedKind: sitePlacementNeed
  affectedHolonOrScope: OKS-G1-CORPUS-A / участок посадки
  affectedStructureKindCandidates:
    - MaterialSpatialStructure
    - TransformationFlowStructure
    - ModuleInterfaceStructure
  supportedQuestion: какие spatial / external-flow структуры становятся ограниченными при текущей посадке корпуса?
  admissibleUse: вход в BDPF.3A для architectureStructuringNeed
  nonAdmissibleUse: не выбирает вариант посадки; не подтверждает ПД; не является gate
  freshnessBoundary: пока актуальна версия ГПЗУ и не изменены ограничения участка
  missingOrAmbiguousData: нет проверенной схемы движения спецтехники в текущей BIM/ПД проекции
  sourceReturnCondition: при споре о границах или проездах вернуться к GPZU/source owner и актуальным нормативным constraints
  likelyReceivingPatternRef: BDPF.3A
```

---

### Шаг 5. Соберите `currentRoleAssignmentRefs`

`currentRoleAssignmentRefs` фиксируют, кто сейчас автор, reviewer, approver, publisher, coordinator или source owner **в конкретном bounded context и window**. Должность или подпись без assignment не достаточны.

Форма:

```text
RoleAssignmentCandidateRow:
  roleAssignmentRef:
  holderRef:
  roleRef:
  boundedContextRef:
  assignmentWindow:
  evidenceOrSourceRef:
  relevantToScenarioBecause:
  nonAdmissibleUse:
  missingAssignmentData:
```

Пример:

```text
RoleAssignmentCandidateRow:
  roleAssignmentRef: RA-G1-GIP-REVIEWER-2026-07
  holderRef: Ivanov-AA
  roleRef: DesignDecisionReviewer
  boundedContextRef: Project-G1.DesignSupport.2026-07
  assignmentWindow: 2026-07-01..2026-07-31
  evidenceOrSourceRef: protocol-2026-07-01-role-matrix
  relevantToScenarioBecause: reviewer for placement and source-signal interpretation before P2S handoff
  nonAdmissibleUse: role assignment is not approval, not evidence of PAD, not proof of review work completion
  missingAssignmentData: approval role assignment not yet recovered
```

---

### Шаг 6. Соберите `currentEvidenceRefs`

`currentEvidenceRefs` — только claim-specific evidence candidates. Не пишите «есть расчёт» без claim.

Форма:

```text
EvidenceCandidateRow:
  evidenceRef:
  evidenceCarrierRef:
  claimCandidateRef:
  claimText:
  claimScope:
  evidenceKind:
    calculation | model | normativeCheck | simulation | comparison |
    expertJudgement | sourceDocument | fieldData | issueRecord |
    reviewSessionResult | acceptedDeviation | other
  evidenceProducingWorkRef:
  evidenceInterpretingRoleAssignmentRef:
  admissibleUse:
  nonAdmissibleUse:
  freshnessOrTimeWindow:
  reliabilityNotes:
  unresolvedEvidenceGap:
  likelyReceivingPatternRef: BDPF.8 | A.10 | B.3 | BDPF.6B | other
```

Пример:

```text
EvidenceCandidateRow:
  evidenceRef: EVID-FIRE-ACCESS-SKETCHCHECK-001
  evidenceCarrierRef: CARRIER-GENPLAN-DWG-2026-06-30
  claimCandidateRef: CLAIM-FIRE-ACCESS-GEOMETRY-001
  claimText: текущая схема генплана оставляет непрерывный пожарный проезд вдоль фасада F1
  claimScope: только участок посадки корпуса G1, версия генплана 2026-06-30
  evidenceKind: model
  evidenceProducingWorkRef: unknown
  evidenceInterpretingRoleAssignmentRef: RA-FIRE-REVIEWER-2026-07 or missing
  admissibleUse: candidate evidence gap marker for BDPF.8
  nonAdmissibleUse: не доказывает весь PAD, не подтверждает эвакуацию, не проводит readiness gate
  freshnessOrTimeWindow: до изменения генплана или BIM-модели
  reliabilityNotes: проверка визуальная, без трассировки к нормативному расчёту
  unresolvedEvidenceGap: нужен claim-specific check и reviewer role assignment
  likelyReceivingPatternRef: BDPF.8
```

---

### Шаг 7. Соберите `currentToolOrRepositoryRefs`

Инструменты и репозитории нужны для трассировки, но не дают truth/evidence/decision сами по себе.

Форма:

```text
ToolOrRepositoryRow:
  toolOrRepositoryRef:
  kind: CDE | BIMAuthoringTool | IssueTracker | CalculationTool | DocumentRepository | Dashboard | Other
  locationOrAccessRef:
  versionPolicy:
  relevantCarrierRefs:
  relevantSourceRefs:
  whatCanBeRecovered:
  whatIsLostOrNotCaptured:
  nonAdmissibleUse:
  sourceReturnCondition:
```

Пример:

```text
ToolOrRepositoryRow:
  toolOrRepositoryRef: CDE-G1-PROJECTWISE
  kind: CDE
  locationOrAccessRef: ProjectWise:/G1/
  versionPolicy: controlled upload with revision labels; role ownership partially missing
  relevantCarrierRefs:
    - CARRIER-GENPLAN-DWG-2026-06-30
    - CARRIER-BIM-G1-2026-07-01
  whatCanBeRecovered: carrier versions and publication dates
  whatIsLostOrNotCaptured: why selected structure changed; which source signal triggered the change
  nonAdmissibleUse: repository status is not approval, evidence, PAD, or gate
  sourceReturnCondition: if version lineage is incomplete, return to publication owner and issue tracker
```

---

### Шаг 8. Зафиксируйте `currentDefectPatternRefs`

`currentDefectPatternRefs` — повторяемые дефектные паттерны текущего состояния. Это не обвинение и не root cause proof. Это recognition material для следующего owner.

Типовой классификатор:

| Defect pattern | Симптом | Следующий owner |
|---|---|---|
| `sourceJumpToDecision` | исходные данные используются как будто они уже выбрали решение | `BDPF.3`, `BDPF.3A`, `BDPF.6A`, `BDPF.6C`, `BDPF.7` |
| `carrierAsDecision` | ПД/BIM/таблица выглядит как решение | `BDPF.7`, `BDPF.7A`, `BDPF.10`, `E.17` |
| `evidenceAsGeneralProof` | расчёт/модель «обосновывает решение вообще» | `BDPF.8`, `A.10`, `B.3` |
| `roleLabelAsApproval` | должность, подпись или статус читаются как assignment/approval | `A.2.1`, `BDPF.2`, `BDPF.7` |
| `hiddenArchitectureStructuringNeed` | не видно, какую структуру затрагивает сигнал | `BDPF.3A`, `BDPF.6` |
| `representationLossHidden` | selected/expected structure потеряна в ПД/BIM/views | `BDPF.10`, `C.33`, `C.30.AD.BA` |
| `comparisonCollapsedToScore` | варианты сведены к одному score без trade-offs | `BDPF.6B`, `BDPF.6C` |
| `readinessAsProof` | readiness/gate используется как доказательство | `BDPF.9`, `A.21`, `BDPF.8` |
| `expertCommentAsRootCause` | замечание эксперта принято за причину дефекта | `BDPF.11`, `DesignChangeImpactTrace` |

Форма:

```text
DefectPatternRow:
  defectPatternRef:
  defectPatternKind:
  observedInCarrierRefs:
  observedSymptom:
  suspectedWeakTransition:
  notYetClaimed:
  likelyReceivingPatternRef:
  repairOrSourceReturnHint:
```

---

### Шаг 9. Запишите `currentRepresentationLossNotes`

Это NSTD-style loss account для ПД/BIM/views. Нужно указать, какая структура не прошла в carrier или прошла с потерями.

Форма:

```text
RepresentationLossNote:
  lossNoteRef:
  carrierOrViewRef:
  sourceOrDecisionMemoryRef:
  affectedStructureKindRef:
  selectedOrExpectedOrUnknownStructure:
  whatIsPreserved:
  whatIsCoarsenedOrLost:
  readerMisreadRisk:
  sourceReturnCondition:
  likelyReceivingPatternRef: BDPF.10 | C.33 | C.30.AD.BA | BDPF.11 | other
```

Пример:

```text
RepresentationLossNote:
  lossNoteRef: LOSS-GPZU-FIRE-ACCESS-BIM-001
  carrierOrViewRef: CARRIER-BIM-G1-2026-07-01
  sourceOrDecisionMemoryRef: SIG-GPZU-FIRE-ACCESS-001
  affectedStructureKindRef: TransformationFlowStructure
  selectedOrExpectedOrUnknownStructure: expected external emergency vehicle flow around corpus G1
  whatIsPreserved: габаритная зона проезда показана в 2D DWG
  whatIsCoarsenedOrLost: в BIM не показаны проверенные траектории, радиусы разворота и связь с selected structure
  readerMisreadRisk: reviewer may read visible road geometry as proof of fire-access adequacy
  sourceReturnCondition: return to source signal, normative check, and BDPF.8 evidence trace before reliance
  likelyReceivingPatternRef: BDPF.10
```

---

### Шаг 10. Сформулируйте `firstP2SQuestion`

`firstP2SQuestion` — главный выход `CurrentStateMap`. Он должен переводить текущее состояние в следующий P2S-владелец.

Формула:

```text
firstP2SQuestion:
  Given <source signals / current carriers / observed defect>,
  which <unknown/candidate/selected/expected/represented structure> of <describedHolonRef>
  is under pressure,
  and which <BDPF/FPF owner> must receive the next claim?
```

Русская рабочая форма:

```text
Какой source signal из <carrier/source> создаёт какую architectureStructuringNeed
для какой структуры <describedHolonRef>,
и какой следующий owner должен принять claim: BDPF.3A, BDPF.6, BDPF.6A, BDPF.6C, BDPF.7, BDPF.8, BDPF.10 или BDPF.11?
```

Хорошо:

```text
firstP2SQuestion:
  Как source signals из ГПЗУ и текущей схемы генплана создают `sitePlacementNeed`
  для MaterialSpatialStructure и TransformationFlowStructure корпуса G1,
  и какие candidate configurations надо сформировать до PAD по посадке корпуса?
```

Плохо:

```text
firstP2SQuestion:
  Правильно ли посажен корпус?
```

Почему плохо: вопрос перескакивает к оценке решения, не называет source signals, structure kind и next owner.

---

### Шаг 11. Запишите `nonUseBoundary`

Используйте жёсткую формулу:

```text
nonUseBoundary:
  CurrentStateMap is not PAD, not evidence, not gate, not work plan, not approval,
  not proof of design correctness, not PD completeness check, and not regulatory compliance proof.
  It is admissible only as starting-state carrier for P2S reconstruction of one declared decision scenario.
```

Русская форма:

```text
nonUseBoundary:
  Эта CurrentStateMap не принимает проектное решение, не доказывает claim,
  не подтверждает готовность к экспертизе, не заменяет ПД/BIM/views,
  не является work plan и не подтверждает соответствие нормам.
  Она допустима только как стартовый carrier для восстановления P2S-цепочки по одному decision scenario.
```

---

## 6. Как выбрать порядок изложения внутри носителя

Для `CurrentStateMap` допустимы три обычных ordering rules.

| Ordering rule | Когда выбирать | Что сохраняет | Что теряет или ослабляет |
|---|---|---|---|
| `source-intake` | Когда главная неясность в исходных данных и source signals | связь carrier → source signal → needKind | decision memory и trade-off могут быть не видны |
| `decision-memory` | Когда уже заявлено решение, но неясно почему оно принято | связь спор/решение → основания → missing links | может создать ложное впечатление, что решение уже PAD |
| `representation-loss` | Когда ПД/BIM/views скрывают selected/expected structures | потери переноса в carriers | может недопоказать source signals и roles |
| `mixed` | Когда нужно удержать несколько маршрутов | несколько отношений чтения | выше риск спутать порядок чтения с доказательством |

В носителе укажите:

```text
narrativeRouteDiscipline:
  orderingRuleKind: source-intake
  orderRationale: эксперт должен сначала увидеть carriers и extracted source signals, затем дефект перехода к structure need
  preservedSourceRelations:
    - carrier -> extractedSignal
    - extractedSignal -> candidateNeedKind
    - candidateNeedKind -> affectedStructureKindCandidates
  coarsenedOrLostSourceRelations:
    - full decision rationale not yet reconstructed
    - evidence sufficiency not yet evaluated
  blockedRouteOverread:
    - order of sections is not work sequence, not proof order, not approval route
```

---

## 7. Field-by-field краткая шпаргалка

| Поле `CurrentStateMap` | Что писать | Что не писать |
|---|---|---|
| `currentDecisionOrIssueRef` | один ref на спор, issue, decision pressure | весь проект, всю ПД, общий аудит |
| `describedHolonRef` | физический ОКС/корпус/подсистема/участок | BIM, ПД, файл, замечание |
| `currentCarrierRefs` | carriers с версиями, владельцами, use boundary | «есть ПД», «есть BIM» без версии и границы |
| `currentSourceRefs` | source carriers + extracted source signals | исходные документы как будто они уже evidence или decision |
| `currentRoleAssignmentRefs` | holder + role + context + window | должность, подпись, статус без assignment |
| `currentEvidenceRefs` | claim-specific evidence candidates и gaps | «расчёт есть, значит обосновано» |
| `currentToolOrRepositoryRefs` | CDE/BIM/issue tracker как места восстановления | tool status as approval/evidence/gate |
| `currentDefectPatternRefs` | наблюдаемые дефектные переходы | root cause proof без проверки |
| `currentRepresentationLossNotes` | preserved/lost/coarsened structure in carriers | «в модели всё видно» без source-return |
| `firstP2SQuestion` | вопрос к next BDPF owner | «правильно ли решение?» |
| `nonUseBoundary` | явное, что карта не делает | пустое поле |

---

## 8. Минимальная табличная форма для воркшопа

### 8.1. Таблица carriers

| carrierRef | kind | version/date | owner | what it shows | what it does not show | nonAdmissibleUse | sourceReturnCondition |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

### 8.2. Таблица source signals

| sourceSignalRef | sourceCarrierRef | extractedSignal | needKind | affectedStructureKindCandidates | supportedQuestion | missingData | receivingPattern |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

### 8.3. Таблица role assignments

| roleAssignmentRef | holderRef | roleRef | boundedContextRef | window | evidence/source | nonAdmissibleUse | missingData |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

### 8.4. Таблица evidence candidates

| evidenceRef | claimText | claimScope | evidenceCarrierRef | evidenceKind | admissibleUse | nonAdmissibleUse | gap |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

### 8.5. Таблица representation losses

| lossNoteRef | carrier/view | affectedStructureKind | what is preserved | what is lost/coarsened | misread risk | source return | receivingPattern |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

---

## 9. Пример 1 — ГПЗУ и посадка корпуса

```text
CurrentStateMapCarrier@Project:
  carrierId: CSM-G1-GPZU-PLACEMENT-001
  carrierKind: current-state-map-publication-carrier
  carrierVersion: v0.1
  createdAt: 2026-07-02
  createdByRoleAssignmentRef: RA-EXPERT-SUPPORT-AUTHOR-2026-07
  reviewedByRoleAssignmentRefs:
    - RA-GIP-REVIEWER-2026-07
  pilotRef: Pilot-P2S-G0G1-APL-001
  projectRef: Project-G1
  declaredUse: зафиксировать стартовое состояние спора о посадке корпуса до P2S-восстановления
  intendedReaderOrOperator:
    - эксперт сопровождения
    - ГИП
    - координатор ПД/BIM

  narrativeRouteDiscipline:
    routeFamily: architecture-mediated
    sourceTemporalPosture: current design-state reconstruction
    orderingRuleKind: source-intake
    orderRationale: сначала восстановить source signals из ГПЗУ и текущих carriers, затем вывести architectureStructuringNeed
    preservedSourceRelations:
      - GPZU carrier -> extracted sitePlacementNeed signals
      - signals -> MaterialSpatialStructure / TransformationFlowStructure pressure
      - current BIM/PD projection -> representation loss notes
    foregroundedSourceRelations:
      - constraints on placement and emergency vehicle flow
    coarsenedOrLostSourceRelations:
      - full comparison of placement configurations not yet available
      - evidence sufficiency for fire access not yet available
    sourceReturnCondition: return to GPZU, normative constraints, current genplan/BIM versions, and BDPF.8 evidence owner before reliance
    blockedRouteOverread: section order is not proof order, not work plan, not approval route

  currentStateMap:
    currentDecisionOrIssueRef: ISSUE-G1-GPZU-PLACEMENT-001
    describedHolonRef:
      holonId: OKS-G1-CORPUS-A
      holonName: корпус G1 / участок А
      holonKind: building
      lifecycleSlice: design-documentation
      boundedContextRef: Project-G1.DesignSupport.2026-07
      holonScope: посадка корпуса, пожарные проезды, внешние пространственные ограничения
      environmentContext: участок, красные линии, ЗОУИТ, смежные сети
      excludedHolonScope: эксплуатация после ввода; весь комплекс G0/G1 вне участка А

    currentCarrierRefs:
      - carrierRef: CARRIER-GPZU-2026-02-14-PDF
        carrierKind: SourceDocument
        versionOrDate: 2026-02-14
        whatItShows: границы участка, допустимые параметры, ограничения
        whatItDoesNotShow: не выбирает вариант посадки корпуса
        nonAdmissibleUse: not PAD, not proof, not gate
      - carrierRef: CARRIER-GENPLAN-DWG-2026-06-30
        carrierKind: Drawing
        versionOrDate: 2026-06-30
        whatItShows: текущий вариант генплана
        whatItDoesNotShow: не показывает comparison basis и accepted losses
        nonAdmissibleUse: not architecture decision
      - carrierRef: CARRIER-BIM-G1-2026-07-01
        carrierKind: BIMModel
        versionOrDate: 2026-07-01
        whatItShows: modelled massing and road geometry
        whatItDoesNotShow: validated emergency vehicle trajectory and source-to-structure rationale
        nonAdmissibleUse: not OKS, not proof, not gate

    currentSourceRefs:
      - sourceRef: SIG-GPZU-BOUNDARY-001
        sourceCarrierRef: CARRIER-GPZU-2026-02-14-PDF
        extractedSignal: building placement is constrained by site boundary and permitted development envelope
        candidateNeedKind: sitePlacementNeed
        affectedStructureKindCandidates:
          - MaterialSpatialStructure
          - ModuleInterfaceStructure
        nonAdmissibleUse: does not choose spatial configuration
      - sourceRef: SIG-GPZU-FIRE-ACCESS-001
        sourceCarrierRef: CARRIER-GPZU-2026-02-14-PDF
        extractedSignal: emergency vehicle access must remain possible along facade F1
        candidateNeedKind: sitePlacementNeed
        affectedStructureKindCandidates:
          - TransformationFlowStructure
          - MaterialSpatialStructure
        nonAdmissibleUse: does not prove fire-safety adequacy

    currentRoleAssignmentRefs:
      - RA-EXPERT-SUPPORT-AUTHOR-2026-07
      - RA-GIP-REVIEWER-2026-07
      - missing: decisionApproverRoleAssignmentRef for PAD not recovered

    currentEvidenceRefs:
      - evidenceRef: EVID-FIRE-ACCESS-SKETCHCHECK-001
        claimText: current genplan appears to preserve emergency access path along F1
        claimScope: visual sketch check only; no swept-path calculation
        evidenceKind: model
        nonAdmissibleUse: not proof of PAD, not regulatory compliance, not readiness
        unresolvedEvidenceGap: need claim-specific evidence trace for access geometry

    currentToolOrRepositoryRefs:
      - CDE-G1-PROJECTWISE
      - BIM-AUTHORING-REVIT-G1
      - ISSUE-TRACKER-G1

    currentDefectPatternRefs:
      - defectPatternRef: DEFECT-SOURCE-JUMP-001
        defectPatternKind: sourceJumpToDecision
        observedSymptom: GPZU is cited as if it directly justified current placement
        suspectedWeakTransition: missing architectureStructuringNeed and candidate configurations
        likelyReceivingPatternRef: BDPF.3A
      - defectPatternRef: DEFECT-REPLOSS-001
        defectPatternKind: representationLossHidden
        observedSymptom: BIM geometry is read as sufficient proof of access
        likelyReceivingPatternRef: BDPF.10 / BDPF.8

    currentRepresentationLossNotes:
      - lossNoteRef: LOSS-FIRE-ACCESS-BIM-001
        carrierOrViewRef: CARRIER-BIM-G1-2026-07-01
        affectedStructureKindRef: TransformationFlowStructure
        whatIsPreserved: rough road geometry near facade F1
        whatIsCoarsenedOrLost: swept-path relation, access operation scenario, evidence trace
        readerMisreadRisk: reviewer may treat visible road as proof of emergency access adequacy
        sourceReturnCondition: return to source signal, swept-path evidence, and BDPF.8

    firstP2SQuestion: >
      Какие source signals из ГПЗУ создают `sitePlacementNeed` для
      MaterialSpatialStructure и TransformationFlowStructure корпуса G1,
      и какие candidate placement configurations нужно сформировать до PAD?

    nonUseBoundary: >
      Эта карта не является PAD, доказательством пожарного доступа, gate,
      work plan, approval, BIM-standard или проверкой комплектности ПД.
      Она допустима только как стартовый carrier для P2S-восстановления
      decision scenario ISSUE-G1-GPZU-PLACEMENT-001.

  nextOwnerRouting:
    likelyNextBDPFPatternRef: BDPF.3A
    neighboringFPFOwnerRefs:
      - C.32.P2S
      - C.30.ASV
      - BDPF.6
      - BDPF.6A
      - BDPF.8
    stopOrReturnReason: no PAD until architectureStructuringNeed and candidate configurations are recoverable
```

---

## 10. Пример 2 — Технологическое задание и функционально-планировочная структура

```text
CurrentStateMap:
  currentDecisionOrIssueRef: ISSUE-G1-TECH-FLOW-003
  describedHolonRef: OKS-G1-PRODUCTION-ZONE-B
  currentCarrierRefs:
    - CARRIER-TECH-ASSIGNMENT-2026-05-20
    - CARRIER-PLAN-AR-2026-06-28
    - CARRIER-BIM-G1-2026-07-01
    - CARRIER-EXPERT-COMMENT-117
  currentSourceRefs:
    - sourceRef: SIG-TECH-FLOW-CLEAN-DIRTY-SEPARATION-001
      sourceCarrierRef: CARRIER-TECH-ASSIGNMENT-2026-05-20
      extractedSignal: clean and dirty flows must not cross in normal operation
      candidateNeedKind: useScenarioNeed
      affectedStructureKindCandidates:
        - FunctionalPlanningStructure
        - TransformationFlowStructure
        - ControlOperationStructure
      nonAdmissibleUse: does not by itself choose layout or prove sanitary compliance
  currentRoleAssignmentRefs:
    - RA-TECHNOLOGIST-SOURCE-OWNER-2026-07
    - RA-ARCHITECT-AUTHOR-2026-07
    - missing: reviewer role for flow separation not recovered
  currentEvidenceRefs:
    - evidenceRef: GAP-FLOW-COMPARISON-001
      claimText: no claim-specific evidence yet; comparison of flow alternatives missing
      evidenceKind: other
      unresolvedEvidenceGap: need route diagrams / adjacency matrix / scenario-based review
  currentToolOrRepositoryRefs:
    - CDE-G1-PROJECTWISE
    - ISSUE-TRACKER-G1-COMMENTS
  currentDefectPatternRefs:
    - hiddenArchitectureStructuringNeed
    - comparisonCollapsedToScore
  currentRepresentationLossNotes:
    - carrierOrViewRef: CARRIER-PLAN-AR-2026-06-28
      affectedStructureKindRef: TransformationFlowStructure
      whatIsPreserved: room adjacency in plan
      whatIsCoarsenedOrLost: operational flow sequence and conflict points
      readerMisreadRisk: adjacency may be read as proof of scenario support
      sourceReturnCondition: return to use scenario and BDPF.4/BDPF.5 before PAD
  firstP2SQuestion: >
    Как source signal о clean/dirty flow separation создаёт `useScenarioNeed`
    для FunctionalPlanningStructure и TransformationFlowStructure зоны B,
    и какие candidate configurations надо сравнить перед выбранным решением?
  nonUseBoundary: >
    Карта не доказывает санитарную допустимость, не выбирает планировку,
    не заменяет UseConceptRecord, SystemConceptRecord, ComparisonBasis или PAD.
```

Следующий owner:

```text
nextOwnerRouting:
  likelyNextBDPFPatternRef:
    - BDPF.4 UseConceptRecord
    - BDPF.5 SystemConceptRecord
    - BDPF.6 ArchitectureQuestionCard
    - BDPF.6A CandidateArchitecturePalette
```

---

## 11. Пример 3 — ТУ и инженерные мощности

```text
CurrentStateMap:
  currentDecisionOrIssueRef: ISSUE-G1-MEP-CAPACITY-002
  describedHolonRef: OKS-G1-ENGINEERING-SYSTEMS-SLICE
  currentCarrierRefs:
    - CARRIER-TU-ELECTRICITY-2026-04-10
    - CARRIER-MEP-SCHEME-2026-06-25
    - CARRIER-LOAD-CALC-XLSX-2026-06-26
    - CARRIER-BIM-MEP-2026-07-01
  currentSourceRefs:
    - sourceRef: SIG-TU-POWER-LIMIT-001
      sourceCarrierRef: CARRIER-TU-ELECTRICITY-2026-04-10
      extractedSignal: available connection capacity is limited to 1.2 MW under current TU
      candidateNeedKind: engineeringCapacityNeed
      affectedStructureKindCandidates:
        - EngineeringSystemsStructure
        - ModuleInterfaceStructure
        - ControlOperationStructure
      admissibleUse: input to architectureStructuringNeed and engineering systems structure triage
      nonAdmissibleUse: does not prove sufficiency of MEP scheme and does not select load-management strategy
  currentRoleAssignmentRefs:
    - RA-MEP-AUTHOR-2026-07
    - RA-GIP-REVIEWER-2026-07
  currentEvidenceRefs:
    - evidenceRef: EVID-LOAD-CALC-001
      claimText: calculated installed load under scheme S1 is 1.35 MW before diversity factor
      claimScope: MEP scheme S1, calculation XLSX 2026-06-26
      evidenceKind: calculation
      admissibleUse: candidate eval input for BDPF.6B
      nonAdmissibleUse: not selected set, not PAD, not proof of compliance
      unresolvedEvidenceGap: diversity factor and control scenario not tied to use scenarios
  currentToolOrRepositoryRefs:
    - CDE-G1-MEP
    - CALC-REPOSITORY-G1
  currentDefectPatternRefs:
    - evidenceAsGeneralProof
    - sourceJumpToDecision
  currentRepresentationLossNotes:
    - carrierOrViewRef: CARRIER-BIM-MEP-2026-07-01
      affectedStructureKindRef: EngineeringSystemsStructure
      whatIsPreserved: equipment placement and modeled connections
      whatIsCoarsenedOrLost: load-management control logic and operating modes
      readerMisreadRisk: modeled equipment may be read as capacity proof
      sourceReturnCondition: return to MEP calculation, control scenario, and BDPF.8 evidence trace
  firstP2SQuestion: >
    Как TU capacity limit и текущий load calculation создают `engineeringCapacityNeed`
    для EngineeringSystemsStructure и ControlOperationStructure,
    и нужен ли CandidateArchitecturePalette для схемы подключения / load-management до PAD?
  nonUseBoundary: >
    Карта не подтверждает достаточность инженерной схемы, не проводит gate,
    не заменяет calculation evidence trace, comparison или PAD.
```

---

## 12. Проверка качества `CurrentStateMap` перед передачей в следующий P2S-шаг

Используйте короткую шкалу:

| Значение | Смысл |
|---:|---|
| `0` | wrong-kind: это не карта текущего состояния, а решение/отчёт/перечень файлов |
| `1` | named only: scenario назван, но fields пустые или общие |
| `2` | orientation only: карта помогает ориентироваться, но source signals / losses / firstP2SQuestion слабые |
| `3` | locally usable with visible limits: можно переходить к BDPF.3/3A с явными gap |
| `4` | good for pilot use: один scenario, carriers, sources, roles, evidence, losses и firstP2SQuestion воспроизводимы |
| `5` | replayable: другой reviewer может восстановить тот же P2S-вход и source-return без устных пояснений |

Минимальный floor для пилота: `3`. Для reliance-bearing use: не ниже `4`, но сама `CurrentStateMap` всё равно не становится evidence, PAD или gate.

### Check table

| Check | Passing condition | Value |
|---|---|---:|
| `CSM-1 oneScenarioOnly` | Один decision scenario; excluded scope назван |  |
| `CSM-2 describedHolonNotCarrier` | `describedHolonRef` — ОКС/подсистема, не BIM/ПД |  |
| `CSM-3 carrierInventoryRecoverable` | carriers имеют ref, version/date, owner/use boundary |  |
| `CSM-4 sourceSignalsSeparated` | source carrier отделён от extracted signal |  |
| `CSM-5 sourceDoesNotChooseDecision` | ни один source signal не трактуется как selected solution |  |
| `CSM-6 rolesAreAssignments` | ключевые roles имеют holder/role/context/window или gap |  |
| `CSM-7 evidenceIsClaimSpecific` | evidence привязано к claim/scope или записан gap |  |
| `CSM-8 toolNotAuthority` | tools/repositories не трактуются как approval/evidence/gate |  |
| `CSM-9 defectPatternsVisible` | текущие дефектные переходы классифицированы |  |
| `CSM-10 representationLossVisible` | preserved/lost/coarsened structure и misread risk названы |  |
| `CSM-11 firstP2SQuestionActionable` | вопрос называет source signal, structure, next owner |  |
| `CSM-12 nonUseBoundaryPresent` | граница non-use явно записана |  |

---

## 13. Типовые stop conditions

Остановите сборку и вернитесь на предыдущий шаг, если:

1. `currentDecisionOrIssueRef` описывает весь проект, а не один scenario.
2. `describedHolonRef` — BIM, файл, раздел ПД или замечание, а не ОКС/подсистема.
3. В `currentSourceRefs` перечислены документы, но нет `extractedSignal`.
4. `firstP2SQuestion` звучит как «правильно ли решение?» вместо вопроса о structuring need и structure kind.
5. Evidence описано как «расчёт есть», но нет claim/scope/non-admissible use.
6. Role assignments заменены должностями или подписями.
7. Порядок изложения выглядит как proof order, approval route или work plan.
8. `nonUseBoundary` отсутствует.

---

## 14. Route to next BDPF owner

| Что обнаружено в `CurrentStateMap` | Следующий owner |
|---|---|
| Неясно, что за ОКС/подсистема | `BDPF.1 BuiltAssetSystemCard` |
| Есть carriers, но нет extracted source signals | `BDPF.3 DesignSourceSignalUseRecord` |
| Есть source signals, но нет structuring need | `BDPF.3A BuiltAssetProblemToStructureFlowCard` |
| Сценарии использования скрыты или противоречат carrier-ам | `BDPF.4 UseConceptRecord` |
| Не видна системная логика | `BDPF.5 SystemConceptRecord` |
| Неясно, какая структура меняет решение | `BDPF.6 ArchitectureQuestionCard` |
| Видны несколько возможных конфигураций | `BDPF.6A CandidateArchitecturePalette` |
| Есть eval/расчёт, но нет comparison basis | `BDPF.6B` / `BDPF.6C` |
| Решение уже заявлено, но не как PAD | `BDPF.7 ArchitectureDecisionRelation@Project` |
| Нужен readable carrier уже принятого решения | `BDPF.7A` / `BDPF.7B` |
| Evidence не привязано к claim/scope | `BDPF.8 DesignEvidenceTrace` |
| Вопрос о переходе дальше/readiness | `BDPF.9 DesignReadinessGate` |
| ПД/BIM/views теряют selected/expected structure | `BDPF.10 ProjectDocumentationProjection` |
| Повторяющиеся замечания указывают на методический дефект | `BDPF.11 DesignMethodFeedbackRecord` |

---

## 15. Готовая пустая форма для копирования

```text
# CurrentStateMap — <scenario-id>

CurrentStateMapCarrier@Project:
  carrierId:
  carrierKind: current-state-map-publication-carrier
  carrierVersion: v0.1
  createdAt:
  createdByRoleAssignmentRef:
  reviewedByRoleAssignmentRefs:
  pilotRef: Pilot-P2S-G0G1-APL-001
  projectRef:
  declaredUse:
  intendedReaderOrOperator:
    - эксперт сопровождения
    - ГИП / ГАП
    - координатор ПД/BIM
    - технический заказчик / заказчик as decision-reader
  sourceDPFRefs:
    - DPF-building-design.md@draft-v0.4
    - NarrativizationAndNarrativeStudiesPrinciplesFramework@2026-06-30
    - FPFCore@June2026

  narrativeRouteDiscipline:
    routeFamily: architecture-mediated
    sourceTemporalPosture: current design-state reconstruction
    orderingRuleKind:
    orderRationale:
    preservedSourceRelations:
    foregroundedSourceRelations:
    coarsenedOrLostSourceRelations:
    sourceReturnCondition:
    blockedRouteOverread:

  currentStateMap:
    currentDecisionOrIssueRef:
    describedHolonRef:
      holonId:
      holonName:
      holonKind:
      lifecycleSlice:
      boundedContextRef:
      holonScope:
      environmentContext:
      excludedHolonScope:

    currentCarrierRefs:
      - carrierRef:
        carrierKind:
        titleOrName:
        versionOrDate:
        ownerOrPublisher:
        locationOrRepositoryRef:
        whatItShows:
        whatItDoesNotShow:
        admissibleUseInCurrentStateMap:
        nonAdmissibleUse:
        sourceReturnCondition:

    currentSourceRefs:
      - sourceRef:
        sourceCarrierRef:
        sourceKind:
        issueDateOrVersion:
        extractedSignal:
        candidateNeedKind:
        affectedHolonOrScope:
        affectedStructureKindCandidates:
        supportedQuestion:
        admissibleUse:
        nonAdmissibleUse:
        freshnessBoundary:
        missingOrAmbiguousData:
        sourceReturnCondition:
        likelyReceivingPatternRef:

    currentRoleAssignmentRefs:
      - roleAssignmentRef:
        holderRef:
        roleRef:
        boundedContextRef:
        assignmentWindow:
        evidenceOrSourceRef:
        relevantToScenarioBecause:
        nonAdmissibleUse:
        missingAssignmentData:

    currentEvidenceRefs:
      - evidenceRef:
        evidenceCarrierRef:
        claimCandidateRef:
        claimText:
        claimScope:
        evidenceKind:
        evidenceProducingWorkRef:
        evidenceInterpretingRoleAssignmentRef:
        admissibleUse:
        nonAdmissibleUse:
        freshnessOrTimeWindow:
        reliabilityNotes:
        unresolvedEvidenceGap:
        likelyReceivingPatternRef:

    currentToolOrRepositoryRefs:
      - toolOrRepositoryRef:
        kind:
        locationOrAccessRef:
        versionPolicy:
        relevantCarrierRefs:
        relevantSourceRefs:
        whatCanBeRecovered:
        whatIsLostOrNotCaptured:
        nonAdmissibleUse:
        sourceReturnCondition:

    currentDefectPatternRefs:
      - defectPatternRef:
        defectPatternKind:
        observedInCarrierRefs:
        observedSymptom:
        suspectedWeakTransition:
        notYetClaimed:
        likelyReceivingPatternRef:
        repairOrSourceReturnHint:

    currentRepresentationLossNotes:
      - lossNoteRef:
        carrierOrViewRef:
        sourceOrDecisionMemoryRef:
        affectedStructureKindRef:
        selectedOrExpectedOrUnknownStructure:
        whatIsPreserved:
        whatIsCoarsenedOrLost:
        readerMisreadRisk:
        sourceReturnCondition:
        likelyReceivingPatternRef:

    firstP2SQuestion:

    nonUseBoundary: >
      Эта CurrentStateMap не принимает проектное решение, не доказывает claim,
      не подтверждает готовность к экспертизе, не заменяет ПД/BIM/views,
      не является work plan и не подтверждает соответствие нормам.
      Она допустима только как стартовый carrier для восстановления P2S-цепочки
      по одному decision scenario.

  nextOwnerRouting:
    likelyNextBDPFPatternRef:
    neighboringFPFOwnerRefs:
    stopOrReturnReason:

  qualityCheck:
    oneScenarioOnly:
    describedHolonNotCarrier:
    carrierInventoryRecoverable:
    sourceSignalsSeparatedFromCarriers:
    sourceDoesNotChooseDecision:
    rolesAreAssignmentsNotTitles:
    evidenceIsClaimSpecific:
    toolNotAuthority:
    defectPatternsVisible:
    representationLossVisible:
    firstP2SQuestionActionable:
    nonUseBoundaryPresent:
    readyForNextP2SStep:
```

---

## 16. Минимальный prompt для фасилитатора

```text
Собери CurrentStateMap для одного decision scenario в BA-P2S-пилоте.

Сценарий / спор:
<описать в 2-3 строках>

ОКС / подсистема:
<что является describedHolonRef>

Доступные carriers:
<ПД, BIM, IFC, таблицы, ТЗ, ТУ, ГПЗУ, изыскания, замечания, расчёты, CDE, issue tracker>

Собери:
1. currentDecisionOrIssueRef;
2. describedHolonRef, не carrier;
3. currentCarrierRefs с version/date, owner, whatItShows, whatItDoesNotShow, nonAdmissibleUse;
4. currentSourceRefs как source carrier + extracted source signal + needKind + affected structure kinds;
5. currentRoleAssignmentRefs как holder/role/context/window или gap;
6. currentEvidenceRefs как claim-specific evidence candidates или gaps;
7. currentToolOrRepositoryRefs без превращения tool status в evidence/approval;
8. currentDefectPatternRefs;
9. currentRepresentationLossNotes с preserved/lost/source-return;
10. firstP2SQuestion, который ведёт к BDPF.3A/BDPF.6/BDPF.6A/BDPF.6C/BDPF.7/BDPF.8/BDPF.10/BDPF.11;
11. nonUseBoundary.

Используй routeFamily=architecture-mediated и явно укажи orderingRuleKind.
Не делай PAD, evidence trace, gate или work plan.
```

---

## 17. Короткое правило завершения

`CurrentStateMap` готова для следующего P2S-шага, если другой reviewer может по ней ответить:

```text
1. О каком одном decision scenario идёт речь?
2. Какой физический ОКС / subsystem является describedHolonRef?
3. Через какие carriers текущая ситуация видна?
4. Какие source signals извлечены, и какие needKind они создают?
5. Какие structure kinds становятся unknown/candidate/selected/expected/represented?
6. Какие roles, evidence и tools уже видны, а какие только gaps?
7. Какие representation losses и misread risks есть в ПД/BIM/views?
8. Какой первый P2S-вопрос и следующий BDPF owner?
9. Что эта карта не имеет права доказывать, решать или разрешать?
```

Если хотя бы на вопросы 1, 2, 4, 5, 8 или 9 нельзя ответить по carrier-у без устного пояснения, карта остаётся `orientation only` и не должна передаваться как pilot-ready вход.
