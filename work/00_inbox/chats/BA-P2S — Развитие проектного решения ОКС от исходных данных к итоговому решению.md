# BA-P2S — Развитие проектного решения ОКС от исходных данных к итоговому решению

Link: https://chatgpt.com/g/g-p-6a3a407d2f30819197a4665bfa85dd41-metodologiia-soprovozhdeniia-proektirovaniia/c/6a424784-43ac-83ea-822b-a040d0f9a779

> Type: локальный project-use pattern под C.32.P2S / C.30.AD.BA
> 
> Status: рабочий черновик для методологии сопровождения проектирования
> 
> Primary EoC: ОКС как физический / будущий built asset, то есть описываемый holon
>
> Не EoC: BIM-модель, комплект ПД/РД, ведомость, чертёж, дашборд, ТЭП, экспертное заключение, график, согласование

## 1. Problem frame

Есть исходные данные по ОКС:
 - ТЗ, 
 - ИРД, 
 - ГПЗУ, 
 - результаты изысканий, 
 - ТУ, 
 - ограничения площадки, 
 - требования заказчика, 
 - нормативные требования, 
 - существующие сети, 
 - данные эксплуатации или реконструкции

Но пока не ясно:
 - какие структуры ОКС должны быть выбраны, 
 - какие альтернативы допустимы, 
 - какие потери принимаются, 
 - и что именно можно передавать дальнейшую работу.

```markdown
ProblemToStructureArchitecturingFlowCard@Project
для ОКС:
  describedHolonRef: ОКС
  boundedContextRef: стадия / контур проектирования
  problemPressure: какое давление создают исходные данные
  unknownStructure: какие структуры ещё не определены
  candidateStructureKindRefs: какие типы структур надо синтезировать
  architectureCharacteristicRefs: какие характеристики надо удержать
  neighboringOwnerForNextClaim: какой следующий FPF-владелец нужен
```

%% `problemPressure` - как вариант заменить, на `architectureStructuringNeed`, но мне кажется, что первый вариант лучше, как рабочий %%

| Поле                         | Что означает                                                                                                          | Пример для ОКС                                                                                                                                                         |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `unknownStructure`           | Конкретная структура ОКС ещё не известна, не выбрана, не доказана или не наблюдена. Это неопределённость содержания.  | Неизвестно, как разделить чистые/грязные потоки в больнице; неизвестна фактическая несущая способность существующих плит; неясно, где пройдёт магистральный MEP-ствол. |
| `candidateStructureKindRefs` | Какие **типы архитектурно значимых структур** нужно рассматривать. Это не вариант решения, а классификатор структуры. | `MaterialSpatialStructure`, `PlacementDeploymentStructure`, `TransformationFlowStructure`, `ControlStructure`, `FunctionalStructure`, `ModuleInterfaceStructure`.      |

FPF C.30.ASV задаёт ArchitectureStructureKindRef как локальный классификатор над architecture-relevant U.Structure, а не как новый root-kind. Там прямо перечислены такие значения, как FunctionalStructure, TransformationFlowStructure, ControlStructure, ModuleInterfaceStructure, PlacementDeploymentStructure, MaterialSpatialStructure, InformationDataStructure, SecurityTrustBoundaryStructure и другие.

Для ОКС полезно локально маппить так:

| Практическая структура ОКС                       | FPF-near structure kind                                                             |
| ------------------------------------------------ | ----------------------------------------------------------------------------------- |
| Генплан, посадка, подъезды, связи с участком     | `PlacementDeploymentStructure`                                                      |
| Объёмно-планировочная схема, помещения, зоны     | `MaterialSpatialStructure` + `FunctionalStructure`                                  |
| Потоки пациентов, персонала, материалов, отходов | `TransformationFlowStructure`                                                       |
| Несущая схема                                    | `MaterialSpatialStructure` / `OtherDeclaredStructureKind` with local definition     |
| Инженерные системы и MEP-интерфейсы              | `ModuleInterfaceStructure`, `FunctionalStructure`, `TransformationFlowStructure`    |
| Пожарные отсеки, эвакуация, дымоудаление         | `ControlStructure`, `TransformationFlowStructure`, `ConstraintRequirementStructure` |
| BMS, диспетчеризация, автоматика                 | `ControlStructure`                                                                  |
| Идентификация помещений, систем, оборудования    | description/designation relation under `C.30.AD.BA`, with structure refs            |
| Стоимость, энергия, эксплуатация                 | usually characteristic/eval/source relation; not structure kind by default          |

Правило: не перечислять все возможные структуры “для полноты”. C.30.ASV требует выбирать минимальный набор structure-kind, который меняет следующий архитектурный ход; иначе структура превращается в чеклист.

### architectureCharacteristicRefs и связь с целями / потребностями / ConOps

Цели и потребности живут на стороне ConOps / stakeholder needs / operational scenarios / value concerns. architectureCharacteristicRefs — это уже архитектурные характеристики, то есть свойства выбранных или кандидатных структур, по которым можно понять, насколько структура помогает ConOps.

Цепочка такая:
```markdown
stakeholder need / ConOps need
→ operational scenario
→ required capability / function / constraint / value protection
→ architecture characteristic with bearer and scale
→ candidate or selected structure
→ C.16 measure / C.25 Q-Bundle / C.32.ACE eval
```
Пример:

```markdown
ConOps need:
  "потоки инфекционных и неинфекционных пациентов не должны пересекаться"

Architecture characteristics:
  flowSeparationIntegrity
  infectionControlSafety
  operationalThroughput
  maintainabilityOfIsolationZones

Candidate structures:
  separate entrances;
  clean/dirty corridor split;
  pressure cascade;
  dedicated elevator group;
  separated waste route.
```
То есть характеристика не равна цели. Цель говорит зачем. Характеристика говорит какое свойство структуры надо удержать и как потом читать/измерять/оценивать.

FPF разделяет characteristic, measurement и eval: C.16 применяется для измерений, координат, шкал, единиц и evidence stub; C.25 — когда качество составное; C.32.ACE — когда нужна eval-программа или eval-result по архитектурным критериям.

### neighboringOwnerForNextClaim

Это следующий FPF-паттерн-владелец, который должен принять следующий claim.

Примеры:

| Текущая ситуация                                        | `neighboringOwnerForNextClaim`       |
| ------------------------------------------------------- | ------------------------------------ |
| Сигнал ещё сырой: жалоба, риск, фрагмент ТЗ             | `C.22.2` ProblemCard                 |
| Нужно оформить архитектуру ОКС как claim                | `C.30`                               |
| Нужно определить, какая структура видна в представлении | `C.30.ASV`                           |
| Нужно породить варианты                                 | `C.32`                               |
| Нужно построить критерии качества                       | `C.32.ACS` / `C.25`                  |
| Нужно измерять или моделировать характеристику          | `C.16` / `C.32.ACE`                  |
| Нужно сравнить варианты                                 | `A.19.CPM`                           |
| Нужно выбрать selected set                              | `A.19.SelectorMechanism` / `G.5`     |
| Нужно принять проектное архитектурное решение           | `C.32.PAD`                           |
| Нужно опубликовать BIM/IFC/виды/описания                | `C.30.AD.BA` / `E.17`                |
| Нужно передать в метод/план/работу                      | `A.15`, `A.15.2`, `A.15.5`, `A.15.1` |
| Нужно evidence / assurance / gate                       | `A.10`, `B.3`, `A.21`                |


