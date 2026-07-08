# Анализ исходных данных как первый этап услуги экспертного сопровождения проектирования

> Черновой фрагмент для развития `DPF-building-design.md`.
>
> Контекст: экспертное сопровождение проектирования ОКС. Проектировщик проводит анализ исходных данных. Экспертиза на этом этапе не подменяет проектировщика и не выбирает проектное решение, а отслеживает, что анализ выполнен в форме, пригодной для дальнейшей P2S-цепочки.

## 1. Короткий ответ

Анализ исходных данных должен проводиться не как свободный текст «исходные данные изучены» и не как чек-лист наличия файлов. Рабочая форма — **пакет анализа исходных данных**, состоящий из нескольких трассируемых записей:

```text
InitialDataAnalysisPackage@Project:
  packageId:
  projectRef:
  objectOrSiteRef:
  designStageOrServiceStep:
  sourceCarrierInventoryRef:
  designSourceSignalUseRecordRefs:
  sourceGapAndAmbiguityRegisterRef:
  initialUseScenarioExtractionRef:
  initialBuiltAssetSystemCardRef:
  builtAssetProblemToStructureFlowCardRefs:
  sourceAnalysisReadinessGateRef:
  expertTrackingRecordRef:
  admissibleUse:
  nonAdmissibleUse:
  sourceReturnCondition:
```

Смысл пакета: показать не «все документы собраны», а **какие проектные сигналы извлечены из ТЗ, отраслевого/технологического ТЗ, участка, ТУ и других источников; какие потребности, ограничения и неопределённости они создают; какие структуры ОКС становятся неизвестными, спорными или ограниченными; какой следующий DPF/FPF-owner должен принять claim**.

Рабочая FPF-опора формы: `C.32.P2S` для перехода от problem-side материала к структурам, `C.30` для удержания архитектурного объекта, `E.4.DPF`/`E.4.PFR` для DPF-пакета и relation records, `A.10` для границы evidence-use, `B.3` для assurance/reliance-границы, `A.21` для gate/readiness-границы.

### 1.1. Назначение сущностей и слотов пакета

