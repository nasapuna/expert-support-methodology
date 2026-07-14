# Первый полезный архитектурный результат: инвариантный вход на услугу сопровождения проектирования

> **Статус результата:** первый `C.32.P2S`-результат для последующей архитектурной работы над BDPF.  
> **Это не:** выбранная архитектура пакета, `PFAD`, договорное обязательство проектировщика, чек-лист комплектности или решение о готовности проекта.  
> **Объект архитектурной работы:** структура входа на услугу сопровождения архитектурно значимого проектного решения в `BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1`.

## 1. Выбранный ход по FPF

Для текущего вопроса применяется карточка `ARCHITECTURE` из README FPF, **Template A**:

```text
C.32.P2S Solution
→ ProblemToStructureArchitecturingFlowCard@Project
```

Причина выбора: проблема относится не к использованию уже существующего архитектурного описания, а к ещё не определённой связи между входным состоянием проекта и структурой материала, который должен открыть дальнейшую проектную работу. Поэтому `C.30.AD` здесь преждевременен: сначала необходимо сделать reviewable сам problem-to-structure ход.

Доменная опора внутри BDPF:

- `BDPF.1` — физический ОКС и его граница;
- `BDPF.1A` — площадка и отдельная relation размещения;
- `BDPF.3` — исходный carrier и извлечённый из него signal;
- `BDPF.3A` — перевод problem pressure в structuring need;
- `BDPF.3B` — насыщенный пакет анализа исходных данных для одного bounded service entry.

## 2. Текущий архитектурный вопрос

### 2.1. Рабочая формулировка

**Какая инвариантная структура входа на услугу должна быть закреплена в BDPF, чтобы проектировщик мог передать проект в сопровождение при любом фактическом состоянии проекта — от почти полного отсутствия исходных данных до уже разработанной ПД/BIM и принятых проектных решений — без подмены содержания перечнем документов и без ложного вывода о достаточности входа?**

### 2.2. Почему это архитектурный вопрос

Вопрос затрагивает одновременно:

- interface между проектировщиком и ролью сопровождения;
- состав и границу publication/navigation package;
- связь физических ОКС и площадки с их описаниями;
- положение проекта в decision thread: `unknown`, `candidate`, `selected`, `expected`, `represented`, `actual`;
- source-use, currentness, gaps и return owners;
- разделение авторства проектной позиции, проверки и дальнейшей разработки;
- допустимые и заблокированные uses полученного входа.

Фиксированный список файлов не решает этот вопрос. Он либо требует отсутствующие carriers, либо принимает большой объём наработок за достаточную проектную позицию.

## 3. Заполненная `ProblemToStructureArchitecturingFlowCard@Project`