## 2. Problem

В проектировании ОКС часто происходит подмена:

исходные данные → сразу проектное решение → сразу комплект документации.

## 3. Forces

| Сила                                           | Напряжение                                                                                                              |
| ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Исходные данные богаты                         | Они кажутся достаточными, но сами не выбирают структуру ОКС.                                                            |
| Проектировщик хочет быстрее “рисовать решение” | Но пока не названы структура, носитель функции, ограничения, альтернативы и критерии.                                   |
| BIM/модель удобны                              | Но модель остаётся описанием, а не ОКС и не решением.                                                                   |
| Нормативы и ТУ выглядят как готовый ответ      | Но они задают ограничения, admissibility и источники, а не весь синтез структуры.                                       |
| Нужно выбрать вариант                          | Но один красивый вариант, расчётный score или предпочтение заказчика не должны скрывать альтернативы.                   |
| Итог нужен в документации                      | Но проектная документация — публикация/описание выбранных структур и решений, а не само решение и не реализованный ОКС. |
| Реализация позже покажет расхождение           | Ожидаемая структура в проекте и фактическая структура в строительстве/эксплуатации должны быть связаны обратной связью. |


## 4. Solution — как должно развиваться проектное решение

### 4.1. Зафиксируй ОКС и контекст

Не начинай с документа. Начни с EoC.

```markdown

describedHolonRef: ОКС / корпус / здание / сооружение / очередь / реконструируемый объект
boundedContextRef: стадия и контур:
  предпроект / ПД / РД / вариантное проектирование / реконструкция / эксплуатационная модернизация

```

Минимальный вопрос:
> “Архитектура какого ОКС, в каком контексте, для какого проектного давления сейчас развивается?”

Для FPF-паттерна полезнее задавать контекст как состояние архитектурной работы и степень закрытия пространства вариантов.

Предлагаю форму:

```markdown
boundedContextRef:
  holonScope:
  lifecycleSlice:
  nqdWorkState:
  closurePosture:
  sourceMaturity:
  decisionMaturity:
  publicationMaturity:
```

#### NQD-like work states

| `nqdWorkState`           | Что означает                                                     | Что допустимо делать                                       | Что ещё нельзя                          |
| ------------------------ | ---------------------------------------------------------------- | ---------------------------------------------------------- | --------------------------------------- |
| `SignalIntake`           | Есть исходные сигналы, но проблема ещё не сформирована           | Собирать source signals, делать ProblemCard                | Нельзя делать architecture decision     |
| `ProblemShaping`         | Проблемная сторона reviewable, но структуры ещё не восстановлены | Формировать `architectureStructuringNeed`                  | Нельзя утверждать выбранную структуру   |
| `StructureKindTriage`    | Понятны типы структур, которые надо рассматривать                | Заполнить `candidateStructureKindRefs`, `unknownStructure` | Нельзя считать это candidate solution   |
| `CriteriaShaping`        | Появляются характеристики и критерии                             | Делать HCS/ACS, Q-Bundle, measurement plan                 | Нельзя оптимизировать без bearer/scale  |
| `CandidateGeneration`    | Синтезируются варианты                                           | Создавать `CandidateArchitecturePalette`                   | Нельзя выбрать победителя               |
| `FrontIllumination`      | Варианты оценены, виден trade-off front                          | Делать C.32.ACE, C.16, CPM input                           | Нельзя сворачивать в один score         |
| `RetainedSetPublication` | Публикуется shortlist / selected set                             | G.5 / selected-set publication                             | Это ещё не PAD decision                 |
| `ArchitectureCommitment` | Принимается проектное архитектурное решение                      | `C.32.PAD`                                                 | Нельзя путать с ADR или BIM             |
| `DescriptionPublication` | Публикуются views/BIM/IFC/описания                               | `C.30.AD.BA`, `E.17`                                       | Описание не становится ОКС или решением |
| `WorkPreparation`        | Решение передаётся в метод/план/readiness                        | A.15-family                                                | План не является выполненной работой    |
| `RealizationObservation` | Появляются actual structures                                     | performed work, inspection, commissioning                  | Нельзя подменять факт моделью           |
| `FeedbackRepair`         | Фактическая структура или eval возвращает вопрос                 | C.32.FAIL / C.32.PAD repair / E.23 / G.11                  | Нельзя “залатать” только текстом        |

Пример boundedContextRef
```markdown
boundedContextRef:
  holonScope: HospitalBuilding.BlockA
  lifecycleSlice: design-to-commissioning
  nqdWorkState: CandidateGeneration
  closurePosture: optionSpaceOpen
  sourceMaturity: surveyAndConOpsAcceptedButMEPInterfacesUnstable
  decisionMaturity: noPADYet
  publicationMaturity: internalCandidateViewsOnly
```

### 4.2. Преврати исходные данные в давление, а не в решение

Исходные данные надо раскладывать не как “входной архив”, а как source signals и constraints.

```markdown
problemPressure:
  pressureKind:
    regulatoryConstraint
    siteConstraint
    functionalDemand
    capacityDemand
    safetyPressure
    constructabilityPressure
    operationOrMaintenancePressure
    costOrSchedulePressure
    actualStructureDivergesFromExpectedStructure
    otherDeclared
  sourceSignalRefs:
    ТЗ
    ГПЗУ
    ИРД
    результаты изысканий
    ТУ
    технологическое задание
    требования пожарной безопасности
    требования эксплуатации
    данные обследования
    ограничения площадки
  currentStopOrReturnReason:
    что пока нельзя утверждать
```

Если исходные данные ещё не дают reviewable problem-side record, остановись на C.22.2 / ProblemCard.