| Сущность / слот | Что фиксирует | Зачем | Для чего используется / граница неиспользования |
|---|---|---|---|
| `InitialDataAnalysisPackage@Project` | Связанный пакет записей анализа исходных данных в рамках проекта, ОКС и шага услуги. | Чтобы анализ был не текстовым отчётом, а проверяемым набором records. | Используется как вход в BDPF.3/3A/4/5/6 и readiness gate; не является проектным решением, доказательством корректности решения или разрешением на работу. |
| `packageId` | Устойчивый идентификатор пакета, версии или выпуска. | Чтобы можно было ссылаться на конкретный набор анализа и отличать его от следующих редакций. | Используется для трассировки и refresh; сам по себе не подтверждает полноту или качество анализа. |
| `projectRef` | Проектный контекст, в котором анализ имеет силу. | Чтобы не переносить source signal в другой проект без проверки применимости. | Ограничивает область применения записей; не заменяет объект капитального строительства. |
| `objectOrSiteRef` | ОКС, часть ОКС, участок или внешний контекст, к которому относится анализ. | Чтобы главный объект внимания оставался ОКС и состояние проектных решений о нём. | Привязывает source signals к affected holon/scope; не является ссылкой на файл, ИК или статус документа. |
| `designStageOrServiceStep` | Стадию проектирования или шаг услуги, на котором предъявлен пакет. | Чтобы требовать только релевантную зрелость анализа для текущего шага. | Определяет допустимый readiness threshold; не доказывает зрелость проектного решения. |
| `sourceCarrierInventoryRef` | Ссылку на реестр исходных carriers: что получено, от кого, в какой версии и статусе анализа. | Чтобы отделить наличие carrier-а от извлечённого проектного сигнала. | Используется для provenance, freshness и source return; не является доказательством применимости содержания. |
| `designSourceSignalUseRecordRefs` | Ссылки на записи извлечённых source signals и их допустимого использования. | Чтобы каждый значимый пункт источника стал проектным сигналом с `needKind`, scope и structure impact. | Используется как вход в P2S и следующие BDPF-records; не выбирает проектное решение и не доказывает его. |
| `sourceGapAndAmbiguityRegisterRef` | Реестр пробелов, противоречий, устаревших данных и неясных владельцев. | Чтобы неопределённость была управляемой, а не скрытой в тексте отчёта. | Используется для block/reservation/source-return; не является автоматическим замечанием к проектному решению. |
| `initialUseScenarioExtractionRef` | Первичное извлечение сценариев использования из ТЗ, технологического задания, требований эксплуатации и иных источников. | Чтобы перейти от разрозненных требований к использованию ОКС без отдельного ConOps-carrier. | Даёт материал для `UseConceptRecord`; не является финальной концепцией использования и не выбирает решение. |
| `initialBuiltAssetSystemCardRef` | Первичную карточку ОКС как системы в окружении: границы, stakeholders, интерфейсы, нерешённые вопросы. | Чтобы source signals не анализировались «в воздухе», вне ОКС и его окружения. | Даёт системный anchor для BDPF.1/5; не является системной концепцией в полном смысле и не заменяет PAD. |
| `builtAssetProblemToStructureFlowCardRefs` | P2S-карты, где source signals доведены до `architectureStructuringNeed`, unknown/candidate structure kinds и next owner. | Чтобы был виден переход от problem-side давления к структурам ОКС. | Используется для BDPF.3A/6 и последующего synthesis; не является selected structure, candidate configuration или PAD. |
| `sourceAnalysisReadinessGateRef` | Gate-решение по готовности пакета анализа к следующему проектному шагу. | Чтобы явно различить `pass`, `passWithReservations`, `hold`, `reject`, `abstain`. | Управляет допуском к следующему шагу услуги; не доказывает допустимость будущего решения и не является выполненной проектной работой. |
| `expertTrackingRecordRef` | След экспертного отслеживания: что проверено, какие reservations, deviations, source returns и next actions зафиксированы. | Чтобы экспертиза отслеживала связность пакета, не подменяя проектировщика. | Используется для service tracking и feedback; не является исходным анализом проектировщика, PAD или evidence sufficiency. |
| `admissibleUse` | Разрешённые способы использования пакета и его записей. | Чтобы downstream-работа понимала, на что можно опереться. | Ограничивает передачу в BDPF/FPF-owner; не расширяет силу source carrier-а сверх указанного scope. |
| `nonAdmissibleUse` | Запрещённые stronger readings: что пакет не доказывает и чем не является. | Чтобы carrier, статус, gate или экспертный комментарий не подменили решение, evidence или work. | Блокирует неправильное использование; не является отдельным дефектом, пока не нарушена граница. |
| `sourceReturnCondition` | Условия возврата к источнику или пересмотра пакета. | Чтобы изменение версии, владельца, применимости или конфликт источников не осталось незамеченным. | Запускает refresh/reopen; не является автоматическим запретом на все дальнейшие шаги, если gate допускает работу с reservation. |

Минимальный результат для старта услуги:

```text
исходный carrier
→ extracted source signal
→ needKind
→ affected holon/scope
→ affected structure kind
→ architectureStructuringNeed
→ missing/ambiguous data
→ sourceReturnCondition
→ receivingPatternRef
→ readiness status
```

### 1.2. Текстовое описание цепочки