```text
ProblemToStructureArchitecturingFlowCard@Project:
  flowId: P2S-BDPF-SERVICE-ENTRY-001

  describedHolonRef:
    BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1

  boundedContextRef:
    service entry for FPF-grounded support of one architecture-significant
    built-asset design question

  architectingHolonOrRoleRef:
    BDPF package steward / architecture-responsible framework author

  firstGoverningPatternRef:
    C.32.P2S

  problemPressure:
    pressureKind:
      service-entry interface uncertainty

    problemPressureSignalRefs:
      - project maturity and volume of source materials vary from case to case
      - a fixed document checklist is not invariant to project maturity
      - document presence does not establish source use, currentness,
        architecture state, decision adequacy or readiness
      - current BDPF has a thin ServiceEntryConcernBundle@Project and a rich
        InitialDataAnalysisPackage@Project, but does not yet expose a common
        semantic minimum between them

    architectureConcernRefs:
      - define the invariant semantic content of service entry
      - separate mandatory entry positions from variable carrier payload
      - keep missing, stale, conflicting and not-material information explicit
      - preserve author/reviewer and source-return boundaries

    currentStopOrReturnReason:
      no selected structure yet distributes invariant and conditional content
      among ServiceEntryConcernBundle@Project,
      InitialDataAnalysisPackage@Project and any possible additional local record

  architectureContent:
    candidateStructureKindRefs:
      - service-entry relation structure
      - publication/navigation package structure
      - source-use and currentness relation structure
      - decision-thread-state handoff structure
      - role-assignment and return-owner structure

    architectureCharacteristicRefs:
      - maturity invariance
      - carrier independence
      - minimum useful completeness
      - traceability and recoverability
      - currentness visibility
      - conditional extensibility
      - role separation
      - low entry burden
      - blocked-overread visibility

  structuralInformation:
    unknownStructure:
      - exact invariant slot set for every service entry
      - exact boundary between mandatory semantic envelope and variable payload
      - allocation of invariant slots among existing BDPF records
      - admissible local state readings for absent, unknown, stale,
        conflicting and not-material content
      - profile relation between a common entry kernel and service-specific extensions

    selectedStructure:
      none; no framework architecture decision has been made

    capturedInDescriptionsOrDecisions:
      - ServiceEntryConcernBundle@Project currently captures built asset,
        site, placement relation, declared service use, unknowns,
        allowed/blocked uses and reopen condition
      - InitialDataAnalysisPackage@Project currently captures a rich source-analysis
        package with inventory, signal-use records, gaps, P2S cards,
        readiness use and role assignments

    latentOrHiddenStructure:
      - the invariant is a qualified statement for each mandatory position,
        not the existence of a prescribed document
      - absence of information must be represented as an explicit project state
        with consequence and owner, not as an unstructured omission
      - existing design carriers are variable payload and do not become
        architecture, decision or evidence by presence

    lostStructure:
      - current BDPF does not state one maturity-independent minimum
        that every designer handoff must make recoverable
      - current BDPF does not yet decide whether that minimum belongs in an
        expanded ServiceEntryConcernBundle, a separate entry declaration,
        or a profiled package architecture

    strongerStructureInspectionReturnCondition:
      return when the declared service family, BDPF edition, role boundary,
      project decision-thread state or service-entry use changes

  governingPatternForNextClaim:
    C.32 Architecture Candidate Synthesis;
    after candidate comparison and selection, E.4.PFAD
```

> В `candidateStructureKindRefs` выше пока стоят рабочие structure-family cues. Следующий ход должен либо восстановить для них точные `ArchitectureStructureKindRef`, либо сохранить их как unresolved cues с явным owner; текущая карточка не выдаёт их за уже admitted kinds.

## 4. Рабочая архитектурная гипотеза, которую карточка делает проверяемой

### 4.1. Основной принцип

**Инвариантным входом должен быть не комплект документов, а адресуемая декларация исходной проектной позиции.**

Она состоит из двух слоёв:

1. **Обязательная смысловая оболочка** — присутствует при любом объёме исходных данных и наработок.
2. **Переменный payload** — фактически имеющиеся ТЗ, ИРД, ТУ, изыскания, обследования, расчёты, ПД, BIM/IFC, протоколы, замечания, ранее принятые решения и иные carriers.

Количество и глубина carriers меняют только payload. Они не меняют обязательные смысловые позиции оболочки.

### 4.2. Инвариантные позиции входа