#### Таблица needKind
| `needKind`                    | Какую информацию даёт                                                                            | Какие структуры обычно затрагивает                                                                                    | Что не решает само по себе                                                     |
| ----------------------------- | ------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| `regulatoryConstraintNeed`    | Норматив, ТУ, ограничение, обязательное условие, запрет, допустимый диапазон                     | `ConstraintRequirementStructure`, `ControlStructure`, `MaterialSpatialStructure`, `TransformationFlowStructure`       | Не выбирает планировку или конструктивную схему; задаёт boundary/admissibility |
| `sitePlacementNeed`           | Ограничения участка: красные линии, подъезды, рельеф, инсоляция, охранные зоны, соседние объекты | `PlacementDeploymentStructure`, `MaterialSpatialStructure`, `TransformationFlowStructure`                             | Не доказывает функциональную достаточность                                     |
| `functionalScenarioNeed`      | Что пользователи/операторы должны делать в ОКС; ConOps-сценарии                                  | `FunctionalStructure`, `TransformationFlowStructure`, `MaterialSpatialStructure`                                      | Не задаёт один вариант компоновки                                              |
| `capacityThroughputNeed`      | Требуемые мощности, потоки, очереди, пиковые нагрузки, пропускная способность                    | `TransformationFlowStructure`, `MEP-related structures`, `ControlStructure`                                           | Не выбирает carrier/bearer без вариантного синтеза                             |
| `safetyLossControlNeed`       | Какие потери надо предотвратить: пожар, инфекция, авария, травмы, отказ систем                   | `ControlStructure`, `SecurityTrustBoundaryStructure`, `TransformationFlowStructure`, `ConstraintRequirementStructure` | Не является safety proof или assurance                                         |
| `constructabilityNeed`        | Что должно быть строимо: монтаж, доступ, временные схемы, логистика, очередность                 | `WorkMethodStructure`, `PlacementDeploymentStructure`, `MaterialSpatialStructure`                                     | Не является work plan или performed work                                       |
| `operationMaintenanceNeed`    | Как объект будет эксплуатироваться, обслуживаться, ремонтироваться, обновляться                  | `ModuleInterfaceStructure`, `PlacementDeploymentStructure`, `ControlStructure`, `InformationDataStructure`            | Не является эксплуатационным evidence                                          |
| `costScheduleExposureNeed`    | Стоимостные и календарные ограничения, чувствительности, риск перерасхода                        | characteristic/eval/work-source relation; sometimes structures                                                        | Не выбирает архитектуру по одному числу                                        |
| `existingAssetDivergenceNeed` | Фактическое состояние существующего ОКС отличается от ожидаемого/документированного              | `actualStructureRefs`, `sourceReturnCondition`, `MaterialSpatialStructure`, `MEP`, `ControlStructure`                 | Не является автоматическим redesign; требует source-return                     |
| `informationRelianceNeed`     | BIM/IFC/обследование/реестр/цифровой двойник используется как источник                           | `C.30.AD.BA` description/source relation                                                                              | Не делает модель ОКС, evidence, gate или decision                              |
| `otherDeclaredNeed`           | Локально объявленная потребность                                                                 | Должна назвать affected structures и governing pattern                                                                | Нельзя оставлять как “прочее” без definition                                   |

#### Таблица source signals

| Source signal                        | Что извлекать                                                                      | Типичные ошибки                                                                   |
| ------------------------------------ | ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| ТЗ / задание заказчика               | Цели, ограничения, функции, мощности, критерии приёмки, приоритеты                 | Сразу считать ТЗ решением или выбранной архитектурой                              |
| ConOps / эксплуатационные сценарии   | Роли пользователей, режимы работы, последовательности действий, потоки, исключения | Считать сценарий планировкой                                                      |
| ГПЗУ / градостроительные ограничения | Границы, зоны, высоты, отступы, регламенты участка                                 | Считать, что участок уже выбрал объёмно-планировочную структуру                   |
| ИРД / разрешительная база            | Правовые и административные условия применения                                     | Смешивать разрешение, evidence, gate и architecture decision                      |
| Инженерные изыскания                 | Геология, гидрология, топография, экология, существующие условия                   | Считать отчёт достаточным для выбора конструктивной схемы без candidate synthesis |
| Обследование существующего ОКС       | Фактические конструкции, дефекты, скрытые элементы, расхождение с документацией    | Считать старые чертежи actual structure                                           |
| ТУ ресурсоснабжающих организаций     | Точки подключения, мощности, ограничения, условия, резервирование                  | Считать ТУ инженерным решением                                                    |
| Технологическое задание              | Производственные/медицинские/лабораторные/логистические процессы                   | Смешивать технологический процесс и архитектурную структуру                       |
| Пожарные требования                  | Отсеки, эвакуация, системы обнаружения/управления, дымоудаление                    | Считать план эвакуации safety assurance                                           |
| Требования эксплуатации              | Доступ, обслуживание, режимы ремонта, отказоустойчивость, замены                   | Добавить “эксплуатацию” как общий вид без selected structures                     |
| BIM / IFC / цифровой двойник         | Описание, view, source relation, designation, currentness                          | Подменять ОКС моделью; `C.30.AD.BA` прямо блокирует это                           |
| Стоимостные/сроковые данные          | Constraints, exposure, trade-off, eval input                                       | Выбрать архитектуру по одному cost score                                          |
| Экспертные заключения                | Source signal, evidence candidate, issue cue                                       | Считать авторитет решением или proof                                              |

#### Что такое reviewable problem-side record

В этом контексте это не “исходные данные собраны в папку”. Это минимальная problem-side карточка, которую другой участник может проверить и понять:

```markdown
ReviewableProblemSideRecord:
  describedHolonRef:
  boundedContextRef:
  sourceSignalRefs:
  acceptedProblemSignal:
  architectureStructuringNeed:
  affectedHolonOrScope:
  unknowns:
  sourceSupportPosture:
  validationBoundary:
  freshnessBoundary:
  currentStopOrReturnReason:
  firstReceivingPatternRef:
```

Пример:
```markdown
ReviewableProblemSideRecord:
  describedHolonRef: HospitalBuilding.BlockA
  boundedContextRef: SignalIntake → ProblemShaping
  sourceSignalRefs:
    ConOps.PatientFlow.v2
    ExistingBuildingSurvey.v1
    FireSafetyConstraints.v1
  acceptedProblemSignal:
    public patient flow, staff flow, dirty logistics flow, and emergency flow
    cannot be assumed compatible in the current layout.
  architectureStructuringNeed:
    needKind: functionalScenarioNeed + safetyLossControlNeed
    plain: need to choose or refine flow and spatial structures
  unknowns:
    location of separated dirty route;
    feasible vertical transport separation;
    fire-compartment alignment.
  validationBoundary:
    not yet a candidate architecture;
    not yet a code compliance proof.
  firstReceivingPatternRef:
    C.30.ASV then C.32
```

C.32.P2S говорит: если источник ещё только problem-side signal, сначала использовать C.22.2, и только потом продолжать P2S.

### 4.3. Назови структуры ОКС, которые должны измениться или быть выбраны

Проектное решение развивается не “по разделам документации”, а по выбираемым структурам ОКС.
Пример типовых structure-kind для ОКС:

| Structure kind                          | Что проектно выбирается                                                 |
| --------------------------------------- | ----------------------------------------------------------------------- |
| Site / placement structure              | посадка на участке, связи с окружением, зоны, подъезды                  |
| Spatial-planning structure              | планировочная схема, функциональные зоны, потоки людей/материалов       |
| Load-bearing structure                  | конструктивная схема, несущие элементы, устойчивость                    |
| Envelope structure                      | ограждающие конструкции, тепловой/влажностный контур                    |
| MEP / engineering systems structure     | инженерные системы, интерфейсы, трассировки, резервирование             |
| Fire / evacuation / control structure   | пожарные отсеки, эвакуация, автоматика, управление рисками              |
| Construction-method structure           | технологичность строительства, очередность, временные структуры         |
| Operation / maintenance structure       | доступность обслуживания, ремонтопригодность, эксплуатационные сценарии |
| Reference-designation / asset structure | идентификация помещений, систем, оборудования, asset hierarchy          |