1. **Исходный carrier** — конкретный носитель исходного материала: ТЗ, технологическое задание, ГПЗУ, ТУ, изыскания, обследование, письмо, схема, модель. Он нужен для provenance: откуда взят материал, кто владелец, какая версия и где точное место в источнике. Carrier используется как точка возврата и проверки currentness, но не как проектное решение и не как доказательство корректности решения.
2. **Extracted source signal** — не копия пункта источника, а извлечённый проектный сигнал: потребность, ограничение, режим, интерфейс, риск, неопределённость или требуемый сценарий. Он нужен, чтобы отделить «документ получен» от «из документа извлечено то, что влияет на ОКС». Signal передаётся в P2S-цепочку и downstream records.
3. **`needKind`** — тип давления, которое создаёт signal: размещение, сценарий использования, инженерная мощность, нормативное ограничение, геотехническая/конструктивная потребность, реализация строительства, информационная надёжность. Он нужен для маршрутизации: разные потребности попадают к разным structure kinds, вопросам и owners.
4. **Affected holon/scope** — ОКС, часть ОКС, участок, зона, подсистема, интерфейс или lifecycle slice, которого касается signal. Он нужен, чтобы анализ не сместился в carrier/file-level и не потерял entity-of-concern. Scope показывает, где именно состояние проектного решения становится неизвестным, спорным или ограниченным.
5. **Affected structure kind** — тип структуры, который затронут: spatial, functional, flow, structural, engineering, interface, control, operational, construction-realization. Он нужен, чтобы source signal не прыгал сразу в готовое решение, а сначала называл тип структуры, который надо рассмотреть.
6. **`architectureStructuringNeed`** — формулировка архитектурной потребности: какую структуру ОКС нужно выявить, ограничить, синтезировать, сравнить или вернуть к источнику. Она нужна как мост `C.32.P2S` между problem-side материалом и architecture work. Это ещё не candidate configuration и не PAD.
7. **Missing/ambiguous data** — недостающие, неоднозначные, устаревшие или конфликтующие данные, без которых нельзя честно закрыть следующий claim. Они нужны, чтобы неопределённость стала управляемым register item: block, allow with assumption, allow with reservation или source return.
8. **`sourceReturnCondition`** — условие, при котором нужно вернуться к исходному carrier-у, владельцу источника или source pack: новая версия ТЗ, уточнение ТУ, конфликт с изысканиями, изменение посадки, смена применимости нормы. Оно нужно для refresh/reopen и для защиты downstream-решений от устаревшего основания.
9. **`receivingPatternRef`** — следующий BDPF/FPF-owner, который должен принять claim: например `BDPF.3A`, `BDPF.4`, `BDPF.5`, `BDPF.6`, `BDPF.8`, `BDPF.9`, `BDPF.11`. Он нужен, чтобы запись не зависала в отчёте, а попадала в конкретный следующий проектный вопрос, evidence route, gate или feedback route.
10. **Readiness status** — состояние готовности записи или пакета для следующего шага: `pass`, `passWithReservations`, `hold`, `reject`, `abstain` либо локальные статусы анализа вроде `analyzedWithGaps`. Он нужен, чтобы явно сказать, что можно делать дальше, что нельзя и какие reservations сохраняются. Readiness status не является proof, PAD или выполненной работой.

### 1.3. Различение `affectedStructureKindRefs` и `architectureStructuringNeed`

В анализе исходных данных нельзя смешивать `affectedStructureKindRefs` и `architectureStructuringNeed`.

`affectedStructureKindRefs` отвечает на вопрос:

```text
Какой тип структуры ОКС затронут source signal?
```

Это классификация зоны структурного воздействия: `functional`, `spatial`, `flow`, `structural`, `engineering`, `interface`, `control`, `operational`, `construction-realization` и т.д.

`architectureStructuringNeed` отвечает на вопрос:

```text
Какую архитектурную работу теперь нужно выполнить из-за этого source signal?
```

Это формулировка потребности: какую структуру нужно выявить, ограничить, синтезировать, сравнить, проверить или вернуть к источнику.

Рабочая формула:

```text
affectedStructureKindRefs = куда смотреть
architectureStructuringNeed = зачем туда смотреть и что там стало проблемой
```

Ошибка:

```text
architectureStructuringNeed: FunctionalPlanningStructure
```

Почему ошибка: `FunctionalPlanningStructure` — это structure kind, а не потребность в архитектурном структурировании.

Допустимо:

```text
affectedStructureKindRefs:
  - FunctionalPlanningStructure
  - TransformationFlowStructure
  - ControlOperationStructure

architectureStructuringNeed:
  needKind: useScenarioNeed
  sourceSignalRefs:
    - TZ-PatientFlow-001
  architectureConcernRefs:
    - separation of emergency/planned/infectious patient flows
  affectedHolonRefs:
    - приемно-диагностический блок больничного корпуса
  currentStopOrReturnReason:
    нельзя выбрать планировочную структуру приемного блока без схемы потоков
    пациентов, персонала, материалов и отходов
  sourceReturnCondition:
    вернуть к ТЗ/медтехнологии при изменении состава потоков, режимов отделений
    или санитарно-эпидемиологических требований
```

Минимальная проверка: если `affectedStructureKindRefs` заполнен, но `architectureStructuringNeed` отсутствует, то source signal только классифицирован, но ещё не доведён до P2S.