| Инвариантная позиция | Что проектировщик должен сделать recoverable | Допустимое заполнение при отсутствии развитых наработок | Что не считается эквивалентом |
| --- | --- | --- | --- |
| **1. Declared service use** | Для какого конкретного следующего use передаётся проект: восстановление решения, анализ исходных данных, формирование architecture question, сравнение вариантов, handoff в разработку и т.п. | Краткая формулировка текущего проектного вопроса и ожидаемого результата услуги. | «Провести аудит проекта» или «проверить документацию» без bounded use. |
| **2. Subject and boundary** | Какой физический ОКС, площадка или relation размещения являются primary subject; стадия/lifecycle slice и граница рассмотрения. | Минимальная `BuiltAssetSystemFrame`; при material site concern — `SiteFrame` и placement relation; иначе явное основание, почему площадочная позиция сейчас не material. | Договорный предмет, кадастровый номер, комплект ПД или BIM-модель как замена физическому ОКС/площадке. |
| **3. Current project posture** | Где проект находится по текущему вопросу: структура неизвестна, есть candidates, выбрана структура, существует PAD, есть только represented structure в ПД/BIM либо известна actual structure. | Явное `unknown` с указанием того, что именно не восстановлено. | Стадия «П»/«Р», процент готовности или наличие модели без указания состояния конкретной структуры/решения. |
| **4. Available material and currentness** | Перечень фактически передаваемых carriers с owner, edition/date, scope, access и currentness cue. | Пустой или минимальный inventory с прямым указанием, что материалы не представлены либо недоступны. | Просто папка файлов, ссылка на CDE или фраза «всё актуальное приложено». |
| **5. Current design basis** | Какие requirements, constraints, assumptions, issues, preferences и ранее принятые решения проектировщик сейчас использует. | Краткая декларация известных допущений и ограничений; неизвестное не заполняется вымышленным «консервативным решением». | Ссылка на весь документ как универсальное основание или прямой переход от требования к выбранной конфигурации. |
| **6. Unknowns, conflicts and return owners** | Какие данные отсутствуют, противоречат друг другу, устарели или не покрывают текущий scope; как это влияет на вопрос; кто должен получить источник или выполнить probe. | `unknownWithOwner`, `conflictingOrStaleWithReturn` либо `notMaterialForDeclaredUse` с основанием. | Общий статус «исходных данных недостаточно» без affected question, consequence и owner. |
| **7. Allowed and blocked uses** | Что допустимо делать на текущем входе и какие claims/решения пока заблокированы. | Например: разрешено сформировать use/system concept и провести bounded probes; запрещены PAD, reliance-bearing review или вывод о пригодности площадки. | Общий зелёный/красный статус, одобрение или «можно продолжать проектирование» без declared use. |
| **8. Authorship, review and refresh responsibility** | Кто является автором переданной проектной позиции, кто выполняет review, кто владеет обновлением источников и повторным выпуском входа. | Минимальные role refs и source-return condition. | Должность, подпись или статус согласования как доказательство выполненного анализа и инженерной достаточности. |

### 4.3. Правило заполнения, обеспечивающее независимость от объёма данных

Для каждой инвариантной позиции должен быть не обязательно документ, но обязательно **одно квалифицированное состояние**. Рабочие local readings для следующей архитектурной проработки:

```text
providedByReference
  — позиция раскрыта через адресуемый carrier/record с owner и edition;

declaredCurrentPosition
  — проектировщик прямо сформулировал текущую проектную позицию
    или assumption, даже если отдельного carrier ещё нет;

unknownWithOwnerAndReturn
  — содержание неизвестно; указан affected question,
    consequence, requested source/probe и owner;

conflictingOrStaleWithReturn
  — известны конфликт или потеря currentness;
    указан blocked use и условие возврата;

notMaterialForDeclaredServiceUse
  — позиция осознанно не раскрывается, потому что не влияет
    на заявленный service use; основание остаётся видимым.
```

Это пока **candidate local value set**, а не новый FPF kind или выбранная BDPF-норма. Его задача — дать `C.32` материал для сравнения архитектурных конфигураций.

## 5. Практическая формула входа для проектировщика

Рабочая формула, которую можно использовать как design constraint для следующего хода:

> **Проектировщик передаёт на вход услуги не фиксированный комплект документов, а адресуемую декларацию исходной проектной позиции: объект и границу рассмотрения, заявленный use услуги, текущее состояние решения и структуры, состав и актуальность имеющихся carriers, применяемые требования/ограничения/допущения, открытые неизвестные и конфликты с owners, а также допустимые и заблокированные дальнейшие uses. Все имеющиеся ПД/BIM/ИРД/изыскания/расчёты прикладываются как переменный payload к этой декларации.**

При отсутствии материалов вход всё равно может быть корректно сформирован — как минимальная проектная позиция с явными unknowns, blocked uses и source-return route. При большом объёме материалов он также остаётся корректным, потому что carriers получают scope, currentness и relation к текущему вопросу, а не принимаются за достаточность по факту наличия.

## 6. Граница слова «должен»

Текущий результат определяет **архитектурное содержание входа**, но сам по себе не создаёт обязанность проектировщика.