Принцип: architectureContent — это не “разделы проекта”. Это содержание архитектурной работы, привязанное к структурам, характеристикам и вариантам.

```markdown
architectureContent:
  candidateStructureKindRefs:
  selectedStructureRefs?:
  expectedStructureRefs?:
  actualStructureRefs?:
  architectureCharacteristicRefs:
  architectureCharacteristicCriteriaSetRef?:
  qBundleRefs?:
  candidateSynthesisRef?:
```
| Поле                                       | Что должно быть внутри                                                                | Пример для больницы                                                                                       |
| ------------------------------------------ | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `candidateStructureKindRefs`               | Типы структур, которые надо рассмотреть                                               | `MaterialSpatialStructure`, `TransformationFlowStructure`, `ControlStructure`, `ModuleInterfaceStructure` |
| `selectedStructureRefs`                    | Уже выбранные структуры, если они есть                                                | selected clean/dirty flow separation; selected fire-compartment layout                                    |
| `expectedStructureRefs`                    | Структуры, которые должны появиться после проектирования/строительства                | expected separated patient/staff/logistics circulation                                                    |
| `actualStructureRefs`                      | Структуры, которые реально наблюдены после реализации, обследования или эксплуатации  | actual route crosses dirty logistics near imaging department                                              |
| `architectureCharacteristicRefs`           | Характеристики, ради которых структуры сравниваются/выбираются                        | infection-control safety, throughput, maintainability, adaptability                                       |
| `architectureCharacteristicCriteriaSetRef` | Ссылка на C.32.ACS criteria set, где характеристики получили bearer, scale, use class | HospitalACS-v1                                                                                            |
| `qBundleRefs`                              | Ссылки на C.25, если качество составное                                               | SafetyQBundle, MaintainabilityQBundle                                                                     |
| `candidateSynthesisRef`                    | Ссылка на C.32 candidate palette                                                      | CandidateArchitecturePalette@HospitalBlockA-v1                                                            |



### 4.4. Зафиксируй структурную неопределённость

Перед генерацией вариантов явно запиши, что ещё неизвестно.

```markdown
structuralInformation:
  unknownStructure:
    какие носители функции ещё не найдены
    какие интерфейсы не определены
    какие размещения конфликтуют
    какие системы конкурируют за пространство/мощность/доступ
  selectedStructure:
    что уже выбрано и чем подтверждено
  expectedStructure:
    что должно появиться в решении
  latentOrHiddenStructure:
    что может быть скрыто в модели/чертежах
  lostStructure:
    что теряется при укрупнении, схеме, BIM-view или таблице
  sourceReturnCondition:
    когда надо вернуться к изысканиям, модели, расчёту, источнику или эксперту
```
| Поле                                | Что означает                                             | Пример для ОКС                                                                                                                                                                                 |
| ----------------------------------- | -------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `unknownStructure`                  | Что ещё не известно или не выбрано                       | Неизвестно, где провести грязный логистический поток без пересечения с пациентами; неизвестна фактическая несущая способность перекрытий; неизвестна доступность обслуживания ВК/ОВ.           |
| `selectedStructure`                 | Что уже выбрано как структура                            | Выбрана схема с отдельным сервисным ядром; выбрана конструктивная сетка 8,4×8,4; выбрана схема пожарных отсеков.                                                                               |
| `expectedStructure`                 | Какая структура должна быть реализована                  | После строительства должны быть независимые public/staff/logistics flows; оборудование должно обслуживаться из технических зон без входа в стерильные помещения.                               |
| `actualStructure`                   | Что фактически наблюдается                               | На авторском надзоре обнаружено, что трасса медгазов изменилась; при commissioning видно, что сервисный маршрут пересекает поток пациентов.                                                    |
| `capturedInDescriptionsOrDecisions` | Что попало в BIM, чертеж, PAD, ADR, таблицу              | BIM содержит помещения и трассы MEP; PAD фиксирует выбранную flow structure; чертёж показывает fire compartments.                                                                              |
| `handedToMethodsOrWork`             | Что передано в метод, расчёт, моделирование, стройработы | Передать выбранную fire-compartment structure в пожарное моделирование; передать MEP zoning в BIM-координацию; передать конструктивную сетку в расчётную модель.                               |
| `latentOrHiddenStructure`           | Что есть в объекте, но не видно в текущем виде           | Зависимость обслуживания от съёмных потолков; скрытая связь между pressure cascade и дверными режимами; временные монтажные проёмы.                                                            |
| `lostStructure`                     | Что потеряно при укрупнении, схеме, виде, таблице        | План 1:500 потерял вертикальные потоки; BIM-view скрыл последовательность монтажа; таблица помещений потеряла adjacencies.                                                                     |
| `sourceReturnCondition`             | Когда надо вернуться к источнику                         | Если BIM clash затрагивает evacuation route; если обследование не подтвердило несущую способность; если ConOps изменил поток пациентов; если commissioning показал actual/expected divergence. |



### 4.5. Определи architecture characteristics до оптимизации

Не сравнивай варианты до того, как сказал, что значит “лучше”.

Примеры для ОКС:
```markdown
architectureCharacteristicRefs:
  safety / безопасность
  regulatory fit / нормативная пригодность
  constructability / строимость
  maintainability / обслуживаемость
  adaptability / адаптируемость
  operational continuity / эксплуатационная непрерывность
  energy performance / энергетическая результативность
  lifecycle cost exposure / жизненный стоимостной профиль
  source-return cost / стоимость возврата к источникам
```
| Characteristic                         | ConOps / need связь                                  | Bearer / structure                       | Возможные C.16 metrics                                                         | C.25?                                           | C.32.ACE eval example                            |
| -------------------------------------- | ---------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------ | ----------------------------------------------- | ------------------------------------------------ |
| `lifeSafety`                           | Люди должны безопасно покинуть или переждать событие | fire/evacuation/control structures       | RSET/ASET, travel distance, evacuation capacity, smoke extraction rate         | Да, safety обычно bundle                        | Fire scenario simulation + code review           |
| `infectionControlSafety`               | Разделить инфекционные/чистые потоки                 | flow/spatial/MEP/control                 | count of crossings, pressure cascade compliance, ACH, isolation-room adjacency | Да                                              | Scenario walkthrough + airflow simulation        |
| `functionalThroughput`                 | Обслужить заданный поток пациентов/пользователей     | spatial + transformation-flow structures | patients/hour, queue length, bottleneck utilization, room turnover time        | Иногда                                          | Discrete-event simulation                        |
| `maintainability`                      | Обслуживать системы без остановки критичных функций  | MEP, access, module/interface structures | % equipment with required clearance, MTTR, access route length                 | Да                                              | Maintenance walkthrough + BIM clearance check    |
| `adaptability`                         | Перестраивать функции при изменении программы        | grid, spatial, MEP zoning                | % reconfigurable area, spare shaft capacity, change cost/time                  | Да                                              | Scenario set for future departments              |
| `constructability`                     | Построить с допустимыми рисками, сроками, логистикой | work-method, placement, material-spatial | number of temporary works, crane reach conflicts, sequence clashes             | Да                                              | 4D sequencing review                             |
| `energyPerformance`                    | Эксплуатировать в целевом энергопрофиле              | envelope, MEP, control                   | kWh/m²·year, peak load, U-value, COP, demand response                          | Иногда                                          | Energy model comparison                          |
| `operationalContinuity`                | Работать при отказах/ремонте                         | MEP redundancy, control, zoning          | downtime, N+1 coverage, recovery time, service interruption area               | Да                                              | Failure scenario eval                            |
| `regulatoryFit`                        | Проект должен быть admissible для норм/экспертизы    | constraint/control/spatial structures    | compliance state, deviations count, unresolved constraints                     | Не совсем quality; часто gate/evidence-adjacent | Compliance matrix review, not decision by itself |
| `lifecycleCostExposure`                | CAPEX/OPEX/замены не должны разрушать value case     | materials, MEP, maintenance structure    | NPV, replacement cycles, cost variance, sensitivity                            | Да                                              | Life-cycle cost scenario eval                    |
| `epiplexity / structural entanglement` | Структура должна быть управляемой и изменяемой       | architecture structure relations         | coupling density, dependency cycles, hidden interface count                    | Может быть bundle                               | DSM/graph review, not decision alone             |