## 2. Почему не достаточно обычного «отчёта об анализе»

В BDPF исходные данные не выбирают проектное решение. Они создают давление на проектное рассуждение: потребности, ограничения, неизвестные структуры, требования к синтезу вариантов и условия возврата к источнику. Поэтому свободный отчёт без трассировки обычно скрывает главный переход:

```text
source signal → architectureStructuringNeed → unknown/candidate structures
```

Для сопровождения услуги важен именно этот переход. Экспертиза должна видеть, что проектировщик не просто получил ТЗ, участок и ТУ, а извлёк из них проектные сигналы и разложил их по структурам ОКС.

## 3. Роли на этапе анализа исходных данных

| Роль | Что делает | Чего не делает |
|---|---|---|
| Проектировщик | Извлекает source signals, классифицирует `needKind`, связывает сигналы с ОКС, сценариями, структурами, неопределённостями и следующими проектными вопросами. | Не должен выдавать исходные данные за готовое проектное решение. |
| Эксперт сопровождения | Проверяет наличие и пригодность записей анализа: есть ли carrier inventory, source-signal matrix, gaps, source-return conditions, P2S-связь и readiness gate. | Не проводит анализ вместо проектировщика и не выбирает решение на основании исходных данных. |
| Заказчик / технический заказчик | Уточняет источник, приоритет, версию, владельца требования, недостающие данные, допущения и условия возврата к источнику. | Не должен подменять source signal утверждением «такое решение принять». |

## 4. Минимальный состав пакета анализа

### 4.1. Реестр исходных carriers

```text
SourceCarrierInventory@Project:
  inventoryId:
  projectRef:
  objectOrSiteRef:
  carrierRows:
    - sourceCarrierRef:
      sourceKind:
      sourceOwner:
      issueDateOrVersion:
      receivedDate:
      validityOrFreshnessBoundary:
      readableScope:
      extractionStatus:
        notReceived | receivedNotAnalyzed | analyzed | analyzedWithGaps | obsolete | sourceReturnRequired
      extractedSignalRecordRefs:
      missingPagesOrAttachments:
      sourceReturnCondition:
  nonAdmissibleUse:
```

Этот реестр отвечает только на вопрос: **что получено, от кого, в какой версии, в каком статусе анализа, и куда возвращаться при изменении**. Он не является доказательством корректности данных и не является разрешением проектировать.

### 4.2. Матрица source signals

Для каждого значимого сигнала заполняется `DesignSourceSignalUseRecord` или табличная строка с теми же полями.

```text
DesignSourceSignalUseRecord@Project:
  sourceSignalRef:
  sourceCarrierRef:
  sourceKind:
  sourceOwner:
  issueDateOrVersion:
  exactSourceLocus:
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

Практический табличный вид:

| Поле | Что писать |
|---|---|
| `sourceCarrierRef` | ТЗ, отраслевое/технологическое ТЗ, ГПЗУ, материалы по участку, ТУ, изыскания, обследование, письмо, протокол, схема, модель. |
| `exactSourceLocus` | Раздел, пункт, лист, приложение, координата, версия, дата. |
| `extractedSignal` | Не копия всего пункта, а проектный сигнал: ограничение, режим, требуемый сценарий, мощность, интерфейс, риск, неопределённость. |
| `needKind` | Тип потребности: `sitePlacementNeed`, `useScenarioNeed`, `engineeringCapacityNeed`, `regulatoryConstraintNeed`, `geotechnicalOrStructuralNeed`, `constructionRealizationNeed`, `informationRelianceNeed`. |
| `affectedHolonOrScope` | ОКС целиком, участок, функциональная зона, конструктивная система, инженерная система, технологическая зона, вход/выход, эксплуатационная подсистема. |
| `affectedStructureKindRefs` | Пространственная, функциональная, потоковая, конструктивная, инженерная, интерфейсная, управляющая, эксплуатационная, организационно-строительная структура. |
| `supportedQuestion` | Какой вопрос теперь нужно решить: посадка, сценарий использования, мощности, трассировка, эвакуация, несущая схема, этапность, доступность обслуживания и т.д. |
| `missingOrAmbiguousData` | Чего не хватает или что противоречит другому источнику. |
| `sourceReturnCondition` | Когда нужно вернуться к источнику: новая версия ТЗ, уточнение ТУ, получение ГПЗУ, изменение посадки, конфликт с изысканиями. |
| `receivingPatternRef` | Куда передаётся claim: BDPF.1, BDPF.3A, BDPF.4, BDPF.5, BDPF.6, BDPF.6B, BDPF.8, BDPF.9, BDPF.11. |

### 4.3. Реестр пробелов, противоречий и source-return

```text
SourceGapAndAmbiguityRegister@Project:
  registerId:
  projectRef:
  gapRows:
    - gapId:
      sourceSignalRefs:
      affectedHolonOrScope:
      affectedStructureKindRefs:
      gapKind:
        missingSource | ambiguousRequirement | conflictBetweenSources | staleSource | insufficientPrecision | ownerUnclear | assumptionNeeded
      designImpact:
      currentDisposition:
        blockNextStep | allowWithAssumption | allowWithReservation | sourceReturnRequired | noImpactForCurrentScope
      requiredClarification:
      clarificationOwner:
      dueOrReviewPoint:
      receivingPatternRef:
      reopenCondition:
```

Это критично для начального этапа, где часто есть ТЗ, отраслевое ТЗ, участок и часть ТУ, но ещё нет полного комплекта. Неполнота не всегда блокирует старт, но она должна быть явно классифицирована: что можно анализировать, что можно только предполагать, а что блокирует переход к следующему шагу.

### 4.4. Первичная карта использования

Если отдельный ConOps/carrier не ведётся, сценарии использования извлекаются из практических источников: ТЗ, отраслевого/технологического ТЗ, требований эксплуатации, ТУ, обследования, замечаний, явно описанных сценариев.

```text
InitialUseScenarioExtraction@Project:
  extractionId:
  objectRef:
  sourceSignalRefs:
  userGroups:
  beneficiaryGroups:
  operatingRoles:
  primaryUseScenarioCandidates:
  secondaryUseScenarioCandidates:
  maintenanceScenarioCandidates:
  emergencyScenarioCandidates:
  logisticsAndAccessScenarioCandidates:
  scenarioConflicts:
  downstreamUseConceptRecordRef:
  nonAdmissibleUse:
```

Эта запись не доказывает спрос, не является проектным решением и не заменяет `UseConceptRecord`. Она даёт материал для BDPF.4.

### 4.5. Первичная карточка ОКС как системы

```text
InitialBuiltAssetSystemCard@Project:
  objectRef:
  objectName:
  objectKind:
  lifecyclePhase:
  environmentContext:
  siteRef:
  beneficiaryStakeholders:
  operatingStakeholders:
  regulatoryAndSiteConstraints:
  valueStatementCandidate:
  primaryUseScenarioRefs:
  systemBoundaryCandidate:
  externalInterfaceCandidates:
  unresolvedSystemQuestions:
  downstreamBuiltAssetSystemCardRef:
```

Она нужна, чтобы проектировщик не анализировал исходные данные «в воздухе». Каждый сигнал должен быть привязан к ОКС, участку, окружению, подсистеме или жизненному срезу.

### 4.6. P2S-карта: от исходного сигнала к структурам ОКС

```text
BuiltAssetProblemToStructureFlowCard@InitialDataAnalysis:
  flowId:
  describedHolonRef:
  boundedContextRef:
    holonScope:
    lifecycleSlice:
    nqdWorkState: SignalIntake | ProblemShaping | StructureKindTriage
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
    architectureCharacteristicRefs:
    qBundleRefs:
  structuralInformation:
    unknownStructure:
    latentOrHiddenStructure:
    lostStructure:
    sourceReturnCondition:
  neighboringOwnerForNextClaim:
```

На этапе анализа исходных данных эта карта обычно ещё не содержит выбранных структур. Нормальное состояние — `SignalIntake`, `ProblemShaping` или `StructureKindTriage`. Ошибка — сразу писать выбранное решение.

### 4.7. Gate экспертного отслеживания

```text
SourceAnalysisReadinessGate@Project:
  gateId:
  gateProfile: sourceAnalysisReadiness
  designStep: initialDataAnalysis
  objectScope:
  requiredRecords:
    - SourceCarrierInventory@Project
    - DesignSourceSignalUseRecord@Project[*]
    - SourceGapAndAmbiguityRegister@Project
    - InitialUseScenarioExtraction@Project
    - InitialBuiltAssetSystemCard@Project
    - BuiltAssetProblemToStructureFlowCard@InitialDataAnalysis[*]
  requiredEvidence:
    - sourceCarrierRefs
    - version/date/owner refs
    - exactSourceLocus refs
  blockingGaps:
  acceptedDeviations:
  gateDecision: pass | passWithReservations | hold | reject | abstain
  decisionBasis:
  nextAllowedWork:
  nonAllowedWork:
  nonAdmissibleUse:
```

Экспертный gate не доказывает допустимость будущего проектного решения. Он только фиксирует, что проектировщик предъявил достаточный след анализа исходных данных для перехода к концепции использования, концепции системы и архитектурным вопросам.

## 5. Типовой стартовый набор источников

| Исходный carrier | Типовые source signals | Типовой `needKind` | Куда передавать |
|---|---|---|---|
| ТЗ заказчика | Назначение объекта, целевые показатели, состав зон, ограничения бюджета/сроков, требования к разделам, требования к режимам работы. | `useScenarioNeed`, `regulatoryConstraintNeed`, `constructionRealizationNeed` | BDPF.1, BDPF.4, BDPF.5, BDPF.6 |
| Отраслевое / технологическое ТЗ | Технологические процессы, режимы, потоки людей/материалов/транспорта, требования к безопасности, санитарии, чистым/грязным зонам, обслуживанию. | `useScenarioNeed`, `engineeringCapacityNeed`, `regulatoryConstraintNeed` | BDPF.4, BDPF.5, BDPF.6, BDPF.6B |
| Участок / ГПЗУ / градостроительные ограничения | Границы, параметры застройки, красные линии, сервитуты, ЗОУИТ, подъезды, внешние интерфейсы, ограничения посадки. | `sitePlacementNeed`, `regulatoryConstraintNeed` | BDPF.1, BDPF.3A, BDPF.6 |
| ТУ на подключение | Точки подключения, мощности, режимы, ограничения трасс, сроки действия, условия присоединения. | `engineeringCapacityNeed`, `regulatoryConstraintNeed` | BDPF.5, BDPF.6, BDPF.8, BDPF.9 |
| Инженерные изыскания, если есть | Геология, гидрология, нагрузки среды, ограничения оснований, риски участка. | `geotechnicalOrStructuralNeed`, `sitePlacementNeed` | BDPF.3A, BDPF.6B, BDPF.8 |
| Обследование существующего объекта, если есть | Текущее состояние, скрытые дефекты, ограничения реконструкции, неизвестные структуры. | `informationRelianceNeed`, `geotechnicalOrStructuralNeed`, `expertReviewNeed` | BDPF.3A, BDPF.5, BDPF.8, BDPF.11 |

## 6. Пример табличной строки анализа

| Поле | Пример |
|---|---|
| `sourceCarrierRef` | `TZ-001`, раздел «Назначение и показатели объекта» |
| `extractedSignal` | Требуется объект с раздельными потоками посетителей, персонала и обслуживания. |
| `needKind` | `useScenarioNeed` |
| `affectedHolonOrScope` | ОКС целиком; входная группа; сервисная зона; эксплуатационные маршруты. |
| `affectedStructureKindRefs` | FunctionalStructure, FlowStructure, SpatialStructure, InterfaceStructure, ControlStructure. |
| `architectureStructuringNeed` | Нужно определить, какие потоки должны быть разведены пространственно, организационно или управляюще, и какие unknown/candidate structures возникают для входной группы, сервисной зоны и эксплуатационных маршрутов. |
| `supportedQuestion` | Какие потоки должны быть разделены пространственно, организационно или управляюще? |
| `missingOrAmbiguousData` | Не указан пиковый поток, режимы обслуживания, конфликт с пожарной эвакуацией не проверен. |
| `sourceReturnCondition` | Вернуться к ТЗ/технологическому заданию при уточнении численности, режима работы или сценариев обслуживания. |
| `receivingPatternRef` | BDPF.4 → BDPF.5 → BDPF.6 |
| `expertTrackingStatus` | `analyzedWithGaps`; допускается переход к UseConcept только с явной gap-row. |

## 7. Что отслеживает экспертиза

Экспертиза на старте услуги должна отслеживать не «правильность решения», а **проведённость и пригодность анализа**:

1. Все известные исходные carriers зарегистрированы с владельцем, датой, версией и статусом анализа.
2. По каждому значимому carrier есть извлечённые source signals или обоснованное указание, что в текущем scope actionable signal нет.
3. Каждый source signal имеет `needKind`, affected scope, affected structure kind, admissible/non-admissible use и source-return condition.
4. Неопределённости и противоречия вынесены в отдельный register, а не спрятаны в тексте.
5. Сигналы переведены хотя бы до `architectureStructuringNeed` и candidate/unknown structure kinds.
6. Есть начальная связь с BDPF.1/BDPF.4/BDPF.5/BDPF.6, то есть с ОКС, использованием, системой и архитектурными вопросами.
7. Gate фиксирует одно из решений: `pass`, `passWithReservations`, `hold`, `reject`, `abstain`.
8. Gate прямо указывает, какие работы допустимы дальше, а какие недопустимы до source return.

## 8. Что не принимать как анализ исходных данных

| Непригодная форма | Почему не годится | Исправление |
|---|---|---|
| «Перечень исходных данных» | Показывает наличие carriers, но не показывает извлечённые проектные сигналы. | Добавить `DesignSourceSignalUseRecord` по каждому значимому сигналу. |
| «Требования учтены» | Не показывает, какие структуры затронуты и какие решения ещё нельзя принимать. | Разложить требования на source signals, needKind, structure kind и receiving owner. |
| Копирование пунктов ТЗ | Переносит текст, но не выполняет проектное распознавание. | Выделить extractedSignal и supportedQuestion. |
| «Анализ выполнен, замечаний нет» | Не создаёт трассируемой P2S-цепочки. | Показать carrier → signal → need → structure → gap/source return. |
| Ранняя фиксация решения | Подменяет анализ исходных данных проектным решением. | Вернуть запись в `SignalIntake`, `ProblemShaping` или `StructureKindTriage`. |
| Expert checklist без проектных records | Проверяет форму взаимодействия, но не ход проектного рассуждения. | Использовать `SourceAnalysisReadinessGate` поверх records проектировщика. |

## 9. Сервисная цепочка предоставления услуги от анализа исходных данных

```text
ServiceStart
→ SourceCarrierInventory
→ SourceSignalExtraction
→ SourceGapAndAmbiguityRegister
→ InitialUseScenarioExtraction
→ InitialBuiltAssetSystemCard
→ ProblemToStructureFlowCard
→ SourceAnalysisReadinessGate
→ UseConceptRecord
→ SystemConceptRecord
→ ArchitectureQuestionCard
→ CandidateArchitecturePalette / stop reason
→ Criteria / eval / comparison
→ PAD
→ EvidenceTrace
→ DocumentationProjection
→ ExpertReview
→ FeedbackRepair / source return
```

### 9.1. Шаги услуги

| Шаг | Исполнитель | Рабочий продукт | Экспертное отслеживание |
|---|---|---|---|
| 1. Зафиксировать контур услуги | Проектировщик + эксперт + заказчик | `ServiceStartRecord`, scope, object/site, stage, roles | Эксперт проверяет, что не смешаны услуга сопровождения, проектное решение и проверка ПД. |
| 2. Собрать реестр carriers | Проектировщик | `SourceCarrierInventory@Project` | Проверка полноты регистрации: ТЗ, отраслевое ТЗ, участок, ТУ, известные изыскания/обследования. |
| 3. Извлечь source signals | Проектировщик | `DesignSourceSignalUseRecord[*]` | Проверка наличия extractedSignal, needKind, affected scope, source locus. |
| 4. Зафиксировать пробелы | Проектировщик | `SourceGapAndAmbiguityRegister` | Проверка, что дефицит данных не спрятан и имеет disposition. |
| 5. Развернуть использование | Проектировщик | `InitialUseScenarioExtraction` | Проверка, что сценарии извлекаются из источников и не превращаются в решение. |
| 6. Развернуть ОКС как систему | Проектировщик | `InitialBuiltAssetSystemCard` | Проверка, что сигналы привязаны к объекту, участку, подсистемам и интерфейсам. |
| 7. Перевести problem-side в структуры | Проектировщик | `BuiltAssetProblemToStructureFlowCard` | Проверка, что исходные данные доведены до `architectureStructuringNeed`, unknown/candidate structures и next owner. |
| 8. Провести gate анализа | Эксперт | `SourceAnalysisReadinessGate` | `pass/passWithReservations/hold/reject/abstain`; эксперт не выбирает проектное решение. |
| 9. Передать в следующий проектный шаг | Проектировщик | BDPF.4/5/6 records | Эксперт отслеживает, что последующие решения опираются на source-signal records и source-return conditions. |

## 10. Минимальный threshold прохождения начального анализа

Анализ исходных данных можно считать проведённым для перехода к BDPF.4/BDPF.5/BDPF.6, если выполнены условия:

```text
CC-ID-1: Все известные carriers зарегистрированы с sourceOwner, date/version и freshness boundary.
CC-ID-2: Для каждого carrier указано extractionStatus.
CC-ID-3: Есть 5-10 ключевых DesignSourceSignalUseRecord для стартового scope или обоснование меньшего числа.
CC-ID-4: Каждый key signal имеет needKind и affectedStructureKindRefs; это классификация зоны структурного воздействия, а не architectureStructuringNeed.
CC-ID-5: Каждый key signal имеет supportedQuestion и receivingPatternRef.
CC-ID-6: Все missing/ambiguous/conflicting items вынесены в gap register.
CC-ID-7: Есть хотя бы одна P2S-карта, где source signals доведены от affectedStructureKindRefs до architectureStructuringNeed.
CC-ID-8: Gate явно указывает, что можно делать дальше, что нельзя, и к каким источникам надо вернуться.
CC-ID-9: Никакой carrier, checklist, статус или expert comment не объявлен проектным решением, доказательством или разрешением на work-entry.
```

## 11. Рекомендуемая вставка в `DPF-building-design.md`

```markdown
# BDPF.3B — Анализ исходных данных как стартовая услуга сопровождения