Когда необходимо закрепить, что проектировщик действительно обязан передать этот состав:

- содержание выдачи должно быть связано с project-local `PromiseContent`/требованием к услуге;
- обязанность, permission или prohibition должны быть оформлены у прямого deontic owner (`U.Commitment`);
- приемка выдачи должна иметь отдельную acceptance binding;
- role assignment и instituting/approval act должны оставаться отдельными от инженерной достаточности входа.

Иными словами, BDPF может определить **что должно быть смыслово представлено**; договор, регламент или проектное решение по полномочиям определяет **кто, когда и на каком основании обязан это передать**.

## 7. Что этот результат блокирует

До следующего архитектурного хода нельзя:

- выпускать универсальный чек-лист обязательных файлов как архитектуру входа;
- делать `InitialDataAnalysisPackage@Project` обязательным в полном составе для любой услуги;
- считать наличие ПД/BIM доказательством существования PAD или актуальной selected structure;
- считать отсутствие исходных данных невозможностью начать любую полезную работу;
- считать большой объём исходных данных готовностью к reliance-bearing review;
- вводить новый durable BDPF record только потому, что для него уже придумано имя и поля.

## 8. Конкретный следующий ход в проекте

**Следующий ход — открыть `C.32 Architecture Candidate Synthesis` и материализовать один `CandidateArchitecturePalette@Project` с `paletteId: BDPF-ServiceEntry` для распределения инвариантных позиций между BDPF records.**

В палитру должны войти как минимум три структурно различимых кандидата:

### Кандидат A — расширенный `ServiceEntryConcernBundle`

Один существующий bundle получает все инвариантные позиции, а `InitialDataAnalysisPackage` остаётся условным расширением для source-analysis services.

### Кандидат B — тонкий concern bundle + отдельная декларация входного состояния

`ServiceEntryConcernBundle` сохраняет только ОКС, площадку, placement relation и declared use; отдельный DPF-local record несёт project posture, carriers, currentness, unknowns, allowed/blocked uses и responsibility refs.

### Кандидат C — общий entry kernel + service-specific profiles

BDPF определяет общий инвариантный kernel, а профили услуг добавляют условные extensions: source analysis, decision reconstruction, candidate comparison, developer handoff и т.п.

Сравнение кандидатов следует вести как минимум по следующим characteristics:

- инвариантность к стадии и объёму наработок;
- способность открыть первый полезный ход при неполных данных;
- отсутствие carrier-as-truth и checklist-as-method;
- трассируемость source/decision/unknowns;
- updateability при изменении источников;
- понятность для ГИП/ГАП и ведущих специалистов;
- стоимость заполнения до первого полезного результата;
- совместимость с `BDPF.1/1A/3/3A/3B/7/10/12`;
- отсутствие скрытого превращения package в gate, approval или performed work.

**Выход следующего хода:** кандидатная палитра с gain/loss и source-return conditions. Только после неё можно принимать framework-level architecture decision через `E.4.PFAD` и вносить изменения в `BDPF.1A`, `BDPF.3B`, Pattern Index и acceptance cases.

## 9. Критерий завершения текущего хода

Текущий P2S-ход завершён, потому что теперь reviewable:

- EntityOfConcern архитектурной работы;
- problem pressure;
- неизвестная структура;
- существующие частичные структуры BDPF;
- рабочая гипотеза «инвариантная оболочка + переменный payload»;
- конкретный receiving pattern и точный следующий результат.

Возврат к этой карточке требуется, если изменится семейство услуг, роль проектировщика/сопровождения, граница обязательного входа, версия BDPF либо проект решит, что вход должен быть не publication/relation structure, а contract/acceptance result у другого governing owner.

---

## Source basis

- `FPF-Spec.md`: README card `ARCHITECTURE`; `C.32.P2S — Problem-to-Structure Architecturing Unfolding`.
- `BuiltAssetDesignPrinciplesFramework.md`: `BDPF.1`, `BDPF.1A`, `BDPF.3`, `BDPF.3A`, `BDPF.3B`, existing `ServiceEntryConcernBundle@Project` and `InitialDataAnalysisPackage@Project`.