### 4.6. Сгенерируй кандидатные конфигурации

Теперь можно делать варианты.

```markdown
candidateSetOrPaletteRef:
  вариант 1: структура A
  вариант 2: структура B
  вариант 3: структура C
```
Каждый вариант должен называть:

```markdown
candidateArchitectureConfiguration:
  affectedStructureRefs:
  intendedGain:
  acceptedLoss?:
  constraints:
  bearerFeasibility:
  sourceReturnCondition:
  nonAdmissibleUse:
```

C.32.P2S отправляет синтез кандидатных конфигураций в C.32, а сравнение/выбор/публикацию выбранного множества — к своим владельцам: A.19.CPM, A.19.SelectorMechanism, C.18, C.19, G.5, C.11

#### Пример candidate configuration для больницы

```markdown
CandidateArchitectureConfiguration@Project:
  candidateRef: HOSP-C1

  candidateName:
    separated diagnostic-treatment spine with independent service core

  describedHolonRef:
    HospitalBuilding.BlockA

  boundedContextRef:
    holonScope: HospitalBuilding.BlockA
    lifecycleSlice: design-to-commissioning
    nqdWorkState: CandidateGeneration
    closurePosture: optionSpaceOpen

  affectedStructureRefs:
    MaterialSpatialStructure:
      two diagnostic-treatment bars connected by controlled clinical spine;
      public atrium separated from clinical support zone.

    TransformationFlowStructure:
      public/patient flow separated from staff/logistics/waste flow;
      emergency route reaches imaging without crossing public waiting.

    ModuleInterfaceStructure:
      MEP risers grouped in service core;
      medical gases and HVAC zones aligned with clinical clusters.

    ControlStructure:
      fire compartments aligned with clinical clusters;
      smoke control and access-control zones follow the same split.

  architectureCharacteristicRefs:
    infectionControlSafety
    functionalThroughput
    maintainability
    operationalContinuity
    lifecycleCostExposure

  intendedGain:
    reduce clean/dirty crossings;
    improve maintenance access;
    simplify fire-control zoning;
    keep future clinical expansion possible.

  acceptedLoss:
    longer façade perimeter;
    increased initial MEP shaft concentration risk;
    more complex service-core coordination.

  constraints:
    existing urban boundary;
    utility connection point fixed at north-east;
    maximum building height;
    emergency access from south.

  bearerFeasibility:
    service core can carry MEP and logistics if shaft dimensions
    and fire separation are validated.

  sourceReturnCondition:
    return to site constraints if service access conflicts with fire lane;
    return to ConOps if emergency imaging route assumptions change;
    return to MEP source model if riser capacity is insufficient.

  nonAdmissibleUse:
    not a project architecture decision;
    not a BIM specification;
    not regulatory proof;
    not construction work authorization.
```

### 4.7. Сравни варианты, но не делай “победителя по красивости”

Сравнение должно быть отдельным шагом:

```markdown
comparisonBasis:
  evaluatedCandidates:
  characteristics:
  evidenceRefs:
  missingEvidence:
  protectedTradeOffs:
  unacceptableLosses:
  retainedAlternatives:
```

Правило: score, экспертное предпочтение, Pareto-точка, BIM-коллизия или расчёт не выбирают архитектуру сами по себе. Они становятся входом в comparison / selection / decision owner.

| Пункт                  | Значение                                                                   | Пример                                                                                   |
| ---------------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `evaluatedCandidates`  | Какие варианты сравниваются; каждый должен иметь candidateRef              | HOSP-C1 service core; HOSP-C2 distributed clinical clusters; HOSP-C3 vertical separation |
| `characteristics`      | По каким архитектурным характеристикам сравниваются варианты               | infection-control safety, throughput, maintainability, cost exposure                     |
| `evidenceRefs`         | Какие источники, расчёты, evals, simulations поддерживают чтение           | flow simulation, fire scenario eval, energy model, cost model, expert review             |
| `missingEvidence`      | Чего не хватает для честного сравнения                                     | нет обследования existing shafts; нет updated ConOps night-mode; нет smoke simulation    |
| `protectedTradeOffs`   | Что нельзя свернуть в один score                                           | safety не компенсируется CAPEX; maintainability не должна исчезнуть из-за throughput     |
| `unacceptableLosses`   | Потери, при которых вариант нельзя выбирать                                | dirty/clean crossing remains; emergency access blocked; no maintainable AHU access       |
| `retainedAlternatives` | Варианты, которые не выбраны сейчас, но остаются в portfolio/front/archive | HOSP-C2 retained for future expansion scenario                                           |


### 4.8. Прими проектное архитектурное решение

Когда commitment уже нужен, делай ArchitectureDecisionRelation@Project, а не сразу “оформляй раздел”.

Минимум:

```markdown
ArchitectureDecisionRelation@Project:
  describedHolonRef: ОКС
  boundedContextRef:
  decisionQuestion:
  candidateBasisRef:
  selectedArchitectureOption:
  affectedSelectedStructures:
  architectureCharacteristicTradeOff:
  acceptedLosses:
  methodAndWorkConsequences:
  sourceReturnCondition:
  reopenOrSupersessionCondition:
```

В C.32.P2S этот шаг принадлежит C.32.PAD: decision relation должен назвать selected architecture option, affected structures, trade-off, accepted losses, method/work consequences, source-return и условия repair/supersession.

#### Пример ArchitectureDecisionRelation@Project для больницы