## Problem frame

Используйте этот паттерн, когда услугу экспертного сопровождения нужно начинать не с произвольного текущего момента и не с проверки ПД, а с анализа исходных данных: ТЗ, отраслевого или технологического ТЗ, участка, ГПЗУ, ТУ, изысканий, обследований, требований эксплуатации и иных исходных carriers.

Проектировщик проводит анализ. Экспертиза отслеживает, что анализ проведён в форме, пригодной для дальнейшей P2S-цепочки.

## Рабочий продукт

`InitialDataAnalysisPackage@Project`, включающий:

- `SourceCarrierInventory@Project`;
- `DesignSourceSignalUseRecord@Project[*]`;
- `SourceGapAndAmbiguityRegister@Project`;
- `InitialUseScenarioExtraction@Project`;
- `InitialBuiltAssetSystemCard@Project`;
- `BuiltAssetProblemToStructureFlowCard@InitialDataAnalysis[*]`;
- `SourceAnalysisReadinessGate@Project`;
- `ExpertTrackingRecord@Project`.

## Минимальное правило

Анализ исходных данных не считается проведённым, если предъявлен только перечень документов или утверждение «исходные данные учтены».

Анализ считается проведённым для следующего проектного шага, если видно:

1. какие исходные carriers получены;
2. какие source signals из них извлечены;
3. какие `needKind` они создают;
4. какие структуры ОКС становятся неизвестными, спорными или ограниченными;
5. какие пробелы, противоречия и source-return conditions остаются;
6. какой следующий BDPF/FPF-owner должен принять claim;
7. какой readiness status допускает или блокирует следующий шаг.

Экспертный gate не выбирает проектное решение и не доказывает его допустимость. Он фиксирует, что проектировщик предъявил проверяемый след анализа исходных данных.
```

## 12. Итоговая формула для услуги

```text
Проектировщик обязан предъявить не “анализ исходных данных” как текст,
а трассируемый InitialDataAnalysisPackage:
source carrier → extracted source signal → needKind → affected structure
→ architectureStructuringNeed → gap/source return → receiving owner → readiness.

Экспертиза обязана отслеживать наличие, связность и пригодность этого пакета,
но не подменять проектировщика и не превращать gate в проектное решение.
```