```markdown
ArchitectureDecisionRelation@Project:
  decisionRef:
    PAD-HOSP-BlockA-FlowMEPFire-v1

  describedHolonRef:
    HospitalBuilding.BlockA

  boundedContextRef:
    nqdWorkState: ArchitectureCommitment
    lifecycleSlice: design-to-commissioning
    closurePosture: localClosureForDesignDevelopment

  decisionQuestion:
    Which spatial-flow-MEP-fire architecture option shall guide
    further design development for HospitalBuilding.BlockA?

  candidateBasisRef:
    CandidateArchitecturePalette@HospitalBlockA-v1
    comparisonBasis: FlowSafetyMaintainabilityComparison-v1

  selectedArchitectureOption:
    HOSP-C1 separated diagnostic-treatment spine
    with independent service core

  affectedSelectedStructures:
    selected MaterialSpatialStructure:
      clinical bars + public atrium + service core

    selected TransformationFlowStructure:
      separated public/patient/staff/logistics/waste flows

    selected ModuleInterfaceStructure:
      MEP shafts concentrated in service core with clinical-zone branches

    selected ControlStructure:
      fire compartments and smoke-control zones aligned with clinical clusters

  architectureCharacteristicTradeOff:
    improves infectionControlSafety and maintainability;
    improves fire-control legibility;
    increases façade perimeter and service-core coordination risk;
    may increase initial CAPEX.

  acceptedLosses:
    longer horizontal travel for part of staff routes;
    higher service-core coordination complexity;
    provisional +4–7% MEP coordination cost exposure.

  methodAndWorkConsequences:
    update spatial model and room adjacency matrix;
    run fire scenario simulation;
    run patient/logistics flow simulation;
    update MEP shaft sizing;
    create BIM coordination work package;
    prepare constructability review for service core.

  sourceReturnCondition:
    reopen if flow simulation shows clean/dirty crossing;
    reopen if fire authority rejects compartment strategy;
    reopen if MEP shaft sizing cannot carry peak demand;
    reopen if existing-structure survey blocks service core placement.

  reopenOrSupersessionCondition:
    supersede by PAD-HOSP-BlockA-v2 if any sourceReturnCondition is triggered
    or if ConOps changes major patient-flow assumptions.

  nonAdmissibleUse:
    not a construction permit;
    not performed work;
    not a safety proof;
    not a BIM model by itself.
```

## 4.9. Только потом публикуй проектные описания

После решения выпускаются не “само решение”, а описания и виды выбранных структур:

```markdown
ArchitectureDescription@Context / BuiltAssetArchitectureDescriptionUseCard:
  architectureClaimRef:
  describedHolonRef: ОКС
  selectedStructureRefs:
  viewSet:
    генплан
    планировочные решения
    конструктивная схема
    инженерные системы
    пожарная безопасность
    организация строительства
    эксплуатационная модель
    BIM / IFC / asset register
  correspondenceRefs:
  admissibleUse:
  nonAdmissibleUse:
```

Для ОКС особенно применим C.30.AD.BA: он говорит использовать built-asset architecture-description pattern для BIM, IFC, asset registers, digital-twin views, handover tables, cost/energy views и reference designations; при этом текущий вопрос об evidence, assurance, decision, work или gate должен уходить к прямому владельцу.

| Поле                              | Что писать                                                                                                                                                     |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `architectureClaimRef`            | Ссылка на `ArchitectureOf@Context` или PAD/architecture claim, который описывается. Не ссылка на файл.                                                         |
| `describedHolonRef`               | Физический ОКС: здание, корпус, сооружение, очередь, зона реконструкции.                                                                                       |
| `boundedContextRef`               | Контекст: NQD state, lifecycle slice, scope, maturity.                                                                                                         |
| `builtAssetKindCue`               | Facility, plant, bridge, campus building, infrastructure asset, etc. Для локального ОКС: `hospitalFacility`, `industrialBuilding`, `bridge`, `campusBuilding`. |
| `selectedStructureRefs`           | Конкретные выбранные структуры: flow structure, fire compartment structure, MEP zoning, structural grid.                                                       |
| `structureKindRefs`               | Классификаторы: `MaterialSpatialStructure`, `TransformationFlowStructure`, `ControlStructure`, etc.                                                            |
| `architectureStructuralViewRefs`  | Виды, каждый с viewpoint и selected structure. Например: fire-safety structural view, MEP interface view, public/staff/logistics flow view.                    |
| `referenceDesignationRefs`        | Схемы обозначений помещений, систем, оборудования. Не proof of identity/parthood.                                                                              |
| `assetInformationRefs`            | Asset register, COBie-like handover table, equipment data, maintenance data.                                                                                   |
| `digitalTwinViewRefs`             | Run-side views, BMS/sensor-connected descriptions, forecast/simulation views.                                                                                  |
| `publicationOrExchangeRefs`       | BIM model, IFC exchange, PDF set, model federation, dashboard publication.                                                                                     |
| `correspondenceRefs`              | Как виды соответствуют друг другу: room id ↔ asset id ↔ MEP equipment ↔ fire zone ↔ BIM element.                                                               |
| `sourceReturnCondition`           | Когда нужно вернуться к исходной модели, обследованию, расчёту, ConOps, ТУ, source view.                                                                       |
| `DesignRunTagRefs`                | Пометки design/run, если описание связывает проектную модель, as-built, эксплуатацию, датчики, maintenance work.                                               |
| `admissibleUse`                   | Для чего можно использовать: design coordination, structure recovery, source navigation, candidate comparison input.                                           |
| `nonAdmissibleUse`                | Чего это не доказывает: safety proof, gate passage, performed work, construction authorization, final decision.                                                |
| `firstNeighborPatternApplication` | Следующий owner: `C.30.ASV`, `C.32.PAD`, `A.10`, `B.3`, `A.15`, etc.                                                                                           |


### 4.10. Передай решение в метод, план и работу

Проектное решение должно породить ограничения и ожидания для работы, но не заменять работу.

```markdown
decisionAndWorkDocking:
  methodDescriptionRefs:
    как проектировать / проверять / детализировать / строить
  workPlanRefs:
    какие работы запланированы
  readinessRefs:
    что должно быть готово до запуска работ
  performedWorkRefs:
    появятся только после фактического выполнения
```

C.32.P2S разрешает P2S ссылаться на method/work refs, но сами claims про method, work plan, readiness и performed work остаются у A.15-family.

#### 1. Что делать practically
| Шаг                            | Что создать                                                      | Пример                                                                                                  |
| ------------------------------ | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| 1. Extract method implications | Какие методы теперь нужны из-за решения                          | fire simulation method, flow simulation method, BIM coordination method, structural verification method |
| 2. Create method descriptions  | Как именно эти методы применяются                                | “Проверить clean/dirty flow crossings по сценариям ConOps v2”                                           |
| 3. Create work plans           | Какие работы должны быть выполнены, кем, когда, с какими входами | WorkPlan: update MEP service core model; WorkPlan: run smoke control scenario                           |
| 4. Establish readiness         | Есть ли full kit для запуска работы                              | источники актуальны, PAD принят, BIM baseline есть, роли назначены, критерии проверки есть              |
| 5. Execute work                | Только после выполнения появляются `performedWorkRefs`           | фактически выполнен расчёт, проведена BIM-координация, проведён авторский надзор                        |
| 6. Record variance             | Что изменилось относительно expected structures                  | MEP shaft moved; fire damper location changed; actual access clearance reduced                          |
| 7. Feed back                   | Вернуть в P2S/PAD/AD/ACE при расхождении                         | source return or decision repair                                                                        |

#### 2. Минимальный блок

```markdown
decisionAndWorkDocking:
  architectureDecisionRef:
    PAD-HOSP-BlockA-FlowMEPFire-v1

  methodDescriptionRefs:
    FireScenarioSimulationMethodDescription-v1
    PatientLogisticsFlowSimulationMethodDescription-v1
    BIMCoordinationMethodDescription-v1
    MEPServiceCoreSizingMethodDescription-v1

  workPlanRefs:
    WorkPlan-BIM-ServiceCore-Update-v1
    WorkPlan-FireSimulation-v1
    WorkPlan-FlowSimulation-v1
    WorkPlan-ConstructabilityReview-v1

  readinessRefs:
    WorkEntryReadiness-BIM-ServiceCore-Update-v1
      requires:
        PAD-HOSP-BlockA-FlowMEPFire-v1
        ConOps.PatientFlow.v2
        ExistingStructureSurvey.v1
        MEPPreliminaryLoad.v1

  performedWorkRefs:
    empty until work actually occurs
```

### 4.11. Проверь actual structures и верни обратную связь

Финальное проектное решение не заканчивает поток. После детализации, строительства, авторского надзора, commissioning или эксплуатации надо сравнивать:

```markdown
feedback:
  actualStructureRefs:
  measurementRefs:
  evalResultRefs:
  operationOrUseObservationRefs:
  sourceReturnOrRepair:
    new C.32 synthesis?
    C.32.PAD decision repair?
    C.32.ADA adequacy repair?
    C.30.AD source return?
    E.23 improvement loop?
```

C.32.P2S требует feedback route: проверку actual selected structures, результатов architecture-characteristics и функциональных/Capability implications через operation, inspection, measurement, eval, telemetry, decay, source-return или decision-repair trigger.

#### Actual structures + feedback: пример действия
Сценарий:

> После commissioning больничного корпуса BMS-логи, обход эксплуатации и фактическая проверка маршрутов показывают, что путь вывоза грязного белья пересекает поток амбулаторных пациентов возле imaging zone. В PAD ожидалось полное разделение потоков.

Действие:

```markdown
feedback:
  operationOrUseObservationRefs:
    CommissioningWalkthrough-HOSP-BlockA-2026-11-12
    BMSAccessLog-FlowDoors-v1
    OperationsObservation-DirtyLinenRoute-v1

  actualStructureRefs:
    ActualTransformationFlowStructure-HOSP-BlockA-v1

  expectedStructureRefs:
    ExpectedSeparatedFlowStructure-PAD-HOSP-BlockA-FlowMEPFire-v1

  measurementRefs:
    C16.Measurement:
      Characteristic: flowSeparationIntegrity
      Bearer: ActualTransformationFlowStructure-HOSP-BlockA-v1
      Scale: crossingCountPerScenario
      Value: 1 critical crossing in daytime outpatient scenario
      EvidenceStub: commissioning observation + door log + route walkthrough

  evalResultRefs:
    C32.ACE:
      evalPurpose: triggerNextSynthesis
      resultForm: qualitativeState + evidenceFinding
      finding: expected separated flow not realized for daytime scenario

  ownerSpecificReturnOrRepair:
    c32NextSynthesisExit:
      generate repair candidates:
        R1: reroute dirty linen via service elevator B
        R2: add time-window operational control
        R3: modify partition and door access control

    c32PadOrAdaDecisionRepairOrSupersessionExit:
      reopen PAD-HOSP-BlockA-FlowMEPFire-v1
      because accepted selected structure was not realized

    c30DescriptionOrViewSourceReturnRef:
      update as-built BIM and flow structural view;
      do not treat old design BIM as actual structure

    workPlanRefs:
      create WorkPlan-FlowRepair-Study-v1 after repair candidate selection
```

Это ровно тот feedback route, который C.32.P2S требует: actual selected structures, architecture-characteristic results, observations, measurements, evals, telemetry, decay/source-return and owner-specific repair exits.


### 5. Archetypal grounding — пример для ОКС

Tell. Хорошее проектное решение ОКС не “появляется из исходных данных”. Проектировщик превращает давление исходных данных в выбранные структуры: сначала выявляет, какие структуры не определены или неадекватны; затем строит альтернативы; затем принимает решение с видимыми trade-offs; затем публикует описания; затем передаёт ограничения в работу; затем проверяет, появилась ли ожидаемая структура в фактическом ОКС.

Show. У больничного корпуса есть давление: растёт поток пациентов, существующая планировка конфликтует с инфекционным контролем, есть ограничения участка и инженерных сетей. Первый P2S-pass не требует “сделать красивую схему”. Он называет:
```markdown
describedHolonRef: больничный корпус
boundedContextRef: предпроект / ПД
problemPressure:
  pressureKind: flowSafetyAndCapacityPressure
  sourceSignalRefs: ТЗ, обследование, потоки, санитарные требования, ТУ
architectureContent:
  candidateStructureKindRefs:
    spatial-planning structure
    sterile/contaminated flow structure
    MEP capacity/interface structure
    fire/evacuation structure
  architectureCharacteristicRefs:
    safety, throughput, maintainability, adaptability
structuralInformation:
  unknownStructure: носитель разделения потоков
  selectedStructure: пока отсутствует
  sourceReturnCondition: вернуть к обследованию и потокам, если схема скрывает конфликт
neighboringOwnerForNextClaim: C.32
```

Дальше C.32 синтезирует варианты: централизованное ядро, разделённые функциональные блоки, гибридная схема с отдельными потоками. C.32.PAD фиксирует выбранное решение и принятые потери. C.30.AD.BA и публикационные паттерны оформляют BIM/чертежи/виды как описания. A.15-family ведёт планирование и выполненные работы. Эксплуатационные данные возвращают вопрос, если actual flow structure не совпала с expected structure.

### 6. Bias-annotation

| Bias                         | Как сдерживать                                                                                                             |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Description-as-solution bias | Чертёж, BIM, схема, раздел ПД — не решение сами по себе. Сначала назови selected structures и decision relation.           |
| Source-data determinism      | ИД не “выдают” решение. Они создают pressure, constraints и source-return conditions.                                      |
| Single-winner bias           | Не принимай единственный вариант по score/привычке/авторитету. Держи candidate plurality до comparison/decision owner.     |
| BIM-as-asset bias            | BIM/IFC/digital twin описывают ОКС, но не являются ОКС.                                                                    |
| Work takeover                | P2S не авторизует работу. Метод, план, readiness и performed work идут в A.15-family.                                      |
| Eval-as-decision             | Расчёт, метрика, коллизия, energy score или cost view не принимают решение. Они входят в eval/comparison/decision цепочку. |


### 7. Conformance checklist

| ID        | Проверка                                                                                                                           |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| BA-P2S-1  | Назван физический ОКС как `describedHolonRef`, а не BIM/ПД/таблица.                                                                |
| BA-P2S-2  | Назван `boundedContextRef`: стадия, границы проектирования, lifecycle-срез.                                                        |
| BA-P2S-3  | Исходные данные разложены на `sourceSignalRefs`, constraints и pressure, а не превращены прямо в solution.                         |
| BA-P2S-4  | Есть хотя бы один `unknownStructure` или `candidateStructureKindRef`.                                                              |
| BA-P2S-5  | Architecture characteristics отделены от метрик, расчётов, eval results и решений.                                                 |
| BA-P2S-6  | Есть несколько кандидатных конфигураций или явно указан stop reason, почему plurality пока невозможна.                             |
| BA-P2S-7  | Project architecture decision оформлен как decision relation с affected structures, trade-off, accepted losses и reopen condition. |
| BA-P2S-8  | BIM, IFC, чертежи, спецификации, дашборды и цифровой двойник опубликованы как descriptions/views с admissible use.                 |
| BA-P2S-9  | Work plan, readiness и performed work не подменены проектным решением.                                                             |
| BA-P2S-10 | Есть feedback route от actual structures / эксплуатации / авторского надзора / commissioning к repair или source-return.           |


### 8. Common anti-patterns

| Anti-pattern                | Симптом                                            | Repair                                                                                       |
| --------------------------- | -------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| “Исходные данные → решение” | После анализа ИД сразу появляется один вариант.    | Вставь P2S-card: pressure, unknown structures, candidate structures, characteristics.        |
| “BIM = решение”             | Модель ведёт себя как доказательство или decision. | Верни BIM в `C.30.AD.BA`: description/view/publication, не architecture decision.            |
| “Раздел ПД = архитектура”   | Комплект документации считается самим решением.    | Назови selected structures и decision relation; раздел ПД — публикация описаний.             |
| “Расчёт выбрал вариант”     | Вариант выбран по одному числу.                    | Отправь измерение в `C.16`, eval в `C.32.ACE`, comparison/selection — к их владельцам.       |
| “Нет обратной связи”        | После выпуска ПД поток закрыт.                     | Добавь actual-structure feedback: строительство, commissioning, эксплуатация, source-return. |

### 9. Consequences

Паттерн даёт проверяемую трассу:
```markdown
Исходные данные
→ problem pressure
→ unknown/candidate structures
→ architecture characteristics
→ candidate configurations
→ comparison / retention / selection
→ ArchitectureDecisionRelation
→ descriptions/views/BIM/ПД
→ method/work-plan/readiness
→ performed work / actual structures
→ feedback / repair / source-return
```


Ключевая дисциплина: итоговое проектное решение — это не один документ и не модель. Это связка:
```markdown
selected structures of ОКС
+ ArchitectureDecisionRelation
+ accepted losses / trade-offs
+ architecture descriptions and views
+ method/work consequences
+ source-return and reopen conditions

```

C.32.P2S прямо формулирует общий смысл: pressure and structural uncertainty become candidate, selected, expected, realized, and evaluated selected structures with owner-specific return or repair exits.

### 10. Rationale

Такой ход защищает проект от главной ошибки: “хорошо оформленный носитель” начинает считаться “хорошим проектным решением”. Для ОКС это особенно критично, потому что проект живёт в нескольких носителях — BIM, чертежи, таблицы, расчёты, согласования, ТУ, цифровой двойник, asset register, эксплуатационные данные. C.30.AD.BA специально удерживает границу: built asset, architecture claim, description, view, publication, source relation, evidence, work и authority остаются разными объектами.

### 11. SoTA-echoing

Для built asset допускай привычные инженерные носители — BIM, IFC, ISO 19650-подобную информационную дисциплину, reference designation, digital twin, asset register — но только как description/source/publication discipline. Не импортируй их классификации как FPF-онтологию и не давай им authority по внешнему виду.

### 12. Relations

Главная последовательность владельцев:
```markdown
C.22.2   — если исходный сигнал ещё не стал problem-side record
C.30     — grounded architecture claim по ОКС и selected structures
A.22     — selected structure как таковая
C.30.AD.BA — built-asset descriptions: BIM, IFC, digital twin, asset views
C.32.P2S — связанный поток pressure → structure → decision → work → feedback
C.32     — синтез кандидатных конфигураций
A.19.CPM / SelectorMechanism / C.11 / G.5 — сравнение, выбор, публикация selected set
C.32.PAD — project architecture decision
C.32.ADR / E.17 / E.24.PUB — публикации, ADR-like records, views
A.15 / A.15.2 / A.15.5 / A.15.1 — method, work plan, readiness, performed work
C.16 / C.25 / C.32.ACE — measurement, Q-bundle, eval
E.23 / G.11 — improvement / currentness refresh
```

### Обновлённый skeleton BA-P2S

```markdown
ProblemToStructureArchitecturingFlowCard@Project:
  flowId:

  describedHolonRef:
    # physical ОКС / corpus / facility / bridge / infrastructure asset

  boundedContextRef:
    holonScope:
    lifecycleSlice:
    nqdWorkState:
    closurePosture:
    sourceMaturity:
    decisionMaturity:
    publicationMaturity:

  architectingHolonOrRoleRef?:

  firstGoverningOwnerRef:

  architectureStructuringNeed:
    # local replacement for C.32.P2S.problemPressure
    needKind:
    sourceSignalRefs:
    conOpsNeedRefs?:
    architectureConcernRefs?:
    affectedHolonRefs:
    currentStopOrReturnReason?:
    sourceReturnCondition?:

  architectureContent:
    candidateStructureKindRefs:
    selectedStructureRefs?:
    expectedStructureRefs?:
    actualStructureRefs?:
    architectureCharacteristicRefs:
    architectureCharacteristicCriteriaSetRef?:
    qBundleRefs?:
    candidateSynthesisRef?:

  structuralInformation:
    unknownStructure:
    selectedStructure:
    expectedStructure:
    actualStructure:
    capturedInDescriptionsOrDecisions:
    handedToMethodsOrWork:
    latentOrHiddenStructure:
    lostStructure:
    sourceReturnCondition:

  decisionAndWorkDocking:
    candidateSetOrPaletteRef?:
    comparisonBasisRef?:
    selectedSetRef?:
    architectureDecisionRef?:
    adrProjectionRef?:
    methodDescriptionRefs?:
    workPlanRefs?:
    readinessRefs?:
    performedWorkRefs?:

  builtAssetDescriptionDocking?:
    builtAssetArchitectureDescriptionUseCardRef?:
    bimOrIFCRefs?:
    assetInformationRefs?:
    referenceDesignationRefs?:
    digitalTwinViewRefs?:
    publicationOrExchangeRefs?:
    DesignRunTagRefs?:

  feedback:
    evalProgramRefs?:
    evalResultRefs?:
    measurementRefs?:
    operationOrUseObservationRefs?:
    actualStructureRefs?:
    freshnessOrDecaySignalRefs?:
    ownerSpecificReturnOrRepair:
      c32NextSynthesisExit?
      c32PadOrAdaDecisionRepairOrSupersessionExit?
      e23ImprovementCycleRef?
      g11CurrentnessRefreshRef?
      e18TransformationFlowRefreshRef?
      c18C19ArchiveFrontPoolUpdateRef?
      c30DescriptionOrViewSourceReturnRef?

  neighboringOwnerForNextClaim:
```