# Built Asset Design Principles Framework

> **Русское рабочее имя:** рамка принципов разработки, фиксации и сопровождения архитектурно значимых проектных решений для объектов капитального строительства.
>
> **Назначение:** сделать переход от исходных материалов и проектной проблемы к раздельным рамкам физического ОКС и площадки размещения, relation между ними, структурам, вариантам, проектному архитектурному решению, claim-specific evidence, ПД/BIM-проекциям, readiness boundary и обратной связи явным, проверяемым и улучшаемым.

- **Framework family:** Domain Principle Framework
- **Package edition ref:** `BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1`
- **Supersedes:** `BuiltAssetDesignPrinciplesFramework@2026-07-12-v0.5`
- **Public pattern prefix:** `BDPF.*`
- **Dependency:** `FPFCorePatternSet@July2026`, прежде всего `A.1`, `A.1.1`, `B.1.2`, `E.10.D2`, `A.2.1`, `A.3.2`, `A.7`, `A.10`, `A.15`, `A.15.5`, `A.19.ECS`, `A.21`, `A.22`, `B.3`, `C.16`, `C.25`, `C.30`, `C.30.AD`, `C.30.AD.BA`, `C.30.ASV`, `C.32`, `C.32.P2S`, `C.32.ACS`, `C.32.ACE`, `C.32.PAD`, `C.32.ADR`, `C.32.ADA`, `C.33`, `C.34`, `C.35`, `E.4.DPF`, `E.4.DPF.DA`, `E.4.PFAD`, `E.4.PFR`, `E.8`, `E.17`, `E.21`, `E.22`, `E.23`, `G.2` и `G.11`
- **Declared domain:** разработка и экспертное/техническое сопровождение архитектурно значимых междисциплинарных решений зданий, сооружений и инфраструктурных ОКС в проектном контуре
- **Scope boundary:** пакет не претендует на охват всей дисциплинарной инженерии; он применяется там, где выбранная структура ОКС связывает несколько решений, представлений, ролей или жизненных режимов
- **Qualification:** `locallyUsableWithVisibleLimits` для ограниченного пилота по одному существенному проектному решению; не нормативная база, не регламент государственной или негосударственной экспертизы и не `stable`-пакет для безусловного enterprise-reliance
- **Revision posture:** содержательная и архитектурная редакция с явным site-start contour; квалификационный статус не повышен, отдельная `E.21`-оценка `BDPF.1A` и field-pilot evidence отсутствуют
- **Produced-carrier posture:** AI-assisted revision candidate; package stewardship, project applicability and any reliance-bearing admission remain human/project-owner decisions
- **Legacy aliases:** `DPF.*` допустимы только для чтения старых записей; новые ссылки используют `BDPF.*`

---

# Table of Contents

Используйте Readme, когда выбираете первый вход из текущей проектной проблемы. Используйте Preface, когда нужна общая логика пакета. Открывайте support maps только из `Relations`, low-value repair, source-return или refresh condition; они не являются обязательным предварительным чтением.

| Рабочий триггер | Первый вход | Первый полезный результат |
| --- | --- | --- |
| ПД/BIM уже есть, но не видно, почему принято решение. | `BDPF.7`, затем `BDPF.8` и `BDPF.10` | Восстановленный `ArchitectureDecisionRelation@Project` с основаниями, потерями, evidence exits и projection refs. |
| На старте услуги площадка смешана с ОКС, участком или комплектом документов. | `BDPF.1A`, затем пакетный вход `BDPF.3B` | Раздельные `BuiltAssetSystemFrame@Project`, `SiteFrame@Project` и `BuiltAssetSitePlacementRelation@Project`. |
| Исходных материалов много, но неизвестно, какие проектные вопросы они поддерживают. | `BDPF.3` или пакетный вход `BDPF.3B` | `DesignSourceSignalUseRecord@Project` либо `InitialDataAnalysisPackage@Project`. |
| Из требования или замечания сделали прямой скачок к решению. | `BDPF.3A` | `BuiltAssetProblemToStructureFlowCard@Project` с structuring need, unknown/candidate structures и next owner. |
| Неясно, для каких ролей, режимов и сценариев проектируется объект. | `BDPF.4` | `UseConceptRecord@Project` с source-bounded scenario rows и конфликтами использования. |
| Есть сценарии, но отсутствует единая системная логика объекта. | `BDPF.5` | `SystemConceptRecord@Project` с границей, функциями, потоками, интерфейсами, режимами и bearer structures. |
| Спор затрагивает несколько разделов и решений одновременно. | `BDPF.6` | `BuiltAssetArchitectureQuestionCard@Project`. |
| Один вариант выбран слишком рано либо сравнение сведено к одному score. | `BDPF.6A`, `BDPF.6B`, `BDPF.6C` | Палитра конфигураций, lawful criteria/eval и retained set без скрытого победителя. |
| Нужно принять архитектурно значимое решение. | `BDPF.7` | PAD relation с selected/expected structures, trade-offs, losses, method docking и reopen. |
| Нужно понять, чем поддержан конкретный claim. | `BDPF.8` | `DesignClaimEvidenceTrace@Project`, scoped to one claim and receiving use. |
| Нужно понять, где и с какими потерями решение представлено. | `BDPF.10` | Architecture-description/documentation projection with captured/lost structure. |
| Нужно понять, достаточно ли решение для review, передачи в разработку или публикации. | `BDPF.12`, при boundary-crossing — `BDPF.9` | Координатная оценка достаточности и direct-owner readiness/gate use. |
| Изменились исходные данные или повторяется одно замечание. | `BDPF.11` | `DesignChangeImpactTrace@Project` или `DesignMethodFeedbackRecord@Project` с owner-specific return. |

## Working threads — relation groups, not workflow stages

| Thread | Pattern group | Use |
| --- | --- | --- |
| `source-to-structure` | `BDPF.1`, `BDPF.1A`, `BDPF.3`, `BDPF.3A`, `BDPF.3B`, `BDPF.4`, `BDPF.5`, `BDPF.6` | Развести ОКС, площадку и placement relation; восстановить source pressure, use/system logic и architecture question. |
| `candidate-to-decision` | `BDPF.6A`, `BDPF.6B`, `BDPF.6C`, `BDPF.7` | Удержать plurality, построить lawful comparison basis и принять PAD. |
| `decision-to-reliance` | `BDPF.7A`, `BDPF.7B`, `BDPF.8`, `BDPF.9`, `BDPF.10`, `BDPF.12` | Опубликовать, доказательно ограничить, спроецировать и оценить решение для declared use. |
| `change-to-repair` | `BDPF.2`, `BDPF.11` | Сделать способ разработки явным и вернуть source/defect change к smallest owner. |

Эти thread-группы показывают соседство паттернов. Они не являются стадиями проекта, WorkPlan, обязательной последовательностью или требованием материализовать все records.

| Раздел | Назначение |
| --- | --- |
| Readme | Выбрать первый паттерн по текущему дефекту, а не по предполагаемой стадии проекта. |
| Preface | Понять P2S-спину, различение объекта и carriers, локальное закрытие, source return и record-kind discipline. |
| Package Carrier Structure-Account | Увидеть, какую структуру домена этот carrier показывает и что намеренно оставляет за пределами. |
| Framework Context and PFAD | Проверить границу DPF, Core-owner routing и выбранную архитектуру пакета. |
| Pattern Index | Найти action-guiding паттерн, его роль в пакете и первый результат. |
| `BDPF.1..BDPF.12`, включая `BDPF.1A` | Применить паттерн к текущему проектному вопросу. |
| Acceptance cases | Проверить переносимость паттернов на неоднородных проектных ситуациях. |
| Support maps and package records | Восстановить owner, source use, термин, edition relation или package relation, когда на карту указывает паттерн. |
| First bounded pilot | Ограничить первое применение одним решением и наблюдаемым declared use. |
| Package adequacy and E.21 records | Увидеть текущие пределы пакета, материализованные priority-pattern evaluations и low-value repairs. |
| Refresh route | Вернуть source, Core, carrier, field-use или quality change к smallest affected locus. |

---

# Readme — First Practical Entries

BDPF нужен не для того, чтобы выпускать ещё один комплект форм. Он нужен, когда проектное решение должно оставаться восстанавливаемым как инженерное рассуждение:

```text
physical built asset frame + physical site frame + placement relation
→ source-bearing material
→ source signal and problem pressure
→ architecture structuring need
→ unknown and candidate structures
→ architecture characteristics and evaluation basis
→ candidate configurations and retained set
→ project architecture decision
→ claim-specific evidence and assurance exits
→ architecture description and PD/BIM projection
→ readiness boundary, feedback, source return and repair
```

Это **не обязательная последовательность работ**. Вход выбирается по текущему дефекту. Если PAD уже существует, не надо искусственно начинать с `BDPF.1`; если source signal ещё не стабилизирован, нельзя перескакивать к `BDPF.7` только потому, что проекту нужен быстрый ответ.

### Architecture-significance test

BDPF оправдан, когда текущий вопрос удовлетворяет хотя бы одному условию:

- выбранная структура влияет более чем на одну дисциплину, роль, view или lifecycle mode;
- локальное решение перераспределяет flows, interfaces, load paths, control relations, temporary/permanent states или accepted losses;
- решение должно пережить передачу между командами, изменение source или смену carrier;
- ошибка обратима только с существенной стоимостью, задержкой или потерей доказательной базы.

Если вопрос сводится к локальному дисциплинарному расчёту, оформлению одного carrier или исполнению уже определённого метода без architecture question, используйте прямой discipline/FPF owner.

### Minimum-use rule

Материализуйте только тот record, который нужен следующему declared use. Один корректный `DesignSourceSignalUseRecord@Project`, `BuiltAssetArchitectureQuestionCard@Project` или `ArchitectureDecisionRelation@Project` лучше полного набора пустых форм. Полный decision thread восстанавливается по ссылкам и owners; он не обязан храниться в одном файле или появляться за один проход.

## First Practical Entry 1 — Восстановить решение из ПД/BIM

Начните с `BDPF.7`. Назовите вопрос, выбранные структуры, альтернативы, принятые потери, source refs, evidence exits, role assignments и reopen condition. Затем `BDPF.10` покажет, где решение представлено и что carrier потерял; `BDPF.8` проверит claim-specific evidence.

Типовой результат: один `ArchitectureDecisionRelation@Project` и один `ProjectDocumentationProjection@Project`.

## First Practical Entry 2 — Провести анализ исходных данных

Для стартовой услуги сначала используйте `BDPF.1` и `BDPF.1A`: назовите физический ОКС, физическую площадку и отдельную relation размещения между ними. Не используйте ГПЗУ, кадастровый идентификатор, топосъёмку, отчёт об изысканиях, BIM/GIS или договорный предмет как `siteRef`.

Для одного материала используйте `BDPF.3`; для комплекта ТЗ, ТУ, ИРД, изысканий, обследований, требований эксплуатации и иных carriers используйте `BDPF.3B`. Каждый извлечённый signal получает scope, affected subject, admissible/non-admissible use, currentness и receiving owner.

Типовой результат: `InitialDataAnalysisPackage@Project`, который ссылается на `ServiceEntryConcernBundle@Project`, две отдельные рамки, placement relation, source inventory, signal-use records, site structure/interface map, site characteristic profile, site uncertainty register, P2S cards и bounded readiness use.

## First Practical Entry 3 — Перевести проблему в архитектурную работу

Используйте `BDPF.3A`, когда формулировка звучит как «нужно учесть», «есть ограничение», «эксперт требует» или «модель показывает», но ещё не названо, какая структура ОКС неизвестна, спорна или должна измениться.

Типовой результат: `BuiltAssetProblemToStructureFlowCard@Project` с минимальным набором exact `ArchitectureStructureKindRef` либо честных unresolved cues, а также владельцем следующего claim.

## First Practical Entry 4 — Сформировать и сравнить варианты

Используйте `BDPF.6` для архитектурного вопроса, `BDPF.6A` для нескольких конфигураций, `BDPF.6B` для characteristics/criteria/eval и `BDPF.6C` для comparison и retained set. Не превращайте расчёт, simulation, экспертное предпочтение или один score в решение.

Типовой результат: `CandidateArchitecturePalette@Project`, `BuiltAssetArchitectureCriteriaSet@Project`, `ComparisonBasis@Project` и `RetainedArchitectureSetPublication@Project`.

## First Practical Entry 5 — Оценить достаточность и readiness

Используйте `BDPF.12`, чтобы проверить одно решение для одного declared use: internal discussion, architecture review, developer handoff, ADR-like publication или reliance-bearing review. Если текущий вопрос — переход через организационную границу, используйте `BDPF.9` как доменный профиль `A.21`/`A.15.5`, а не как доказательство качества решения.

Типовой результат: `BuiltAssetArchitectureDecisionAdequacyEvaluation@Project` и, если нужен boundary decision, `BuiltAssetDesignReadinessUse@Project`.

## First Practical Entry 6 — Вернуть дефект к правильному владельцу

Используйте `BDPF.11`, когда замечание, clash, source change, representation loss или повторяющаяся несогласованность указывают не только на правку файла. Сначала определите suspect relations, затем выберите самый малый owner-specific return: source refresh, PAD repair, evidence refresh, projection repair, method repair или package refresh.

Типовой результат: `DesignChangeImpactTrace@Project` либо `DesignMethodFeedbackRecord@Project`.

## Non-use boundary

Не используйте BDPF как:

- нормативную базу или замену применимым законам, техническим регламентам, СП, ГОСТ, СТУ, ТУ и требованиям заказчика;
- BIM-стандарт, CDE-регламент, EIR/BEP/IDS-шаблон, классификатор или IFC-схему;
- регламент экспертизы, процедуру согласования или матрицу полномочий;
- чек-лист комплектности ПД;
- доказательство безопасности, соответствия, стоимости, сроков или качества ОКС;
- универсальный WorkPlan проектирования.

Когда текущий вопрос является исключительно нормативным claim, evidence sufficiency, assurance, gate, work authorization, publication, legal permission или role authority, применяйте прямой FPF/project owner и возвращайтесь в BDPF только при наличии source-to-structure-to-decision задачи.

---

# Preface — Cross-Cutting Ideas And Principles

## 1. ОКС, площадка, relation размещения и carriers — разные объекты

Физический ОКС и физическая площадка размещения являются разными domain `EntityOfConcern`. Площадка — физическая территория с релевантными природными и антропогенными составляющими в объявленной context-local delimitation, а не кадастровый номер, ГПЗУ, топосъёмка, изыскания или BIM/GIS-модель.

Размещение конкретного ОКС на конкретной площадке задаётся отдельной relation. Именно она несёт взаимные ограничения, boundary crossings, внешние потоки, candidate placements и принимаемые потери, которые нельзя приписать только ОКС или только площадке.

`BuiltAssetSystemFrame@Project`, `SiteFrame@Project`, `BuiltAssetSitePlacementRelation@Project`, ПД, BIM/IFC, расчёты, таблицы, замечания, протоколы и статусы являются descriptions, relation records, views, publications, carriers или evidence carriers в зависимости от claim. Детальность и формальный статус не превращают их в физический ОКС, площадку, архитектуру, решение, proof, gate или performed work.

## 2. Исходный материал не выбирает решение

ТЗ, ГПЗУ, ТУ, изыскания, обследование, требование эксплуатации, нормативный источник или замечание создают problem pressure, ограничения и source-return conditions. Они не выбирают конфигурацию без синтеза кандидатов, характеристики, сравнения и PAD.

## 3. P2S — связующая спина, а не универсальный workflow

`C.32.P2S` связывает problem pressure со структурами, кандидатами, решениями, work docking и feedback. BDPF специализирует эту связь для ОКС. Отдельные claims остаются у своих владельцев: architecture claim у `C.30`, candidate synthesis у `C.32`, PAD у `C.32.PAD`, evidence у `A.10`, assurance у `B.3`, gate у `A.21`, work у `A.15`, publication у `E.17`, currentness у `G.11`.

## 4. Состояния структуры нельзя смешивать

Для одного и того же ОКС могут одновременно существовать:

- `unknownStructure` — структура ещё не восстановлена;
- `candidateStructure` — один из рассматриваемых вариантов;
- `selectedStructure` — структура, выбранная архитектурным решением;
- `expectedStructure` — структура, которую должно создать или сохранить последующее проектирование/строительство;
- `representedStructure` — то, что показано в ПД/BIM/views;
- `actualStructure` — фактически реализованная или обследованная структура.

Совпадение имён и геометрии не доказывает correspondence. Для reliance-bearing use нужны `C.33`/`C.34`, evidence и source return.

## 5. Варианты сохраняются до законного схлопывания

Candidate palette, comparison, retained set, local choice и PAD — разные relations. BDPF не требует всегда генерировать много вариантов, но требует либо plurality, либо честный `stopReasonIfNoPlurality`. Один привычный вариант не становится решением только потому, что команда не сформулировала альтернативы.

## 6. Характеристики имеют bearer, scale и защищаемый trade-off

«Надёжность», «безопасность», «эффективность», «технологичность», «гибкость» и «качество» часто являются Q-bundles. Перед оценкой укажите bearer structure, characteristic, scale, measure/eval, evidence basis, missingness rule, protected counter-characteristic и proxy risk. Улучшение видимого score не должно скрывать ухудшение проектной ценности.

## 7. Решение, его запись и его принятие различаются

`ArchitectureDecisionRelation@Project` фиксирует commitment по selected structures, trade-offs, losses и reopen conditions. ADR/карточка/журнал — publication projection. Подпись, согласование или approval-looking status — speech act/status use, а не доказательство инженерной достаточности. Role names не заменяют `RoleAssignment`.

## 8. Доказательство поддерживает claim в scope

Расчёт, модель, simulation, normative check, испытание, экспертное judgement или machine-readable validation поддерживают конкретный claim при конкретных предпосылках. Они не «обосновывают решение вообще». Assurance, compliance, gate и decision остаются отдельными claims.

## 9. Readiness — локальное закрытие, а не истина

Gate закрывает вопрос «достаточно ли текущего комплекта для следующего declared use». Он не доказывает, что решение верно, не выполняет работу и не создаёт полномочие сам по себе. Reopen condition обязателен, потому что source, evidence, context и structure могут измениться.

## 10. Feedback возвращается к самому малому владельцу

Замечание может указывать на дефект carrier, projection, evidence, PAD, candidate basis, source use или method. Исправление только текста допустимо лишь тогда, когда defect действительно локален в тексте. Повторяющаяся ошибка должна возвращаться в `E.23` improvement или `G.11` refresh.

## 11. BDPF охватывает architecture-significant design, а не всю инженерную разработку

Пакет становится текущим, когда вопрос касается selected structures ОКС, междисциплинарных interfaces, распределения functions/flows, temporary/permanent states, material trade-offs или передачи архитектурного намерения между ролями. Локальные расчётные методы, деталировка, подбор оборудования, сметное нормирование, календарное планирование, statutory review и construction work остаются у прямых владельцев, если они не создают source-to-structure-to-decision question.

## 12. Decision-thread invariants

| Distinction | Required reading | Blocked collapse |
| --- | --- | --- |
| source carrier ↔ source-use signal | carrier может нести несколько signals и scopes | документ не выбирает решение и не поддерживает все claims |
| problem pressure ↔ structuring need | pressure должен быть переведён в вопрос о structure | requirement/comment не становится готовой configuration |
| candidate ↔ retained ↔ selected | synthesis, comparison, selected-set publication и PAD — разные relations | shortlist/front не является решением |
| selected ↔ expected ↔ represented ↔ actual structure | каждое состояние имеет собственного owner и evidence boundary | геометрическое совпадение или одинаковое имя не доказывает correspondence |
| characteristic ↔ measure/eval ↔ comparison ↔ decision | bearer, scale, evidence and missingness предшествуют choice | score/simulation не принимает решение |
| PAD ↔ ADR/publication ↔ speech act | relation, её projection и instituting/approval act различены | подписанный record не доказывает engineering adequacy |
| evidence ↔ assurance ↔ gate/readiness | claim support, reliance judgement и boundary decision различены | evidence volume или green status не создаёт permission |
| method ↔ method description ↔ WorkPlan ↔ Work | способ, его описание, намерение и фактическое выполнение различены | process diagram/checklist не доказывает performed work |

## 13. Record-kind discipline

BDPF-local names обозначают project records and relation uses, а не автоматически новые `U.*` kinds.

| Name ending / family | Default reading | Non-admissible reading |
| --- | --- | --- |
| `Frame`, `Concept`, `QuestionCard` | bounded description or relation record that prepares a next claim | physical asset, architecture or decision by form |
| `Palette`, `CriteriaSet`, `ComparisonBasis` | candidate/evaluation/comparison records under Core owners | selected architecture or PAD |
| `ArchitectureDecisionRelation` | filled Core-governed PAD relation | ADR file, approval status or gate |
| `Projection`, `RecordProjection`, `Package` | publication/navigation/representation relation over governed values | source of new semantics or evidence by completeness |
| `Trace` | source-, evidence- or impact-use relation | proof, assurance or root-cause verdict |
| `Evaluation` | declared-use ordinal evaluation | approval, gate decision, assurance level or global score |
| local `*Cue` or prompt label | discovery aid that must resolve to an exact project/Core owner before reliance | durable kind or universal classification |

A repeated local form becomes a durable ontic only through `E.24`/`E.24.CD`; frequency, capitalization or schema shape is not admission.

## 14. Language and register discipline

Русский текст несёт working-reader explanation. Английские identifiers сохраняют exact FPF/project names, relation slots and cross-package references. Не переводите canonical ids разными словами в разных местах; вместо этого давайте короткое русское пояснение на первом употреблении. Слова «система», «архитектура», «структура», «решение», «готовность», «проверка», «соответствие» и «модель» требуют owner recovery, когда начинают влиять на reliance or work.

---

# Package Carrier Structure-Account Note

Этот all-in-one файл является publication carrier редакции BDPF для руководителей проектирования, ГИП/ГАП, архитекторов, конструкторов, инженеров, BIM/информационных координаторов, технических заказчиков и специалистов сопровождения, которым нужно восстановить и проверить ход разработки существенного проектного решения.

```text
FrameworkCarrierStructureCapture@BuiltAssetDesignPrinciplesFramework:
  evaluatedCarrierRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  declaredUse: make built-asset design-decision development explicit, reviewable and improvable for one bounded project decision
  selectedSourceStructureDenominator:
    - FPF problem-to-structure architecturing, architecture, decision, evidence, gate, publication and improvement owners
    - built-asset system and architecture-description practice
    - project information management, information delivery and machine-readable exchange/checking practice
  foregroundedStructure:
    - physical built asset and physical site as distinct EntityOfConcern positions
    - built-asset-to-site placement relation with context-local boundaries, interfaces and unknowns
    - source signal and problem pressure
    - use and system concept
    - architecture question and candidate structures
    - characteristics, eval, comparison and retained set
    - PAD, ADR projection and decision-use package
    - claim-specific evidence
    - PD/BIM/view projection and representation loss
    - readiness, feedback, impact and repair
    - decision-adequacy evaluation
  intentionallyCoarsenedAbstractedOmittedOrDeferredStructure:
    - jurisdiction-specific regulatory content and legal interpretation
    - detailed discipline design methods and calculations
    - procurement, cost, schedule and construction management methods as independent bodies of knowledge
    - full BIM/CDE/IFC/IDS implementation instructions
    - statutory expert-review procedure
    - operation-phase asset management beyond source-return to design
    - project organization-specific authority matrices and work plans
  qualitativeCarrierEpiplexityForDeclaredUse: 4
  whyNot5: the publication carrier now exposes the complete selected decision-development structure and owner returns, but heterogeneous field use, formal E.21 runs for every pattern and repeated pilot evidence are not yet available
  sourceReturnCondition: return to the direct FPF owner, project-pinned source, applicable regulation, discipline method, evidence record or local role/authority record whenever the claim becomes normative, evidential, assurance-bearing, work-authorizing, discipline-specific or legally consequential
```

```text
StructuralInformationAdequacyNote@BuiltAssetDesignPrinciplesFramework-v0.5.1:
  describedCarrierRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  declaredArchitectureUse: recover and apply the selected BDPF problem-solution structure for one bounded architecture-significant project decision
  capturedSelectedStructure:
    - first-entry routes and non-use boundary
    - domain pattern set and relation groups
    - Core owner routing and local record-kind posture
    - source-to-structure, candidate-to-decision, decision-to-reliance and change-to-repair relations
    - package quality, source return and refresh routes
  missingOrDeferredStructure:
    - project-specific role authority, legal applicability and regulatory interpretation
    - discipline calculation methods and validated evidence
    - completed field-pilot results and enterprise adoption evidence
    - access-service implementation and callable-use currentness
  missingStructureReturn:
    - project/direct FPF owner for project claims
    - Source Use And Refresh Map for package source payload
    - E.21 records for individual pattern quality
    - E.4.DPF.DA for package adequacy
    - G.11 for currentness
  adequacyDisposition: adequateForBoundedPilotInspectionWithVisibleLimits
  nonAdmissibleUse: proof that the package covers the whole built-asset design domain or that any project decision is correct
```

```text
ProducedCarrierAdmissionNote@BuiltAssetDesignPrinciplesFramework-v0.5.1:
  producedCarrierRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  productionPosture: AI-assisted revision of an existing human/project carrier
  sourceCarrierRefs:
    - BuiltAssetDesignPrinciplesFramework@2026-07-12-v0.5
    - FPF Core Conceptual Specification@July2026
  admittedUseNow: content review, bounded pilot preparation and steward comparison against the superseded carrier
  notYetAdmittedUse: statutory, enterprise, contractual, safety, compliance or unreviewed reliance-bearing use
  humanOrProjectOwnerRequiredFor: source applicability, field adoption, role authority, publication approval and qualification change
  reopenCondition: steward finding, Core/source edition change, E.21 result, field pilot or project-use contradiction
```

Значение `4` относится только к тому, насколько этот carrier показывает выбранную структуру BDPF для заявленного пилотного использования. Оно не означает полноту строительной науки, правильность конкретного ОКС или готовность пакета к безусловному публичному/enterprise reliance.

---

# Framework Context — Package Boundary And Owner Routing

BDPF добавляет доменные problem-solution moves и локальные записи; он не вводит новые Core `U.*` kinds. `BuiltAssetSystemFrame` и `SiteFrame` описывают разные физические holons; `BuiltAssetSitePlacementRelation` описывает relation между ними. Эти формы и остальные BDPF records остаются DPF-local relation/description/publication records, пока отдельное FPF-решение не установит иной kind.

| Текущий claim | Прямой владелец | Роль BDPF | Заблокированный overread |
| --- | --- | --- | --- |
| Что является физическим ОКС и какова его граница | `A.1`, `A.1.1`, `B.1.2` | `BDPF.1` даёт built-asset first-use frame | Карточка или BIM-модель не становится ОКС. |
| Что является физической площадкой и как она связана с ОКС | `A.1`, `A.1.1`, `B.1.2`, `E.10.D2` | `BDPF.1A` разводит `SiteFrame` и placement relation | Участок, его номер, линия на плане или комплект изысканий не становится площадкой; relation не становится третьим физическим объектом. |
| Как problem pressure развивается в структуры | `C.32.P2S` | `BDPF.3`, `BDPF.3A`, `BDPF.3B` специализируют built-asset intake | Source signal не выбирает решение. |
| Какая архитектура/структура текущая | `A.22`, `C.30`, `C.30.ASV` | `BDPF.5`, `BDPF.6` дают доменные вопросы и structure families | Схема, раздел ПД или view не становится архитектурой. |
| Как синтезируются кандидаты | `C.32` | `BDPF.6A` задаёт built-asset candidate palette | Palette не выбирает победителя. |
| Как задаются characteristics и eval | `C.16`, `C.25`, `C.32.ACS`, `C.32.ACE` | `BDPF.6B` задаёт built-asset criteria/eval rows | Measure, score и simulation не становятся решением. |
| Как сравниваются и удерживаются варианты | `A.19.CPM`, `A.19.SelectorMechanism`, `G.5`, `C.11` | `BDPF.6C` делает comparison basis и retained set читаемыми | Retained set не является PAD. |
| Как принимается project architecture decision | `C.32.PAD` | `BDPF.7` добавляет built-asset concerns, projection и source returns | ADR, approval или gate не являются PAD. |
| Как решение публикуется | `C.32.ADR`, `E.17`, `E.24.PUB` | `BDPF.7A`, `BDPF.7B` | Читаемый package не создаёт решение или evidence. |
| Чем поддерживается claim | `A.10`; assurance — `B.3` | `BDPF.8` задаёт claim-specific trace | Расчёт не обосновывает всё решение. |
| Готов ли boundary-crossing | `A.15.5`, `A.21` | `BDPF.9` задаёт built-asset gate profiles | Readiness не доказывает качество и не выполняет work. |
| Где решение представлено | `C.30.AD.BA`, `C.33`, `C.34`, `E.17` | `BDPF.10` связывает selected/expected structures с ПД/BIM/views | Carrier или machine check не становятся ОКС, PAD или compliance proof. |
| Что делать с замечанием или source change | `C.32.FAIL`, `E.23`, `G.11` и owner конкретного claim | `BDPF.11` выбирает smallest return | Замечание не доказывает истинность/ложность PAD само по себе. |
| Достаточно ли решение для declared use | `C.32.ADA`, `E.22`, `E.23` | `BDPF.12` специализирует evaluation для built assets | Evaluation не является approval, gate, assurance или work authorization. |

## Principle-Framework Architecture Decision for this edition

```text
PrincipleFrameworkArchitectureDecision@BuiltAssetDesignPrinciplesFramework-v0.5.1:
  frameworkDecisionId: PFAD-BDPF-2026-07-13-001
  governedFrameworkRef: BuiltAssetDesignPrinciplesFramework
  boundedContextRef: FPF-grounded development and support of architecture-significant built-asset design decisions
  frameworkEditionRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  fpfCoreEditionRef: FPFCorePatternSet@July2026
  decisionQuestion: Which domain pattern set, relation structure and publication carrier should support one bounded built-asset architecture decision without redefining FPF Core or becoming a universal design methodology?
  sourceBasisRefs:
    - FPF Core Conceptual Specification@July2026
    - SourceUseAndRefreshMap@BuiltAssetDesignPrinciplesFramework
    - BuiltAssetDesignPrinciplesFramework@2026-07-12-v0.5
  namingDecisionRefs:
    - NameCard@BuiltAssetDesignPrinciplesFramework
    - public prefix BDPF.*; legacy DPF.* read-only
  selectedPatternSetRefs:
    - BDPF.1
    - BDPF.1A
    - BDPF.2
    - BDPF.3
    - BDPF.3A
    - BDPF.3B
    - BDPF.4
    - BDPF.5
    - BDPF.6
    - BDPF.6A
    - BDPF.6B
    - BDPF.6C
    - BDPF.7
    - BDPF.7A
    - BDPF.7B
    - BDPF.8
    - BDPF.9
    - BDPF.10
    - BDPF.11
    - BDPF.12
  selectedPatternRelationRefs:
    - source-to-structure
    - candidate-to-decision
    - decision-to-reliance
    - change-to-repair
    - PFR-BDPF-*
  publicationUnitRefs:
    - this all-in-one carrier with front door, pattern bodies, acceptance cases, support records, quality records and refresh route
  accessCarrierRefs: none in this edition
  dependencyAndEditionRefs:
    - FrameworkEditionDependencyRecord@BuiltAssetDesignPrinciplesFramework
    - NameAndEditionRoute@BuiltAssetDesignPrinciplesFramework
  qualityEvaluationRefs:
    - DPFPackageAdequacyEvaluation@BuiltAssetDesignPrinciplesFramework-v0.5.1
    - E21-BDPF-3A-v0.5.1
    - E21-BDPF-7-v0.5.1
    - E21-BDPF-10-v0.5.1
    - E21-BDPF-12-v0.5.1
  admissionReviewRefs: none; qualification remains locallyUsableWithVisibleLimits
  rejectedAlternatives:
    - treat BDPF as a universal building-design process or WorkPlan
    - define a second architecture, evidence, gate or decision ontology parallel to FPF Core
    - reduce the package to a BIM/document-completeness checklist
    - split the carrier into repository files before relation and quality records are stable
    - promote the edition to stable or enterprise-ready without field evidence
  rationaleRefs:
    - architecture-significance test
    - decision-thread invariants
    - package source map and acceptance probes
    - priority-pattern E.21 evaluations
  consequences:
    - domain use is narrowed to architecture-significant decisions
    - pattern roles and local-record kinds are explicit
    - Core-owner routing and reverse-dependency block remain mandatory
    - field-transfer and enterprise-adoption claims remain open
  publicationCarrierRefs:
    - BuiltAssetDesignPrinciplesFramework-improved-v0.5.1.md
  sourceReturnConditions:
    - direct FPF owner for Core claims
    - project/domain source owner for engineering, regulatory and authority claims
    - Source Use And Refresh Map for package source payload
  refreshOrSupersessionConditions:
    - selected pattern set or relation groups change
    - Core dependency boundary changes
    - package carrier/access architecture changes
    - priority E.21 or E.4.DPF.DA result falls below floor
    - field pilots contradict the selected problem-solution architecture
```

### Pattern roles inside the selected set

| Role | Patterns | What the role adds | What it must not become |
| --- | --- | --- | --- |
| Domain action pattern | `BDPF.1`, `1A`, `3`, `3A`, `4`, `5`, `6`, `6A`, `6B`, `6C`, `7`, `8`, `10`, `11` | Built-asset recognition, action guidance, records and worked cases around structure/decision work | duplicate Core ontology or discipline encyclopedia |
| Method/composition pattern | `BDPF.2`, `3B` | Reusable decision-development method description and bounded service-entry package | WorkPlan, performed work or universal process |
| Publication/navigation pattern | `BDPF.7A`, `7B` | Reader-specific projections and compact access to governed values | decision, evidence or approval by presentation |
| Routing/profile pattern | `BDPF.9` | Select the direct readiness/gate/publication/authority owner and bind a built-asset use profile | second gate kernel or custom status lattice |
| Evaluation pattern | `BDPF.12` | Apply the complete `C.32.ADA` coordinate set to a built-asset PAD for one declared use | approval, assurance, gate or global quality score |

---

# Pattern Index

| ID | Паттерн | Package role | Direct Core owner(s) | Первый результат | Первый use |
| --- | --- | --- | --- | --- | --- |
| `BDPF.1` | ОКС как целевая система в контексте | domain action | `A.1`, `A.1.1`, `B.1.2` | `BuiltAssetSystemFrame@Project` | Восстановить physical built asset, context, boundary and lifecycle slice. |
| `BDPF.1A` | Площадка размещения как физический holon в контексте | domain action | `A.1`, `A.1.1`, `B.1.2`, `E.10.D2` | `SiteFrame@Project` + `BuiltAssetSitePlacementRelation@Project` | Развести физическую площадку, её context-local boundaries и relation размещения ОКС. |
| `BDPF.2` | Способ разработки проектного решения | method/composition | `A.3.1`, `A.3.2`, `A.15` | `DesignDecisionDevelopmentMethodDescription@Project` | Сделать повторяемый способ разработки одного decision family явным. |
| `BDPF.3` | Исходный материал как source signal | domain action | `A.2.4`, `A.10`, `C.32.P2S`, `G.11` | `DesignSourceSignalUseRecord@Project` | Извлечь bounded signal and receiving owner without source-to-solution jump. |
| `BDPF.3A` | Развитие problem pressure в структуры ОКС, площадки или placement relation | domain action | `C.32.P2S` | `BuiltAssetProblemToStructureFlowCard@Project` | Назвать structuring need, unknown structure and next owner. |
| `BDPF.3B` | Анализ исходных данных как стартовый пакет | composition/publication | `E.17`, `A.15.1`, `A.21`, `C.32.P2S` | `InitialDataAnalysisPackage@Project` | Собрать traceable source-analysis package вместо перечня файлов. |
| `BDPF.4` | Концепция использования | domain action | `C.2.1`, `A.6.F`, `C.25` | `UseConceptRecord@Project` | Связать roles, modes, scenarios and conflicts with downstream structure pressure. |
| `BDPF.5` | Концепция системы | domain action | `A.6.F`, `A.3.4`, `C.30.TFS-REL` | `SystemConceptRecord@Project` | Восстановить function-bearer-flow-interface-control logic. |
| `BDPF.6` | Архитектурный вопрос ОКС, площадки или placement relation | domain action | `A.22`, `C.30`, `C.30.ASV` | `BuiltAssetArchitectureQuestionCard@Project` | Выделить unknown/selected structure relation, которая меняет несколько решений. |
| `BDPF.6A` | Кандидатные архитектурные конфигурации | domain action | `C.32`, `C.35` | `CandidateArchitecturePalette@Project` | Сформировать coherent plurality or honest no-plurality reason. |
| `BDPF.6B` | Архитектурные характеристики, criteria и eval | domain action | `C.16`, `C.25`, `C.32.ACS`, `C.32.ACE` | `BuiltAssetArchitectureCriteriaSet@Project` | Построить lawful evaluation basis without hidden optimization policy. |
| `BDPF.6C` | Comparison и retained set | domain action | `A.19.CPM`, `A.19.SelectorMechanism`, `G.5`, `C.11` | `ComparisonBasis@Project` | Разделить comparison, pool treatment, set publication, choice and PAD. |
| `BDPF.7` | Проектное архитектурное решение | domain action | `C.32.PAD` | `ArchitectureDecisionRelation@Project` | Зафиксировать commitment по selected structures, losses, work docking and reopen. |
| `BDPF.7A` | ADR-проекция решения | publication | `C.32.ADR`, `E.17` | `ArchitectureDecisionRecordProjection@Project` | Сделать PAD читаемым without turning record into decision. |
| `BDPF.7B` | Минимальный пакет чтения решения | publication/navigation | `E.17`, `E.24.PUB` | `MinimalDecisionUsePackage@Project` | Дать одному reader use компактный route to governed values. |
| `BDPF.8` | Claim-specific evidence решения | domain action | `A.10`; assurance — `B.3` | `DesignClaimEvidenceTrace@Project` | Связать one claim with evidence, scope, freshness and limitations. |
| `BDPF.9` | Готовность проектного boundary-crossing | routing/profile | `A.15.5`, `A.21` | `BuiltAssetDesignReadinessUse@Project` | Выбрать direct readiness/gate owner and bind a use profile. |
| `BDPF.10` | Проекция решения в ПД/BIM/views | domain representation use | `C.30.AD.BA`, `C.33`, `C.34` | `ProjectDocumentationProjection@Project` | Показать represented, lost and non-represented selected structure. |
| `BDPF.11` | Feedback, impact и repair | domain repair | `C.32.FAIL`, `E.23`, `G.11` | `DesignChangeImpactTrace@Project` | Вернуть change/defect through supported impact paths to the smallest owner. |
| `BDPF.12` | Достаточность решения для declared use | evaluation | `C.32.ADA`, `E.22`, `E.23` | `BuiltAssetArchitectureDecisionAdequacyEvaluation@Project` | Найти blocking coordinate and exact repair before reliance. |

---
# Pattern Bodies

## BDPF.1 — ОКС как целевая система в контексте

> **Type:** DPF pattern body
>
> **Primary EntityOfConcern:** one physical built asset or subsystem under a bounded delimitation-and-use question; `BuiltAssetSystemFrame@Project` is the first DPF-local description result.

### BDPF.1:1 - Problem frame

Используйте этот паттерн, когда объект обсуждается как комплект разделов ПД, BIM-модель, пятно застройки, перечень помещений, сумма инженерных систем или набор замечаний, но невозможно однозначно сказать, **какой физический ОКС рассматривается как система**, где проходит его граница и какую работу/ценность он должен обеспечивать.

Первый полезный ход: назовите физический built asset, bounded context, lifecycle slice, окружение, границу, внешние interfaces, ключевые use scenarios и открытые unknowns. Делайте это до архитектурного вопроса и до проектного решения.

Если паттерн пропущен, разные дисциплины оптимизируют разные implicit objects: АР — объём и планировку, КР — расчётную схему, ИОС — собственные сети, заказчик — функции и площадь, а проектная команда ошибочно считает, что речь идёт об одном и том же system-of-interest.

Что это даёт: последующие source signals, use scenarios, system concept, architecture questions, PAD, evidence и projections получают один recoverable `describedHolonRef`.

Не этот паттерн, если физический ОКС и его граница уже устойчивы, а текущий вопрос относится только к selected structure (`BDPF.6`), architecture description (`BDPF.10`), evidence (`BDPF.8`) или work planning (`A.15.2`).

### BDPF.1:2 - Problem

В строительном проекте слово «объект» часто меняет смысл без объявления: земельный участок, здание, очередь, корпус, секция, помещение, технологическая линия, инженерная система, пакет ПД или договорный предмет. Из-за этого requirements, source signals, characteristics и decisions оказываются формально связанными, но относятся к разным wholes или lifecycle slices.

Нужна минимальная доменная рамка, которая не создаёт новый вид `U.System`, но заставляет проект назвать system-of-interest и его boundary before use.

### BDPF.1:3 - Forces

| Force | Tension |
| --- | --- |
| Договорный объект vs физическая система | Договор и стадия задают scope, но не всегда совпадают с инженерной границей. |
| Междисциплинарность vs локальная оптимизация | Разделы ПД требуют специализации, однако selected structures пересекают разделы. |
| Ранний этап vs полнота | Граница и scenarios ещё уточняются, но полное отсутствие frame делает дальнейшие decisions невосстановимыми. |
| Существующий vs проектируемый объект | При реконструкции текущая, ожидаемая и представленная структуры различаются. |
| Полезность vs overformalization | Нужен тонкий first-use frame, а не исчерпывающая системная модель. |

### BDPF.1:4 - Solution

Создайте минимальный `BuiltAssetSystemFrame@Project`:

```text
BuiltAssetSystemFrame@Project:
  frameId:
  builtAssetRef:
  boundedContextRef:
  lifecycleSlice:
  currentOrProposedPosture: existing | proposed | mixed
  environmentRef:
  systemBoundaryStatement:
  includedHolonRefs:
  excludedEnvironmentRefs:
  externalInterfaceRefs:
  beneficiaryRoleOrGroupRefs:
  operatingAndMaintainingRoleRefs:
  primaryUseScenarioRefs:
  valueAndLossClaimRefs:
  sourceBasisRefs:
  currentUnknowns:
  sourceReturnCondition:
  nonAdmissibleUse:
```

Применяйте рамку в шесть ходов:

1. **Назовите bearer.** Укажите физический ОКС/подсистему, а не файл, раздел, модель или договорный ярлык.
2. **Зафиксируйте context и lifecycle slice.** Одно и то же здание в проектировании, строительстве, эксплуатации и реконструкции допускает разные локальные claims.
3. **Проведите boundary.** Перечислите включённые holons, environment и boundary-crossing interfaces, влияющие на решение.
4. **Привяжите use и value.** Назовите роли/группы и сценарии, ради которых system frame нужен сейчас. Детализация сценариев выполняется в `BDPF.4`.
5. **Разделите current/proposed.** Для реконструкции отдельно укажите существующий объект и проектируемое изменение; не считайте обследовательную модель actual structure без evidence.
6. **Запишите unknowns и return.** Рамка достаточна, когда она предотвращает следующий неверный архитектурный ход. Не заполняйте её «на полноту».

Локальная мантра: **сначала физический ОКС и его граница; затем описания и решения о нём**.

### BDPF.1:5 - Archetypal Grounding

**Реконструкция лечебного корпуса.** В ИК фигурируют «корпус № 2», BIM существующего положения, проектируемая пристройка и общая котельная кампуса. Слабый проектный разговор называет объектом то модель, то корпус, то пристройку. Рамка фиксирует:

```text
builtAssetRef: лечебный корпус вместе с проектируемой пристройкой в scope данного решения
excludedEnvironmentRefs: общая котельная как внешняя supplying system
externalInterfaceRefs: тепло, электроснабжение, медицинские газы, транспортный и пешеходный доступ
currentOrProposedPosture: mixed
currentUnknowns: фактическая несущая способность отдельных участков; допустимая граница вмешательства
```

После этого геотехнический signal не «относится ко всему проекту», а привязывается к foundation/load-bearing structure нужного holon slice; BIM существующего положения остаётся description/evidence carrier, а не самим корпусом.

**Near miss:** «Объект — комплект ПД по договору». Это допустимый contract scope cue, но не system boundary. Требуется отдельный `builtAssetRef`.

### BDPF.1:6 - Bias-Annotation

Паттерн блокирует document-bias и discipline-silo bias: carrier или раздел ПД становится объектом проектирования, а локальная дисциплина — whole. Он также блокирует building-only bias: BDPF применим к сооружениям и инфраструктурным assets, если физический holon и context названы.

### BDPF.1:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF1-1` | `builtAssetRef` указывает на физический ОКС/подсистему, не на carrier. |
| `CC-BDPF1-2` | Bounded context и lifecycle slice явны. |
| `CC-BDPF1-3` | Boundary включает environment и минимум один существенный external interface либо объясняет их отсутствие. |
| `CC-BDPF1-4` | Current/proposed posture различён, если проект касается существующего объекта. |
| `CC-BDPF1-5` | Use/value refs достаточны для следующего pattern use, но не подменяют `BDPF.4`. |
| `CC-BDPF1-6` | Unknowns и source-return condition указаны там, где рамка зависит от неполных данных. |
| `CC-BDPF1-7` | Рамка не используется как architecture decision, evidence, gate или work plan. |

### BDPF.1:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Объект = комплект ПД | Description scope заменяет физический bearer. | Назвать `builtAssetRef` и `systemBoundaryStatement`. |
| Объект = пятно застройки | Пространственная проекция скрывает use, interfaces и system behavior. | Добавить environment, scenarios и external interfaces. |
| Объект = сумма разделов | Междисциплинарные структуры остаются без owner. | Восстановить whole и downstream `BDPF.5/6`. |
| Existing model = actual asset | Description overread. | Назвать source/evidence relation и uncertainty. |
| Полная системная модель до первого хода | Анализ становится дорогим и задерживает решение. | Остановиться на smallest frame, предотвращающем следующий wrong move. |

### BDPF.1:9 - Consequences

Преимущество — единый bearer для последующей трассировки. Цена — явный boundary спор в начале; этот спор полезнее, чем поздняя несогласованность решений о разных implicit objects.

### BDPF.1:10 - Rationale

FPF начинает с различения entity, holon, system и description. Для ОКС это особенно важно: документация обычно появляется раньше, чем команда явно формулирует physical system-of-interest. BDPF.1 переносит это различение в первый доменный working result.

### BDPF.1:11 - SoTA-Echoing

- Из `ISO/IEC/IEEE 15288:2023` принимается дисциплина system-of-interest и рекурсивного применения lifecycle thinking; не принимается чтение списка процессов как фактически выполненной работы или готового метода данного проекта.
- Из `ISO/IEC/IEEE 42010:2022` принимается различение entity of interest и architecture description; description не становится архитектурой или объектом.
- Из FPF `A.1`, `A.1.1`, `B.1.2` и `C.30` принимается holon/context/boundary/architecture discipline.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-15288-2023`, `SRC-BDPF-42010-2022`; exact adopted payload and currentness return to `Source Use And Refresh Map`.

### BDPF.1:12 - Relations

Uses `A.1`, `A.1.1`, `A.7`, `B.1.2`, `A.22`, `C.30`, `C.30.AD.BA`, `BDPF.4`, `BDPF.5` and `BDPF.6`. Reopen when physical scope, lifecycle slice, environment, system boundary, source basis or current/proposed posture changes. Open `Built-Asset Design Precision Restoration And Owner Map` when «объект», «система», «модель» или «граница» остаются overloaded.

### BDPF.1:End

---

## BDPF.1A — Площадка размещения как физический holon в контексте

> **Type:** DPF pattern body
>
> **Primary EntityOfConcern:** one physical site-of-placement under a bounded identity, delimitation, structure, characteristic and interface question; `SiteFrame@Project` is the first DPF-local description result. The placement relation is separate and does not become a third physical holon.

### BDPF.1A:1 - Problem frame

Используйте паттерн на старте услуги, когда площадку называют «участком», ГПЗУ, кадастровым номером, топографической основой, комплектом изысканий, пятном застройки или environment ОКС, но неясно, **какой физический holon рассматривается**, по какому identity rule, в каких context-local границах и через какую relation на нём предполагается размещать ОКС.

Первый полезный ход: создайте отдельные `BuiltAssetSystemFrame@Project` и `SiteFrame@Project`, затем назовите `BuiltAssetSitePlacementRelation@Project`. Не объединяйте их одним словом «объект».

Если паттерн пропущен, правовая граница молча становится инженерной, документ — площадкой, характеристика документа — свойством территории, а ограничение конкретной посадки приписывается всему ОКС или всей площадке.

Что это даёт: площадочные sources, structures, characteristics, unknowns и placement alternatives получают правильного bearer и source-return owner до candidate synthesis.

Не этот паттерн, если текущий вопрос только о source-use relation (`BDPF.3`), criteria/eval (`BDPF.6B`), evidence (`BDPF.8`) или work authorization. Эта рамка не является разрешением на проектирование или работы.

### BDPF.1A:2 - Problem

Одна площадка в проектном контуре обычно имеет несколько несовпадающих delimitation relations: правовую, область изысканий, candidate-placement envelope, планируемую зону работ, территорию будущего обслуживания и influence/interface zone. Это не обязательно разные площадки, но и не одна универсальная «граница участка».

Значимые свойства могут принадлежать не площадке как таковой, а конкретной relation размещения конкретного ОКС: доступность, инсоляция, подключаемость, влияние на соседние holons, construction-realization burden и резерв развития.

### BDPF.1A:3 - Forces

| Force | Tension |
| --- | --- |
| Legal parcel vs physical site | Правовая идентификация важна, но не исчерпывает физический holon и engineering influence. |
| One site vs several boundaries | Разные claims требуют разных context-local delimitations. |
| Early uncertainty vs actionable frame | Данных мало, но отсутствие identity и placement relation блокирует честный next use. |
| Site property vs placement property | Source может поддерживать свойство площадки или только конкретной посадки. |
| Carrier convenience vs ontic discipline | План, GIS/BIM и отчёт удобны, но остаются descriptions/evidence carriers. |
| Design scope vs lifecycle overreach | Planned construction/operation scenarios учитываются без отдельного post-design lifecycle loop. |

### BDPF.1A:4 - Solution

Создайте три раздельные записи:

```text
SiteFrame@Project:
  siteFrameId:
  siteRef:
  siteIdentityRule:
  boundedContextRef:
  designConcernWindowRef:
  currentOrProposedPosture: existing | proposed | mixed
  legalParcelBoundaryRefs:
  engineeringStudyBoundaryRefs:
  candidatePlacementBoundaryRefs:
  plannedConstructionWorkBoundaryRefs:
  plannedOperationalTerritoryBoundaryRefs:
  influenceAndInterfaceBoundaryRefs:
  includedPhysicalHolonRefs:
  excludedEnvironmentRefs:
  adjacentHolonRefs:
  existingSiteStructureRefs:
  externalInterfaceRefs:
  sourceBasisRefs:
  siteStructureAndInterfaceMapRef:
  siteCharacteristicProfileRef:
  currentUnknowns:
  sourceReturnCondition:
  nonAdmissibleUse:

BuiltAssetSitePlacementRelation@Project:
  relationId:
  builtAssetRef:
  siteRef:
  boundedContextRef:
  designConcernWindowRef:
  placementState:
    unknown | candidate | selected | expected | represented | actual
  occupiedOrInfluenceEnvelopeRef:
  affectedSiteStructureRefs:
  affectedBuiltAssetStructureRefs:
  boundaryCrossingInterfaceRefs:
  externalFlowRefs:
  mutualConstraintRefs:
  placementCharacteristicRefs:
  sourceBasisRefs:
  currentUnknowns:
  candidatePlacementRefs:
  selectedPlacementRef?:
  evidenceNeedRefs:
  nonAdmissibleUse:
  reopenCondition:

SiteStructureAndInterfaceMap@Project:
  siteRef:
  selectedStructureKindRefs:
  terrainAndDrainageStructureRefs:
  geologicalAndGroundwaterStructureRefs:
  existingBuiltAndUtilityStructureRefs:
  transportAndAccessStructureRefs:
  ecologicalAndProtectedStructureRefs:
  externalUtilityInterfaceRefs:
  neighbouringHolonRelationRefs:
  plannedTemporaryConstructionStructureRefs:
  capturedStructureRefs:
  latentOrMissingStructureRefs:
  sourceReturnCondition:
```

Для navigation/service composition:

```text
ServiceEntryConcernBundle@Project:
  builtAssetSystemFrameRef:
  siteFrameRef:
  builtAssetSitePlacementRelationRef:
  declaredServiceUse:
  currentUnknowns:
  allowedNextUses:
  blockedUses:
  reopenCondition:
```

Bundle — координационная publication, не физический объект, Core-kind, решение о размещении или evidence.

```text
SiteCharacteristicReading@Project:
  readingId:
  bearerRef: siteRef | placementRelationRef | selectedSiteStructureRef
  characteristicRef:
  boundedContextRef:
  scenarioAndDesignConcernWindowRef:
  scaleRef:
  coordinateOrValue:
  unitRef?:
  evidenceStubRef:
  sourceCarrierRef:
  sourceEditionOrObservationDate:
  qualificationWindow:
  epistemicPosture:
    observed | sourceAsserted | modelDerived | assumed | unknown | conflicting
  uncertaintyOrRange:
  missingness:
    notMeasured | insufficientEvidence | notApplicable | notMaterialForCurrentUse
  admissibleUse:
  nonAdmissibleUse:
  affectedArchitectureQuestionRefs:
  sourceReturnCondition:

SiteUncertaintyRegister@Project:
  uncertaintyId:
  siteRef:
  affectedPlacementRelationRef?:
  affectedStructureOrCharacteristicRef:
  uncertaintyKind:
    missing | ambiguous | conflicting | stale | underSampled | modelDependent
  currentKnownRangeOrPosture:
  affectedQuestionOrDecisionRef:
  consequenceIfWrong:
  allowedWorkNow:
  blockedWorkOrReliance:
  requestedSourceOrProbe:
  probeOwnerRef:
  stopOrReturnCondition:
```

Применяйте семь passes: identity; claim-specific delimitation; structure/interface; explicit placement state; structure/constraint/characteristic separation; unknown-to-probe routing; scope boundary. Planned construction/operation boundaries остаются design concern windows: паттерн не вводит ConOps carrier, performed work, authorization или post-design feedback loop.

### BDPF.1A:5 - Archetypal Grounding

**Старт услуги для нового производственного ОКС.** Вход содержит кадастровую выписку, ГПЗУ, топосъёмку, изыскания и ТУ. Слабая формула: «участок изучен; посадка возможна».

Рамка различает физическую площадку, legal parcel boundary, engineering-study boundary и external utility interface. Placement relation остаётся `unknown`: source подтверждает положение сети и ограниченную мощность, но не выбранную посадку. Уровень грунтовых вод публикуется как reading для точек и qualification window, а не как безусловное свойство всей площадки.

Первый допустимый next use — сформировать site/placement architecture questions и probes. Заблокированы claims о пригодности площадки «вообще», выбранной посадке, безопасности, compliance и разрешении работ.

### BDPF.1A:6 - Bias-Annotation

Паттерн блокирует parcel-as-site, carrier-as-holon, one-boundary bias, site-plus-building aggregate bias и characteristic-totalization, а также превращение planned lifecycle scenarios в post-design loop.

### BDPF.1A:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF1A-1` | `siteRef` names one physical site; carrier and identifiers remain refs. |
| `CC-BDPF1A-2` | Built asset, site and placement relation are three distinct positions. |
| `CC-BDPF1A-3` | Context, identity rule and each material boundary use are explicit. |
| `CC-BDPF1A-4` | Site structures/interfaces are recovered or marked missing. |
| `CC-BDPF1A-5` | Each material reading names bearer, scale, evidence/currentness and uncertainty. |
| `CC-BDPF1A-6` | Critical unknowns route to exact question, probe/source and owner. |
| `CC-BDPF1A-7` | Frames/relation are not read as suitability, PAD, gate or authorization. |
| `CC-BDPF1A-8` | Planned lifecycle windows remain design inputs, not performed work. |

### BDPF.1A:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Площадка = кадастровый участок | Legal identity replaces physical holon. | Recover `siteRef` and claim-specific boundaries. |
| Площадка = комплект изысканий | Carrier becomes bearer. | Separate source-use records and SiteFrame. |
| ОКС + площадка = один «объект» | Boundaries and owners merge. | Keep two frames and placement relation. |
| Один score «готовности участка» | Non-aggregable unknowns disappear. | Publish characteristic vector and uncertainty register. |
| Получен документ = свойство доказано | Evidence scope/currentness hidden. | Use reading + `A.10` evidence path. |
| Relation = выбранная посадка | States collapse. | Keep explicit placement state. |

### BDPF.1A:9 - Consequences

Преимущество — анализ снимает неопределённость о самой площадке и placement relation, а не только о carriers. Цена — несколько context-local boundaries и явные unknowns вместо общего статуса.

### BDPF.1A:10 - Rationale

Локальная FPF-опора разводит physical holon, bounded context, delimitation/boundary crossing и description episteme. BDPF.1A специализирует эти различения без нового Core-kind и без копирования FPF.

### BDPF.1A:11 - SoTA-Echoing

- Local FPF `A.1`, `A.1.1`, `B.1.2` supply holon/context/delimitation discipline.
- Local FPF `E.10.D2` preserves site vs description/carrier.
- Local FPF `A.19.ECS`, `C.16`, `A.10` bound characteristic and evidence use.
- Package source-use ref: `SRC-BDPF-FPF-JUL2026`; exact payload returns to `Source Use And Refresh Map`.

### BDPF.1A:12 - Relations

Uses `A.1`, `A.1.1`, `B.1.2`, `E.10.D2`, `A.19.ECS`, `C.16`, `A.10`, `BDPF.1`, `BDPF.3`, `BDPF.3A`, `BDPF.3B`, `BDPF.5`, `BDPF.6`, `BDPF.6B`, `BDPF.8` and `BDPF.9`. Reopen when site identity, context, boundary use, physical structure, source/evidence window, characteristic, placement state or built-asset frame changes.

### BDPF.1A:End

---

## BDPF.2 — Способ разработки проектного решения

> **Type:** DPF pattern body
>
> **Primary EntityOfConcern:** the reusable way of developing one built-asset architecture-decision family; `DesignDecisionDevelopmentMethodDescription@Project` is its project-pinned `U.MethodDescription` use.

### BDPF.2:1 - Problem frame

Используйте паттерн, когда проектная организация предъявляет календарный план, перечень разделов, матрицу согласований или набор контрольных точек, но не может показать **каким воспроизводимым способом** source signals превращаются в candidate structures, comparison, PAD, evidence и projection.

Первый полезный ход: опишите способ разработки одного класса решений — input condition, expected output, обязательные intermediate epistemes, роли, decision/quality boundaries и feedback — не превращая описание метода в work plan или доказательство выполненной работы.

Если паттерн пропущен, ошибки исправляются локальной правкой ПД; команда не может определить, какой шаг рассуждения отсутствовал и как предотвратить повторение.

Что это даёт: экспертное сопровождение проверяет не только carrier outcome, но и recoverable design method.

Не этот паттерн, если текущий вопрос — конкретный WorkPlan (`A.15.2`), readiness (`BDPF.9`), performed work (`A.15.1`) или package-level DPF authoring (`E.4.DPF`).

### BDPF.2:2 - Problem

Разработка проектного решения часто скрыта внутри личного опыта ведущего специалиста и структуры выпуска ПД. Формальная процедура перечисляет действия, но не объясняет, какие промежуточные знания должны появиться, кто может их проверить, какой claim закрывается и где необходимо вернуться к источнику.

### BDPF.2:3 - Forces

| Force | Tension |
| --- | --- |
| Tacit expertise vs replayability | Опыт ускоряет работу, но плохо переносится между командами и версиями проекта. |
| Method vs plan | Устойчивый способ действия не равен датированному плану. |
| Minimal apparatus vs reliance | Для простого решения достаточно тонкого метода; критичное решение требует roles, evidence и gates. |
| Discipline autonomy vs system coherence | Специалисты должны сохранять профессиональный метод, но междисциплинарные transitions должны быть явны. |
| Standard process vs local problem | Внешний process framework полезен как source, но не определяет automatically local method. |

### BDPF.2:4 - Solution

Создайте `DesignDecisionDevelopmentMethodDescription@Project` для **одного повторяющегося decision family**, а не для всего проекта сразу.

```text
DesignDecisionDevelopmentMethodDescription@Project:
  methodDescriptionId:
  governedDecisionFamily:
  builtAssetScopeRef:
  entryCondition:
  expectedOutputKind:
  requiredIntermediateResultKinds:
  methodMoves:
    - moveId:
      inputKindRefs:
      actionGuidance:
      outputKindRef:
      stopOrReturnCondition:
      receivingOwnerRef:
  roleAssignmentRequirements:
  separationOfDutiesRefs:
  evidenceAndEvalRequirements:
  readinessProfiles:
  feedbackAndRefreshRoute:
  nonGoals:
  nonAdmissibleUse:
```

Рекомендуемая минимальная method spine для reliance-bearing architecture decision:

```text
physical built asset frame
→ bounded source-signal use
→ problem-to-structure card
→ use/system concept as needed
→ architecture question
→ candidate palette or no-plurality reason
→ criteria/eval and comparison basis
→ retained set
→ PAD
→ claim-specific evidence
→ PD/BIM projection
→ declared-use adequacy evaluation
→ readiness/feedback return when current
```

Правила применения:

1. Начните с конкретного decision family: например, «выбор несущей схемы корпуса», а не «проектирование здания».
2. Для каждого move укажите результат, который должен существовать после применения, и receiving owner.
3. Не превращайте method spine в обязательный total order. Укажите prerequisites и conditional exits; некоторые records могут уже существовать.
4. Role names materialize as `RoleAssignment` only for reliance-bearing work. Должность или подпись не доказывает enactment.
5. Если method description используется для планирования, создайте отдельный `U.WorkPlan`; если работа выполнена — отдельный `U.Work` и evidence.
6. Feedback меняет method description только после `BDPF.11` и, при повторном улучшении, `E.23`.

Локальная мантра: **метод говорит, какой результат должен появиться и почему; план — когда и кем; work — что фактически произошло**.

### BDPF.2:5 - Archetypal Grounding

**Выбор расположения центральной инженерной зоны.** Слабый метод: «АР выдаёт план, ИОС согласует, BIM-координатор проверяет коллизии». Он описывает передачи carriers, но не decision development.

Исправленный method slice:

1. `BDPF.4/5`: восстановить maintenance, emergency и operating scenarios, flows и interfaces.
2. `BDPF.6`: сформулировать architecture question о spatial, engineering-systems и module-interface structures.
3. `BDPF.6A`: синтезировать минимум две configuration либо записать обоснованный no-plurality reason.
4. `BDPF.6B/6C`: сравнить доступность обслуживания, длину трасс, резервирование, пожарные ограничения и construction phasing без hidden scalar winner.
5. `BDPF.7`: принять PAD, указать accepted losses и developer refinement boundary.
6. `BDPF.10`: проверить, что selected structures представлены в plans/models/specifications.

BIM clash check остаётся validation/evidence input, а не методом выбора архитектуры.

### BDPF.2:6 - Bias-Annotation

Паттерн блокирует document-production bias, stage-gate bias и checklist-as-method. Он также блокирует обратную ошибку: превращение BDPF в обязательную универсальную методологию вместо configurable method description для конкретного decision family.

### BDPF.2:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF2-1` | Governed decision family и built-asset scope названы. |
| `CC-BDPF2-2` | Entry condition и expected output kind различены. |
| `CC-BDPF2-3` | Каждый move производит exact result и имеет stop/return condition. |
| `CC-BDPF2-4` | Method description не подменяет WorkPlan и performed Work. |
| `CC-BDPF2-5` | Role requirements используют `RoleAssignment` для reliance-bearing claims. |
| `CC-BDPF2-6` | Evidence/eval/gate остаются у прямых owners. |
| `CC-BDPF2-7` | Feedback route указывает smallest method repair, а не автоматическую перепись всего метода. |

### BDPF.2:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Разделы ПД как method steps | Carrier structure заменяет reasoning structure. | Назвать intermediate knowledge results. |
| Календарь как метод | Intent schedule подменяет reusable way of doing. | Отделить `U.WorkPlan`. |
| Чек-лист как Solution | Checks не говорят, как получить result. | Добавить positive action spine и exact outputs. |
| Подпись как выполнение | Role/status overread. | `RoleAssignment` + performed work/evidence when current. |
| Единый метод для всех решений | Apparatus становится чрезмерным. | Описывать decision families и conditional branches. |

### BDPF.2:9 - Consequences

Метод становится inspectable и улучшаемым, а повторяющиеся defects можно связать с конкретным move. Цена — необходимость различать method, method description, plan, readiness и work.

### BDPF.2:10 - Rationale

Проектная документация показывает часть результата, но не гарантирует recoverable design method. FPF quartet позволяет отделить reusable method from its description and enactment; BDPF связывает это с built-asset decision chain.

### BDPF.2:11 - SoTA-Echoing

- Из `ISO/IEC/IEEE 15288:2023` и `ISO/IEC/IEEE 24748-2:2024` адаптируется рекурсивное и итеративное lifecycle/process thinking; process catalogue не импортируется как project WorkPlan.
- Из `ISO/IEC/IEEE 24774:2021` принимается требование описывать purpose/outcomes процесса; BDPF переводит его в exact intermediate results и owner exits.
- Из FPF `A.3.2`, `A.15`, `B.1.5`, `E.18.1` принимается method-description/work/P2W separation.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-15288-2023`, `SRC-BDPF-24748-2-2024`, `SRC-BDPF-24774-2021`; exact process/method applicability returns to `Source Use And Refresh Map`.

### BDPF.2:12 - Relations

Uses `A.3.1`, `A.3.2`, `A.15`, `A.15.1`, `A.15.2`, `A.15.5`, `B.1.5`, `E.18.1`, `BDPF.1`, `BDPF.3A`, `BDPF.7`, `BDPF.11` and `BDPF.12`. Reopen when decision family, entry condition, required results, roles, evidence basis or repeated defect pattern changes.

### BDPF.2:End

---

## BDPF.3 — Исходный материал как source signal

> **Type:** DPF pattern body
>
> **Primary EntityOfConcern:** one bounded source-use relation between a source-bearing carrier, an extracted design signal and its receiving claim owner; `DesignSourceSignalUseRecord@Project` is the first record.

### BDPF.3:1 - Problem frame

Используйте этот паттерн, когда ТЗ, ИРД, ГПЗУ, ТУ, изыскания, обследование, нормативный источник, требование эксплуатации, BIM/IFC, экспертное замечание или иное material передано проекту, но ещё неизвестно, **какой bounded signal из него извлечён**, какую структуру он затрагивает и для какого claim его допустимо использовать.

Первый полезный ход: отделите carrier от extracted signal; зафиксируйте source owner/edition, scope, uncertainty, admissible use, non-admissible use, affected structure/characteristic и receiving owner.

Если паттерн пропущен, команда говорит «учтено по документу», а later decision inherits unstated assumptions, stale editions и неверную область применения.

Что это даёт: source material становится reviewable input к problem shaping, evidence или constraint work, но не решением.

Не этот паттерн, если требуется оценить sufficiency evidence для конкретного claim (`BDPF.8`) или package-level SoTA/source synthesis (`G.2`).

### BDPF.3:2 - Problem

Один carrier может содержать несколько signals с разными scopes; один signal может поддерживать несколько вопросов, но не одинаково. Кроме того, source authority, evidence use и design constraint — разные relations. Без source-use record документ становится универсальным «основанием» и скрывает currentness debt.

### BDPF.3:3 - Forces

| Force | Tension |
| --- | --- |
| Source authority vs local extraction | Источник может быть официальным, но interpretation остаётся scoped. |
| Rich carrier vs atomic signal | Большой отчёт нельзя честно привязать к решению одной ссылкой. |
| Speed vs currentness | Проекту нужен быстрый ход, но outdated source может изменить решение. |
| Constraint vs evidence | Требование ограничивает решение; расчёт/наблюдение может поддерживать claim; один carrier иногда играет обе роли. |
| Uncertainty vs false closure | Missing/ambiguous data должны оставаться видимыми. |

### BDPF.3:4 - Solution

Создавайте одну запись на один materially different signal/use:

```text
DesignSourceSignalUseRecord@Project:
  signalUseId:
  sourceCarrierRef:
  sourceKind:
  sourceOwnerRef:
  sourceEditionOrDate:
  sourceScope:
  extractedSignal:
  signalClaimKind:
    observation | requirement | constraint | assumption | issue | preference | forecast | modelOutput | otherDeclared
  affectedBuiltAssetRef?:
  affectedSiteRef?:
  affectedPlacementRelationRef?:
  affectedStructureKindRefs:
  affectedSiteStructureRefs?:
  affectedArchitectureCharacteristicRefs:
  affectedSiteCharacteristicRefs?:
  supportedQuestionRefs:
  uncertaintyAndAmbiguity:
  admissibleUse:
  nonAdmissibleUse:
  freshnessOrValidityWindow:
  sourceReturnCondition:
  receivingOwnerRef:
  affectedDecisionOrProjectionRefs:
```

Применяйте запись так:

1. **Pin source.** Назовите carrier, owner, edition/date и scope. «Последняя версия» без ref не допускается.
2. **Extract signal.** Переформулируйте только то, что source действительно несёт; отделите quote/fact от interpretation.
3. **Classify claim.** Observation, requirement, constraint, assumption, issue и model output имеют разные downstream owners.
4. **Name one affected subject and structure.** Укажите ОКС, площадку или placement relation; не перегружайте `affectedBuiltAssetRef` площадочным смыслом. Если structure ещё неизвестна, отправьте signal в `BDPF.3A`.
5. **Bound use.** Укажите admissible и non-admissible use. Официальность source не расширяет scope автоматически.
6. **Set return.** Currentness, missing data, contradiction или changed owner создают reopen.

Полезный `needKind` может использоваться как local cue, но не как новый FPF kind:

| Cue | Типичная structuring need | Не даёт автоматически |
| --- | --- | --- |
| `sitePlacementNeed` | spatial/interface/external-flow structures | посадку или объёмное решение |
| `geotechnicalOrStructuralNeed` | foundation/load-bearing/material structures | выбранную конструктивную схему |
| `engineeringCapacityNeed` | engineering/interface/control structures | достаточную инженерную конфигурацию |
| `useScenarioNeed` | functional/flow/control/maintenance structures | UseConcept или PAD |
| `constructionRealizationNeed` | temporary/construction/logistics structures | WorkPlan строительства |
| `informationRelianceNeed` | description, captured/lost structure, source currentness | доказательство или решение |
| `reviewDefectNeed` | suspect evidence/decision/method/projection | истинность или ложность PAD |

### BDPF.3:5 - Archetypal Grounding

**Инженерно-геологический отчёт.** Слабая запись: «По изысканиям принять свайный фундамент». Source carrier содержит слои грунтов, характеристики, groundwater observations, limitations и recommendations; он не выбирает architecture option.

Исправленная запись:

```text
extractedSignal: в пределах исследованных скважин слабый водонасыщенный слой и указанная uncertainty ограничивают допустимые foundation/load-bearing configurations
signalClaimKind: observation + model interpretation
admissibleUse: сформировать geotechnical structuring need, candidate foundation schemes и evidence plan
nonAdmissibleUse: прямой выбор свайной схемы; подтверждение settlement для нерассмотренных loads/configurations
receivingOwnerRef: BDPF.3A, затем BDPF.6/6A/6B
sourceReturnCondition: изменённая посадка, нагрузки, дополнительные изыскания или revised model
```

**Near miss:** ТУ на подключение задают capacity/interface constraint, но не подтверждают adequacy внутренней системы.

### BDPF.3:6 - Bias-Annotation

Паттерн блокирует authority bias, document-as-evidence bias и stale-source laundering. Он также блокирует «атомизацию ради атомизации»: отдельная запись нужна только когда signal/use materially отличается.

### BDPF.3:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF3-1` | Carrier и extracted signal различены. |
| `CC-BDPF3-2` | Source owner, edition/date и scope recoverable. |
| `CC-BDPF3-3` | Claim kind и uncertainty указаны. |
| `CC-BDPF3-4` | Affected built asset/structure либо honest unknown названы. |
| `CC-BDPF3-5` | Admissible и non-admissible use явны. |
| `CC-BDPF3-6` | Receiving owner принимает следующий claim. |
| `CC-BDPF3-7` | Source return triggered by freshness, contradiction or scope change. |

### BDPF.3:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| «Учтено по документу» | Signal и use не восстанавливаются. | Записать extracted signal и supported question. |
| Source = decision | Constraint/observation выбирает option. | Перейти в `BDPF.3A/6A/6C/7`. |
| Whole-report citation | Несколько claims смешаны одной ссылкой. | Разделить materially different signal-use rows. |
| Актуально по умолчанию | Currentness скрыта. | Pin edition/window и source-return. |
| Неизвестное превращено в conservative solution | Uncertainty закрывается без candidate work. | Сохранить unknown и receiving owner. |

### BDPF.3:9 - Consequences

Source trace становится дороже на несколько строк, но дешевле изменения неверно истолкованного решения. Запись позволяет impact analysis при source change.

### BDPF.3:10 - Rationale

FPF различает source, evidence use, claim и decision. В built-asset projects высокая документная плотность делает это различение критичным: сам факт наличия ИК не означает их controlled use.

### BDPF.3:11 - SoTA-Echoing

- Из ISO 19650 series адаптируется editioned information management and exchange discipline; information-container status не становится engineering truth или PAD.
- Из requirements-engineering practice адаптируется trace from source statement to scoped requirement/constraint; requirement не импортируется как solution.
- Из FPF `C.22.2`, `A.10`, `A.2.4`, `G.2` и `G.11` принимается problem/source/evidence/currentness separation.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-19650-1-2018`, `SRC-BDPF-19650-2-2018`; exact source/container applicability returns to `Source Use And Refresh Map`.

### BDPF.3:12 - Relations

Uses `C.22.2`, `A.2.4`, `A.10`, `B.3`, `C.32.P2S`, `G.2`, `G.11`, `BDPF.1`, `BDPF.1A`, `BDPF.3A`, `BDPF.3B`, `BDPF.8` and `BDPF.11`. Open `Source Use And Refresh Map` when exact source family, edition or adopted/rejected payload matters.

### BDPF.3:End

---
## BDPF.3A — Развитие problem pressure в структуры ОКС, площадки или placement relation

> **Type:** DPF pattern body
>
> **Primary EntityOfConcern:** one problem-pressure-to-architecture-structuring relation for exactly one subject: physical built asset, physical site or placement relation; `BuiltAssetProblemToStructureFlowCard@Project` is its thin project record under `C.32.P2S`.

### BDPF.3A:1 - Problem frame

Используйте этот паттерн, когда source signal, requirement, issue, constraint, expert comment или design defect уже сформулирован, но команда ещё не знает, **какая structure или relation выбранного subject неизвестна, спорна или должна измениться**.

Первый полезный ход: назовите `architectureStructuringNeed`, smallest useful structure kinds, current unknown, characteristics under pressure и governing owner следующего claim. Не переходите к candidate configuration, пока structure question не recoverable.

Если паттерн пропущен, requirement превращается в локальную drawing edit, а problem pressure — в преждевременное решение. Позже невозможно понять, почему один раздел изменился, а связанная структура других дисциплин осталась прежней.

Что это даёт: problem-side material становится architecture-ready без подмены candidate synthesis или PAD.

Не этот паттерн, если текущий вопрос уже является grounded architecture claim (`C.30`/`BDPF.6`), candidate synthesis (`BDPF.6A`) или конкретным decision (`BDPF.7`).

### BDPF.3A:2 - Problem

Строительный source material обычно формулирует pressure языком требований, параметров, замечаний и запретов. Архитектурная работа требует другого вопроса: какая selected/unknown structure определяет выполнение требований и какие alternatives возможны. Между этими формами нужен явный bridge.

### BDPF.3A:3 - Forces

| Force | Tension |
| --- | --- |
| Requirement language vs structure language | «Обеспечить» не говорит, какой bearer или relation должен измениться. |
| Smallest useful structure set vs checklist | Нужен минимум для следующего хода, не полный каталог structure kinds. |
| Structural uncertainty vs premature solution | Unknown должен оставаться unknown до candidate work. |
| Local issue vs cross-disciplinary effects | Один pressure может затронуть spatial, flow, control, load-bearing и interface structures. |
| Connected flow vs owner discipline | P2S должен связывать ход, не поглощая Core owners. |

### BDPF.3A:4 - Solution

Создайте thin flow card, заполняя только поля, предотвращающие следующий неверный ход:

```text
BuiltAssetProblemToStructureFlowCard@Project:
  flowId:
  subjectPosture:
    builtAsset | site | builtAssetSitePlacementRelation
  describedBuiltAssetRef?:
  describedSiteRef?:
  describedPlacementRelationRef?:
  boundedContextRef:
  designConcernWindowRef:
  problemPressureRefs:
  sourceSignalUseRefs:
  architectureStructuringNeed:
  currentUnknownStructureOrRelation:
  smallestUsefulArchitectureStructureKindRefs:
  unresolvedStructureFamilyCueRows?:
    - cueLabel:
      proposedStructureKindReading:
      resolutionOwnerRef:
  affectedArchitectureCharacteristicRefs:
  candidateStructureCueRefs:
  currentStopOrReturnReason:
  structuralInformationNotes:
    captured:
    latentOrHidden:
    lostOrMissing:
  receivingOwnerForNextClaim:
  sourceReturnCondition:
```

Рабочий ход:

1. **Recover one subject and problem pressure.** Для ОКС используйте `BDPF.1`; для площадки/placement relation — `BDPF.1A`. Одна card сохраняет один primary subject.
2. **State structuring need.** Используйте action form: «выбрать», «разделить», «связать», «распределить», «проверить», «вернуть к источнику» определённую structure.
3. **Name unknown.** Напишите, что именно неизвестно: bearer, boundary, allocation, interface, flow path, control relation, load path, temporary state и т.п.
4. **Select smallest structure kinds.** Use exact project `ArchitectureStructureKindRef` values where recovered. Otherwise publish a lower-case cue with `resolutionOwnerRef`; a cue is not a durable kind.
5. **Name characteristics under pressure.** Если characteristic или scale не recoverable, направьте в `C.16.P`/`BDPF.6B`.
6. **Assign next owner.** `BDPF.6` для architecture question, `BDPF.6A` для candidate palette, `BDPF.8` для evidence gap, `BDPF.10` для representation loss, `BDPF.11` для repair.
7. **Stop.** Flow card не должна содержать fictitious selected structures или PAD.

Примеры `architectureStructuringNeed`:

- «выбрать spatial/flow structure, обеспечивающую раздельные потоки пациентов и логистики»;
- «восстановить actual load-bearing structure существующего участка до выбора усиления»;
- «синтезировать interface structure между внутренней сетью и ограниченным внешним подключением»;
- «проверить, какая temporary construction structure сохраняет эксплуатационный режим действующего корпуса».

### BDPF.3A:5 - Archetypal Grounding

**Ограниченная электрическая мощность.** ТУ фиксируют допустимую мощность. Слабый ход — «уменьшить установленную мощность оборудования». P2S-card восстанавливает:

```text
architectureStructuringNeed: синтезировать engineering/control/operating-mode structures, сохраняющие critical use scenarios при ограничении внешнего interface
currentUnknownStructureOrRelation: распределение нагрузок, приоритеты, резервирование, режимы отключения и local generation relation
unresolvedStructureFamilyCueRows:
  - cueLabel: engineeringSystemsCue
    proposedStructureKindReading: supply, distribution, conversion and redundancy relations
    resolutionOwnerRef: BDPF.5/BDPF.6
  - cueLabel: controlOperationCue
    proposedStructureKindReading: prioritization, load shedding, sensing and operating-mode relations
    resolutionOwnerRef: BDPF.5/BDPF.6
  - cueLabel: moduleInterfaceCue
    proposedStructureKindReading: external connection and internal subsystem boundary relations
    resolutionOwnerRef: BDPF.6
  - cueLabel: transformationFlowCue
    proposedStructureKindReading: energy flow from external interface through conversion/distribution to critical loads
    resolutionOwnerRef: BDPF.5/C.30.TFS-REL
receivingOwnerForNextClaim: BDPF.5, BDPF.6, BDPF.6A
```

Это открывает варианты: load shedding, staged operation, redundancy policy, local generation, storage, change of use scenario. Source signal перестаёт автоматически выбирать один equipment reduction.

**Near miss:** замечание «не обеспечен доступ для обслуживания» сначала превращается в maintenance scenario + spatial/flow/interface structuring need, а не в произвольное увеличение прохода.

### BDPF.3A:6 - Bias-Annotation

Паттерн блокирует requirement-to-solution jump, drawing-locality bias и structure-kind maximalism. Он также блокирует P2S-as-workflow: карта соединяет current relations, но не утверждает, что все позиции должны выполняться последовательно.

### BDPF.3A:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF3A-1` | Exactly one `subjectPosture`, matching subject ref and bounded context are named. |
| `CC-BDPF3A-2` | Problem pressure связан с source-use refs либо honest local observation. |
| `CC-BDPF3A-3` | `architectureStructuringNeed` сформулирован как structure question, не как выбранное решение. |
| `CC-BDPF3A-4` | Current unknown and smallest exact structure-kind refs are explicit; unresolved cues have a resolution owner. |
| `CC-BDPF3A-5` | Characteristics under pressure названы или отправлены к owner. |
| `CC-BDPF3A-6` | Receiving owner для следующего claim указан. |
| `CC-BDPF3A-7` | Lost/missing structural information имеет source-return condition. |

### BDPF.3A:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| «Требуется сделать X» | Solution встроен в problem statement. | Переписать как unknown structure + structuring need. |
| Каталог всех structure kinds | Рабочий вопрос теряется. | Оставить `smallestUsefulArchitectureStructureKindRefs`; unresolved labels keep as lower-case cues with owner. |
| P2S-card как PAD | Candidate/selected structures выдуманы. | Остановиться на receiving owner. |
| Local drawing fix | Cross-disciplinary relation не рассматривается. | Проверить affected structures/interfaces. |
| `nqdWorkState` как обязательная стадия | Local reading aid превращается в workflow authority. | Использовать direct fields и current stop reason. |

### BDPF.3A:9 - Consequences

Появляется явный architecture entry и trace from pressure to structure. Цена — необходимость признать unknown вместо немедленного ответа.

### BDPF.3A:10 - Rationale

`C.32.P2S` уже владеет общим problem-to-structure unfolding. BDPF.3A не создаёт новый lifecycle; он даёт built-asset thin use card и доменные prompts для structure recovery.

### BDPF.3A:11 - SoTA-Echoing

- Из FPF `C.32.P2S` принимается connected flow with governing-pattern-specific exits.
- Из architecture-description practice принимается concern-to-structure discipline; viewpoint или document section не становятся structure kind.
- Из systems-engineering problem framing принимается separation of need/problem from solution; процессная терминология не становится project order.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-15288-2023`, `SRC-BDPF-42010-2022`; exact adopted payload and currentness return to the source map.

### BDPF.3A:12 - Relations

Specializes `C.32.P2S`; uses `C.22.2`, `A.22`, `C.30`, `C.30.ASV`, `C.33`, `BDPF.1`, `BDPF.1A`, `BDPF.3`, `BDPF.5`, `BDPF.6`, `BDPF.6A`, `BDPF.8`, `BDPF.10` and `BDPF.11`. Reopen when source signal, affected holon, unknown structure, characteristic pressure or receiving owner changes.

### BDPF.3A:End

---

## BDPF.3B — Анализ исходных данных как стартовый пакет сопровождения

> **Type:** DPF composition pattern body
>
> **Primary EntityOfConcern:** `InitialDataAnalysisPackage@Project`, a publication/navigation package that composes source-use and problem-to-structure records for one bounded service entry.

### BDPF.3B:1 - Problem frame

Используйте паттерн, когда сопровождение начинается с анализа комплекта ТЗ, участка, ТУ, изысканий, обследований, требований эксплуатации и иных carriers, а результат должен быть пригоден для дальнейшей P2S-работы, а не только читаться как обзорный отчёт.

Первый полезный ход: собрать inventory, signal-use records, gap/ambiguity register, initial use/system extraction, P2S cards и profile-specific readiness use в один package с explicit non-use boundary.

Если паттерн пропущен, «анализ исходных данных» заканчивается перечнем файлов, summary или замечаниями без receiving owners. Проект не может доказать, что materials transformed into reviewable design pressure.

Что это даёт: проектировщик остаётся автором анализа; сопровождающая/экспертная роль получает inspectable trace и может указать missing relation, не подменяя design work.

Не этот паттерн для одного source signal (`BDPF.3`), для performed analysis work (`A.15.1`) или для project architecture decision (`BDPF.7`).

### BDPF.3B:2 - Problem

Комплект исходных данных неоднороден: часть документов отсутствует, часть противоречива, часть устарела, а часть содержит сведения, относящиеся к другим scopes. Свободный отчёт трудно обновлять и использовать для impact analysis. Нужен composition package с typed internal refs.

### BDPF.3B:3 - Forces

| Force | Tension |
| --- | --- |
| Fast service entry vs deep design | Пакет должен быстро открыть next work, но не симулировать завершённое проектирование. |
| Package readability vs source atomicity | Reader нужен один вход, но signals должны оставаться адресуемыми. |
| Expert oversight vs author responsibility | Сопровождение проверяет trace, а не выполняет анализ вместо проектировщика. |
| Readiness vs proof | Direct-owner readiness/gate relation может ограничить следующий use, но не подтверждает PAD. |
| Currentness vs package stability | Source changes должны обновлять impacted rows, а не требовать переписывать весь report. |

### BDPF.3B:4 - Solution

Соберите:

```text
InitialDataAnalysisPackage@Project:
  packageId:
  packageProfile: initialBuiltAssetAndSiteAnalysis
  projectRef:
  serviceEntryConcernBundleRef:
  initialBuiltAssetSystemFrameRef:
  initialSiteFrameRef:
  builtAssetSitePlacementRelationRef:
  boundedContextRef:
  declaredReaderUse:
  sourceCarrierInventoryRef:
  designSourceSignalUseRecordRefs:
  sourceGapAndAmbiguityRegisterRef:
  initialUseScenarioExtractionRef:
  siteStructureAndInterfaceMapRef:
  siteCharacteristicProfileRef:
  siteUncertaintyRegisterRef:
  problemToStructureFlowCardRefs:
  sourceAnalysisReadinessUseRef:
  analysisPerformedWorkRef:
  authorAndReviewerRoleAssignmentRefs:
  allowedNextUses:
  blockedUses:
  admissibleUse:
  nonAdmissibleUse:
  sourceReturnCondition:
```

Минимальный internal content:

```text
SourceCarrierInventory@Project:
  carrierRef | kind | owner | edition/date | receivedState | scope | accessibility | currentnessCue

SourceGapAndAmbiguityRegister@Project:
  gapId | affectedSignalOrQuestion | ambiguityOrConflict | impact | requestedSourceOrProbe | owner | stop/return

InitialUseScenarioExtraction@Project:
  scenarioCue | sourceRef | role/mode | downstream BDPF.4 need | uncertainty
```

Применение:

1. `BDPF.1/1A` establish separate built-asset/site frames and one placement relation; no carrier fills a physical ref.
2. Inventory фиксирует не только наличие, но edition, owner, scope и access limits.
3. Каждый materially useful signal оформляется через `BDPF.3` with one primary affected subject.
4. Site structures/interfaces/readings and unknown-to-probe returns are explicit.
5. Gaps/contradictions не скрываются общим status «недостаточно»; указываются affected questions и next acquisition/probe.
6. Initial use/system extraction является cue set для `BDPF.4/5`, не законченной концепцией.
7. Каждый architecture-relevant pressure получает `BDPF.3A` card.
8. Readiness use проверяет готовность **следа анализа** к следующему declared use. Если существует настоящий `A.21` gate, он использует собственный profile/check set/decision log; иначе результат остаётся direct-owner readiness disposition. Ни один из них не выбирает architecture option.
9. `analysisPerformedWorkRef` указывает на actual work evidence, если project relies on факт проведения анализа; package itself не является work.

### BDPF.3B:5 - Archetypal Grounding

**Реконструкция производственного корпуса.** Пакет содержит 42 файла. Свободный summary сообщает: «данные в основном достаточны». Controlled package выявляет:

- обследование несущих конструкций не покрывает участок нового оборудования;
- ТУ на электроснабжение относится к прошлой peak-load assumption;
- технологическое задание содержит два несовместимых режима;
- BIM существующего положения не имеет currentness evidence для части помещений;
- каждый gap связан с specific P2S question и owner.

`SourceAnalysisReadinessUse` фиксирует bounded disposition: разрешено продолжить разработку use/system concepts и два candidate-structure probes при явно сохранённых gaps; PAD и publication reliance остаются blocked. Если organization materializes an actual `A.21` gate, эквивалентный условный outcome публикуется как `GateDecision=degrade`, а не как локальное значение.

### BDPF.3B:6 - Bias-Annotation

Паттерн блокирует file-count completeness, report-as-analysis и expert-substitution. Он также блокирует package maximalism: records добавляются только при receiving use.

### BDPF.3B:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF3B-1` | Package has separate built-asset frame, site frame, placement relation, bounded context and reader use. |
| `CC-BDPF3B-2` | Inventory contains owner, edition, scope and currentness, not only file names. |
| `CC-BDPF3B-3` | Every material signal has one primary subject posture and uses a `BDPF.3` record. |
| `CC-BDPF3B-4` | Site structures, interfaces and characteristic readings are recovered where material; absence is explicit. |
| `CC-BDPF3B-5` | Critical site unknowns point to the affected question or probe and to an acquisition/return owner. |
| `CC-BDPF3B-6` | Initial use/system extraction is marked provisional. |
| `CC-BDPF3B-7` | Architecture pressure is subject-bounded and has P2S cards. |
| `CC-BDPF3B-8` | Readiness use states both allowed and non-allowed next uses. |
| `CC-BDPF3B-9` | Package, performed work, PAD, evidence, suitability and authorization remain distinct. |
### BDPF.3B:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Перечень полученных файлов | No extracted design value. | Add signal-use rows and gaps. |
| Narrative summary without refs | Impact cannot be replayed. | Addressable internal records. |
| «Данных достаточно» | Use-specific readiness hidden. | Declare direct owner, readiness/gate profile when actually present, and allowed/non-allowed uses. |
| Эксперт пишет концепцию за проектировщика | Role/work substitution. | Keep author/reviewer assignments and separate work refs. |
| Package = approval to design | Gate/deontic overread. | Route authorization to direct owner. |

### BDPF.3B:9 - Consequences

Package becomes updateable and reusable; changed sources can identify suspect decisions later. Cost is initial normalization of sources into addressable rows.

### BDPF.3B:10 - Rationale

A publication package is valuable when it connects internal records without merging their kinds. BDPF.3B makes service entry legible while preserving source, work, readiness/gate and decision owners.

### BDPF.3B:11 - SoTA-Echoing

- ISO 19650 information-management practice supplies editioned information-container, exchange and responsibility pressure; BDPF rejects container status as engineering adequacy.
- `ISO 29481-1:2025` supplies process-to-information-delivery discipline; BDPF uses it as source for information need and exchange, not as proof that project work occurred.
- FPF `E.17`, `A.15.1`, `A.21`, `C.32.P2S` govern package, work, gate and flow boundaries.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-19650-1-2018`, `SRC-BDPF-19650-2-2018`, `SRC-BDPF-29481-1-2025`; exact information-delivery applicability returns to `Source Use And Refresh Map`.

### BDPF.3B:12 - Relations

Composes `BDPF.1`, `BDPF.1A`, `BDPF.3`, `BDPF.3A`, provisional inputs to `BDPF.4/5`, and `BDPF.9`; uses `E.17`, `A.15.1`, `A.21`, `G.11`. Reopen on source inventory, ownership, edition, gap, scope or readiness-use change.

### BDPF.3B:End

---

## BDPF.4 — Концепция использования

> **Type:** DPF pattern body
>
> **Primary EntityOfConcern:** the source-bounded use-scenario structure of one physical built asset for one declared design use; `UseConceptRecord@Project` is its description episteme.

### BDPF.4:1 - Problem frame

Используйте паттерн, когда назначение и технико-экономические показатели известны, но проект не показывает, **кто, в каких режимах, при каких triggers и с какими success/failure conditions использует объект**.

Первый полезный ход: создать несколько source-bounded scenario rows, включая normal, maintenance, emergency и logistics/access cases, затем назвать conflicts и downstream structure pressures.

Если паттерн пропущен, функциональные и пространственные решения строятся вокруг статического перечня помещений; maintenance, accessibility, emergency и transition modes обнаруживаются после детализации.

Что это даёт: architecture questions и system concept получают scenario-based basis без превращения scenario prose в requirement authority или evidence.

Не этот паттерн, если текущий вопрос только о stakeholder value/ethics (`D.*`), system composition (`BDPF.5`) или work plan эксплуатации (`A.15.2`).

### BDPF.4:2 - Problem

«Назначение объекта» слишком грубо для архитектурных решений. Один и тот же asset может иметь normal, peak, degraded, emergency, cleaning, repair, loading, commissioning и evacuation modes. Эти scenarios конфликтуют по пространству, flows, controls и access.

### BDPF.4:3 - Forces

| Force | Tension |
| --- | --- |
| Broad purpose vs actionable scenario | «Больница» или «склад» не задают behavior. |
| Primary use vs lifecycle support | Maintenance and emergency scenarios редки, но architecture-bearing. |
| User voice vs source evidence | Interview/brief useful, but scenario claim still needs source and uncertainty. |
| Scenario richness vs analysis burden | Нужен smallest set that changes structures. |
| Conflicts vs consensus language | Good concept exposes incompatible needs rather than smoothing them. |

### BDPF.4:4 - Solution

Создайте `UseConceptRecord@Project` из scenario rows:

```text
UseScenarioClaimRow@Project:
  scenarioId:
  sourceSignalUseRefs:
  participatingRoleOrGroupRefs:
  modeAndTrigger:
  preconditions:
  intendedOutcome:
  mainInteractionOrFlow:
  exceptionalOrFailureConditions:
  timeAndCapacityEnvelope:
  affectedBuiltAssetScope:
  impliedFunctionOrCapabilityRefs:
  affectedStructureKindRefs:
  affectedArchitectureCharacteristicRefs:
  uncertaintyAndEvidenceNeed:
  nonAdmissibleUse:

UseConceptRecord@Project:
  useConceptId:
  builtAssetFrameRef:
  declaredUse:
  primaryScenarioRefs:
  maintenanceScenarioRefs:
  emergencyScenarioRefs:
  logisticsAndAccessScenarioRefs:
  transitionOrDegradedModeScenarioRefs:
  scenarioConflictRows:
  valueAndLossClaimRefs:
  downstreamSystemConceptRef:
  sourceReturnCondition:
```

Рабочий ход:

1. Выберите scenarios, которые materially change structure or decision.
2. Для каждого укажите source refs, roles/groups, trigger/mode, outcome, flow и failure condition.
3. Отделите intended scenario от observed operation; observed claims требуют evidence/currentness.
4. Найдите conflicts: peak vs maintenance, accessibility vs security, evacuation vs smoke control, public flow vs logistics, operation vs construction phasing.
5. Переведите conflicts в function/capability/constraint/characteristic implications, не в готовые design moves.
6. Передайте downstream в `BDPF.5/6`; источник и uncertainty остаются recoverable.

### BDPF.4:5 - Archetypal Grounding

**Логистический терминал.** Static brief перечисляет зоны. Use concept добавляет:

- normal inbound/outbound vehicle and goods flows;
- peak seasonal mode;
- hazardous/temperature-controlled handling;
- maintenance of dock equipment without stopping all operations;
- fire/evacuation mode;
- pedestrian staff access crossing vehicle flows.

Conflict row показывает, что увеличение throughput через общий yard ухудшает safety and emergency access. Это создаёт spatial/flow/control architecture questions; не выбирает конкретную схему yard.

**Near miss:** «Пользователь должен иметь удобный доступ» — слишком broad; требуется роль, mode, path, envelope и measure/evidence need.

### BDPF.4:6 - Bias-Annotation

Паттерн блокирует room-list bias, happy-path bias и persona-as-evidence. Он не требует exhaustive сценариев: only architecture-bearing scenarios and conflicts.

### BDPF.4:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF4-1` | Built asset frame and declared use are named. |
| `CC-BDPF4-2` | Scenario rows include role/group, mode/trigger, outcome and flow/interaction. |
| `CC-BDPF4-3` | Source refs and uncertainty are visible. |
| `CC-BDPF4-4` | Maintenance/emergency/logistics/degraded cases considered or justified absent. |
| `CC-BDPF4-5` | Conflicts produce downstream pressure, not hidden compromise. |
| `CC-BDPF4-6` | Scenario claims do not become proof of demand, work plan or PAD. |

### BDPF.4:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Назначение = use concept | No role/mode/flow. | Add scenario rows. |
| Только normal operation | Rare but architecture-bearing modes lost. | Add maintenance/emergency/degraded probes. |
| Scenario = solution sketch | Premature structure choice. | Keep implications and send to `BDPF.5/6`. |
| Persona without source | Narrative confidence replaces basis. | Pin source/uncertainty. |
| Exhaustive scenario theatre | Cost without decision effect. | Keep scenarios that change structure/characteristics. |

### BDPF.4:9 - Consequences

System concept becomes grounded in use rather than room lists. Cost is explicit conflict management and uncertainty.

### BDPF.4:10 - Rationale

Use scenarios are not a new Core ontology in BDPF; they are local description records that organize project claims and route them to functions, structures and evidence owners.

### BDPF.4:11 - SoTA-Echoing

- Systems-engineering stakeholder-needs/use-case practice contributes role, mode and outcome structure; BDPF rejects scenario document as requirement authority by itself.
- FPF `C.2.1`, `A.6.F`, `C.30.TFS-REL`, `C.28` and `D.*` keep description, function, flow, causal and value claims separate.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-15288-2023`, `SRC-BDPF-42010-2022`; exact scenario/viewpoint applicability returns to `Source Use And Refresh Map`.

### BDPF.4:12 - Relations

Uses `BDPF.1`, `BDPF.3`, `C.2.1`, `A.6.F`, `C.30.TFS-REL`, `C.25`, `D.1-D.5`, `BDPF.5`, `BDPF.6`, `BDPF.6B` and `BDPF.8`. Reopen when user roles, operating modes, capacity envelope, source basis or scenario conflict changes.

### BDPF.4:End

---

## BDPF.5 — Концепция системы

> **Type:** DPF pattern body
>
> **Primary EntityOfConcern:** the functional, flow, interface, control, mode and bearer logic of one physical system named by value. The default subject is the built asset; a site is admitted only when the current claim actually treats it as a natural/technical/operating system.

### BDPF.5:1 - Problem frame

Используйте паттерн, когда scenarios уже названы, но проект всё ещё организован как независимые discipline outputs и не показывает, **как выбранный physical system работает как целое**: обычно это ОКС; площадка допускается только при явном natural/technical/operating-system reading.

Первый полезный ход: сформировать thin system concept with boundary, functions, flows, interfaces, operating modes, critical dependencies, unknown/candidate bearer structures and downstream architecture questions.

Если паттерн пропущен, междисциплинарные assumptions расходятся: помещение существует без service flows, equipment without maintenance access, control mode without sensor/actuator structure, construction sequence without temporary stability structure.

Что это даёт: architecture questions возникают из system logic, а не из границ разделов ПД.

Не этот паттерн, если требуется grounded selected architecture (`BDPF.6`/`C.30`), detailed discipline method или actual operating dynamics.

### BDPF.5:2 - Problem

Сценарии показывают desired use, но не определяют способ системного обеспечения. Нужна промежуточная description, которая связывает functions/capabilities with physical and informational bearers, interfaces, flows, controls and modes while keeping unknowns visible.

### BDPF.5:3 - Forces

| Force | Tension |
| --- | --- |
| Functional intent vs physical bearer | Function wording легко остаётся без allocating structure. |
| Discipline decomposition vs cross-boundary flows | Разделы удобны для работы, но energy, people, material, information and control cross them. |
| Conceptual simplicity vs critical dependencies | Concept должен быть thin, но не скрывать single points, interfaces and temporary modes. |
| Future design vs actual structure | Concept proposes logic; it does not claim actual realization. |
| Function vs work | Что объект должен обеспечивать не равно plan/work по его созданию. |

### BDPF.5:4 - Solution

Создайте:

```text
SystemConceptRecord@Project:
  systemConceptId:
  subjectPosture: builtAsset | site
  builtAssetFrameRef?:
  siteFrameRef?:
  useConceptRef:
  boundedContextRef:
  systemBoundaryRef:
  subsystemAndExternalSystemRefs:
  functionRows:
    - functionOrCapabilityClaimRef:
      sourceScenarioRefs:
      candidateBearerStructureRefs:
      modeRefs:
      successAndFailureCondition:
  flowRows:
    - flowKind:
      sourceAndSinkRefs:
      pathOrTransformationStructureRef:
      boundaryCrossingRefs:
  interfaceRows:
  controlAndOperatingModeRows:
  criticalDependencyRows:
  constraintsAndArchitectureCharacteristicRefs:
  unknownOrCandidateStructureRefs:
  unresolvedSystemQuestions:
  downstreamArchitectureQuestionRefs:
  sourceReturnCondition:
  nonAdmissibleUse:
```

Применяйте в пять passes:

1. **Subject/boundary pass:** выберите один physical system; built asset подтверждается через `BDPF.1`, site — через `BDPF.1A` только при material system reading. Placement relation не становится system subject.
2. **Function-to-bearer pass:** для architecture-bearing functions назовите candidate physical/information/control bearers; если bearer unknown — сохраните unknown.
3. **Flow/interface pass:** покажите boundary crossings and interfaces, not only components.
4. **Mode/dependency pass:** укажите normal, degraded, emergency, maintenance and construction-relevant modes; выделите critical dependencies.
5. **Question pass:** преобразуйте unresolved relations into `BDPF.6` architecture questions. Не принимайте selected structures внутри system concept.

Типовые области — prompts, не completeness checklist:

| Domain lens | Что восстанавливать |
| --- | --- |
| Functional-planning | Functions, zones, adjacency and use interactions. |
| Material-spatial | Location, geometry, environmental and site relations. |
| Load-bearing | Load paths, stability, foundation and temporary-state relations. |
| Engineering systems | Supply, distribution, conversion, redundancy, maintenance and control. |
| Technology/process | Material/product/patient/vehicle flows and process equipment. |
| Operation/control | Sensing, actuation, dispatch, modes and failure response. |
| Safety/emergency | Hazard scenarios, compartmentation, evacuation, smoke/fire/control relations. |
| Construction realization | Temporary structures, phasing, logistics and retained operation. |

### BDPF.5:5 - Archetypal Grounding

**Помещение с изоляционным режимом в больнице.** Room list says «изолятор». System concept relates:

- patient/staff/material flows;
- pressure-control function and ventilation bearer;
- airlock/spatial bearer;
- monitoring/control interface;
- cleaning and filter maintenance mode;
- emergency power and degraded-mode behavior;
- interfaces with fire compartment and medical gases.

The concept reveals architecture questions about spatial, engineering, control and maintenance structures. It does not select equipment or prove infection control performance.

### BDPF.5:6 - Bias-Annotation

Паттерн блокирует component-list bias, function-without-bearer и discipline-boundary blindness. Он также блокирует «концепция как красиво оформленное решение»: selected structures remain downstream.

### BDPF.5:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF5-1` | System concept names one physical system subject and the matching built-asset or site frame; the two frames are not merged. |
| `CC-BDPF5-2` | A site-system reading is used only when the site itself has material functions, transformations, modes or interfaces. |
| `CC-BDPF5-3` | Architecture-bearing functions have bearer candidates or an explicit unknown. |
| `CC-BDPF5-4` | Flows, boundary crossings and material interfaces are visible. |
| `CC-BDPF5-5` | Operating, degraded and maintenance modes describe the system, not planned work occurrences. |
| `CC-BDPF5-6` | Critical dependencies and unresolved questions are explicit. |
| `CC-BDPF5-7` | Concept routes to architecture questions rather than claiming PAD, placement selection or suitability. |
### BDPF.5:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Список подсистем | Relations and flows absent. | Add function-bearer-flow-interface rows. |
| Функция без bearer | Unrealizable intent. | Name candidate bearer or unknown. |
| Только steady-state mode | Failure/maintenance structures hidden. | Add materially different modes. |
| Diagram = system concept | Carrier overread. | Keep description relation and source return. |
| Concept = selected design | Candidate/decision collapse. | Route to `BDPF.6/6A/7`. |

### BDPF.5:9 - Consequences

The project gains one cross-disciplinary logic and a controlled list of architecture questions. Cost is making assumptions and dependencies explicit before detailed drawings.

### BDPF.5:10 - Rationale

Built assets are physical systems whose functions, flows, interfaces and controls are distributed across discipline views. A system concept is a useful DPF-local description only when it preserves bearer and boundary discipline.

### BDPF.5:11 - SoTA-Echoing

- Systems-engineering functional and interface analysis is adapted to built assets; process lists and diagrams are not treated as performed work or actual structure.
- FPF `A.6.F`, `A.3.4`, `C.30.TFS-REL`, `C.30.ASV` supply function/transformation-flow/structural-view boundaries.
- `ISO/IEC/IEEE 42010:2022` supports concern/viewpoint discipline; viewpoint is not a structure or decision.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-15288-2023`, `SRC-BDPF-42010-2022`; exact system/architecture applicability returns to `Source Use And Refresh Map`.

### BDPF.5:12 - Relations

Uses `BDPF.1`, `BDPF.1A`, `BDPF.4`, `A.6.F`, `A.3.4`, `C.30.TFS-REL`, `C.30.ASV`, `C.25`, `BDPF.6`, `BDPF.6B` and `BDPF.8`. Reopen when use scenarios, boundary, functions, modes, interfaces, dependencies or source basis changes.

### BDPF.5:End

---

## BDPF.6 — Архитектурный вопрос ОКС, площадки или placement relation

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** one architecture-bearing question about structures/relations of exactly one subject: physical built asset, physical site or placement relation; `BuiltAssetArchitectureQuestionCard@Project` is the first project record.

### BDPF.6:1 - Problem frame

Используйте этот паттерн, когда спор, неопределённость или defect затрагивает несколько проектных решений и должен быть восстановлен как вопрос о structure физического ОКС, structure физической площадки либо structure отношения размещения между ними, а не как вопрос о том, какой раздел ПД исправить.

**Первый полезный ход:** выберите один `subjectPosture`, укажите соответствующий physical ref (`describedBuiltAssetRef`, `describedSiteRef` или `describedPlacementRelationRef`), bounded context, concern, exact project `ArchitectureStructureKindRef` values or honest unresolved structure-family cues, current structural unknown and one next architecture move.

**Что ломается без паттерна:** команда спорит о планировке, трассе, несущей схеме, площадочной сети, доступе, рельефе или BIM-clash на уровне готовых ответов. Связь со scenario/system pressure и architecture characteristics скрывается; локальная правка переносит residual в другую подсистему, участок, режим или lifecycle slice.

**Что это даёт:** спор становится reviewable architecture question с одним primary physical subject, для которого можно синтезировать coherent configurations, назначить criteria/eval и вернуть каждый stronger claim прямому FPF-owner.

**Не этот паттерн**, если текущи candidate synthesis, comparison, PAD, evidence, architecture-description adequacy или defect repair. Используйте соответственно `BDPF.6A`, `BDPF.6C`, `BDPF.7`, `BDPF.8`, `BDPF.10` или `BDPF.11`.
### BDPF.6:2 - Problem

В строительном проектировании архитектурно значимые вопросы часто маскируются формами документов и дисциплинарными границами:

- «как пройти экспертизу по разделу ПБ» вместо вопроса о spatial, flow and control structures;
- «куда поставить венткамеру» вместо вопроса о spatial allocation, service flows, maintenance access and interfaces;
- «устранить clash» вместо вопроса о несовместимых selected, expected and represented structures;
- «утвердить планировку» без восстановления use scenarios, load-bearing, engineering and evacuation consequences.

Архитектурный вопрос появляется там, где выбранная structure relation меняет несколько последующих решений, распределяет constraints между подсистемами, связывает permanent and temporary states или создаёт длительный trade-off. Он не определяется масштабом картинки, названием стадии или должностью автора.

### BDPF.6:3 - Forces

| Force | Tension |
| --- | --- |
| Дисциплинарная локальность | Участник видит собственный section/carrier, тогда как structure пересекает несколько descriptions and roles. |
| Срочность ответа | Проекту нужен ход сейчас, но раннее solution wording закрывает ещё не исследованную plurality. |
| Полнота vs usefulness | Полный каталог structures перегружает работу; слишком узкий вопрос переносит residual. |
| Viewpoint vs structure | Concern/viewpoint выбирает чтение, но не становится structure kind or selected structure. |
| Carrier pressure | Clash, схема, письмо или замечание выглядят как сам вопрос, хотя являются source/publication carriers. |
| Локальное улучшение vs межуровневый ущерб | Улучшение одной подсистемы может ухудшить operation, safety, construction or adjacent scope. |
| Local cue vs durable kind | Удобная подсказка ускоряет discovery, но capitalization can accidentally mint a shadow ontology. |

### BDPF.6:4 - Solution

Создайте одну карточку вопроса до синтеза конфигураций.

```text
BuiltAssetArchitectureQuestionCard@Project:
  questionId:
  subjectPosture:
    builtAsset | site | builtAssetSitePlacementRelation
  describedBuiltAssetRef?:
  describedSiteRef?:
  describedPlacementRelationRef?:
  boundedContextRef:
  designConcernWindowRef:
  sourceSignalUseRefs:
  useConceptRefs:
  systemConceptRefs:
  architectureConcern:
  affectedStakeholderOrRoleRefs:
  viewpointRefs:
  problemPressureSummary:
  smallestUsefulArchitectureStructureKindRefs:
  unresolvedStructureFamilyCueRows?:
    - cueLabel:
      proposedStructureKindReading:
      resolutionOwnerRef:
      stopOrReturnCondition:
  currentSelectedStructureRefs?:
  currentExpectedStructureRefs?:
  currentRepresentedStructureRefs?:
  unknownStructureRefs:
  candidateStructureCueRefs?:
  affectedArchitectureCharacteristicRefs:
  crossScopeResidualRefs?:
  affectedInterfaceOrFlowRefs?:
  affectedDecisionRefs?:
  architectureQuestion:
  firstArchitectureMove:
    inspect | split | relate | synthesizeCandidates | evaluate | returnToSource | assignGoverningPattern | stop
  nonArchitectureClaimExits:
  nonAdmissibleUse:
  sourceReturnCondition:
  reopenCondition:
```

Примените шесть passes:

1. **Subject/context pass.** Выберите один primary subject; для physical refs используйте `BDPF.1/1A`. File/model/section не используется как subject ref.
2. **Pressure pass.** Свяжите вопрос с source-signal uses, use/system concepts and concern. Отделите observed defect from hypothesized cause.
3. **Structure-owner pass.** Запишите exact project/Core-governed `ArchitectureStructureKindRef` values. Когда точный kind ещё не восстановлен, оставьте lower-case cue row with `resolutionOwnerRef`; не маскируйте cue capitalization as ontology.
4. **State pass.** Разделите current selected, expected, represented, candidate-cue and unknown structures. Совпадающее название не доказывает correspondence.
5. **Residual pass.** Проверьте, не переносит ли локальный ответ residual в другой scope, lifecycle slice, temporary/permanent state or role use. При cross-scope conflict откройте `C.30.ILC`.
6. **Move pass.** Назовите один first architecture move and stop. Не записывайте preferred configuration в карточку вопроса, если plurality ещё должна быть синтезирована.

#### Structure-family cues — discovery aids, not kinds

Следующие labels допустимы только как lower-case discovery cues. Они **не являются** `U.Kind`, не являются готовыми `ArchitectureStructureKindRef` и не создают новую built-asset ontology. Перед reliance каждый live cue разрешается через `C.30`/`C.30.ASV` в exact project structure-kind ref либо остаётся unresolved с owner and stop condition.

| Cue label | Что он помогает спросить | Заблокированный overread |
| --- | --- | --- |
| `functionalPlanningCue` | functions, zones, adjacency, accessibility and scenario allocation | раздел АР или room schedule = structure kind |
| `materialSpatialCue` | siting, geometry, distances, environmental and spatial relations | drawing/plan = physical structure |
| `loadBearingCue` | load paths, stability, foundations, deformation and temporary states | calculation model = actual load-bearing structure |
| `engineeringSystemsCue` | generation, conversion, distribution, redundancy, isolation and maintenance | ИОС carrier = engineering system |
| `transformationFlowCue` | people, vehicle, material, energy, air, water, information or construction flows | arrow diagram = performed transformation/work |
| `controlOperationCue` | sensing, actuation, dispatch, modes and failure response | automation description = safety proof |
| `moduleInterfaceCue` | subsystem boundaries, penetrations, connection grammar, replacement and isolation | any contact = module interface |
| `constructionTemporaryCue` | phasing, temporary supports, logistics, retained operation and transition states | ПОС/WorkPlan = architecture or performed work |
| `informationDescriptionCue` | reference designation, federation, correspondence and information-container relations | information structure = physical ОКС |
| `scaleEvolutionCue` | expansion, reconstruction, adaptability, future-state compatibility and scale windows | future promise = current capability/evidence |

Список — не completeness checklist. Если next move зависит от одной spatial relation, не добавляйте десять cues ради видимости системности.

### BDPF.6:5 - Archetypal Grounding

**Размещение вертикального коммуникационного ядра многофункционального здания.** Исходная формулировка: «согласовать ядро до выпуска АР и КР».

Карточка восстанавливает:

- `subjectPosture`: `builtAsset`;
- `describedBuiltAssetRef`: секция здания в current planning/fire/structural context;
- pressure: routes for users and mobility-impaired occupants, evacuation, lateral stiffness, engineering risers, net-to-gross and construction sequencing;
- unresolved cue set: `functionalPlanningCue`, `materialSpatialCue`, `loadBearingCue`, `transformationFlowCue`, `moduleInterfaceCue`;
- resolution owner: architecture lead resolves those cues into project-pinned structure-kind refs before candidate evaluation;
- question: какая configuration ядра удерживает scenario, evacuation, structural and service-distribution characteristics при допустимых потерях area and flexibility;
- first move: `synthesizeCandidates`.

Карточка не выбирает central or offset core и не доказывает fire safety. Она создаёт reviewable input to `BDPF.6A`.
### BDPF.6:6 - Bias-Annotation

Паттерн блокирует drawing-first bias, discipline-silo bias, solution-in-question bias and classifier-completion bias. Дополнительно он блокирует shadow-kind bias: useful local cue is not promoted into durable ontology by capitalization or table position.

### BDPF.6:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF6-1` | One `subjectPosture` and exactly one matching physical subject ref are named with bounded context and concern window. |
| `CC-BDPF6-2` | Built asset, site and placement relation are not merged or substituted by a carrier, parcel identifier or project section. |
| `CC-BDPF6-3` | Pressure is linked to source/use/system refs, not only to carrier or opinion. |
| `CC-BDPF6-4` | The smallest exact `ArchitectureStructureKindRef` set is named; unresolved cues have owner and stop/return condition. |
| `CC-BDPF6-5` | Selected, expected, represented, candidate-cue and unknown structure states are not collapsed. |
| `CC-BDPF6-6` | Concern/viewpoint is separate from structure, decision and evidence. |
| `CC-BDPF6-7` | Cross-scope, site-interface and temporary/permanent-state residuals were checked or marked not material with basis. |
| `CC-BDPF6-8` | One admissible `firstArchitectureMove` and its stop are named. |
| `CC-BDPF6-9` | Non-architecture claims have direct-owner exits. |
| `CC-BDPF6-10` | No local cue label is relied on as a durable kind by spelling alone. |
### BDPF.6:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Вопрос как выбор готового ответа | Candidate plurality hidden. | Rewrite through unknown structure, characteristic pressure and constraint. |
| Вопрос как замечание | Carrier/source wording replaces problem pressure. | Extract signal and affected relation through `BDPF.3/3A`. |
| Полный классификатор в каждой карточке | Formal completeness hides live structure. | Keep the smallest exact refs; retain unresolved cues only with owner. |
| CamelCase cue as ontology | Local prompt silently becomes a project/Core kind. | Use lower-case cue, resolve through `C.30/C.30.ASV`, or keep unresolved. |
| Viewpoint как решение | Concern obtains decision authority. | Use viewpoint only for selection/reading. |
| Clash как архитектурная причина | Represented intersection is treated as root cause. | Check selected/expected/represented correspondence first. |
| Локальная оптимизация | Residual moves to another scope. | Open `C.30.ILC` and return to candidate synthesis. |

### BDPF.6:9 - Consequences

Преимущество — architecture disputes become comparable and routable before detail design. Цена — participants must temporarily keep the question open, recover exact structure kinds and resist convenient shadow ontology.

### BDPF.6:10 - Rationale

`C.30` owns grounded architecture through selected structures of a holon in context; `C.30.ASV` owns structure-kind/view adequacy. BDPF contributes built-asset recognition prompts, not a parallel architecture ontology.

### BDPF.6:11 - SoTA-Echoing

- Architecture-description practice contributes concern/viewpoint discipline; BDPF preserves viewpoint ≠ structure.
- Systems-engineering and built-asset coordination contribute early cross-discipline question framing; candidate, eval, evidence and decision claims retain separate owners.
- Clash detection and model federation remain description/probe inputs, not automatic architecture diagnosis.
- Package source-use refs: `SRC-BDPF-42010-2022`, `SRC-BDPF-19650-1-2018`, `SRC-BDPF-FPF-JUL2026`; exact applicability returns to `Source Use And Refresh Map`.

### BDPF.6:12 - Relations

Uses `BDPF.1`, `BDPF.1A`, `BDPF.3A`, `BDPF.4`, `BDPF.5`, `A.22`, `C.30`, `C.30.ASV`, `C.30.ILC`, `C.30.TFS-REL`, `C.33`, `C.34`, `BDPF.6A`, `BDPF.6B`, `BDPF.10` and `BDPF.11`. Reopen when holon boundary, source pressure, scenario/system concept, structure-kind resolution, characteristic, residual or represented structure changes. Open `Built-Asset Design Precision Restoration And Owner Map` when words such as «архитектура», «система», «интерфейс», «уровень» or «решение» hide the current kind.

### BDPF.6:End

---

## BDPF.6A — Кандидатные архитектурные конфигурации

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** a plurality of coherent candidate architecture configurations answering one bounded architecture question; `CandidateArchitecturePalette@Project` is the set-use record under `C.32`.

### BDPF.6A:1 - Problem frame

Используйте этот паттерн, когда architecture question уже reviewable, но проект преждевременно сходится к одному ответу либо хранит альтернативы только в памяти участников.

**Первый полезный ход:** создайте plurality из структурно различимых конфигураций или запишите проверяемый `stopReasonIfNoPlurality`.

**Что ломается без паттерна:** исходный или привычный вариант получает статус «базового» без конкуренции; варианты отличаются только оформлением; assumptions и losses появляются после выбора.

**Что это даёт:** candidate space становится inspectable до comparison, а отсутствие plurality перестаёт маскироваться под уверенность.

**Не этот паттерн**, если текущая задача — собрать source signals, определить question, оценить candidates, выбрать retained set или принять PAD. Используйте `BDPF.3A`, `BDPF.6`, `BDPF.6B`, `BDPF.6C` или `BDPF.7`.

### BDPF.6A:2 - Problem

В проектировании ОКС один early scheme быстро обрастает расчётами, BIM-детализацией и организационной инерцией. После этого comparison становится сравнением разработанного варианта с карикатурными альтернативами. Candidate plurality должна появиться до того, как глубина carrier-а или sunk cost будет принята за качество структуры.

Plurality не означает обязательные три варианта для каждого узла. Она означает, что либо существует хотя бы два структурно различимых admissible candidates, либо проект честно показывает, почему пространство пока нельзя расширить: source gap, hard constraint, missing capability, unresolved upstream decision или disproportional search cost.

### BDPF.6A:3 - Forces

| Force | Tension |
| --- | --- |
| Скорость vs exploration health | Раннее сужение ускоряет выпуск, но скрывает better structures и stepping stones. |
| Сопоставимость vs различимость | Варианты должны отвечать одному вопросу, но быть структурно отличимыми. |
| Реализм vs детализация | Candidate должен быть достаточно конкретным для eval, но не обязан быть детально спроектирован. |
| Hard constraints vs design freedom | Ограничения исключают варианты, но не должны скрыто предопределять один ответ. |
| Search cost vs reversal cost | Дополнительный вариант стоит времени; ошибочный PAD может стоить значительно больше. |
| Human/AI generation vs admission | Generated scheme может расширить palette, но не становится candidate architecture без source and structure recovery. |

### BDPF.6A:4 - Solution

```text
CandidateArchitecturePalette@Project:
  paletteId:
  describedHolonRef:
  boundedContextRef:
  architectureQuestionRef:
  decisionBoundaryRef:
  sourceSignalUseRefs:
  candidateArchitectureStructureKindRefs:
  architectureCharacteristicRefs:
  currentOrBaselineConfigurationRef?:
  generationMethodOrWorkRefs?:
  candidateConfigurations:
    - candidateId:
      configurationSummary:
      changeFromCurrentOrBaseline:
      selectedStructureHypotheses:
      expectedStructureHypotheses:
      configurationCoherenceRows:
      scenarioCoverageRefs:
      operatingAndFailureModeCoverageRefs:
      temporaryPermanentStateRelation:
      governingConstraintRefs:
      sourceAssumptions:
      internalIncompatibilitiesOrUnknowns:
      expectedGains:
      expectedLosses:
      interfaceAndCrossScopeEffects:
      evidenceNeeded:
      sourceReturnCondition:
      nonAdmissibleReading:
  rejectedBeforeEvaluationRows?:
    - candidateOrFamilyRef:
      rejectionBasis:
      governingOwnerRef:
      reopenCondition:
  searchCoverageNote:
  retainedExplorationRefs?:
  stopReasonIfNoPlurality?:
  nextComparisonOrProbeOwner:
  nonAdmissibleUse:
  reopenCondition:
```

#### Candidate construction rules

1. **Same question and decision boundary.** Все candidates отвечают одной `architectureQuestionRef` в одном bounded context and one decision boundary. Если question or boundary changed, create a branch or a new palette.
2. **Baseline is a candidate, not truth.** Existing/current/base configuration may remain in the set, but it gets the same source, loss and coherence inspection as every other candidate.
3. **Structural difference.** Отличие должно затрагивать хотя бы одну selected-structure hypothesis or material interface/flow/control relation. Разные brands at the same structure are not automatically different architecture configurations.
4. **Coherent whole.** Candidate is a compatible configuration, not a collage of the locally best features. `configurationCoherenceRows` show how selected hypotheses, interfaces, modes and temporary/permanent states can coexist; unresolved internal conflicts stay visible.
5. **Scenario and state coverage.** Each candidate states which use, maintenance, degraded, emergency and construction-relevant scenarios it covers and how temporary states lead to the expected permanent structure.
6. **Comparable maturity.** Do not compare a fully developed candidate with a one-line strawman. Use one minimum description envelope and name justified exceptions.
7. **Assumption visibility.** Each configuration shows source assumptions, unknowns, expected gains/losses, cross-scope effects and evidence needed.
8. **No winner.** Palette does not rank, retain or choose. Preferred wording exits to comparison, local choice or PAD owner.
9. **Honest stop.** If plurality is not currently lawful or affordable, fill `stopReasonIfNoPlurality`, next probe owner and reopen condition. «Заказчик уже решил» is a bounded authority/commitment input, not structural proof that alternatives do not exist.

Для AI/algorithm-generated carriers сначала примените `C.35`: восстановите source, generated carrier, described structure, constraints, losses и admission responsibility.

### BDPF.6A:5 - Archetypal Grounding

**Система холодоснабжения комплекса.** Вопрос: какая distribution/plant configuration обеспечивает peak and part-load operation, phased commissioning, maintenance access and acceptable resilience.

Palette содержит:

- централизованную plant + ring distribution;
- две зональные plants + separated loops;
- hybrid plant with local high-criticality modules.

Для каждого варианта зафиксированы spatial occupation, hydraulic/control structure, redundancy assumptions, maintenance isolation, energy/equipment implications, construction phasing и evidence needed. Palette не объявляет hybrid «оптимальным» и не сворачивает reliability, capex, energy and maintainability в один score.

### BDPF.6A:6 - Bias-Annotation

Паттерн блокирует first-scheme anchoring, pseudo-alternative и detail-as-quality bias. Generated plurality не считается exploration health, если варианты не прошли source/structure admission.

### BDPF.6A:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF6A-1` | Palette привязана к одному architecture question и context. |
| `CC-BDPF6A-2` | Есть ≥2 structurally distinct candidates либо explicit stop reason. |
| `CC-BDPF6A-3` | Candidates are structurally distinct, internally coherent and described on a comparable minimum envelope. |
| `CC-BDPF6A-4` | Baseline status, source assumptions, scenario/state coverage, expected gains/losses and evidence needs are visible. |
| `CC-BDPF6A-5` | Candidate, selected set и PAD не смешаны. |
| `CC-BDPF6A-6` | Pre-evaluation rejection имеет owner, basis and reopen. |
| `CC-BDPF6A-7` | AI/generated candidates прошли `C.35` admission boundary. |
| `CC-BDPF6A-8` | Next comparison/probe owner named. |

### BDPF.6A:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Один «рабочий» вариант и два номинальных | Comparison biased by maturity. | Equalize minimum description envelope. |
| Варианты по дисциплинарным файлам | Structure difference hidden. | Compare selected-structure hypotheses. |
| Random option generation | Candidates not tied to pressure/constraints. | Bind each to question, source uses, decision boundary and characteristics. |
| Best-of-each feature collage | One candidate contains mutually incompatible local improvements. | Add coherence rows, interface checks and temporary/permanent-state relation. |
| Favorite candidate label | Selection leaks into synthesis. | Remove ranking language; route to `BDPF.6C`. |
| «Альтернатив нет» без причины | Search prematurely closed. | Publish stop reason, probe and reopen. |
| Generated diagram accepted as candidate | Carrier fluency substitutes for architecture. | Apply `C.35`, `C.33` and source return. |

### BDPF.6A:9 - Consequences

Преимущество — comparison получает честный source set, а ошибки раннего закрытия становятся видимыми. Цена — ограниченная дополнительная работа по вариантам и необходимость управлять unknowns без ложной точности.

### BDPF.6A:10 - Rationale

`C.32` делает candidate architecture synthesis отдельным от comparison and decision. BDPF уточняет minimum candidate envelope для built assets, где depth of drawings and calculations иначе создаёт сильный anchoring effect.

### BDPF.6A:11 - SoTA-Echoing

- Set-based design and option preservation support late responsible commitment; BDPF keeps the set typed and source-bounded rather than importing a universal process.
- Generative design/BIM/optimization tools are candidate-production methods, not architecture admission or selection owners.
- Open-ended search principles support plurality and retained exploration, while project constraints and evidence boundaries remain explicit.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-42010-2022`; generated carriers return through `C.35` and the source map.

### BDPF.6A:12 - Relations

Uses `BDPF.6`, `C.32`, `C.18`, `C.19`, `C.35`, `C.33`, `C.34`, `BDPF.6B`, `BDPF.6C`, `C.11` and `BDPF.7`. Reopen when question, candidate membership, source assumptions, hard constraints, search method, characteristics, evidence needs or stop reason changes.

### BDPF.6A:End

---

## BDPF.6B — Architecture characteristics, criteria и eval

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** the evaluation basis for one candidate set: bearer-bound characteristics of a built-asset structure, site/site structure or placement relation, lawful scales, criterion roles and eval programs; the project records remain distinct uses of `C.32.ACS` and `C.32.ACE`.

### BDPF.6B:1 - Problem frame

Используйте этот паттерн, когда candidates существуют, но слова «лучше», «эффективнее», «надёжнее», «безопаснее», «гибче» или «проще» не имеют bearer, scale, evidence rule, missingness policy и protected trade-offs.

**Первый полезный ход:** превратите broad quality wording в 3–7 decision-relevant criteria rows, сохранив guardrails и counter-characteristics вне скрытой scalarization.

**Что ломается без паттерна:** score подменяет architecture characteristic; один measurable proxy вытесняет source value; ordinal ratings усредняются; unknown превращается в zero; eval result выбирает решение.

**Что это даёт:** candidates становятся сопоставимыми на declared coordinates, а сильные и слабые claims маршрутизируются к measurement/evidence/assurance owners.

**Не этот паттерн**, если live question is candidate generation (`BDPF.6A`), comparison or pool treatment (`BDPF.6C`), local choice/PAD (`C.11`/`BDPF.7`) or evidence/assurance sufficiency (`BDPF.8`/`B.3`). Criteria and eval prepare those uses; they do not perform them.

### BDPF.6B:2 - Problem

Built-asset decisions имеют многомерные последствия: use performance, spatial efficiency, structural behavior, fire and life safety, constructability, maintainability, energy/resource demand, adaptability, cost/time and information reliability. Невозможно ответственно сравнить их одной общей оценкой без явной policy and scale lawfulness.

Характеристика принадлежит bearer structure в context. «Надёжность проекта» без bearer and failure mode — не criteria row. Расчёт или simulation являются methods/work/evidence/eval, но не самой characteristic. Нормативное выполнение может быть eligibility constraint, а не improvement objective.

### BDPF.6B:3 - Forces

| Force | Tension |
| --- | --- |
| Multidimensional value | Решение должно удерживать несколько несводимых characteristics. |
| Measurement availability | Измеримый proxy доступен раньше, чем direct evidence нужного property. |
| Precision vs uncertainty | Точные numbers привлекательны, но assumptions and model error могут доминировать. |
| Optimization vs guardrails | Улучшение одной coordinate может нарушить hard constraint или protected characteristic. |
| Expert judgement vs reproducibility | Judgement необходимо, но basis, scale and role должны быть recoverable. |
| Comparability vs local context | Одинаковое слово может иметь разные bearer/scale/use в разных проектах. |

### BDPF.6B:4 - Solution

```text
BuiltAssetArchitectureCriteriaSet@Project:
  criteriaSetId:
  describedBuiltAssetRef?:
  describedSiteRef?:
  describedPlacementRelationRef?:
  boundedContextRef:
  architectureQuestionRef:
  candidatePaletteRef:
  declaredComparisonUse:
  eligibilityConstraintRefs:
  criteriaRows:
    - criterionId:
      architectureCharacteristicRef:
      bearerPosture: builtAssetStructure | site | siteStructure | builtAssetSitePlacementRelation
      bearerRef:
      concernOrUseRef:
      scenarioAndLifecycleWindowRefs:
      criterionRole: eligibility | dominance | tieBreaker | telemetry | decisionOnlyPreference
      scaleRef:
      valueMeaningRefs:
      polarityOrPreferenceRelation:
      measureOrEvalMethodRef:
      evidenceRule:
      missingnessPolicy:
      aggregationAdmissibility:
      admissibleUse:
      protectedCounterCharacteristicRefs:
      proxyRisk:
      thresholdOrGuardrailRef?:
      sourceReturnCondition:
  nonAggregableTradeoffs:
  prohibitedScalarizationOrAggregation:
  reopenCondition:

BuiltAssetArchitectureEvalProgram@Project:
  evalProgramId:
  criteriaSetRef:
  candidateConfigurationRefs:
  evaluationMethodRefs:
  plannedMeasurementOrAnalysisWorkRefs:
  inputSourceAndModelRefs:
  parityOrScenarioFrameRefs:
  uncertaintyTreatment:
  missingDataTreatment:
  evalResultRefs:
  evidenceTraceRefs:
  limitations:
  admissibleUse:
  nonAdmissibleUse:
  refreshCondition:
```

#### Criteria construction moves

1. **Recover one bearer.** Укажите exact built-asset structure, physical site, site structure or placement relation. Structure, constraint/admissibility and characteristic reading не смешиваются.
2. **Assign a criterion role.** Use `eligibility`, `dominance`, `tieBreaker`, `telemetry` or `decisionOnlyPreference`. A value moves between roles only through an explicit project policy; telemetry and stakeholder preference do not enter dominance by formatting.
3. **Declare scale and value meanings.** Pin ordinal/cardinal status, unit, polarity, level meanings, scenario/lifecycle window and lawful comparison. Do not average ordinal labels without an admitted aggregation mechanism.
4. **Protect counter-characteristics.** Для каждой optimized coordinate спросите: «что может ухудшиться, если это значение улучшится?».
5. **Handle missingness.** Unknown не равен neutral/zero. Используйте explicit `unknown | notApplicable | insufficientEvidence | notMeasured` или project-pinned equivalents.
6. **Keep eval downstream-bounded.** Eval result является input в comparison/decision; он не выбирает candidate и не доказывает claims вне scope.

#### Site/placement starter heads — prompts, not a universal rating

Каждый material head раскладывается по правилу «один bearer + одна characteristic + одна scale». Итог — vector/profile with unknowns, не score «качества участка».

| Starter head | Typical bearer |
| --- | --- |
| `spatialPlacementCapacity` | site + placement relation |
| `terrainAndEarthworkEnvelope` | site/terrain structure |
| `groundSupportEnvelope` | ground structure |
| `waterRegimeEnvelope` | site/water structure |
| `naturalHazardAndClimateExposure` | site + placement relation |
| `externalUtilityInterfaceEnvelope` | site-to-supplying-system relations |
| `transportAndLogisticsAccessEnvelope` | site + external transport relations |
| `existingOccupationAndRelocationBurden` | site structures |
| `environmentalAndNeighbourhoodCompatibility` | placement relation + adjacent holons |
| `constructionRealizationCapacity` | site in planned construction design window |
| `operationalExternalInterfaceFitness` | placement relation as design input |
| `developmentReserveAndChangeCapacity` | site + placement relation |

These heads do not introduce a ConOps carrier, post-design loop or universal site ontology.

#### Minimal built-asset criteria row example

```text
criterionId: maintainableIsolation
architectureCharacteristicRef: ability to isolate one chilled-water branch for planned maintenance
bearerPosture: builtAssetStructure
bearerRef: distribution and valve/control structure of candidate configuration
scenarioAndLifecycleWindowRefs: planned branch isolation during normal operation and one degraded mode
criterionRole: dominance
scaleRef: ordinal 0..4
valueMeaningRefs: level definitions tied to isolation scope, access and retained service
polarityOrPreferenceRelation: higher is preferred subject to spatial and cost guardrails
measureOrEvalMethodRef: scenario walkthrough + model inspection + maintenance-role review
missingnessPolicy: insufficient interface information -> unknown, candidate not compared on this coordinate
aggregationAdmissibility: no cross-characteristic aggregation in this use
protectedCounterCharacteristicRefs: pressure loss; plantroom space; control complexity
proxyRisk: valve count is not maintainability
admissibleUse: comparison of listed candidates under named maintenance scenarios
```

#### Built-asset starter prompts — narrow by decision family

These are source-backed prompts for the first criteria discussion, not a universal rating model. Every row must be narrowed to exact bearer, scale, evidence and criterion role.

| Decision family | Candidate bearer | Typical characteristic pressures | Protected counter-characteristic or loss |
| --- | --- | --- | --- |
| Vertical core and circulation | spatial, flow, load-bearing, service-interface structures | route separation, evacuation capacity, structural stiffness, net usable area, maintenance access | flexibility, future change, construction phasing, interface complexity |
| Foundation/basement concept | foundation, retaining, waterproofing and load-path structures | settlement/deformation, groundwater control, excavation stability, construction access | embodied resources, neighbour impact, inspectability, uncertainty exposure |
| Central plant and distribution | generation, distribution, control and isolation structures | part-load behavior, resilience, branch isolation, route length, phased commissioning | spatial occupation, control complexity, pressure/energy loss, replacement access |
| Façade/enclosure system | envelope, support, joint and access structures | thermal/solar response, movement accommodation, replacement access, water/air control | fire interfaces, embodied impact, logistics, visual intent |
| Reconstruction/phasing | existing/expected/temporary structures and retained-operation relations | continuity of use, temporary stability, access, isolation, reversibility | duration, temporary works burden, operational risk, irreversible intervention |

### BDPF.6B:5 - Archetypal Grounding

**Фасадная система для высотного здания.** Broad labels «энергоэффективность», «ремонтопригодность», «стоимость» распакованы в rows:

- thermal/solar performance for declared orientation and climate scenarios;
- replacement access and unit isolation for maintenance role;
- fire compartment/interface behavior with direct normative/evidence exits;
- structural movement accommodation;
- embodied/operational resource claims only where source and method are pinned;
- capital cost estimate as separate uncertain estimate, not global value score.

Eval returns a vector/profile with unknowns and limitations. It does not issue a PAD or compliance verdict.

### BDPF.6B:6 - Bias-Annotation

Паттерн блокирует metric reification, Goodhart drift, false precision и expert-score authority bias. It also blocks normative-minimum optimization: satisfying a requirement is not automatically «best».

### BDPF.6B:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF6B-1` | Every criterion names one exact bearer posture/ref, characteristic, context and use. |
| `CC-BDPF6B-2` | Site, site structure and placement relation are not collapsed into the built asset or into each other. |
| `CC-BDPF6B-3` | Criterion role, scenario/lifecycle window, scale, value meanings, polarity and comparability are declared. |
| `CC-BDPF6B-4` | Evidence qualification, observation window, uncertainty and missingness policy are explicit. |
| `CC-BDPF6B-5` | Eligibility, dominance, tie-breaker, telemetry and decision-only preference roles are not hidden or moved without policy. |
| `CC-BDPF6B-6` | At least one protected counter-characteristic or explicit `none found` review exists. |
| `CC-BDPF6B-7` | Proxy risk and assumptions are visible. |
| `CC-BDPF6B-8` | Eval program cites candidate editions, methods/work, inputs, scenario/parity frame, uncertainty and limitations. |
| `CC-BDPF6B-9` | No site profile or eval result is treated as suitability, comparison, selected set, PAD or gate decision by form alone. |
### BDPF.6B:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| One weighted total by default | Trade-offs and scale laws hidden. | Publish vector/profile; use lawful comparison owner. |
| Expert score without level meanings | Authority replaces reproducibility. | Define ordinal levels, basis, role and evidence. |
| Unknown = zero | Missing evidence penalizes or rewards silently. | Use explicit missingness state. |
| Proxy as property | Easy metric becomes target. | Name bearer and proxy risk; protect counter-characteristic. |
| Requirement as quality maximum | Eligibility and optimization collapse. | Separate hard constraints from preference coordinates. |
| Simulation as truth | Model assumptions and validity window hidden. | Record model/source/method/uncertainty and evidence boundary. |

### BDPF.6B:9 - Consequences

Преимущество — comparison and PAD can expose real trade-offs instead of hiding them in adjectives or one score. Цена — проект must define value meanings and evidence policy before asking tools or experts to rank options.

### BDPF.6B:10 - Rationale

FPF requires characteristics, scales, evidence and aggregation lawfulness before evaluative use. BDPF specializes this discipline for built-asset architecture without creating a universal building-rating system.

### BDPF.6B:11 - SoTA-Echoing

- Multi-criteria decision practice is used only after criteria kinds and scales are explicit; BDPF rejects hidden totalization.
- Performance-based design, simulation and scenario evaluation provide evidence/eval methods, not automatic decision or assurance.
- Built-asset information models may support measurements and queries, but model completeness/currentness and represented-structure loss remain separate.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-42010-2022`, `SRC-BDPF-19650-1-2018`; exact method and evidence applicability returns to the source map.

### BDPF.6B:12 - Relations

Uses `A.17`, `A.18`, `A.19.ECS`, `C.16`, `C.16.P`, `C.16.Q`, `C.25`, `C.32.ACS`, `C.32.ACE`, `A.10`, `B.3`, `BDPF.1A`, `BDPF.6A`, `BDPF.6C`, `BDPF.8` and `BDPF.12`. Reopen when bearer, scale, criteria role, threshold, evidence basis, missingness policy, candidate set, scenario/parity frame or proxy risk changes.

### BDPF.6B:End

---

## BDPF.6C — Comparison и retained set

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** the comparison-and-retention relations over one current candidate set; `ComparisonBasis@Project` and `RetainedArchitectureSetPublication@Project` are separate results with different owners and effects.

### BDPF.6C:1 - Problem frame

Используйте этот паттерн, когда candidates and eval inputs существуют, но проект смешивает comparison, narrowing, selected-set publication, local choice и PAD.

**Первый полезный ход:** опубликуйте comparison basis и set-valued outcome: retained, rejected, hold/abstain or probe-needed — без скрытой scalarization и без decision commitment.

**Что ломается без паттерна:** таблица comparison автоматически выдаёт winner; incomplete evidence маскируется rank; retained alternative теряется; reader не может восстановить, почему candidate исключён.

**Что это даёт:** decision owner получает честный набор admissible/retained candidates, protected trade-offs и missing evidence.

**Не этот паттерн**, если candidate or criteria/eval basis is not yet stable (`BDPF.6A/6B`), if a local choice is already the exact current result (`C.11`), or if project architecture commitment is current (`BDPF.7`). Do not keep a choice or PAD inside comparison merely to avoid naming authority and accepted losses.

### BDPF.6C:2 - Problem

Comparison answers «как candidates соотносятся под объявленным basis». Selection or shortlist publication answers «какие candidates удерживаются для следующего use». Local choice answers «какой option выбран в данной decision frame». PAD commits selected structures and losses. Эти relations связаны, но не взаимозаменяемы.

В built-asset work comparison часто оформлено в spreadsheet with weights. Видимый итоговый number создаёт ложную тотальность, даже если criteria incomparable, data missing or one hard constraint failed. Паттерн делает outcome set-valued by default and forces explicit abstention when comparison basis insufficient.

### BDPF.6C:3 - Forces

| Force | Tension |
| --- | --- |
| Need to narrow | Project cannot carry every candidate indefinitely, but premature winner hides uncertainty. |
| Incomparable trade-offs | Some candidates are non-dominated under different concerns. |
| Missing evidence | Ranking pressure encourages imputation or silent assumptions. |
| Stakeholder preferences | Legitimate preferences exist, but must be distinguished from characteristic evidence. |
| Decision pressure | Management wants a recommendation, while current result may only justify retained set or probe. |
| Traceability | Exclusion reasons must survive later reopen and source change. |

### BDPF.6C:4 - Solution

```text
ComparisonBasis@Project:
  comparisonId:
  describedHolonRef:
  boundedContextRef:
  architectureQuestionRef:
  sourceCandidatePaletteRef:
  candidateConfigurationRefs:
  criteriaSetRefs:
  evalResultRefs:
  eligibilityRuleRefs:
  comparatorOrComparisonMethodRef:
  dominanceOrPreferenceRelation:
  protectedTradeOffs:
  unacceptableLosses:
  stakeholderPreferenceRefs?:
  decisionOnlyPreferenceRefs?:
  missingEvidence:
  uncertaintyAndMissingnessTreatment:
  nonComparableRows?:
  admissibleUse:
  nonAdmissibleUse:
  reopenCondition:

RetainedArchitectureSetPublication@Project:
  retainedSetId:
  comparisonBasisRef:
  retainedCandidateRefs:
  conditionallyRetainedCandidateRefs?:
  rejectedCandidateRows:
    - candidateRef:
      rejectionBasis:
      evidenceOrConstraintRef:
      reopenCondition:
  holdOrAbstainReason?:
  probeNeededRefs?:
  orderIncluded: true | false
  rankBasisRef?:
  nextDecisionOwner:
  publicationUse:
  nonAdmissibleUse:
  refreshCondition:
```

#### Relation-owner routing

| Current relation | Direct owner | BDPF.6C result boundary |
| --- | --- | --- |
| compare candidate profiles | `A.19.CPM` | comparison relation or non-comparability finding |
| govern a still-live candidate pool | `C.19` | `widen`, `keep frontier`, `narrow` or `sunset` pool-policy result |
| publish a selected/retained set | `A.19.SelectorMechanism` and `G.5` | set-valued publication with basis pins |
| make one local choose/reject/probe/reroute result | `C.11` | `ChoiceResult`; not a PAD by itself |
| commit selected architecture structures and losses | `C.32.PAD` / `BDPF.7` | `ArchitectureDecisionRelation@Project` |

#### Comparison discipline

1. Check candidate and criteria editions/currentness.
2. Apply eligibility constraints before preference comparison; keep the reason and source.
3. Compare only on lawful scales or an explicit comparator. Do not totalize merely because a spreadsheet can.
4. Publish non-dominated/retained candidates and protected trade-offs. Order only if order materially belongs to the receiving use and its basis is declared.
5. Use `hold` or `abstain` when missing evidence can change membership or decision. Do not create rank from unknowns.
6. Keep stakeholder preference as a named decision input, not as retroactive evidence that a characteristic is better.
7. Send retained set to `BDPF.7` only when project architecture decision is current. `RetainedArchitectureSetPublication` itself carries no commitment.

### BDPF.6C:5 - Archetypal Grounding

**Три конфигурации эвакуационно-коммуникационного ядра.** Candidate A has best net area but weak phasing and maintenance access; B improves redundancy and construction sequencing with area loss; C preserves future expansion but has unresolved smoke-control evidence.

Comparison:

- rejects no candidate by arbitrary total score;
- retains A and B as currently admissible non-dominated options;
- conditionally retains C pending a named analysis;
- states that fire-code compliance claims return to direct normative/evidence owner;
- sends a retained set, not a winner, to PAD decision work.

### BDPF.6C:6 - Bias-Annotation

Паттерн блокирует single-winner bias, rank-by-format, hidden-weighting and missing-data laundering. It also blocks preference-as-evidence and «retained = decided».

### BDPF.6C:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF6C-1` | Comparison cites one source palette and current candidate refs. |
| `CC-BDPF6C-2` | Eligibility, comparison and preference relations are distinguishable. |
| `CC-BDPF6C-3` | Comparator, scales and uncertainty treatment are declared. |
| `CC-BDPF6C-4` | Protected trade-offs and unacceptable losses are visible. |
| `CC-BDPF6C-5` | Missing evidence can yield hold/abstain rather than fabricated rank. |
| `CC-BDPF6C-6` | Rejection rows have basis and reopen condition. |
| `CC-BDPF6C-7` | Ordering exists only when explicitly supported and useful. |
| `CC-BDPF6C-8` | Retained set is not represented as PAD, approval or work authorization. |

### BDPF.6C:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Weighted average by default | Incommensurable trade-offs hidden. | Use profiles, dominance or declared comparator. |
| Rank despite missing evidence | False precision. | Hold/abstain and open a probe. |
| Management preference embedded in weights | Preference appears objective. | Publish preference ref separately. |
| Rejected candidate disappears | Later source change cannot reopen it. | Keep rejection basis and reopen condition. |
| Shortlist called decision | Commitment and losses absent. | Route to `BDPF.7`. |
| Comparison report as evidence of all claims | Eval scope widened. | Use claim-specific `BDPF.8` traces. |

### BDPF.6C:9 - Consequences

Преимущество — project decision starts from an inspectable option set and visible uncertainty. Цена — sometimes the honest result is hold/abstain rather than a satisfying winner.

### BDPF.6C:10 - Rationale

FPF separates comparison, selector outcome, local choice and architecture decision. BDPF preserves this split because building decisions combine non-comparable concerns and long-lived consequences.

### BDPF.6C:11 - SoTA-Echoing

- Multi-criteria and set-based design practices support transparent trade-offs, but BDPF requires typed scales and explicit non-use.
- Pareto/front language is admitted only under declared dominance; a visually attractive scatter plot is not automatically a front.
- Decision conferences and stakeholder workshops may produce preference or work evidence, but their minutes/carriers do not become the comparison relation by attendance alone.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-42030-2019`; exact source applicability returns to the source map.

### BDPF.6C:12 - Relations

Uses `A.19.CPM`, `A.19.SelectorMechanism`, `G.5`, `C.11`, `BDPF.6A`, `BDPF.6B`, `A.10`, `B.3`, `BDPF.7` and `BDPF.12`. Reopen when candidate membership, criteria/eval edition, comparator, preference frame, missing evidence, constraint, protected trade-off or receiving decision use changes.

### BDPF.6C:End

---

## BDPF.7 — Проектное архитектурное решение ОКС

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** `ArchitectureDecisionRelation@Project` governed by `C.32.PAD`, with built-asset use fields and checks.

### BDPF.7:1 - Problem frame

Используйте этот паттерн, когда candidate synthesis and comparison дают достаточный basis для текущего commitment по архитектуре ОКС: какие структуры проект будет развивать, какие trade-offs и losses принимает и что должно заставить решение reopen or supersede.

**Первый полезный ход:** создайте `ArchitectureDecisionRelation@Project` до ADR-like записи, подписи, статуса, выпуска ПД или передачи downstream work.

**Что ломается без паттерна:** выбранный вариант существует только как схема, протокол, отметка «согласовано» или инерция детализации. Невозможно восстановить decision question, candidate basis, accepted losses, method implications, role/authority act и reopen condition.

**Что это даёт:** архитектурное решение становится отдельной relation, способной направлять design-development method, evidence, projection and review без подмены carriers.

**Не этот паттерн**, если ещё нет candidate basis or comparison sufficient for decision; вернитесь к `BDPF.6A–6C`. Для publication используйте `BDPF.7A/7B`, для evidence — `BDPF.8`, для adequacy evaluation — `BDPF.12`, для gate/readiness — `BDPF.9`.

### BDPF.7:2 - Problem

Проектное архитектурное решение находится между exploration and downstream work. Оно должно локально закрыть вопрос, но не притворяться вечной истиной. В строительном контуре решение затрагивает физические structures, future expected structure, междисциплинарные interfaces, способ дальнейшего проектирования, evidence obligations, concern coverage и projection into multiple carriers.

Типовые подмены:

- selected candidate or shortlist называется решением без commitment;
- ADR/card или протокол становится decision by publication;
- подпись/approval-looking status принимается за инженерную достаточность;
- расчёт становится decision reason for every concern;
- «выполнить согласно модели» скрывает architect/developer split и lost structure;
- accepted loss не записывается и позже выглядит как дефект исполнения.

### BDPF.7:3 - Forces

| Force | Tension |
| --- | --- |
| Local closure vs open world | Проекту нужен current direction, но sources/evidence/context могут измениться. |
| Structure vs method | Решение commits target structures и может задавать method-use для дальнейшей разработки. |
| Authority vs adequacy | Организационный act может институтировать решение, но не доказывает его engineering adequacy. |
| Cross-disciplinary effects | Один PAD влияет на several descriptions, interfaces, roles and work packages. |
| Detail allocation | Архитектор удерживает selected structures, downstream designers refine lower-level structures. |
| Trade-off honesty | Decision must accept losses explicitly rather than hide them in rationale prose. |
| Publication pressure | Участникам нужен readable record, но carrier не должен создавать новую семантику. |

### BDPF.7:4 - Solution

Используйте Core relation and fill built-asset-relevant slots.

```text
ArchitectureDecisionRelation@Project:
  decisionId:
  decisionSubjectRef:
  describedHolonRef:
  boundedContextRef:
  lifecycleSlice:
  decisionQuestion:
  candidateBasisRefs:
  comparisonOrSelectionRefs:
  selectedArchitectureOptionRefs:
  selectedStructureEffects:
    - structureKindRef:
      selectedStructureRef:
      decisionEffect:
      governingPatternRef:
  expectedStructureRefs:
  architectureCharacteristicTradeoffs:
    - architectureCharacteristicRef:
      expectedGain:
      acceptedLoss:
      criteriaOrEvalRef:
      protectedCounterCharacteristicRef?:
  rejectedAlternativeRows:
    - alternativeRef:
      rejectionBasis:
      reopenCondition:
  retainedAlternativeRefs?:
  sourceBasisRefs:
    sourceSignalRefs:
    useConceptRefs:
    systemConceptRefs:
    architectureQuestionRefs:
  rationaleRefs:
  evidenceOrAssuranceExitRefs:
  stakeholderConcernCoverageRows:
    - concernRef:
      affectedRoleOrGroupRef:
      viewpointRef?:
      affectedStructureRefs:
      evidenceOrAssuranceRefs?:
      acceptedLossOrResidualRef?:
      unresolvedConcernOrReturnCondition?:
  normativeProtectionRiskOrComplianceExitRows?:
    - claimOrConcernRef:
      sourceOrRuleRef:
      affectedStructureRefs:
      directOwnerRef:
      evidenceOrAssuranceRef?:
      unresolvedGap?:
      nonAdmissibleUse:
  methodUseInstructions:
    - methodDescriptionOrPatternRef:
      expectedStructureEffect:
      responsibleRoleAssignmentRef:
      workBoundaryRef:
      readinessExitRef?:
  architectDownstreamRefinementSplit:
    architectureOwnedStructureRefs:
    downstreamRefinementRefs:
    invariantOrConstraintRefs:
    sourceReturnCondition:
  roleAssignmentRefs:
    decisionFormulationRoleAssignmentRef:
    reviewRoleAssignmentRefs:
    decisionHolderRoleAssignmentRef:
    publicationRoleAssignmentRef?:
  decisionInstitutingSpeechActRef?:
  architectureDescriptionRefs?:
  documentationProjectionRefs?:
  residualRisksOrOpenIssues:
  status:
  validFromOrDecisionWindow:
  reopenConditions:
  sourceReturnCondition:
  supersedesDecisionRefs?:
```

#### Decision construction moves

1. **Recover the live decision.** Назовите bounded question and decision subject. Не используйте broad «утвердить концепцию» без конкретного architecture commitment.
2. **Bind candidate basis.** Cite palette, comparison/selection and retained set. Если candidate plurality была intentionally absent, cite the admitted stop reason and decision risk.
3. **State structure effects.** Для каждой affected structure укажите `structureKindRef`, selected structure and decision effect. Не ограничивайтесь названием варианта.
4. **Publish trade-offs and losses.** Record expected gains, accepted losses, protected characteristics and residuals. Loss может быть admissible under current use, но не должен исчезать.
5. **Separate source, evidence and authority.** Source basis explains problem/input; evidence supports named claims; role assignments and optional speech act institute or publish the decision. Ни один из этих owners не заменяет другой.
6. **Dock method and work.** State how downstream roles should preserve or refine structures, but do not turn PAD into universal WorkPlan. Work entry/readiness remains with `A.15.5`/`A.21` and `BDPF.9`.
7. **Set reopen and supersession.** Tie reopen to source change, evidence failure, characteristic shift, candidate discovery, interface mismatch, represented/actual structure feedback or changed use.

#### Minimum decision test

Другой practitioner, не участвовавший в meeting, должен суметь ответить:

- какой вопрос закрыт и для какого scope/window;
- какие candidates and basis были доступны;
- какие selected and expected structures committed;
- какие losses приняты и какие alternatives retained/rejected;
- что должны делать downstream roles и где их freedom starts;
- какие claims требуют evidence/assurance/source return;
- кто holds/institutes the decision and when it reopens.

Если ответ восстанавливается только из устного контекста или reading of drawings, PAD ниже пола.

### BDPF.7:5 - Archetypal Grounding

**Решение по конфигурации вертикального ядра.** После candidate/eval work retained are central compact core and split-offset core. PAD selects split-offset configuration for the current tower section.

Decision relation records:

- selected spatial, evacuation-flow, load-bearing and service-riser structures;
- expected gain in phasing and tenant flexibility;
- accepted loss in net area and interface complexity;
- retained central-core alternative if tenant/use assumptions change;
- evidence exits for evacuation, smoke control, structural behavior and accessibility;
- architect-owned invariants: core zones, protected routes, main load path and interface corridors;
- downstream refinement: shaft subdivision, equipment selection, reinforcement detailing within invariants;
- reopen: changed occupancy mix, fire strategy, structural grid, utility demand or failed evidence.

Meeting minutes and approved drawing may publish this relation but do not substitute for it.

### BDPF.7:6 - Bias-Annotation

Паттерн блокирует record-as-decision, authority-as-truth, decision-by-detail and irreversible-closure bias. It also blocks architect-overreach: PAD governs declared structures, not every downstream design move.

### BDPF.7:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF7-1` | Decision question, subject, holon, context and window are explicit. |
| `CC-BDPF7-2` | Candidate/comparison/selection basis is cited or honest absence/stop reason is visible. |
| `CC-BDPF7-3` | Selected and expected structures are named by structure kind. |
| `CC-BDPF7-4` | Gains, accepted losses, residuals and protected trade-offs are explicit. |
| `CC-BDPF7-5` | Rejected and retained alternatives remain recoverable where material. |
| `CC-BDPF7-6` | Source, evidence, assurance, role authority and instituting act are not collapsed. |
| `CC-BDPF7-7` | Method-use instructions and architect/downstream refinement split are bounded. |
| `CC-BDPF7-8` | Concern coverage includes unresolved returns, not only positive coverage. |
| `CC-BDPF7-9` | Projection refs do not become the decision. |
| `CC-BDPF7-10` | Reopen, source-return and supersession conditions are explicit. |

### BDPF.7:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| «Принят вариант 2» | Structure effects and losses absent. | Fill selected-structure and trade-off rows. |
| Protocol/signature = PAD | Publication or speech act replaces relation. | Separate PAD, instituting act and carrier. |
| Decision from one calculation | Claim-specific evidence widened. | Add evidence exits by claim and concern. |
| Alternatives deleted | Reopen becomes expensive and biased. | Keep retained/rejected basis. |
| PAD as detailed instruction | Architect/developer split lost. | State invariants and refinement freedom. |
| No valid window/reopen | Local closure becomes permanent fiction. | Add source/evidence/use/structure triggers. |
| Stakeholder row as voting score | Concern reading becomes selection mechanism. | Keep concern coverage separate from comparison/decision rule. |

### BDPF.7:9 - Consequences

Преимущество — решение становится durable, reviewable and actionable without merging with evidence or documents. Цена — explicit accepted losses and authority boundaries may expose disagreement that informal approval previously hid.

### BDPF.7:10 - Rationale

`C.32.PAD` governs the project architecture decision after candidate synthesis. BDPF only adds built-asset prompts for concerns, physical/represented structures, project roles and discipline projections; it does not redefine PAD.

### BDPF.7:11 - SoTA-Echoing

- Architecture decision records are useful publication forms, but current architecture practice increasingly distinguishes the decision relation from its record and views.
- Systems lifecycle and decision-management practice support traceability from stakeholder/use pressure to architecture decisions and verification/validation exits.
- Built-asset multidisciplinary coordination requires concern and interface coverage, while statutory approval and compliance claims remain with direct owners.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-42010-2022`, `SRC-BDPF-42030-2019`; exact applicability returns to `Source Use And Refresh Map`.

### BDPF.7:12 - Relations

Uses `C.32.PAD`, `BDPF.6A`, `BDPF.6B`, `BDPF.6C`, `A.2.1`, `A.2.9`, `A.10`, `B.3`, `C.30`, `C.30.AD`, `C.32.ADR`, `C.32.ADA`, `BDPF.7A`, `BDPF.7B`, `BDPF.8`, `BDPF.9`, `BDPF.10`, `BDPF.11` and `BDPF.12`. Reopen when decision question, candidate basis, source, role authority, evidence, use, structure, characteristic pressure, actual/represented correspondence or valid window changes.

### BDPF.7:End

---

## BDPF.7A — ADR / record-проекция проектного решения

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** `ArchitectureDecisionRecordProjection@Project`, governed by `C.32.ADR`, `E.17` and publication discipline.

### BDPF.7A:1 - Problem frame

Используйте этот паттерн, когда PAD существует и должен стать читаемым для конкретных roles, reviews or downstream uses в ADR-like card, journal, explanatory note or another publication carrier.

**Первый полезный ход:** определите reader use and section functions, then project existing PAD without adding new decision semantics.

**Что ломается без паттерна:** удобная запись начинает считаться решением; разные ADR versions расходятся; rationale prose скрывает source/evidence boundary; publication creates commitment that PAD never contained.

**Что это даёт:** PAD получает stable reader-facing projection with source pins, losses, consequences and supersession while remaining recoverable as the governing relation.

**Не этот паттерн**, если PAD ещё не существует (`BDPF.7`), if the live question is claim evidence (`BDPF.8`), decision adequacy (`BDPF.12`), a gate/authority act (`BDPF.9`/`A.2.9`) or representation of selected structures in PD/BIM (`BDPF.10`).

### BDPF.7A:2 - Problem

Один PAD нужен разным readers: architect, discipline designer, reviewer, client, BIM coordinator, construction planner. Publication can select and coarsen different content, but it must not change the decision or widen reliance. A short card may omit evidence detail, yet it must preserve return paths.

The common failure is «document-shaped authority»: a polished template, signature block or repository location gives the record more status than its source relation warrants.

### BDPF.7A:3 - Forces

| Force | Tension |
| --- | --- |
| Readability vs fidelity | Readers need compact record, but decision structure and losses must remain recoverable. |
| One PAD vs multiple readers | Different views are useful, but semantic divergence is dangerous. |
| Stable citation vs evolution | Record needs ID/edition and supersession without freezing the decision forever. |
| Rationale vs evidence | Explanatory prose helps, but must not become proof. |
| Publication vs authority | Publication makes content available; it does not institute decision unless a separate speech act does. |

### BDPF.7A:4 - Solution

```text
ArchitectureDecisionRecordProjection@Project:
  recordId:
  recordEdition:
  architectureDecisionRef:
  decisionEditionOrWindowRef:
  readerRoleOrUseRefs:
  sectionFunctions:
  contextSummary:
  decisionQuestionSummary:
  decisionOutcome:
  selectedStructureRefs:
  expectedStructureRefs:
  rationaleSummary:
  candidateAndComparisonReturnRefs:
  acceptedLossesAndTradeoffs:
  consequences:
  methodUseInstructions:
  architectDownstreamRefinementBoundary:
  evidenceOrAssuranceReturnRefs:
  sourceReturnRefs:
  residualsAndOpenIssues:
  reopenOrSupersessionCondition:
  publicationCarrierRefs:
  accessOrConfidentialityBoundary?:
  nonAdmissibleUse:
```

Apply these rules:

1. `architectureDecisionRef` is mandatory. If no PAD exists, stop and use `BDPF.7`.
2. Every section serves a named reader use; do not copy a universal template merely because fields exist.
3. Preserve selected structures, accepted losses, method boundary and reopen condition even in a short projection.
4. Use source/evidence links instead of compressing strong claims into rationale.
5. Keep `recordEdition` and decision window/edition separate. Updating wording does not silently update PAD.
6. When publication is redacted or coarsened, state omitted structure and source-return boundary.
7. A signature or publication event is recorded through its direct owner; do not let the record body imply an unrecorded approval or authorization.

### BDPF.7A:5 - Archetypal Grounding

A two-page ADR projection for the vertical-core PAD gives a developer team:

- current decision and selected structure map;
- reasons and accepted area/interface losses;
- architect-owned invariants and downstream refinement freedom;
- evidence return links rather than embedded full calculations;
- exact reopen triggers;
- source PAD ref and record edition.

A management summary may omit shaft-level detail, but its coarsening note points back to the PAD and architecture description. Neither publication is a second decision.

### BDPF.7A:6 - Bias-Annotation

Паттерн блокирует template authority, record/PAD collapse and latest-file bias. It also blocks rationale-as-evidence and signature-as-adequacy.

### BDPF.7A:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF7A-1` | Projection points to one existing PAD and its decision window. |
| `CC-BDPF7A-2` | Reader role/use and section functions are explicit. |
| `CC-BDPF7A-3` | Selected structures, losses, consequences and reopen survive the projection. |
| `CC-BDPF7A-4` | Source/evidence/assurance return refs remain visible. |
| `CC-BDPF7A-5` | Record and PAD editions are distinguishable. |
| `CC-BDPF7A-6` | Coarsening/redaction loss is declared where material. |
| `CC-BDPF7A-7` | Publication/signature does not create unrecorded decision authority. |

### BDPF.7A:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| ADR written before PAD | Record becomes hidden decision. | Recover `BDPF.7` first. |
| Universal form filled mechanically | Reader use lost in boilerplate. | Select section functions by use. |
| «See model» as decision outcome | Source structure not recoverable. | State selected structures and exact model return. |
| Evidence summarized as certainty | Scope and limitations lost. | Link to `BDPF.8` traces. |
| Edited ADR silently changes decision | Version drift. | Issue PAD repair/supersession first. |
| Signed card = approved engineering | Speech act and adequacy collapse. | Separate act, PAD and `BDPF.12` evaluation. |

### BDPF.7A:9 - Consequences

Преимущество — one decision can support multiple readers without semantic forks. Цена — carrier authors must manage editions, source pins and deliberate omissions.

### BDPF.7A:10 - Rationale

FPF treats ADR as architecture-decision publication projection, not the decision itself. BDPF keeps that discipline in built-asset projects where decisions are otherwise dispersed across notes, drawings and models.

### BDPF.7A:11 - SoTA-Echoing

- ADR practice contributes concise context/decision/consequence sections; BDPF adds explicit source, structure, loss and reader-use boundaries.
- Multi-view architecture description allows several projections over one governed relation, provided correspondence and source return remain visible.
- Information-management workflows may control document status, but status does not transfer engineering truth or decision adequacy.
- Package source-use refs: `SRC-BDPF-42010-2022`, `SRC-BDPF-42030-2019`, `SRC-BDPF-19650-1-2018`; exact publication/source use returns to the source map.

### BDPF.7A:12 - Relations

Uses `C.32.ADR`, `E.17`, `E.17.AUD`, `E.24.PUB`, `BDPF.7`, `BDPF.8`, `BDPF.10` and `BDPF.12`. Reopen when PAD, reader use, selected structure, loss, record edition, source/evidence currentness, redaction or publication boundary changes.

### BDPF.7A:End

---

## BDPF.7B — Минимальный пакет чтения решения

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** `MinimalDecisionUsePackage@Project`, a navigation/publication package over already governed values.

### BDPF.7B:1 - Problem frame

Используйте этот паттерн, когда участнику нужен компактный и role-specific entry into an existing decision: PAD, ADR projection, key evidence, represented structures, responsibilities and current readiness — без чтения всего repository.

**Первый полезный ход:** соберите только необходимые refs and publication faces для одного `readerUse`.

**Что ломается без паттерна:** «пакет решения» превращается в новый root object, копирует данные, скрывает edition mismatch или воспринимается как доказательство/approval because it looks complete.

**Что это даёт:** one reader gets a compact, edition-pinned navigation surface while every decision, evidence, representation, role and readiness claim remains with its direct owner.

**Не этот паттерн**, если нужно создать or repair PAD (`BDPF.7`), author a semantic ADR projection (`BDPF.7A`), establish evidence sufficiency (`BDPF.8`) or decide boundary readiness/gate (`BDPF.9`).

### BDPF.7B:2 - Problem

Project repositories distribute decision content across cards, drawings, models, calculations, comments and gate records. Reader needs navigation, but a convenience package can create a dangerous illusion: «всё нужное находится здесь, значит всё доказано и актуально».

The package must therefore expose exact owners and missingness rather than absorb their claims.

### BDPF.7B:3 - Forces

| Force | Tension |
| --- | --- |
| Fast access vs source fidelity | Reader needs compact surface, but source values remain distributed. |
| Role specificity vs duplication | Different readers need different slices; copied content drifts. |
| Completeness appearance vs honest missingness | A polished package can hide absent evidence or outdated projection. |
| Access control vs reviewability | Sensitive content may be restricted while decision use still needs bounded access. |

### BDPF.7B:4 - Solution

```text
MinimalDecisionUsePackage@Project:
  packageId:
  packageEdition:
  architectureDecisionRelationRef:
  architectureDecisionRecordProjectionRef?:
  architectureDescriptionOrViewRefs:
  evidenceTraceRefs:
  documentationProjectionRefs:
  roleAssignmentRefs:
  readinessOrGateRefs?:
  residualRiskOrComplianceExitRefs?:
  readerRoleRef:
  readerUse:
  requiredQuestionSet:
  sourceAndEditionPins:
  missingOrRestrictedRefs:
  accessBoundary?:
  admissibleUse:
  nonAdmissibleUse:
  refreshCondition:
```

Rules:

1. Package contains refs/publication faces, not copied substitute values by default.
2. Every included item answers one required reader question. Remove decorative completeness.
3. Pin editions/currentness and show missing/restricted refs.
4. Keep PAD, evidence, gate, projection, role assignment and risk/compliance exits visibly distinct.
5. Refresh package when any source ref changes; do not rely on folder name or «latest» convention.
6. Package may help work only within its `admissibleUse`; it is not work authorization, proof, approval or compliance certificate.

### BDPF.7B:5 - Archetypal Grounding

**Package for MEP designer downstream of vertical-core PAD:** PAD ref, one role-specific ADR face, protected shaft/interface structural view, relevant evidence traces, current projection refs, role assignment and work-entry readiness ref. It excludes full commercial rationale and unrelated alternatives, but shows their source-return locations. A missing smoke-control evidence trace is visible as a blocker, not hidden by package completeness.

### BDPF.7B:6 - Bias-Annotation

Паттерн блокирует package-as-root, latest-folder reliance and completeness-by-appearance. It also blocks link-count as quality.

### BDPF.7B:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF7B-1` | One existing PAD is the package anchor. |
| `CC-BDPF7B-2` | Reader role/use and required questions are named. |
| `CC-BDPF7B-3` | Included refs have current edition/source pins. |
| `CC-BDPF7B-4` | Missing/restricted content is visible. |
| `CC-BDPF7B-5` | Decision, evidence, gate, projection and authority remain separate. |
| `CC-BDPF7B-6` | Refresh condition covers every included source. |
| `CC-BDPF7B-7` | Non-admissible reliance is explicit. |

### BDPF.7B:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Copy everything into one PDF | Source drift and claim collapse. | Use governed refs and selected publication faces. |
| Package called «approved solution» | Appearance grants authority. | State direct PAD/speech-act/gate refs. |
| No reader use | Bloated generic package. | Define required question set. |
| Broken/missing links hidden | False readiness. | Publish missing/restricted rows. |
| Folder `Final` as edition | Currentness not recoverable. | Pin exact edition/currentness. |

### BDPF.7B:9 - Consequences

Преимущество — participants enter a complex decision cheaply without semantic duplication. Цена — package stewardship and link/currentness checks become explicit work.

### BDPF.7B:10 - Rationale

A navigation/publication package is useful when it preserves direct-owner boundaries. It is intentionally not a new decision, evidence bundle kind or gate.

### BDPF.7B:11 - SoTA-Echoing

- Common data environments and information containers improve access and status control, but BDPF keeps container status separate from engineering claims.
- Role-specific information delivery supports small use packages; information need should be reader/use driven rather than document-volume driven.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-19650-1-2018`, `SRC-BDPF-19650-2-2018`, `SRC-BDPF-7817-1-2024`; exact reader/use and status applicability returns to `Source Use And Refresh Map`.

### BDPF.7B:12 - Relations

Uses `BDPF.7`, `BDPF.7A`, `BDPF.8`, `BDPF.9`, `BDPF.10`, `E.17`, `E.24.PUB`, `A.10`, `A.15.4` and `G.11`. Reopen when reader use, PAD, source edition, evidence, projection, role assignment, gate, access or currentness changes.

### BDPF.7B:End

---

## BDPF.8 — Claim-specific evidence проектного решения

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** `DesignClaimEvidenceTrace@Project`, a DPF-local evidence-use trace governed by `A.10`; assurance remains with `B.3`.

### BDPF.8:1 - Problem frame

Используйте этот паттерн, когда решение, criterion result, representation check или review statement содержит claim, на который участник должен полагаться, но basis, scope, evidence-producing work, assumptions, freshness or limitations не восстановлены.

**Первый полезный ход:** перепишите «решение обосновано» как один или несколько atomic claims and create an evidence path for each.

**Что ломается без паттерна:** расчёт, BIM-model, нормативный документ, expert comment or signature поддерживает «решение вообще»; evidence carrier смешивается с evidence-producing work and interpreted result; stale inputs remain invisible.

**Что это даёт:** reliance становится claim-, scope-, time- and source-bounded; gaps can route to new work, lower claim, assurance abstention or decision reopen.

**Не этот паттерн**, если текущий question is assurance level, compliance decision, gate, causal use or work authorization. Use `B.3`, project compliance owner, `A.21`, `C.28` or direct role/speech-act owner.

### BDPF.8:2 - Problem

A built-asset PAD usually depends on heterogeneous evidence:

- source/regulatory interpretations;
- surveys and site investigations;
- calculations and simulations;
- measurements and test results;
- model checks and information queries;
- expert judgement and review work;
- precedent/reference-project evidence;
- accepted deviations and residual risk records.

These items differ in claim type, reliability, scope and freshness. A document list is not an evidence graph. A calculation file is a carrier; its inputs, method, performed work, result interpretation and limitations must be related to the claim.

### BDPF.8:3 - Forces

| Force | Tension |
| --- | --- |
| Multi-source support | One claim may need several evidence paths with different reliability. |
| Model usefulness vs model risk | Simulation gives insight but depends on assumptions, calibration and representation. |
| Regulatory authority vs engineering evidence | Rule applicability and technical performance are related but distinct claims. |
| Currentness vs reuse | Reusing prior evidence saves work but may cross context, edition or condition boundaries. |
| Expert judgement vs traceability | Judgement may be legitimate while still requiring role, basis and uncertainty. |
| Negative results vs schedule pressure | Evidence gap may force lower claim or reopen when project wants closure. |

### BDPF.8:4 - Solution

```text
DesignClaimEvidenceTrace@Project:
  evidenceTraceId:
  governingDecisionOrCriteriaRef?:
  claimRef:
  claimText:
  claimKind:
  claimScope:
  describedHolonOrStructureRefs:
  boundedContextRef:
  receivingUse:
  evidencePathRows:
    - evidenceRef:
      evidenceCarrierRef?:
      evidenceProducingWorkRef?:
      evidenceInterpretingRoleAssignmentRef?:
      sourceOrMethodRef:
      measurementOrEvalResultRef?:
      supportedClaimPart:
      timeOrFreshnessWindow:
      reliabilityOrAssuranceExitRef?:
      limitationOrRivalExplanation:
      sourceReturnCondition:
  assumptionRefs:
  modelOrCalculationBoundary?:
  sourceCurrentnessRefs:
  missingEvidenceOrContradiction:
  claimDisposition:
    supportedForUse | supportedWithLimits | lowerClaim | probeNeeded | abstain | contradictedWithinScope
  admissibleUse:
  nonAdmissibleUse:
  refreshOrReopenCondition:
```

#### Evidence-use moves

1. **Atomize claim.** Split «схема надёжна и соответствует требованиям» into performance, applicability, normative, maintainability and other claims with direct owners.
2. **Name receiving use.** Evidence adequate for option screening may be inadequate for final reliance or statutory submission.
3. **Recover path, not list.** Relate source/method, performed work, result, interpretation role, carrier and supported claim part.
4. **Expose assumptions and rival explanations.** Model boundary, load cases, site conditions, occupancy, degradation, construction tolerances and data quality stay visible.
5. **Check time/currentness.** Pin source edition, survey date, model revision, validity window and changed-condition triggers.
6. **Issue disposition.** When evidence is insufficient, lower the claim, request a probe, abstain or reopen PAD. Do not fill gaps with approval language.
7. **Route assurance separately.** `DesignClaimEvidenceTrace` supports evidence use; named assurance over claim/context belongs to `B.3`.

#### Evidence kind prompts

| Evidence source/use | Required boundary question |
| --- | --- |
| Calculation/model/simulation | What claim, assumptions, calibration, load/scenario set and validity window? |
| Normative source/check | Which edition, applicability interpretation, clause/rule and direct compliance owner? |
| Survey/investigation/field data | What location, method, sampling, uncertainty and currentness? |
| BIM/IFC/model query | Which represented structures, model edition, information completeness and unvalidated loss? |
| Machine-readable rule/check | Which rule specification, checked carrier, run work, result and claims not checked? |
| Expert judgement | Which role assignment, basis, alternatives, uncertainty and conflict/independence boundary? |
| Review comment/session | What defect/question was observed; what claim does the review actually support? |
| Reference project/precedent | Which context bridge and differences limit transfer? |

### BDPF.8:5 - Archetypal Grounding

Weak statement:

> Выбранная безбалочная схема обоснована расчётом.

Repaired evidence traces separate at least:

- ultimate limit-state capacity for named load combinations and structural model assumptions;
- serviceability/deflection and vibration claims under named occupancy/use scenarios;
- punching-shear and robustness checks;
- fire-resistance claim with direct rule/evidence owner;
- constructability and tolerance claim based on separate work/evidence;
- impact on service penetrations and future adaptability, which the structural calculation does not support.

A model revision or changed equipment loads triggers refresh of the affected claims, not an automatic statement that the whole PAD is valid or invalid.

### BDPF.8:6 - Bias-Annotation

Паттерн блокирует evidence-carrier reification, calculation halo, authority citation and stale-evidence inertia. It also blocks evidence-by-volume: many files do not raise support without claim paths.

### BDPF.8:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF8-1` | Claim is atomic enough for one scope and receiving use. |
| `CC-BDPF8-2` | Evidence paths relate source/method, work, result, interpretation and carrier where current. |
| `CC-BDPF8-3` | Assumptions, limitations and rival explanations are visible. |
| `CC-BDPF8-4` | Edition/time/currentness and refresh trigger are explicit. |
| `CC-BDPF8-5` | Normative applicability, performance evidence, assurance and approval remain separate. |
| `CC-BDPF8-6` | Missing/contradictory evidence has an honest disposition. |
| `CC-BDPF8-7` | BIM/machine-check results state represented/checkable structure and loss. |
| `CC-BDPF8-8` | Evidence use does not widen beyond `admissibleUse`. |

### BDPF.8:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| «Есть расчёт» | Carrier without claim path. | Name claim, scope, model and result. |
| Norm citation as proof of performance | Applicability/rule and evidence collapse. | Separate normative and performance claims. |
| Model check = compliance | Rule scope and unvalidated structure hidden. | Record machine-readable validation boundary. |
| Expert approved | Role/speech act replaces evidence. | Record judgement basis or direct authority act separately. |
| Old analogue reused silently | Context/currentness loss. | Add bridge/loss/currentness note. |
| Evidence gap marked «не критично» | Disposition has no owner/basis. | Lower claim, probe, abstain or decision reopen. |
| One evidence package for whole decision | Claim granularity lost. | Create multiple traces and link them to PAD concerns. |

### BDPF.8:9 - Consequences

Преимущество — design reasoning can be audited, refreshed and selectively reopened rather than defended by document volume. Цена — broad assurance language must be decomposed and some attractive certainty will be lowered.

### BDPF.8:10 - Rationale

`A.10` makes evidence a claim-support relation with provenance and scope. BDPF supplies built-asset evidence recognition, but assurance, causal, compliance and gate claims retain direct owners.

### BDPF.8:11 - SoTA-Echoing

- Verification/validation practice supports claim-specific evidence and lifecycle traceability; BDPF prevents the verification artifact from becoming the verified entity.
- Model-based analysis and machine-readable validation improve repeatability when model/rule editions, performed runs and unchecked structure are explicit.
- Information requirements and CDE status can support currentness/provenance, but do not by themselves establish engineering evidence sufficiency.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-15288-2023`, `SRC-BDPF-19650-6-2025`, `SRC-BDPF-IDS-1.0`; exact evidence/checking applicability returns to `Source Use And Refresh Map`.

### BDPF.8:12 - Relations

Uses `A.10`, `A.2.4`, `B.3`, `B.3.4`, `C.16`, `C.28`, `C.33`, `C.34`, `BDPF.3`, `BDPF.6B`, `BDPF.7`, `BDPF.9`, `BDPF.10`, `BDPF.11` and `BDPF.12`. Reopen when claim, receiving use, source edition, assumption, model, evidence-producing work, measurement/eval, reliability, represented structure or time window changes.

### BDPF.8:End

---

## BDPF.9 — Готовность проектного boundary-crossing

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** one boundary-use routing relation that classifies the live readiness, gate, publication, authority or adequacy question and points to its direct owner; `BuiltAssetDesignReadinessUse@Project` is the DPF-local profile/use record.

### BDPF.9:1 - Problem frame

Используйте этот паттерн, когда текущий вопрос звучит «можно ли переходить дальше?», но неясно, является ли это:

- оценкой достаточности решения;
- readiness intended work;
- настоящим gate-decision;
- publication readiness;
- request for approval/authorization;
- только status/cue в carrier.

**Первый полезный ход:** классифицируйте boundary claim, затем используйте либо `BDPF.12`, либо `A.15.5`, либо текущий `A.21 OperationalGate(profile)`; BDPF.9 связывает выбранный direct owner с built-asset profile and allowed/non-allowed next use.

**Что ломается без паттерна:** green status, checklist completion, «готово к экспертизе» or meeting approval is treated as proof, performed work or permission; boundary crossing has no current check set, decision log or missingness.

**Что это даёт:** project closes only the exact next-use question and preserves blockers, reservations, direct-owner checks, decision rationale and reopen conditions.

**Не этот паттерн**, если the direct owner and exact result are already known and no built-asset profile or allowed/non-allowed-use binding is needed. Apply `BDPF.12`, `A.15.5`, `A.21`, `E.17` or the authority owner directly rather than adding a routing record.

### BDPF.9:2 - Problem

Readiness is highly polysemous. A design can be:

- adequate enough for architecture review but not for construction documentation;
- documented enough for publication but not evidence-complete;
- ready for one planned work package but blocked for another;
- passed by an actual gate under a profile;
- merely shown as green by a dashboard.

A generic `DesignReadinessGate` hides these distinctions. This edition therefore does not mint a second gate ontology. It uses `A.15.5` for work-entry readiness and `A.21` only when a real gate decision relation consumes declared checks and publishes `GateDecision + DecisionLogRef`.

### BDPF.9:3 - Forces

| Force | Tension |
| --- | --- |
| Need to proceed | Teams need local closure, but current evidence may justify only a narrower use. |
| Checklist simplicity | A checklist is readable, but row completion is not a gate decision. |
| Organizational authority | A role may authorize crossing, while engineering adequacy remains a separate result. |
| Profile diversity | Source analysis, architecture review, publication and work entry need different checks. |
| Missingness vs schedule | Pressure encourages treating unknown as pass. |
| Reuse vs currentness | A prior gate/readiness result may be stale after source or decision change. |

### BDPF.9:4 - Solution

#### 1. Classify the current boundary claim

| Current question | Direct owner/result | BDPF.9 role |
| --- | --- | --- |
| «Достаточно ли PAD для declared reader/use?» | `BDPF.12` / `C.32.ADA` | Do not use gate language. |
| «Готова ли intended work к входу?» | `A.15.5 WorkEntryReadiness@Context` | Add built-asset work/profile refs and blockers. |
| «Существует ли gate decision по declared checks?» | `A.21 OperationalGate(profile)` | Publish exact gate use and decision log. |
| «Можно ли юридически/организационно разрешить действие?» | local authority + `A.2.8/A.2.9` as applicable | Keep authorization separate from readiness/gate truth. |
| «Готова ли publication face/carrier?» | `E.17` plus project publication owner | Do not infer decision/evidence adequacy. |
| «Dashboard показывает ready» | cue/source pointer until direct relation recovered | Block gate/readiness overread. |

#### 2. Publish a bounded use record

```text
BuiltAssetDesignReadinessUse@Project:
  readinessUseId:
  describedHolonOrDecisionRef:
  boundedContextRef:
  boundaryUseProfile:
    sourceAnalysis | siteStart | architectureDecisionReview | documentationPublication | downstreamWorkEntry | externalReview | projectDefined
  directOwnerRelationFamily:
    WorkEntryReadiness | OperationalGate | PublicationUse | AuthoritySpeechAct | ArchitectureDecisionAdequacyEvaluation
  directOwnerRef:
  intendedNextUseOrWorkRef:
  requiredCheckOrConditionRefs:
  effectiveEvidenceAndSourceRefs:
  currentnessWindow:
  blockingGaps:
  reservationsOrDegradedConditions:
  decisionOrDisposition:
    - for A.21: abstain | pass | degrade | block
    - for A.15.5: use the direct A.15.5 readiness disposition
    - otherwise: use the direct owner value
  allowedNextUseOrWork:
  nonAllowedUseOrWork:
  decisionLogOrRationaleRef:
  authorityOrSpeechActRef?:
  nonAdmissibleUse:
  reopenCondition:
```

#### 3. Use profile-specific minima without turning them into universal workflow

| `boundaryUseProfile` | Minimum live question set | Typical direct returns |
| --- | --- | --- |
| `sourceAnalysis` | Are carriers inventoried, signals/gaps/P2S returns visible, and is the next analysis/design use bounded? | `BDPF.3B`, `A.15.5` or project review owner; not PAD readiness. |
| `siteStart` | Are built asset, physical site and placement relation distinct; are material boundaries, structures, readings and unknown-to-probe returns fit for the named next use? | `BDPF.1/1A/3B` plus the direct work/review owner; never general site suitability. |
| `architectureDecisionReview` | Is PAD adequate enough to review: candidate basis, structures, trade-offs, evidence exits, roles, reopen? | First `BDPF.12`; `A.21` only if an actual review gate exists. |
| `documentationPublication` | Is an existing PAD correctly projected with current refs, represented/lost structure and publication boundary? | `BDPF.10`, `E.17`; not proof that PAD is right. |
| `downstreamWorkEntry` | Does intended work have full-kit inputs, assignments, resources, constraints, current decision/evidence and launch boundary? | `A.15.5`; `A.21 LaunchGate` only when actually defined. |
| `externalReview` | Is the declared package ready for a named external review use under applicable procedure? | Project/regulatory owner plus evidence/publication refs; BDPF does not define statutory acceptance. |

#### 4. Site-start profile

`siteStart` is usable for a named next design use only when physical `siteRef`, context, claim-specific boundaries, separate built-asset/site frames, explicit placement state, current sources, site signals, structures/interfaces, bearer-bound readings, unknown-to-probe returns and allowed/blocked next uses are visible.

Local dispositions `readyForSiteProblemShaping`, `readyForCandidatePlacementSynthesis`, `readyForPlacementComparison`, `usableWithSiteReservations`, `blockedBySiteIdentityOrBoundary` and `blockedBySiteEvidenceGap` are profile results only. They may feed a real `A.21 OperationalGate(profile)`; they are not `GateDecision` values.

#### 5. A.21-specific boundary

When `directOwnerRelationFamily = OperationalGate`, the minimum current relation is:

```text
GateId
+ GateProfile
+ effective GateCheckRef set
+ aggregated CV status
+ GateDecision: abstain | pass | degrade | block
+ DecisionLogRef
```

A checklist, status, CV result, dashboard or readiness note without these fields is not an `A.21` gate decision.

### BDPF.9:5 - Archetypal Grounding

**Architecture-review boundary for a plantroom configuration.** The team first runs `BDPF.12` and finds source-to-structure trace, candidate basis and selected structures at value 4, but one fire-compartment evidence exit at 2. The honest result is not «PAD failed» and not «ready because the meeting is scheduled».

If the organization has an actual architecture-review gate, it consumes named checks. Under its profile the missing evidence check yields `GateDecision=degrade` with a decision log allowing limited coordination work but blocking final publication/reliance. If no gate relation exists, the result remains an adequacy finding plus bounded work-entry/readiness question; no `GateDecision` is invented.

### BDPF.9:6 - Bias-Annotation

Паттерн блокирует green-tile bias, checklist-as-gate, readiness-as-proof and approval-as-work. It also blocks stage-name determinism: profile is selected by current boundary use, not by a universal design stage sequence.

### BDPF.9:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF9-1` | Current boundary claim is classified before gate/readiness wording is used. |
| `CC-BDPF9-2` | Direct owner and exact project-side result ref are present. |
| `CC-BDPF9-3` | Profile, next use/work and currentness window are explicit. |
| `CC-BDPF9-4` | `siteStart` names separate built-asset frame, site frame and placement relation, and does not imply site suitability. |
| `CC-BDPF9-5` | Required checks/conditions and blockers are source/evidence bounded. |
| `CC-BDPF9-6` | `A.21` use has GateId, profile, effective check set, CV aggregate, GateDecision and DecisionLogRef. |
| `CC-BDPF9-7` | Unknown/missing does not silently become pass. |
| `CC-BDPF9-8` | Allowed and non-allowed next uses are both stated. |
| `CC-BDPF9-9` | Authority act, adequacy, evidence, readiness, gate and performed work remain distinct. |
| `CC-BDPF9-10` | Reopen condition covers source, frame, placement relation, decision, evidence, check or work change. |
### BDPF.9:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| «Комплектность 100% = pass» | Carrier/checklist completion replaces gate relation. | Recover direct owner and checks. |
| `passWithReservations` as untyped custom gate value | Gate lattice drift. | Under A.21 use `degrade` and state conditions; otherwise use direct owner vocabulary. |
| Meeting scheduled = review ready | Calendar event replaces readiness. | Check required records/evidence and currentness. |
| Gate pass = decision correct | Boundary decision widens to truth. | Keep PAD adequacy/evidence separate. |
| Approval = work authorized and performed | Speech act, readiness and work collapse. | Record direct act, readiness and `U.Work` separately. |
| Prior pass reused after source change | Stale closure. | Trigger reopen/currentness refresh. |
| Same gate for every stage | Profile and use hidden. | Name boundary-use profile and required checks. |

### BDPF.9:9 - Consequences

Преимущество — переходы становятся explicit and fail-closed without turning every checklist into bureaucracy. Цена — teams must stop using one ambiguous «готово» status for adequacy, publication, work entry and authorization.

### BDPF.9:10 - Rationale

FPF separates work-entry readiness (`A.15.5`), gate decision (`A.21`), evidence, assurance, publication, authority and work. BDPF.9 is a routing and domain-profile pattern, not an alternative gate kernel.

### BDPF.9:11 - SoTA-Echoing

- Stage gates and information-delivery milestones are useful only when their check sets, decision authority, permitted next use and currentness are explicit.
- CDE/document status can support publication workflow but does not establish engineering adequacy or work entry.
- Safety/regulatory gates require their own evidence and rule owners; BDPF records exits without claiming jurisdictional authority.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-19650-2-2018`, `SRC-BDPF-19650-4-2022`; exact organizational and jurisdictional use returns to project owners and the source map.

### BDPF.9:12 - Relations

Uses `A.15`, `A.15.5`, `A.21`, `A.20`, `A.2.8`, `A.2.9`, `A.10`, `B.3`, `E.17`, `BDPF.1A`, `BDPF.3B`, `BDPF.7`, `BDPF.8`, `BDPF.10`, `BDPF.12` and `G.11`. Reopen when profile, direct owner, intended use/work, check set, source/evidence, PAD, publication, authority, resource readiness or currentness changes.

### BDPF.9:End

---

## BDPF.10 — Проекция решения в ПД, BIM/IFC и views

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** the representation/correspondence relation between selected or expected structures of one physical built asset and exact architecture-description, PD/BIM/view or machine-check carriers; the three record forms are conditional outputs under `C.30.AD.BA`, `C.33`, `C.34` and `E.17`.

### BDPF.10:1 - Problem frame

Используйте этот паттерн, когда PAD принят или candidate/expected structures declared, но неизвестно:

- в каких descriptions/views/carriers они представлены;
- для какого concern and reviewer use;
- какая структура captured, weakened, omitted or inconsistent;
- как model/drawing/table/check result returns to the governing source;
- что machine-readable validation действительно проверила.

**Первый полезный ход:** создайте projection relation from selected/expected structures to exact architecture descriptions, views, documentation/model carriers and correspondence notes.

**Что ломается без паттерна:** «решение есть в BIM/ПД» означает только наличие файлов; different discipline views contradict each other; represented structure mistaken for selected/actual structure; model check or IDS pass becomes compliance proof.

**Что это даёт:** review can ask not only «есть ли документ», but «which decision structure is represented, for whom, with what loss and source return».

**Не этот паттерн**, если the live question is creation/repair of PAD (`BDPF.7`), evidence sufficiency (`BDPF.8`), statutory compliance, or an actual-structure claim. Actual structure requires observation/telemetry/evidence and `C.34` correspondence; model detail or document status does not establish it.

### BDPF.10:2 - Problem

A physical built asset cannot be inspected directly during design. Participants rely on architecture descriptions and publication carriers. Every representation selects a viewpoint and loses structure:

- drawing preserves geometry but may hide rationale and modes;
- model preserves object relations but may omit behavior, uncertainty or source basis;
- schedule/specification preserves attributes but weakens spatial relation;
- explanatory note preserves rationale but may not show exact configuration;
- machine-readable rule checks only encoded predicates over available data.

Without explicit correspondence, «model matches decision» becomes an unsupported global claim.

### BDPF.10:3 - Forces

| Force | Tension |
| --- | --- |
| Multiple views | Different concerns need different representations, while underlying selected structures must stay coherent. |
| Information richness vs usability | One carrier cannot expose every relation; omission must remain recoverable. |
| Model federation | Discipline models are coordinated but may have edition, scope and reference differences. |
| Machine readability vs semantic coverage | Automated checks are reproducible but only over encoded rules and represented data. |
| Publication status vs truth | Approved/current status controls use, not physical or engineering correctness. |
| Expected vs represented vs actual | Design carrier describes expected structures; actual realization and telemetry arrive later. |

### BDPF.10:4 - Solution

#### A. Architecture-description use card

```text
BuiltAssetArchitectureDescriptionUseCard@Project:
  descriptionUseId:
  architectureClaimOrDecisionRef:
  describedHolonRef:
  boundedContextRef:
  selectedStructureRefs:
  expectedStructureRefs:
  structureKindRefs:
  viewpointRefs:
  architectureStructuralViewRefs:
  correspondenceRefs:
  referenceDesignationRefs?:
  assetInformationRefs?:
  bimOrIFCRefs?:
  publicationOrExchangeRefs:
  capturedStructureNotes:
  hiddenOrLostStructureNotes:
  sourceReturnCondition:
  admissibleUse:
  nonAdmissibleUse:
  firstNeighborPatternApplication:
```

#### B. Project-documentation projection

```text
ProjectDocumentationProjection@Project:
  projectionId:
  architectureDecisionRef:
  decisionEditionOrWindowRef:
  selectedStructureRefs:
  expectedStructureRefs:
  architectureOwnedInvariantRefs:
  representedStructureRows:
    - structureRef:
      representationRef:
      carrierRef:
      viewOrViewpointRef:
      documentationSectionOrModelScopeRef:
      representationEdition:
      capturedRelations:
      weakenedOrLostRelations:
      reviewerUse:
      correspondenceStatus: aligned | partial | conflict | unknown
      correspondenceOrCrossReferenceRef:
      sourceReturnCondition:
  crossDisciplineCorrespondenceRows:
  unrepresentedStructureOrConcernRows:
  representationConflictRows:
  publicationStatusRefs?:
  admissibleUse:
  nonAdmissibleUse:
  refreshCondition:
```

#### C. Machine-readable validation projection

```text
MachineReadableValidationProjection@Project:
  validationProjectionId:
  governingClaimRef:
  checkedCarrierRefs:
  checkedCarrierEditions:
  machineReadableRuleSpecRefs:
  ruleSpecOwnerRef:
  checkRunWorkRefs:
  checkToolOrMethodDescriptionRef:
  checkResultRefs:
  checkedStructureOrInformationRefs:
  capturedCheckScope:
  lostOrUnvalidatedStructureNotes:
  falsePositiveOrFalseNegativeRisk:
  evidenceOrGateUseRef?:
  admissibleUse:
  nonAdmissibleUse:
  sourceReturnCondition:
  refreshCondition:
```

#### Projection moves

1. Start from a current PAD/architecture claim, not from folder structure.
2. For each selected/expected structure, identify the required view/viewpoint and representation carriers.
3. Record what each representation captures and loses. A cross-reference is useful only if its direction and edition are recoverable.
4. Compare discipline views and model scopes through explicit correspondence; do not infer sameness from shared coordinates or file federation.
5. Record unrepresented concerns and representation conflicts as current gaps, not as silent assumptions.
6. For machine checks, pin rule-spec and carrier editions, performed run, checked predicates and unvalidated structure. Check result may feed `BDPF.8` or `BDPF.9`, but cannot self-promote.
7. Refresh projections whenever PAD, model/document edition, viewpoint, reference designation, information requirement or rule spec changes.

#### Minimum structure-coverage rule

For the declared reader/review use, every `architectureOwnedInvariantRef` or other material selected-structure relation must have exactly one visible disposition:

- represented in at least one exact view/carrier with reviewer use and correspondence status;
- deliberately represented by source reference only, with the return path explicit;
- currently unrepresented, with owner, impact and stop/reopen condition;
- not triggered for this use, with a bounded rationale.

Silence is not a valid disposition. The rule does not require copying every invariant into every carrier; it requires recoverable coverage and loss accounting across the selected view set.

#### Representation-state discipline

```text
selectedStructure  = structure committed by current architecture/decision owner
expectedStructure  = structure expected to result from downstream design/work under current decision
representedStructure = structure made available by a description/view/carrier
actualStructure    = realized structure supported by observation/telemetry/evidence
```

No equality is assumed. Correspondence claims use `C.34`; missing capture uses `C.33`. An `actualStructure` claim additionally requires current observation/telemetry/evidence with its own source and scope; design representation cannot self-promote into actual-state evidence.

### BDPF.10:5 - Archetypal Grounding

**Smoke-control and evacuation structure across carriers.** PAD selects compartment, protected route, shaft and control relations. Projection map links:

- architectural plans/sections to spatial and route structure;
- fire strategy diagrams to scenario and control relations;
- MEP model to shafts, equipment and interfaces;
- control narrative to modes and cause/effect logic;
- schedules to ratings/attributes;
- calculations to claim-specific evidence traces;
- model-check/IDS rules to a subset of information requirements.

The machine check confirms encoded shaft clearance and attribute presence in named model editions. It does not validate smoke movement, system performance, normative sufficiency, installation quality or actual operation.

### BDPF.10:6 - Bias-Annotation

Паттерн блокирует BIM-as-asset, detail-as-fidelity, federation-as-correspondence, latest-file and machine-pass bias. It also blocks one-view truth: every view is concern-selected and loss-bearing.

### BDPF.10:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF10-1` | Projection starts from exact decision/architecture claim and edition/window. |
| `CC-BDPF10-2` | Selected, expected, represented and actual states are distinguishable. |
| `CC-BDPF10-3` | Every architecture-owned invariant/material structure has a represented, source-reference-only, unrepresented or grounded not-triggered disposition. |
| `CC-BDPF10-4` | Captured, weakened/lost and unrepresented structure are visible. |
| `CC-BDPF10-5` | Cross-discipline correspondence status (`aligned|partial|conflict|unknown`) and conflicts are explicit. |
| `CC-BDPF10-6` | Publication status is not treated as evidence/decision/actual structure. |
| `CC-BDPF10-7` | Machine check pins rules, carriers, run work, scope and unvalidated structure. |
| `CC-BDPF10-8` | Source-return and refresh conditions are present. |
| `CC-BDPF10-9` | Stronger evidence, compliance, gate and assurance claims exit to direct owners. |

### BDPF.10:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| «Решение в модели» | Decision relation and structure not named. | Link exact PAD and represented structure rows. |
| Model federation = consistency | Shared container hides semantic conflict. | Record correspondence and conflict rows. |
| LOD/level label = adequate information | Label substitutes for declared use and information need. | State reader use, required structure and captured/lost relations. |
| IDS/rule pass = compliance | Encoded predicate scope widened. | Publish machine-validation boundary and direct compliance exit. |
| Drawing status = truth | Publication state replaces evidence. | Separate status, evidence and decision. |
| Same coordinates = same structure | Geometric alignment mistaken for structural correspondence. | Use `C.34` mapping with preserved/lost structure. |
| Every decision copied to every carrier | Duplication creates drift. | Use source refs and purpose-specific views. |

### BDPF.10:9 - Consequences

Преимущество — documentation/model review becomes a structural adequacy check rather than file-completeness inspection. Цена — teams must maintain explicit correspondence, edition pins and loss notes across carriers.

### BDPF.10:10 - Rationale

`C.30.AD.BA` owns built-asset architecture-description use for BIM, IFC, asset registers, digital-twin views and reference designations. `C.33` and `C.34` govern captured/missing structure and correspondence. BDPF composes these owners for project-decision projection.

### BDPF.10:11 - SoTA-Echoing

The pattern adopts a package-pinned source payload without turning standards into BDPF ontology or asserting that the package pins are universally applicable:

| Source-use ref | Adopt/adapt | Explicit rejection/return |
| --- | --- | --- |
| `SRC-BDPF-42010-2022` | concerns, viewpoints, views, architecture descriptions and correspondences | description/view does not become architecture or decision |
| `SRC-BDPF-19650-1-2018` through `SRC-BDPF-19650-6-2025` | editioned information-container, exchange, security, health-and-safety information and currentness pressure where project-applicable | container status does not establish engineering truth, evidence sufficiency or gate passage |
| `SRC-BDPF-16739-1-2024` | IFC schema/exchange basis | schema instance does not become the asset, PAD or actual structure |
| `SRC-BDPF-29481-1-2025` | information-delivery/exchange-requirement discipline | delivery-process description does not prove performed or adequate engineering work |
| `SRC-BDPF-7817-1-2024` | level-of-information-need distinctions | no universal adequacy score or stage truth |
| `SRC-BDPF-IDS-1.0` | machine-readable information-requirement/checking surface | no general compliance or performance verification |
| `SRC-BDPF-81346-PROJECTPIN` | project-pinned reference-designation relations | label/reference designation does not become physical structure or decision |

Exact edition, applicability and adopted payload return to `Source Use And Refresh Map` and project source-use records.

### BDPF.10:12 - Relations

Uses `C.30.AD`, `C.30.AD.BA`, `C.30.ASV`, `A.22`, `C.33`, `C.34`, `C.35`, `E.17`, `E.24.PUB`, `A.10`, `A.21`, `BDPF.7`, `BDPF.7A`, `BDPF.8`, `BDPF.9`, `BDPF.11` and `G.11`. Reopen when PAD, selected/expected structure, viewpoint, carrier/model edition, reference designation, exchange requirement, rule spec, check run, representation conflict or actual-structure evidence changes.

### BDPF.10:End

---

## BDPF.11 — Feedback, source-change impact и repair

> **Type:** DPF pattern body  
> **Primary EntityOfConcern:** one supported change-or-defect impact relation from a changed source, structure, decision, evidence or representation to the smallest governing owner; the two records are selected by whether the live question is project impact or repeatable method repair.

### BDPF.11:1 - Problem frame

Используйте этот паттерн, когда:

- изменился source signal, assumption, requirement or site condition;
- обнаружен clash, mismatch, unrepresented structure or failed check;
- экспертное/внутреннее review выдаёт замечание;
- defect повторяется в нескольких решениях;
- represented or later observed structure расходится with selected/expected structure.

**Первый полезный ход:** сначала создайте suspectness/impact trace; затем, если defect repeats or points to the way of doing, create method feedback. Не делайте автоматический вывод, что PAD неверен, пока direct owner не проверил affected claim.

**Что ломается без паттерна:** замечание становится доказательством вины/ошибки; source change вызывает либо blanket rework, либо игнорирование; clash чинится в carrier без return to structure; повторяющиеся дефекты остаются individual corrections.

**Что это даёт:** change and defect return to the smallest owner—source, architecture question, candidate basis, PAD, evidence, projection, method, work/readiness or package refresh.

**Не этот паттерн**, если a bounded local carrier defect has already been shown not to affect source, structure, decision, evidence, correspondence or downstream use; repair it under the carrier/publication owner. Do not create a method-feedback record from one anecdote unless a repeatable defect family and evaluation question are current.

### BDPF.11:2 - Problem

Feedback is not one loop. A changed geotechnical parameter, a reviewer comment, a BIM clash, a construction-method constraint and a repeated missing-evidence pattern have different object kinds and return routes.

Two outputs are therefore separated:

- `DesignChangeImpactTrace@Project` answers: what current decisions/structures/evidence/projections become suspect and who must check them?
- `DesignMethodFeedbackRecord@Project` answers: what recurring failure indicates that the method or framework should change and how will that change be evaluated?

Neither record proves that a decision is wrong or that a method improvement worked.

### BDPF.11:3 - Forces

| Force | Tension |
| --- | --- |
| Fast correction vs root cause | Local edit is cheap, but may preserve the defect-producing method. |
| Suspectness vs invalidity | Change can affect a decision without automatically falsifying it. |
| Broad impact vs smallest return | Blanket reopen is costly; too narrow repair misses connected structures. |
| Carrier visibility vs structural cause | Defect appears in drawing/model/comment, while cause may be source, PAD or correspondence. |
| Learning vs blame | Teams need method feedback without converting every defect into personal fault. |
| Current project vs package evolution | Some failures belong to local method; recurring cross-case failures may require BDPF refresh. |

### BDPF.11:4 - Solution

#### A. Source/change impact trace

```text
DesignChangeImpactTrace@Project:
  impactTraceId:
  triggerKind:
    sourceChange | assumptionChange | requirementChange | reviewFinding | representationConflict | machineCheckResult | actualStructureObservation | other
  triggerRef:
  changedCondition:
  changedSourceOrCarrierEditionRef:
  effectiveTimeOrWindow:
  affectedContextOrHolonRefs:
  suspectRelationRows:
    - suspectKind:
        sourceUse | useConcept | systemConcept | architectureQuestion | candidatePalette | criteriaEval | comparisonRetainedSet | PAD | evidence | readiness | projection | method | package
      suspectRef:
      impactPathRefs:
      directConsumerRefs:
      structurallyCoupledOwnerRefs:
      derivedProjectionOrEvidenceRefs:
      impactPathRationale:
      currentDisposition:
        noImpactSupported | reviewNeeded | sourceReturn | repairNeeded | refreshNeeded | hold | unknown
      directOwnerRef:
      evidenceNeeded:
      allowedInterimUse:
      nonAllowedInterimUse:
      reopenOrCloseCondition:
  crossScopePropagationNotes:
  decisionOrWorkAlreadyAffectedRefs?:
  nonAdmissibleUse:
  refreshCondition:
```

#### B. Method feedback record

```text
DesignMethodFeedbackRecord@Project:
  feedbackId:
  feedbackSourceRefs:
  repeatedDefectPattern:
  affectedEntityOrDecisionFamily:
  occurrenceAndScopeEvidence:
  currentMethodDescriptionRef:
  affectedMethodStepOrRelation:
  suspectedMethodFailureMechanism:
  rivalExplanationRefs:
  proposedMethodChange:
  protectedTradeoffs:
  predictedEvaluationResultChange:
  evaluationQuestionFrameRef:
  pilotOrProbeRef:
  decision:
    acceptForProbe | rejectProposal | probeMore | hold | promoteAfterEvidence
  resultingMethodDescriptionRef?:
  packageRefreshCandidateRef?:
  nonAdmissibleUse:
  reevaluationAndReopenCondition:
```

#### Owner-selection table

| Observed trigger | First question | Smallest likely owner |
| --- | --- | --- |
| Source edition/condition changed | Which signal/use/assumption changed and what downstream refs consume it? | `BDPF.3`, `G.11`, then exact downstream owner. |
| Scenario/use changed | Which use/system/structure relations become suspect? | `BDPF.4`, `BDPF.5`, `BDPF.3A`. |
| Architecture residual/clash | Is conflict in selected structure, expected structure, representation or actual realization? | `C.30.ILC`, `C.32.FAIL`, `BDPF.6/10`. |
| Candidate comparison defect | Was candidate space, criterion, scale, evidence or comparator defective? | `BDPF.6A–6C`. |
| PAD inadequacy | Which `C.32.ADA` coordinate is weak? | `BDPF.12` then coordinate repair owner. |
| Evidence failure/staleness | Which claim path is affected? | `BDPF.8`, `A.10`, `B.3.4`. |
| Projection inconsistency | Which selected/expected relation is missing or contradictory? | `BDPF.10`, `C.33`, `C.34`. |
| Readiness/gate defect | Was the direct relation absent, wrong-profiled or stale? | `BDPF.9`, `A.15.5`, `A.21`. |
| Repeated cross-case defect | Is current method causing or failing to prevent the pattern? | `E.22`, `E.23`, `BDPF.2`; possibly package refresh. |

#### Repair discipline

1. **Observe without verdict.** Record trigger and exact source/carrier/work evidence.
2. **Trace suspect relations.** Use refs, not broad stage labels. `suspect` means review needed, not false.
3. **Choose smallest owner.** Repair carrier only when source decision/evidence relation remains adequate; otherwise return upstream.
4. **Bound interim use.** State what may continue while review is open and what is blocked.
5. **Test method changes.** A proposed checklist/template/workshop is not improvement. Use `E.22` to frame evaluation and `E.23` to change and re-evaluate a version.
6. **Escalate package refresh only with cross-case evidence.** One local issue rarely justifies a new BDPF pattern; recurring failure may justify source/quality review.

#### Supported impact-propagation order

Use the smallest evidence-backed propagation order; stop when a `noImpactSupported` boundary is justified.

1. **Direct consumers.** Trace exact records/claims that cite or depend on the changed source, assumption, structure, decision or representation.
2. **Structurally coupled owners.** Follow interfaces, flows, load paths, control relations, temporary/permanent-state relations and cross-scope residuals that can carry the change.
3. **Derived epistemes.** Inspect evidence traces, eval results, ADR/projection faces, PD/BIM views, machine-check results and readiness/gate uses derived from the affected relation.
4. **Work already entered or performed.** Name intended/actual work and resource or reversal consequences only where their refs are current.
5. **Stop or branch.** Close unaffected branches with a supported reason; keep unknown branches as `reviewNeeded` or `unknown`, not as silent no-impact.

### BDPF.11:5 - Archetypal Grounding

**Changed groundwater level after updated investigations.** The new source does not automatically invalidate every foundation and basement decision.

Impact trace:

- marks source-use records and assumptions currentness as changed;
- traces suspect foundation, waterproofing, uplift, temporary works and drainage structure decisions;
- identifies evidence models/calculations consuming the old condition;
- marks affected drawings/model views as potentially stale;
- allows unrelated above-ground coordination to continue;
- blocks final reliance on named basement/foundation claims until owners review.

If several projects repeatedly fail to connect survey updates to suspect decisions, a method feedback record proposes a mandatory source-change impact query in the design-development method and tests whether impact latency decreases without creating blanket rework.

### BDPF.11:6 - Bias-Annotation

Паттерн блокирует comment-as-truth, clash-as-root-cause, change-equals-invalidity and local-fix bias. It also blocks improvement theatre: adding a template without re-evaluated outcome is not method improvement.

### BDPF.11:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF11-1` | Trigger kind, exact ref, edition/time and changed condition are explicit. |
| `CC-BDPF11-2` | Suspectness is separated from invalidity/confirmation. |
| `CC-BDPF11-3` | Impact path reaches exact direct consumers, structurally coupled owners and derived evidence/projection refs where triggered. |
| `CC-BDPF11-4` | Every suspect row has direct owner, evidence needed and close/reopen condition. |
| `CC-BDPF11-5` | Interim allowed and non-allowed uses are bounded. |
| `CC-BDPF11-6` | Propagation stops only at an evidence-backed no-impact boundary; unknown is not converted to no impact. |
| `CC-BDPF11-7` | Method feedback cites repeated-pattern evidence and rival explanations. |
| `CC-BDPF11-8` | Proposed method change has protected trade-offs and re-evaluation route. |
| `CC-BDPF11-9` | Package refresh is based on heterogeneous/cross-case need, not one anecdote. |

### BDPF.11:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Every comment reopens whole design | Costly overreaction. | Trace exact suspect relations and scopes. |
| Comment proves decision wrong | Review source gains false authority. | Route claim to direct evidence/decision owner. |
| Clash fixed geometrically | Selected/interface structure may remain inconsistent. | Check PAD and correspondence before carrier edit. |
| Source change ignored because file status unchanged | Currentness failure. | Trigger impact trace by source edition/condition. |
| Root cause = «human error» | Method/system relation hidden. | Inspect repeat pattern, method step and constraints. |
| Add checklist and declare improvement | No object version/evaluation. | Use `E.22/E.23` with re-evaluation. |
| Every local defect creates new DPF pattern | Package bloat. | Require recurring domain problem and owner gap. |

### BDPF.11:9 - Consequences

Преимущество — changes and defects become selective, reviewable repairs and learning inputs. Цена — projects must maintain refs and accept temporary suspect/hold states rather than binary blame or clearance.

### BDPF.11:10 - Rationale

`C.32.FAIL` governs architecture failure recognition and repair; `E.23` governs actual improvement; `G.11` governs currentness refresh. BDPF.11 composes a built-asset impact/feedback entry without replacing any of those owners.

### BDPF.11:11 - SoTA-Echoing

- Configuration/change management supports impact traceability; BDPF keeps it claim- and structure-specific rather than document-only.
- Issue management and model coordination provide defect carriers, but issue status does not establish root cause or repair adequacy.
- Continuous-improvement practices are adopted only with object-version change and re-evaluation; retrospective discussion alone is not evidence of improvement.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-15288-2023`, `SRC-BDPF-19650-1-2018`; exact project change-control practice remains project-owned.

### BDPF.11:12 - Relations

Uses `C.32.FAIL`, `C.30.ILC`, `C.33`, `C.34`, `A.10`, `B.3.4`, `E.22`, `E.23`, `G.11`, `BDPF.2`, `BDPF.3`, `BDPF.3A`, `BDPF.4–10` and `BDPF.12`. Reopen when trigger, source/currentness, impact path, evidence, direct-owner disposition, method version, evaluation result or cross-case pattern changes.

### BDPF.11:End

---

## BDPF.12 — Достаточность архитектурного решения для declared use

> **Type:** DPF evaluation pattern  
> **Primary EntityOfConcern:** the declared-use adequacy of one current project architecture decision version; `BuiltAssetArchitectureDecisionAdequacyEvaluation@Project` is the BDPF evaluation result using the complete `C.32.ADA` coordinate set.

### BDPF.12:1 - Problem frame

Используйте этот паттерн, когда PAD and optional ADR/projection exist, but project needs to know whether the decision is **good enough for one declared use** and which exact coordinate must be repaired first.

Typical uses:

- internal architecture discussion;
- architecture review;
- downstream designer/developer handoff;
- ADR/publication preparation;
- reliance-bearing external review;
- improvement of one decision version.

**Первый полезный ход:** state declared use and stop condition before evaluation, then evaluate every `C.32.ADA` coordinate with value `0..5`, adjacent-value rationale and repair owner. Do not average.

**Что ломается без паттерна:** complete-looking ADR or model is treated as an adequate decision; review comments remain «неясно/недостаточно»; strong rationale compensates for absent candidate basis, method docking or reopen condition; score becomes approval.

**Что это даёт:** review returns a typed weak-coordinate repair, not a general verdict.

**Не этот паттерн**, если current object is pattern quality (`E.21`), package adequacy (`E.4.DPF.DA`), evidence, assurance, gate passage, compliance, candidate comparison or PAD creation.

### BDPF.12:2 - Problem

Architecture-decision adequacy is multidimensional. A decision may be sufficient for discussion and insufficient for work handoff. A readable record may describe a weak PAD. A strong candidate trace may coexist with absent evidence exits. A complete BIM projection may hide unclear accepted losses.

One number or pass/fail result loses this structure. BDPF therefore reuses the complete `C.32.ADA` coordinate set and value meanings, then supplies built-asset reading prompts and use-specific floors. The result never approves or certifies the decision.

### BDPF.12:3 - Forces

| Force | Tension |
| --- | --- |
| Declared-use variability | Adequacy changes with intended reader/action without becoming arbitrary. |
| Complete inspection vs review cost | Every coordinate matters, but evaluation must remain usable. |
| Weakest-link visibility | One absent critical coordinate cannot be hidden by strong others. |
| Repair precision | Review should name smallest governing pattern. |
| Evidence vs expression | A coordinate can be well expressed while its underlying claim still lacks evidence. |
| Evaluation vs authority | High value is not approval, assurance, gate passage or authorization. |
| Evolution | Decision and evaluation must reopen with source/use/structure change. |

### BDPF.12:4 - Solution

#### Shared result form

```text
BuiltAssetArchitectureDecisionAdequacyEvaluation@Project:
  evaluationId:
  evaluatedDecisionRef:
  evaluatedDecisionEditionOrWindowRef:
  architectureDecisionRecordProjectionRef?:
  documentationProjectionRefs?:
  declaredUse:
  intendedReaderOrOperatorRefs:
  evaluatorRoleAssignmentRef:
  stopCondition:
  coordinateRows:
    - coordinateRef:
      triggerStatus: triggered | notTriggered
      notTriggeredRationale?:
      value: 0 | 1 | 2 | 3 | 4 | 5
      valueLabel:
        absent | namedOnly | partiallyExpressedForDeclaredUse |
        sufficientlyExpressedForDeclaredUse |
        wellExpressedForDeclaredUse |
        exceptionallyExpressedForDeclaredUse
      adjacentValueRationale:
      builtAssetEvidenceLocus:
      repairPatternRef:
      repairInstruction:
      reopenCondition:
  strongestBlockingCoordinates:
  protectedTradeoffs:
  noAveragePolicy: true
  dispositionKind: evaluationOnly
  evaluationDisposition:
    adequateForDeclaredUse | adequateWithVisibleLimits | repairBeforeUse | stopOrReturn
  nonAdmissibleUse:
  reevaluationTrigger:
```

#### Value meanings

| Value | Label | Meaning for the declared decision use |
| ---: | --- | --- |
| `0` | `absent` | Coordinate is not expressed. |
| `1` | `namedOnly` | Named/implied, but unusable for reliance or repair. |
| `2` | `partiallyExpressedForDeclaredUse` | Present but incomplete, misplaced or fragile. |
| `3` | `sufficientlyExpressedForDeclaredUse` | Supports this bounded use with visible limits. |
| `4` | `wellExpressedForDeclaredUse` | Clear refs, boundaries, source return and repair path survive likely project change. |
| `5` | `exceptionallyExpressedForDeclaredUse` | Transfers across another team/slice/adjacent holon with minimal recovery and no hidden owner loss. |

Values are ordinal content evaluations. They are not percentages, maturity stages, votes, reliability levels or gate values.

#### Complete Core coordinate set with built-asset reading prompts

Evaluate all rows. `notTriggered` requires a declared-use reason; it is not a convenience escape.

| `C.32.ADA` coordinate | Built-asset evaluation question | Typical repair owner |
| --- | --- | --- |
| `BoundedDecisionQuestionRecoverability` | Can a new participant recover physical holon/subsystem, context, lifecycle slice, decision subject, status/window and exact question? | `BDPF.7` / `C.32.PAD`. |
| `CandidateBasisAndSelectionTraceability` | Are palette, structurally distinct alternatives or honest no-plurality reason, criteria/eval, comparison and retained set recoverable? | `BDPF.6A–6C`, `C.32`, `A.19.CPM`, `G.5`, `C.11`. |
| `AffectedStructureAndDescriptionAdequacy` | Are selected/expected structures, structure kinds, views, correspondences, represented/lost structure and source return explicit? | `BDPF.6`, `BDPF.10`, `C.30`, `C.30.ASV`, `C.30.AD`, `A.6.F`, `A.6.M`, `C.29`, `C.33`, `C.34`. |
| `ArchitectureCharacteristicTradeoffAdequacy` | Are bearer-bound characteristics, scales, criteria/eval, gains, accepted losses, guardrails and proxy risks visible? | `BDPF.6B`, `C.32.HCS`, `C.32.ACS`, `C.32.ACE`, `C.16`, `C.25`, `C.31`, `C.31.ASAP`. |
| `MethodAndWorkDockingAdequacy` | Can downstream roles see method-use instructions, expected structure effects, work boundary and readiness exit without treating PAD as WorkPlan? | `BDPF.2`, `BDPF.7`, `BDPF.9`, `A.15`, `A.15.1`, `A.15.2`, `A.15.5`, `E.11.PUR`, `C.24`. |
| `ArchitectDeveloperSplitAdequacy` | Are architecture-owned invariants and downstream refinement freedom explicit for disciplines/contractors? | `BDPF.7`, `A.15`, `B.2.P` for claim-kind recovery and `B.2` when whole reidentification is triggered. |
| `PublicationProjectionAdequacy` | Does ADR/PD/BIM projection serve declared readers, preserve decision source/losses and avoid new semantics? | `BDPF.7A`, `BDPF.7B`, `BDPF.10`, `C.32.ADR`, `E.17`, `E.24.PUB`. |
| `EvidenceEvalAndGateExitAdequacy` | Are live eval/evidence/assurance/gate/compliance exits named and non-live claims not fabricated? | `BDPF.8`, `BDPF.9`, `A.10`, `B.3`, `A.21`. |
| `EvolutionAndReopenConditionAdequacy` | Are source change, evidence failure, use change, candidate discovery, actual/represented mismatch and supersession triggers explicit? | `BDPF.7`, `BDPF.11`, `C.32.FAIL`, `C.18`, `C.19`, `E.23`, `G.11`. |
| `TransformerTransformedCorrespondenceAdequacy` | When design organization/method/contract split affects target structures, is transformer↔transformed correspondence and coordination cost visible? | `C.32.CONWAY`, `A.15`, `A.3.4`, `E.18`; `notTriggered` only with reason. |
| `NonOverreadAndReceivingPatternAdequacy` | Are PAD, description, publication, source, evidence, assurance, gate, role, method, work and compliance claims kept with their owners? | `A.7`, `A.6.P`, `E.10`, `F.18`, the precision-restoration map and exact receiving pattern. |
| `ConsequenceAndRepairGuidanceAdequacy` | Can a role act on consequences, losses, blockers and exact repair instructions without vague «доработать»? | Coordinate-specific owner, PAD consequence rows or ADR section functions. |

#### Use-specific stop profiles

These are BDPF local evaluation profiles, not universal project stage gates.

| Declared use | Minimum stop condition | Blocked overread |
| --- | --- | --- |
| `internalDiscussion` | Every triggered coordinate ≥`2`; `BoundedDecisionQuestionRecoverability` ≥`3`; blockers visible. | Does not permit downstream reliance. |
| `architectureReview` | Every triggered coordinate ≥`3`; no `0`; question, candidate basis, structures, trade-offs, evidence exits and reopen ≥`3`. | Not approval or gate passage. |
| `downstreamDesignHandoff` | Every triggered coordinate ≥`4`; especially method/work docking, architect/developer split, publication and non-overread ≥`4`. | Still requires actual role assignment, readiness and work authority. |
| `adrOrDocumentationPublication` | PAD relation coordinates ≥`3`; publication/structure/source-return/non-overread ≥`4`. | Publication does not make PAD adequate for implementation. |
| `relianceBearingExternalReview` | Every triggered coordinate ≥`4`; direct evidence/assurance/compliance/gate owners must independently satisfy their conditions. | ADA value cannot replace external procedure or authority. |
| `improvementDiagnostic` | No minimum; all rows evaluated and low coordinates routed to `E.22/E.23`. | Diagnostic score is not use readiness. |

The floor never permits averaging. One below-floor triggered coordinate remains visible even if all others are `5`.

#### Evaluation method

1. Declare use, readers and stop condition.
2. Pin PAD, ADR/projection and source editions.
3. Evaluate every coordinate; cite exact evidence locus.
4. Give adjacent-value rationale: why lower understates and higher overstates current content.
5. Identify strongest blockers and smallest repair patterns.
6. State an `evaluationOnly` disposition without approval, assurance, gate or authorization language.
7. Re-evaluate the changed decision version; a repair proposal or edited record is not improvement until evaluation changes under the same or explicitly revised frame.

### BDPF.12:5 - Archetypal Grounding

**Vertical-core PAD evaluated for downstream handoff.** Results include:

- bounded question `4`;
- candidate trace `4`;
- affected structures/description `3` because one control-mode correspondence is absent;
- trade-off `4`;
- method/work docking `2` because responsible discipline roles and readiness exit are vague;
- architect/developer split `3`;
- publication projection `4`;
- evidence/gate exits `3`;
- evolution/reopen `4`;
- transformer/transformed correspondence `2` because coordination structure across architect/MEP/structural roles is implicit;
- non-overread `4`;
- consequence/repair guidance `3`.

No average is produced. For `downstreamDesignHandoff` the decision is `repairBeforeUse`; repairs go to `BDPF.7`, `BDPF.2/9`, `C.32.CONWAY` and `BDPF.10`. The PAD is not rejected globally and the review does not issue approval.

### BDPF.12:6 - Bias-Annotation

Паттерн блокирует completeness-as-adequacy, average-score compensation, reviewer-authority and high-score-as-gate bias. It also blocks `notTriggered` laundering and evaluation/evidence collapse.

### BDPF.12:7 - Conformance Checklist

| Check | Passing condition |
| --- | --- |
| `CC-BDPF12-1` | Declared use, readers, evaluated version and stop condition precede values. |
| `CC-BDPF12-2` | Every Core coordinate is scored or grounded `notTriggered`. |
| `CC-BDPF12-3` | Every value has adjacent-value rationale and evidence locus. |
| `CC-BDPF12-4` | No average, weighted total or global percentage exists. |
| `CC-BDPF12-5` | Use-specific floor is applied without stage/gate overread. |
| `CC-BDPF12-6` | Weak coordinates name exact repair pattern and action. |
| `CC-BDPF12-7` | Evidence, assurance, compliance, gate, authority and work remain direct-owner claims. |
| `CC-BDPF12-8` | Protected trade-offs and non-admissible use are explicit. |
| `CC-BDPF12-9` | Changed version is re-evaluated before improvement is claimed. |

### BDPF.12:8 - Common Anti-Patterns and How to Avoid Them

| Anti-pattern | Failure | Repair |
| --- | --- | --- |
| Average adequacy `4.2/5` | Critical weak coordinate hidden. | Remove average; use blockers. |
| Full ADR = adequate PAD | Publication projection substitutes relation. | Evaluate all coordinates separately. |
| Generic «доработать» | No receiving owner. | Name coordinate, pattern and first repair. |
| Score = approve/reject | Evaluation gains authority. | Use direct decision/gate/authority owner. |
| Difficult row marked N/A | Missingness hidden. | Require grounded `notTriggered` or score it. |
| Same floor for discussion and handoff | Declared use ignored. | Apply named use profile. |
| Repair prose, no re-evaluation | Improvement assumed. | Re-run BDPF.12 on new version. |

### BDPF.12:9 - Consequences

Преимущество — review becomes comparable, repair-oriented and resistant to document polish. Цена — evaluation exposes weak coordination/method/owner boundaries that conventional design review may leave tacit.

### BDPF.12:10 - Rationale

This pattern does not invent a new quality model. It specializes `C.32.ADA` for built-asset evidence loci, readers and decision uses, preserving the exact coordinate set, E.21 value labels, no-average rule and repair exits.

### BDPF.12:11 - SoTA-Echoing

- Architecture review practice contributes concern, structure, rationale, correspondence and trade-off checks; BDPF binds them to the current PAD rather than an abstract document-completeness rubric.
- Decision-quality and assurance practices support use-specific evaluation and evidence exits; BDPF keeps evaluation distinct from approval and confidence.
- Multi-party built-asset delivery makes method docking and architect/downstream split especially load-bearing, so those Core ADA coordinates receive explicit domain prompts.
- Package source-use refs: `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-42010-2022`, `SRC-BDPF-42030-2019`; use-specific floors remain evaluation rules, not external review authority.

### BDPF.12:12 - Relations

Specializes/uses `C.32.ADA`; builds on `C.32.PAD`, `C.32.ADR`, `E.21`, `E.22`, `E.23`, `BDPF.6A–6C`, `BDPF.7`, `BDPF.7A`, `BDPF.8`, `BDPF.9`, `BDPF.10`, `BDPF.11`, `A.10`, `B.3` and `A.21`. Reopen when declared use, PAD/projection edition, coordinate evidence, floor, reader role, source, structure, method/work relation, evidence/gate exit or repair result changes.

### BDPF.12:End

---

# Acceptance Cases

These cases test whether the pattern set preserves kinds and gives a useful first repair across heterogeneous built-asset situations. They are **designed acceptance probes**, not field evidence that a project, pattern or package succeeded. A real run must cite project records, role assignments, work and evaluation evidence.

| Case id | Situation | Primary patterns under test | Transfer question |
| --- | --- | --- | --- |
| `AC-BDPF-01` | Start service from mixed built-asset and site carriers | `BDPF.1`, `1A`, `3`, `3A`, `3B`, `6B`, `9` | Can the package keep built asset, physical site and placement relation distinct while producing P2S-ready analysis? |
| `AC-BDPF-02` | High-rise vertical-core architecture decision | `BDPF.4–7`, `8`, `10`, `12` | Can several concerns remain visible through candidate, PAD and projection? |
| `AC-BDPF-03` | Hospital isolation-room system concept | `BDPF.1`, `4`, `5`, `6` | Can functions, flows, modes and bearers be recovered without premature equipment selection? |
| `AC-BDPF-04` | Data-centre cooling candidate comparison | `BDPF.6A–6C`, `7`, `8` | Does the package resist one weighted score and generated-candidate overread? |
| `AC-BDPF-05` | Reconstruction with uncertain actual condition | `BDPF.3`, `8`, `10`, `11` | Can actual/represented/expected structures and source currentness remain distinct? |
| `AC-BDPF-06` | Construction phasing while facility remains operating | `BDPF.4–7`, `9`, `11` | Can temporary structures and work-entry boundaries be handled without turning BDPF into a WorkPlan? |
| `AC-BDPF-07` | IFC/IDS machine check passes | `BDPF.8`, `9`, `10`, `12` | Can a machine pass remain bounded to encoded information predicates? |
| `AC-BDPF-08` | New investigation changes groundwater condition | `BDPF.3`, `8`, `11` | Does source change produce selective suspectness rather than blanket invalidity? |
| `AC-BDPF-09` | Repeated expert comments expose method defect | `BDPF.2`, `11`, `12`, `E.22/E.23` | Can recurring defects change a method only after evaluation and re-evaluation? |
| `AC-BDPF-10` | Package is prepared for external review | `BDPF.7A`, `7B`, `9`, `10`, `12` | Can publication/readiness/authority remain separate from decision adequacy and evidence? |

## AC-BDPF-01 — Initial-data analysis without design-by-document

**Given**

A project receives a client brief, cadastral/planning materials, utility conditions, topographic and geotechnical reports, existing-network drawings and unresolved emails. The service team is asked to «confirm that the site is suitable and issue design recommendations».

**When**

- `BDPF.1` names the physical built asset;
- `BDPF.1A` names the physical site separately, records claim-specific boundaries and creates a placement relation with state `unknown`;
- `BDPF.3B` composes frames, inventory, site structure/interface map, characteristic readings, uncertainty register and P2S records;
- `BDPF.3` extracts signals with one affected subject, scope, currentness and non-use;
- `BDPF.3A` converts signals into subject-bounded structuring needs;
- `BDPF.6B` keeps site/placement readings bearer- and scale-bound without a total score;
- `BDPF.9` classifies the boundary as `siteStart`/source-analysis readiness, not PAD, suitability proof or authorization.

**Passing result**

- built asset frame, site frame and placement relation are separate and linked;
- cadastral id, plans, surveys and reports remain carriers/descriptions/evidence sources;
- material boundaries are distinguished by claim/use;
- site structures/interfaces are recovered or marked missing;
- each material reading has bearer, scale, evidence/currentness, uncertainty and admissible use;
- each critical unknown routes to affected question, requested source/probe and owner;
- allowed and blocked next uses are explicit;
- no result is represented as selected placement, general site suitability, safety, compliance or permission.

**Failure signals**

- ОКС and site are merged as one «object»;
- `siteRef` contains a parcel id, file or model;
- one boundary or one site score is used for all claims;
- receipt of investigations is treated as evidence of every site property;
- `siteStart` disposition is represented as `GateDecision` without a real `A.21` relation.

**Reopen**

Any built-asset/site identity, boundary use, placement state, source currentness, physical site condition, project scope, characteristic evidence or receiving-owner change.

## AC-BDPF-02 — Vertical-core decision across spatial, structural and fire concerns

**Given**

A high-rise project must choose core configuration. Architectural area efficiency, evacuation, accessibility, smoke control, structural stiffness, service risers, construction phasing and future tenant flexibility conflict.

**When**

- `BDPF.4/5` recover use scenarios and system logic;
- `BDPF.6` forms one architecture question with the smallest exact structure-kind refs or owner-bound discovery cues;
- `BDPF.6A` creates structurally distinct candidates;
- `BDPF.6B/6C` evaluate and retain options without a hidden total score;
- `BDPF.7` records PAD and accepted losses;
- `BDPF.8/10` bind evidence and projections;
- `BDPF.12` evaluates handoff adequacy.

**Passing result**

A new discipline designer can recover question, candidate basis, selected/expected structures, losses, evidence exits, architect-owned invariants, refinement freedom, projection refs and reopen conditions. A low method-docking or correspondence coordinate blocks handoff without globally rejecting the PAD.

**Failure signals**

- core location in a drawing is the only decision record;
- evacuation simulation is used to choose the whole architecture;
- approval status is treated as adequacy;
- all structures are marked represented because one federated model exists.

**Reopen**

Changed occupancy, structural grid, fire strategy, utility demand, phased-construction assumption or failed evidence.

## AC-BDPF-03 — Hospital isolation-room system concept

**Given**

A room schedule names an isolation room and pressure class, but staff/patient/material flows, cleaning, filter maintenance, emergency power, controls and fire interfaces are fragmented across disciplines.

**When**

- `BDPF.1` frames the hospital zone and external interfaces;
- `BDPF.4` distinguishes patient, staff, maintenance, emergency and cleaning scenarios;
- `BDPF.5` relates functions, flows, interfaces, modes and candidate bearers;
- `BDPF.6` creates architecture questions for spatial, ventilation/control and maintenance structures.

**Passing result**

The system concept makes normal/degraded/maintenance modes and cross-discipline dependencies reviewable while equipment and exact configuration remain candidates. Infection-control or safety claims route to direct evidence/assurance owners.

**Failure signals**

- room name is treated as use concept;
- pressure setpoint becomes proof of infection control;
- ventilation diagram is treated as the system;
- maintenance access is added only after equipment selection.

**Reopen**

Changed clinical workflow, pathogen/use assumptions, maintenance strategy, control concept or regulatory/source basis.

## AC-BDPF-04 — Data-centre cooling candidates without score collapse

**Given**

Three cooling architectures are proposed: centralized chilled water, distributed modular cooling and a hybrid. A generative tool has produced dozens of layout variants and a consultant offers a weighted score.

**When**

- `C.35` admits generated carriers as candidate material only after source/structure recovery;
- `BDPF.6A` groups structurally meaningful configurations rather than every geometry;
- `BDPF.6B` defines bearer-bound characteristics: capacity envelope, part-load efficiency, maintainable isolation, resilience, spatial/logistics burden, control complexity and phased expansion;
- `BDPF.6C` publishes a retained set or abstains under missing evidence;
- `BDPF.7` makes PAD only after the decision owner accepts trade-offs.

**Passing result**

No single weighted number hides protected counter-characteristics. Unknown evidence remains unknown. Generated fluency/layout quantity does not increase candidate status. The PAD records accepted energy/space/control/resilience losses and reopen triggers.

**Failure signals**

- every tool output is a candidate;
- valve/equipment count is used as maintainability;
- missing reliability evidence is scored zero;
- highest weighted score is called PAD.

**Reopen**

Changed IT-load envelope, redundancy policy, power/cooling source, expansion plan, operating evidence or comparator preference.

## AC-BDPF-05 — Reconstruction and uncertain actual structure

**Given**

A reconstruction project has archival drawings, laser scan, partial openings, an as-built BIM model and contradictory records of reinforcement and concealed utilities.

**When**

- `BDPF.3` creates source-use records by method, location, date and uncertainty;
- `BDPF.8` relates observation/investigation evidence to atomic actual-condition claims;
- `BDPF.10` distinguishes represented structure from supported actual structure and records correspondence/loss;
- `BDPF.11` tracks impacts when openings or surveys change the actual-state basis.

**Passing result**

The model is usable as a representation with explicit confidence/source-return zones. Unknown concealed structure remains unknown. Candidate design and work entry are bounded to the investigation evidence available.

**Failure signals**

- `as-built` label is treated as actual truth;
- geometric scan is assumed to reveal material or load path;
- archive drawing and scan are merged without conflict rows;
- new opening result silently updates only one model view.

**Reopen**

New opening, survey, scan registration change, material test, discovered utility or changed intervention scope.

## AC-BDPF-06 — Construction phasing in an operating facility

**Given**

A hospital wing must be refurbished while adjacent clinical services remain active. Temporary routes, isolation, utilities, infection-control barriers, logistics, emergency response and commissioning transitions affect permanent design.

**When**

- `BDPF.4` captures operating, construction, emergency and maintenance scenarios;
- `BDPF.5/6` treats temporary and permanent flows/interfaces as architecture-bearing where they change structures;
- `BDPF.6A–7` compares phasing-compatible configurations and records PAD consequences;
- `BDPF.9` routes actual work-entry readiness/gates to `A.15.5/A.21`;
- `BDPF.11` returns field/coordination changes to decisions and methods.

**Passing result**

BDPF governs architecture and decision relations, while the actual schedule, method statements, permits and performed work remain direct work/authority objects. Temporary structures have source, evidence and removal/transition conditions.

**Failure signals**

- BDPF pattern list is used as construction WorkPlan;
- a phasing diagram is treated as work authorization;
- temporary structure is absent from PAD because it is «not permanent»;
- gate pass is inferred from checklist/signature.

**Reopen**

Changed operational availability, infection-control rule, logistics route, temporary works design, resource readiness or field condition.

## AC-BDPF-07 — Machine-readable check passes but engineering claim remains open

**Given**

An IFC model passes an IDS rule set checking required objects, classifications, properties and selected clearances. A dashboard shows green and a team claims «model and design comply».

**When**

- `BDPF.10` records exact carrier/rule editions, check run work, checked predicates and unvalidated structure;
- `BDPF.8` identifies which atomic information claims the result supports;
- `BDPF.9` refuses to infer gate passage unless A.21 relation exists;
- `BDPF.12` evaluates projection/owner/non-overread coordinates.

**Passing result**

The green result is admitted only for encoded information requirements within scope. Performance, constructability, actual installation, fire/safety, legal compliance and PAD adequacy remain with direct owners.

**Failure signals**

- rule pass is evidence of all engineering correctness;
- checked model edition is not pinned;
- tool execution is not recorded as work;
- absent properties are repaired without source/decision return;
- dashboard state is called `GateDecision=pass` without A.21 relation.

**Reopen**

Changed model, rule set, schema, mapping, tool interpretation, project information requirement or governing claim.

## AC-BDPF-08 — Groundwater source change and selective impact

**Given**

Updated investigations show a higher design groundwater condition after foundation/basement PAD, calculations and drawings exist.

**When**

`BDPF.11` creates an impact trace from the changed source to affected source-use records, assumptions, foundation/waterproofing/uplift/temporary works structures, evidence traces and projections.

**Passing result**

Affected claims become suspect with direct owners and interim-use limits. Unrelated structures remain usable when no impact is supported. The PAD reopens only where the changed condition changes basis or accepted loss.

**Failure signals**

- whole project is declared invalid;
- change is ignored because document status is approved;
- only drawing notes are updated;
- new calculation is produced without updating source/currentness and PAD relations.

**Reopen**

Further investigation, revised hydrological model, changed basement depth, construction sequence or mitigation candidate.

## AC-BDPF-09 — Repeated comments become a method-improvement question

**Given**

Across several decisions reviewers repeatedly note that alternatives were considered only after one variant was detailed, and evidence appears as unscoped calculation lists.

**When**

- `BDPF.11` aggregates occurrences without blaming individuals;
- `E.22` frames evaluation of the design-decision method;
- a proposed change adds early candidate minimum envelopes and claim-specific evidence traces;
- `E.23` changes one method version and evaluates future decisions through `BDPF.12` and pilot metrics.

**Passing result**

Improvement is claimed only after re-evaluation shows better candidate trace/evidence-exit coordinates while protected trade-offs—time, cognitive load and unnecessary documentation—remain acceptable.

**Failure signals**

- a new checklist/template is itself called improvement;
- comment count is used as direct quality measure without scope;
- method change is mandated from one anecdote;
- no object version or reevaluation exists.

**Reopen**

New evidence of failure, adverse workload/lead-time effects, changed decision family or framework edition.

## AC-BDPF-10 — External-review package without authority overread

**Given**

A project team prepares a compact package for a named external review. PAD, ADR, models, calculations, reports and approvals exist at different editions.

**When**

- `BDPF.7B` creates a reader-specific package with exact refs and missingness;
- `BDPF.10` checks represented/lost structures and editions;
- `BDPF.12` evaluates decision adequacy for `relianceBearingExternalReview`;
- `BDPF.9` points to the actual project/regulatory review gate or keeps the result as readiness/adequacy only.

**Passing result**

The package is navigable and current, but its status is not confused with external acceptance. Direct evidence, assurance, compliance and authority relations remain visible; a missing below-floor coordinate blocks only the stated use.

**Failure signals**

- package completeness is treated as decision adequacy;
- folder/current status is used instead of edition pins;
- external-review scheduling is gate pass;
- high ADA values are called approval;
- restricted or missing evidence is hidden.

**Reopen**

Any source PAD/evidence/model/publication edition, review scope, authority rule, access boundary or external finding changes.

---

# Support Maps And Package Records

Support maps ниже не являются обязательной последовательностью применения. Открывайте их, когда `Relations`, low-value evaluation row, source-return condition, wording problem или edition question указывает на конкретную карту.

## Built-Asset Design Precision Restoration And Owner Map

Используйте карту, когда одно слово начинает одновременно выполнять ontology, evidence, decision, authority, publication or work function. Сначала восстановите текущий kind/relation/use; затем примените direct owner. Не исправляйте проблему заменой одного русского/английского термина другим.

| Trigger wording | Что сначала восстановить | Direct FPF/BDPF owner | Blocked stronger reading |
| --- | --- | --- | --- |
| `объект`, `ОКС`, `здание`, `сооружение` | Physical `U.System`/holon, boundary, environment and current context | `A.1`, `A.1.1`, `B.1.2`, `BDPF.1` | Name, card, parcel, model or documentation package is not the physical asset. |
| `площадка`, `участок`, `территория`, `посадка` | Physical site, claim-specific delimitation, site structure/characteristic or placement relation | `A.1`, `A.1.1`, `B.1.2`, `E.10.D2`, `BDPF.1A` | Parcel id, plan line, survey/report, site score or footprint is not the physical site or general suitability proof. |
| `система` | Is this an acting physical/operational system, system concept, engineering subsystem, information system, description or source label? | `A.1`, `BDPF.5`, `A.6.F`, `C.30.P` | Every organized set or diagram is not a `U.System`. |
| `архитектура` | Selected structures of which holon, in which context, under which question? | `A.22`, `C.30`, `C.30.P`, `BDPF.6` | Diagram, BIM, style, approval or document set is not architecture. |
| `структура` | Structure kind, bearer, selected/expected/represented/actual state and governing relation | `A.22`, `C.30.ASV`, `C.33`, `C.34` | Any hierarchy, layer, list or visual grouping is not automatically architecture structure. |
| `раздел`, `дисциплина` | Description/publication scope, role assignment and represented structure | `E.17`, `A.2.1`, `BDPF.10` | Section boundaries are not necessarily system or architecture boundaries. |
| `исходные данные`, `источник` | Source carrier, extracted signal, source-use relation, edition/currentness and admissible use | `G.2`, `G.11`, `BDPF.3/3B` | File presence does not create a requirement, evidence or decision. |
| `требование` | Requirement/commitment/constraint/source claim, holder, scope, validity and receiving structure question | `A.2.8`, `A.6.B`, local normative owner, `BDPF.3A` | Requirement wording does not select solution or prove compliance. |
| `ограничение` | Law/constraint/admissibility/gate/check/decision limit and current scope | `A.6.B`, `A.20`, `A.21`, direct domain owner | Any negative sentence is not one generic constraint kind. |
| `сценарий` | Source-bounded use, hazard, maintenance, construction or test scenario; role/time/condition | `BDPF.4`, `C.28`, `A.15` as applicable | Scenario is not evidence, WorkPlan or realized event by narration. |
| `концепция` | Use concept, system concept, candidate architecture or publication label | `BDPF.4`, `BDPF.5`, `C.30`, `C.32` | Concept is not PAD, proof or complete specification. |
| `вариант`, `опция`, `альтернатива` | Candidate configuration, retained set member, local OptionSet member or rejected alternative | `BDPF.6A`, `BDPF.6C`, `C.11`, `G.5` | Any different drawing/file is not a structurally distinct candidate. |
| `решение`, `проектное решение` | PAD relation, local choice, detailed design move, status/act or record | `C.32.PAD`, `C.11`, `BDPF.7`, `C.2.P` | ADR, selected set, approval, calculation or drawing is not PAD by label. |
| `обоснование`, `доказано` | Atomic claim, evidence path, assurance context or proof/inference claim | `A.10`, `B.3`, `C.6` when admitted/current, `BDPF.8` | A calculation, citation, expert opinion or file count does not support every claim. |
| `соответствует`, `compliant` | Applicable rule/edition, claim scope, evidence, assurance and decision authority | direct regulatory/project owner, `A.10`, `B.3` | Model/rule check, signature or status is not general compliance. |
| `безопасно` | Hazard/value claim, affected holons, evidence, causal basis, assurance and authority | `D.1–D.5`, `A.10`, `B.3`, `C.28` | Safety wording cannot be generated by PAD, gate or model pass alone. |
| `качество`, `эффективность`, `надёжность`, `гибкость` | Characteristic/Q-Bundle, bearer, scale, evidence and use | `C.16.Q`, `C.25`, `A.19.ECS`, `BDPF.6B` | Broad quality word is not a score, criterion or assurance level. |
| `оценка`, `score`, `рейтинг` | Measurement/eval result, scale, comparator, selection or adequacy coordinate | `C.16`, `A.19.CPM`, `BDPF.6B/6C/12` | Score does not choose, decide, approve or prove. |
| `готово`, `readiness` | Adequacy, work-entry readiness, gate decision, publication state or cue | `A.19.SPR`, `A.15.5`, `A.21`, `BDPF.9/12` | Green tile or checklist completion is not gate passage. |
| `согласовано`, `утверждено`, `одобрено` | Role assignment, speech act, status source, decision relation and effective window | `A.2.1`, `A.2.9`, `A.15.4`, `BDPF.7` | Signature/status does not prove technical adequacy or performed work. |
| `роль`, `ответственный` | `U.Role`, `U.RoleAssignment`, holder, context, window and responsibility/authority claim | `A.2`, `A.2.1`, `A.2.8`, `A.2.9` | Job title or name in a table is not an effective role assignment. |
| `метод`, `процесс`, `workflow`, `этап` | `U.Method`, MethodDescription, transformation flow, WorkPlan, performed Work or presentation order | `A.3.1`, `A.3.2`, `E.18`, `A.15`, `BDPF.2` | Arrow list, stage label or document route is not performed work or universal method. |
| `BIM`, `IFC`, `цифровой двойник`, `модель` | Description/view/carrier, schema/exchange, actual-state evidence relation and EntityOfConcern | `C.30.AD.BA`, `C.2.P`, `BDPF.10` | Model is not asset, PAD, evidence sufficiency, current actual state or work. |
| `вид`, `схема`, `чертёж` | Viewpoint, view, publication carrier and captured/lost structure | `E.17.0`, `C.30.ASV`, `C.33` | View shape does not settle architecture or correspondence. |
| `интерфейс`, `стык`, `подключение` | Module interface, functional port, spatial crossing, protocol, service relation or publication interface | `A.6.RSIR`, `A.6.M`, `C.30.TFS-REL`, direct owner | Any adjacency/contact is not one generic interface relation. |
| `функция`, `назначение` | Functioning relation, capability, role, method, transformation effect or mathematical function | `A.6.F`, `A.2.2`, `A.3.4`, `BDPF.4/5` | Function wording does not name a bearer or prove realization. |
| `clash`, `коллизия`, `замечание`, `issue` | Observation/source carrier, represented-structure conflict, claim defect or change trigger | `BDPF.11`, `C.32.FAIL`, `C.33`, `C.34` | Issue does not establish root cause or falsify PAD automatically. |
| `изменение`, `влияние` | Changed source/condition, affected relation path, suspectness, causal claim or performed transformation | `BDPF.11`, `A.3.4`, `C.28`, `G.11` | Temporal succession or issue linkage is not causal proof. |
| `фактическое состояние` | Actual structure/state supported by observation, evidence and time window | `A.10`, `C.27`, `C.33`, `C.34` | Latest model or report is not actual state without an observation/source relation. |

### Map use rule

```text
trigger phrase
→ recover EntityOfConcern / relation / claim kind / use / scope
→ select direct governing pattern
→ preserve any local source label only as a bounded alias
→ rewrite the project sentence and state blocked overread
```

If no direct owner can be selected because the material is still under-articulated, preserve it as a cue/problem-side record rather than forcing it into BDPF.

---

## Name And Edition Route

```text
NameCard@BuiltAssetDesignPrinciplesFramework:
  governedValueRef: the FPF-grounded domain principle framework whose selected pattern set supports architecture-significant built-asset design-decision development
  governingPatternRef: E.4.DPF with F.18 naming discipline
  boundedContextRef: built-asset design and expert/technical support in the project design contour
  techName: BuiltAssetDesignPrinciplesFramework
  plainPublicName: Built Asset Design Principles Framework
  russianWorkingName: рамка принципов разработки, фиксации и сопровождения архитектурно значимых проектных решений для объектов капитального строительства
  publicPrefix: BDPF
  candidateNameRows:
    - Built Asset Design Principles Framework: selected; concise and stable across building, structure and infrastructure cases
    - Built Asset Architecture Decision Framework: rejected; too narrow because source intake, use/system concept, evidence, projection and feedback are also governed
    - Built Environment Design Principles Framework: rejected; too broad because urban policy, operation and all built-environment practice are outside scope
    - Design Principles Framework: rejected; domain head is not recoverable and legacy DPF alias is collision-prone
  selectionRationale: keeps the domain bearer visible while leaving exact pattern scope to the subtitle, front matter and architecture-significance test
  blockedNameOverread:
    - name does not make the package a universal building-design method, normative standard, ontology or statutory review procedure
    - `Design` does not mean all discipline design work is governed by this package
    - `Principles Framework` does not elevate local record labels into FPF Core kinds
  legacyAliasPolicy: DPF.* is read-only for migrated records; new refs use BDPF.*
  lineageRefs:
    - BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4
    - BuiltAssetDesignPrinciplesFramework@2026-07-12-v0.5
    - BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  refreshCondition: rename only if domain boundary, intended reader interpretation, collision evidence or FPF framework-family naming changes
```

```text
NameAndEditionRoute@BuiltAssetDesignPrinciplesFramework:
  publicPackageName: Built Asset Design Principles Framework
  russianWorkingName: рамка принципов разработки, фиксации и сопровождения архитектурно значимых проектных решений для объектов капитального строительства
  frameworkFamily: Domain Principle Framework
  editionRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  supersedesEditionRef: BuiltAssetDesignPrinciplesFramework@2026-07-12-v0.5
  priorSupersessionRefs:
    - BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4
  localPatternPrefix: BDPF
  legacyAliasPolicy: DPF.* aliases remain read-only migration aliases; do not mint them in new records
  editionState: v0.5.1-content-and-architecture-revision
  localUseStatus: locallyUsableWithVisibleLimits for one bounded decision pilot
  notYetStatus: stable; statutory; enterprise-wide reliance-bearing framework
  fpfCoreEditionRef: FPFCorePatternSet@July2026
  sourceCurrentnessBoundary: see Source Use And Refresh Map
  currentnessWindow: until a relevant FPF Core owner, source standard, regulatory/project source, pilot result, E.21 result or package-adequacy coordinate changes
```

```text
FrameworkEditionDependencyRecord@BuiltAssetDesignPrinciplesFramework:
  frameworkEditionRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  dependsOnEditionRefs:
    - FPFCorePatternSet@July2026
  dependencyReason: BDPF specializes and composes current FPF owners for built-asset system framing, P2S, architecture questions, candidate synthesis, characteristics/eval, PAD/ADR/ADA, evidence, readiness, architecture descriptions, feedback, DPF package quality and refresh
  compatibilityBoundary: BDPF may add domain problem-solution patterns, local records, cases and source-use prompts but may not redefine Core U-kinds or the semantics of C.32.P2S, C.32.PAD, C.32.ADR, C.32.ADA, A.10, A.15.5, A.21, C.30.AD.BA, E.4.DPF or E.21
  deprecationOrSupersessionRefs:
    - BuiltAssetDesignPrinciplesFramework@2026-07-12-v0.5 is superseded for new pattern use
    - BuiltAssetDesignPrinciplesFramework@2026-07-02-draft-v0.4 remains superseded historical lineage
  refreshConditionRefs:
    - relevant FPF Core edition change
    - source-map currentness trigger
    - failed acceptance case or pilot
    - E.21 coordinate below declared floor
    - E.4.DPF.DA package coordinate below declared floor
  e53ConformanceNote: dependency points from BDPF toward FPF Core; FPF Core has no reverse dependency on BDPF
```

```text
FrameworkPackageManifest@BuiltAssetDesignPrinciplesFramework:
  frameworkEditionRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  principleFrameworkArchitectureDecisionRef: PFAD-BDPF-2026-07-13-001
  selectedPatternSetPublicationRef: BDPF.1 through BDPF.12 including BDPF.1A, BDPF.3A, BDPF.3B, BDPF.6A, BDPF.6B, BDPF.6C, BDPF.7A and BDPF.7B
  relationRecordRefs: PFR-BDPF-CORE-DEP-001 through PFR-BDPF-PRODUCED-CARRIER-001
  dependencyAndEditionRecordRefs:
    - FrameworkEditionDependencyRecord@BuiltAssetDesignPrinciplesFramework
    - NameAndEditionRoute@BuiltAssetDesignPrinciplesFramework
  editionStatus: v0.5.1; locallyUsableWithVisibleLimits
  deprecationOrSupersessionRefs:
    - v0.5 superseded for new use; v0.4 remains prior historical lineage; migration notes below
  sourcePackRefs: SourceUseAndRefreshMap@BuiltAssetDesignPrinciplesFramework
  qualityEvidenceRefs:
    - DPFPackageAdequacyEvaluation@BuiltAssetDesignPrinciplesFramework-v0.5.1
    - E21-BDPF-3A-v0.5.1
    - E21-BDPF-7-v0.5.1
    - E21-BDPF-10-v0.5.1
    - E21-BDPF-12-v0.5.1
    - pattern-form structural checks in this carrier
    - no field-transfer or enterprise-adoption evidence yet
  refreshPlanOrCurrentnessRefs: RefreshRoute@BuiltAssetDesignPrinciplesFramework
  firstEntryCarrierRefs:
    - Table of Contents
    - Readme — First Practical Entries
    - Pattern Index
  blockedRuntimeOrBuildReading: this manifest is a declarative publication/package index, not a build manifest, workflow, API, work plan or authority record
```

### Migration from v0.5 to v0.5.1

| v0.5 locus | v0.5.1 disposition | Migration action |
| --- | --- | --- |
| Domain statement covering all built-asset design | Narrowed to architecture-significant, cross-disciplinary decision development | Apply the Architecture-significance test; use direct discipline methods outside this boundary. |
| Package architecture implicit in front matter/relations | Explicit `PFAD-BDPF-2026-07-13-001` | Point package and future split carriers to this decision; do not infer architecture from file order alone. |
| Pattern Index listed records without pattern roles/Core owners | Expanded role/owner index | Migrate reader links; no project decision semantics change. |
| CamelCase structure-family labels in `BDPF.6` | Recast as lower-case discovery cues | Resolve live cues to exact project `ArchitectureStructureKindRef`; do not preserve the old labels as kinds. |
| Candidate rows focused on alternatives but not internal coherence | Coherence, scenario coverage and temporary/permanent-state fields added | Repair only candidate palettes relied on for comparison or PAD. |
| Criteria rows distinguished objective/constraint/telemetry informally | Exact `criterionRole` and aggregation-admissibility fields added | Pin roles before comparison; do not retroactively treat telemetry/preferences as evidence or dominance. |
| `BDPF.9 directOwnerKind` | Replaced by `directOwnerRelationFamily` | Migrate values by relation family; no new Core kind is minted. |
| `BDPF.10` representation rows | Architecture-owned-invariant coverage and correspondence status added | Repair decision projections used for review/handoff; mark unrepresented invariants explicitly. |
| `BDPF.11` broad impact rationale | Direct-consumer, structural-coupling and derived-episteme impact paths added | Re-run only for open or reliance-bearing change cases. |
| Package source table citations without stable local ids | Added `SRC-BDPF-*` source-use ids | Update SoTA sections and future impact traces to cite source-use ids. |
| Priority E.21 evaluations listed as future work | Four complete package-carried evaluations materialized | Use them as authoring-quality evidence only; they are not field-performance proof. |
| Support maps before acceptance cases | Acceptance probes moved before support records | No semantic migration; improves working-reader flow. |

Existing project records are not invalid by edition change. Use `BDPF.11` to decide `noImpactSupported`, local field repair, re-evaluation or reopen.

### Migration from v0.4

| v0.4 locus | v0.5/v0.5.1 disposition | Migration action |
| --- | --- | --- |
| Package front matter and P2S spine | Preserved and tightened | Replace June-2026 dependency with the package-pinned July-2026 FPF edition; use v0.5.1 boundaries. |
| `BDPF.1..8`, `10`, `11` short schemas | Superseded by full `E.8` action-guiding pattern bodies | Preserve project instances where fields map; add missing context/use/source-return/checks. |
| `BDPF.3A` NQD-like state list | Retained only as optional descriptive posture, not mandatory process sequence | Do not infer workflow/stage order from state labels. |
| `BDPF.3B` package | Preserved as composition pattern | Add package-level claim, missingness, readiness-owner and non-use checks. |
| `BDPF.6B` criteria/eval | Preserved and expanded | Add bearer, scale, missingness, counter-characteristic and proxy-risk discipline. |
| `BDPF.6C` selected set | Renamed reader-facing result to `RetainedArchitectureSetPublication@Project` | Keep existing refs through alias note; do not treat as PAD. |
| `BDPF.7` PAD | Preserved under exact `C.32.PAD` owner | Add role/speech-act split, method docking, concern rows and edition/window. |
| `BDPF.7A/7B` | Preserved as publication/navigation patterns | Add reader use, source/edition pins, missingness and no-new-semantics checks. |
| `BDPF.9 DesignReadinessGate` with local values | Semantically replaced | Use `BDPF.9 BuiltAssetDesignReadinessUse`; route actual gate decisions to A.21 values `abstain|pass|degrade|block`, and work-entry readiness to `A.15.5`. Existing `passWithReservations` migrates to A.21 `degrade` only when a true A.21 gate relation exists; otherwise retain direct-owner disposition. |
| `BDPF.10` projection | Preserved and expanded | Separate architecture-description use, documentation projection and machine-validation projection; add selected/expected/represented/actual distinction. |
| Checklist and pilot sections | Retained as support, not pattern substitutes | Use pattern checklists first; package/pilot checklists do not prove pattern or project quality. |
| No decision-adequacy DPF pattern | New `BDPF.12` | Evaluate existing PADs through Core `C.32.ADA` coordinate set before handoff/reliance. |
| v0.4 PFR/source/quality sections | Superseded by records below | Re-pin relation functions, source currentness and package evaluation to v0.5. |

Existing project records are not invalid merely because the framework edition changed. They become **migration candidates**; use `DesignChangeImpactTrace@Project` to decide whether a record needs field repair, owner repair, re-evaluation or no impact.

---

## DPF Relation Records

The records below state load-bearing package relations. Ordinary pattern use does not require reading every record; use them for edition impact, owner routing, reuse and refresh.

| Relation id | Source → target | Relation function | Governing use |
| --- | --- | --- | --- |
| `PFR-BDPF-CORE-DEP-001` | BDPF v0.5.1 → FPF July 2026 | Framework edition dependency | Pin Core owners and block reverse dependency. |
| `PFR-BDPF-P2S-SPEC-001` | `BDPF.3/3A/3B` → `C.32.P2S` | Specialization | Built-asset source/problem-to-structure intake. |
| `PFR-BDPF-SYSTEM-FRAME-001` | `BDPF.1/4/5` → A.1/C.30 family | Specialization | Built-asset system/use/system-concept framing. |
| `PFR-BDPF-SITE-FRAME-001` | `BDPF.1A` → A.1/A.1.1/B.1.2/E.10.D2 | Specialization | Physical site frame, context-local boundaries and separate placement relation. |
| `PFR-BDPF-CANDIDATE-SPEC-001` | `BDPF.6/6A` → C.30/C.32 | Specialization | Architecture question and candidate palette. |
| `PFR-BDPF-EVAL-SPEC-001` | `BDPF.6B` → C.16/C.32.ACS/ACE | Specialization | Built-asset criteria and eval. |
| `PFR-BDPF-COMPARISON-001` | `BDPF.6C` → CPM/Selector/G.5/C.11 | Governing-pattern relation | Comparison, retained set, choice and PAD remain separate. |
| `PFR-BDPF-PAD-SPEC-001` | `BDPF.7` → `C.32.PAD` | Specialization | Built-asset PAD fields/checks. |
| `PFR-BDPF-PUBLICATION-001` | `BDPF.7A/7B` → `C.32.ADR`/E.17 | Publication relation | Decision projections and navigation packages. |
| `PFR-BDPF-EVIDENCE-001` | `BDPF.8` → `A.10` | Specialization | Claim-specific design evidence. |
| `PFR-BDPF-READINESS-001` | `BDPF.9` → A.15.5/A.21 | Governing-pattern relation | Route readiness wording to direct relation. |
| `PFR-BDPF-DESCRIPTION-001` | `BDPF.10` → C.30.AD.BA/C.33/C.34 | Specialization | PD/BIM/view projection and loss/correspondence. |
| `PFR-BDPF-FEEDBACK-001` | `BDPF.11` → C.32.FAIL/E.23/G.11 | Governing-pattern relation | Impact, repair, method improvement and currentness. |
| `PFR-BDPF-ADA-SPEC-001` | `BDPF.12` → `C.32.ADA` | Specialization | Built-asset declared-use decision adequacy. |
| `PFR-BDPF-SOURCE-REUSE-001` | Source map → BDPF patterns | Source or decision reuse | Adopt bounded source payload and currentness. |
| `PFR-BDPF-REFRESH-001` | Quality/source/field triggers → BDPF edition | Quality framing, evaluation, or improvement | Route smallest repair, re-evaluation and edition refresh. |
| `PFR-BDPF-CARRIER-001` | BDPF pattern set → this all-in-one file | Publication relation | Publish selected pattern set and support records. |
| `PFR-BDPF-PFAD-001` | PFAD-BDPF-2026-07-13-001 → BDPF v0.5.1 | Architecture decision link | Bind selected pattern set, relation groups, publication unit and qualification boundary. |
| `PFR-BDPF-PRODUCED-CARRIER-001` | AI-assisted produced carrier → steward/project admission use | Produced-carrier admission | Permit review/pilot preparation without granting unreviewed reliance. |

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-PFAD-001
  sourceRef: PFAD-BDPF-2026-07-13-001
  targetRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  relationFunction: Architecture decision link
  governedUse: bind the selected pattern set, relation groups, publication unit, quality route and qualification limits for this edition
  directGoverningPatternRef: E.4.PFAD and E.4.PFR
  dependencyOrEditionEffect: this edition is interpreted under the PFAD; file order or headings do not independently define framework architecture
  blockedStrongerReading: PFAD does not prove domain completeness, field utility or release readiness
  refreshOrSupersessionCondition: framework content boundary, selected pattern set, relation structure, carrier architecture or qualification changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-PRODUCED-CARRIER-001
  sourceRef: ProducedCarrierAdmissionNote@BuiltAssetDesignPrinciplesFramework-v0.5.1
  targetRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  relationFunction: Produced-carrier admission
  governedUse: distinguish AI-assisted carrier production from steward admission, field applicability and reliance-bearing publication
  directGoverningPatternRef: C.35, C.33, E.17 and E.4.PFR
  dependencyOrEditionEffect: none on FPF Core; establishes only the allowed use of this produced carrier
  blockedStrongerReading: generated/revised fluency does not establish source correctness, human approval, engineering adequacy or enterprise release
  refreshOrSupersessionCondition: source carrier, production method, steward review, quality result or admission use changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-CORE-DEP-001
  sourceRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  targetRef: FPFCorePatternSet@July2026
  relationFunction: Framework edition dependency
  governedUse: BDPF patterns reuse FPF Core owners for holons, contexts, roles, methods/work, P2S, architecture, characteristics/eval, PAD/ADR/ADA, evidence, readiness/gates, publication, quality and refresh
  directGoverningPatternRef: E.4.PFR and E.5.3
  dependencyOrEditionEffect: BDPF depends on Core; Core has no reverse dependency
  blockedStrongerReading: not permission to redefine Core kinds, scales, gate values, decision semantics or pattern form
  refreshOrSupersessionCondition: inspect every affected relation when a cited Core pattern edition changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-P2S-SPEC-001
  sourceRef: BDPF.3, BDPF.3A and BDPF.3B
  targetRef: C.32.P2S
  relationFunction: Specialization
  governedUse: built-asset source carriers and problem pressure are carried into architecture structuring needs, unknown/candidate structures and receiving owners
  directGoverningPatternRef: C.32.P2S
  dependencyOrEditionEffect: BDPF inherits P2S state/owner boundaries and adds built-asset source, use and initial-analysis prompts
  blockedStrongerReading: BDPF does not define one mandatory project workflow and source signals do not select architecture
  sourceReturnCondition: return to C.32.P2S when the relation is no longer built-asset-specific or when actual-structure feedback/work positions become load-bearing
  refreshOrSupersessionCondition: refresh when C.32.P2S slots, source-use practice or project source families change
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-SYSTEM-FRAME-001
  sourceRef: BDPF.1, BDPF.4 and BDPF.5
  targetRef: A.1, A.1.1, A.6.F, C.30 and C.30.TFS-REL
  relationFunction: Specialization
  governedUse: frame the physical built asset, use scenarios and system concept before architecture candidate work
  directGoverningPatternRef: A.1 for system identity and C.30 for architecture claims
  blockedStrongerReading: local frames/records are not new U-kinds, requirements authority, PAD or evidence
  sourceReturnCondition: return to direct Core owner when system identity, function, transformation flow or architecture claim becomes general rather than built-asset-local
  refreshOrSupersessionCondition: refresh when holon boundary, use/system-concept source practice or Core function/architecture semantics change
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-CANDIDATE-SPEC-001
  sourceRef: BDPF.6 and BDPF.6A
  targetRef: C.30, C.30.ILC and C.32
  relationFunction: Specialization
  governedUse: identify a built-asset architecture question and synthesize structurally distinct candidate configurations or an honest stop reason
  directGoverningPatternRef: C.30 for grounded architecture question; C.32 for candidate synthesis
  blockedStrongerReading: structure-family prompts are not a completeness taxonomy; a candidate palette does not compare, select or decide
  sourceReturnCondition: return to C.30/C.32 when a local label hides the selected structure or candidate-synthesis claim
  refreshOrSupersessionCondition: refresh when architecture question, candidate-set or structural-information owner changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-EVAL-SPEC-001
  sourceRef: BDPF.6B
  targetRef: C.16, C.25, C.32.ACS and C.32.ACE
  relationFunction: Specialization
  governedUse: construct bearer-bound built-asset criteria rows and eval programs for candidate configurations
  directGoverningPatternRef: C.32.ACS and C.32.ACE
  preservationOrAdmissionRef: BuiltAssetArchitectureCriteriaSet@Project and BuiltAssetArchitectureEvalProgram@Project
  blockedStrongerReading: criteria/eval do not compare, select, decide, assure or prove beyond named claims
  sourceReturnCondition: return to C.16/A.19.ECS when scale, value meaning, missingness or comparability is defective
  refreshOrSupersessionCondition: refresh when characteristic, bearer, scale, evidence rule, proxy risk or candidate frame changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-COMPARISON-001
  sourceRef: BDPF.6C
  targetRef: A.19.CPM, A.19.SelectorMechanism, G.5 and C.11
  relationFunction: Governing-pattern relation
  governedUse: comparison basis, retained-set publication, selector outcome and local choice are routed to their distinct owners before PAD
  directGoverningPatternRef: A.19.CPM for comparison; G.5 for selected-set publication; C.11 for local choice
  blockedStrongerReading: retained set is not a PAD and a comparison table is not a choice or approval
  sourceReturnCondition: return to the exact owner when ordering, dominance, selector eligibility or local decision becomes current
  refreshOrSupersessionCondition: refresh when source candidate set, comparator, criteria/evidence or receiving use changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-PAD-SPEC-001
  sourceRef: BDPF.7
  targetRef: C.32.PAD
  relationFunction: Specialization
  governedUse: record one built-asset project architecture decision with selected/expected structures, trade-offs, losses, roles, method docking, concern exits and reopen conditions
  directGoverningPatternRef: C.32.PAD
  blockedStrongerReading: PAD is not ADR, approval, evidence, gate, WorkPlan, performed work or statutory decision by form
  sourceReturnCondition: return to C.32.PAD for general decision semantics and to direct evidence/authority/work owners for those claims
  refreshOrSupersessionCondition: refresh when PAD relation slots, candidate basis, role authority, structure or valid window changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-PUBLICATION-001
  sourceRef: BDPF.7A and BDPF.7B
  targetRef: C.32.ADR, E.17, E.17.AUD and E.24.PUB
  relationFunction: Publication relation
  governedUse: expose one existing PAD through reader-specific ADR projections and minimal decision-use navigation packages
  directGoverningPatternRef: C.32.ADR for ADR projection and E.17 for publication
  preservationOrAdmissionRef: architectureDecisionRef plus source/edition pins and declared loss
  blockedStrongerReading: readable, signed, complete-looking or repository-current carrier does not create PAD, evidence, approval, gate or authorization
  sourceReturnCondition: return to PAD and direct evidence/projection/authority sources whenever a publication claim becomes load-bearing
  refreshOrSupersessionCondition: refresh when PAD, reader use, record edition, source pin, loss or access boundary changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-EVIDENCE-001
  sourceRef: BDPF.8
  targetRef: A.10 and B.3
  relationFunction: Specialization
  governedUse: relate built-asset design claims to evidence paths, source/method/work, interpretation, scope, freshness, limitations and disposition
  directGoverningPatternRef: A.10
  blockedStrongerReading: evidence trace is not assurance, proof of the whole decision, compliance, approval, gate or work authorization
  sourceReturnCondition: return to A.10 for evidence relation and B.3 when named assurance is current
  refreshOrSupersessionCondition: refresh when claim, evidence, source/model edition, assumption, receiving use or time window changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-READINESS-001
  sourceRef: BDPF.9
  targetRef: A.15.5, A.21, E.17 and local authority owners
  relationFunction: Governing-pattern relation
  governedUse: classify built-asset readiness wording and publish a bounded use record pointing to the actual direct-owner relation
  directGoverningPatternRef: A.15.5 for work-entry readiness; A.21 for a true gate-decision relation
  blockedStrongerReading: BDPF.9 does not mint a second gate, custom gate lattice, proof, approval or performed work
  sourceReturnCondition: return to the direct owner when readiness, gate, publication or authority is the live claim
  refreshOrSupersessionCondition: refresh when profile, check set, intended work/use, gate decision, source/evidence or currentness changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-DESCRIPTION-001
  sourceRef: BDPF.10
  targetRef: C.30.AD.BA, C.33, C.34 and E.17
  relationFunction: Specialization
  governedUse: project selected/expected built-asset structures into PD/BIM/views and state captured/lost structure, correspondence and machine-validation limits
  directGoverningPatternRef: C.30.AD.BA
  preservationOrAdmissionRef: exact decision/structure refs, viewpoint, carrier edition, captured/lost structure and source-return condition
  blockedStrongerReading: BIM/IFC/drawing/table/check result is not the asset, architecture, PAD, proof, gate or actual structure
  sourceReturnCondition: return to PAD/architecture source and C.33/C.34 whenever loss or correspondence affects reliance
  refreshOrSupersessionCondition: refresh when decision, viewpoint, carrier/schema/rule edition, representation or actual-structure evidence changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-FEEDBACK-001
  sourceRef: BDPF.11
  targetRef: C.32.FAIL, E.23 and G.11
  relationFunction: Governing-pattern relation
  governedUse: route source changes, review findings, representation conflicts and repeated defects to impact review, architecture repair, method improvement or currentness refresh
  directGoverningPatternRef: C.32.FAIL for architecture repair cue; E.23 for actual improvement; G.11 for currentness
  blockedStrongerReading: issue/comment/change trace does not prove invalidity, root cause, improvement or universal method defect
  sourceReturnCondition: return to the smallest direct owner named by the impact row
  refreshOrSupersessionCondition: refresh when trigger, affected relation, method version, evaluation or cross-case defect evidence changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-ADA-SPEC-001
  sourceRef: BDPF.12
  targetRef: C.32.ADA, E.22 and E.23
  relationFunction: Specialization
  governedUse: evaluate one built-asset PAD for one declared use with the complete C.32.ADA coordinate set, shared values, no average and targeted repair
  directGoverningPatternRef: C.32.ADA
  preservationOrAdmissionRef: BuiltAssetArchitectureDecisionAdequacyEvaluation@Project
  blockedStrongerReading: adequacy value is not evidence, assurance, approval, gate, compliance decision, work readiness or pattern quality
  sourceReturnCondition: return to the coordinate-specific direct owner for repair and to E.22/E.23 for improvement framing/loop
  refreshOrSupersessionCondition: refresh when declared use, decision/projection edition, coordinate evidence, floor or repair result changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-SOURCE-REUSE-001
  sourceRef: SourceUseAndRefreshMap@BuiltAssetDesignPrinciplesFramework
  targetRef: BDPF.1 through BDPF.12
  relationFunction: Source or decision reuse
  governedUse: project and external source rows contribute bounded payload to pattern problem frames, solution moves, examples, boundaries and refresh triggers
  directGoverningPatternRef: G.2
  preservationOrAdmissionRef: each source row states adopted payload, rejected overread and currentness trigger
  blockedStrongerReading: bibliography length, standard title or authority citation does not make BDPF normative, complete, evidential or jurisdictionally applicable
  sourceReturnCondition: return to exact source and project applicability owner whenever a source-supported claim becomes load-bearing
  refreshOrSupersessionCondition: refresh when source edition, applicability, rival source, adopted payload or currentness changes
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-REFRESH-001
  sourceRef: E.21 pattern results, E.4.DPF.DA package result, SourceUseAndRefreshMap, field pilot evidence and BDPF.11 impact records
  targetRef: BuiltAssetDesignPrinciplesFramework@current-edition
  relationFunction: Quality framing, evaluation, or improvement
  governedUse: select the smallest pattern, relation, carrier, source-row or package repair; re-evaluate the changed version; publish edition/currentness disposition
  directGoverningPatternRef: E.22 for framing, E.23 for improvement, E.21 for pattern quality, E.4.DPF.DA for package adequacy and G.11 for currentness
  blockedStrongerReading: a refresh trigger does not prove package invalidity, improvement, release readiness or mandatory edition bump
  sourceReturnCondition: return to the exact low coordinate, changed source payload, field finding or affected relation
  refreshOrSupersessionCondition: close only after owner-specific disposition, re-evaluation and edition/supersession publication
```

```text
PatternFrameworkRelationRecord@BuiltAssetDesignPrinciplesFramework:
  relationId: PFR-BDPF-CARRIER-001
  sourceRef: BDPF.1 through BDPF.12 plus package records
  targetRef: BuiltAssetDesignPrinciplesFramework-improved-v0.5.1.md
  relationFunction: Publication relation
  governedUse: publish a navigable all-in-one DPF carrier with front door, full pattern bodies, support maps, relation records, source map, cases, quality result and refresh route
  directGoverningPatternRef: E.4.DPF, E.11 and E.17
  preservationOrAdmissionRef: FrameworkCarrierStructureCapture@BuiltAssetDesignPrinciplesFramework
  blockedStrongerReading: this file is not the domain, physical asset, source pack, work plan, regulatory act or evidence that patterns work in the field
  sourceReturnCondition: return to pattern body, FPF Core owner, source map or project record when a carrier summary becomes load-bearing
  refreshOrSupersessionCondition: publish a new package edition when selected pattern set, relation structure, source basis, quality result or currentness changes
```

---

## Source Use And Refresh Map

> **Map date:** 2026-07-13.  
> **Owner:** `G.2` for source-set/source-use discipline; `G.11` for currentness and refresh.  
> **Boundary:** this map records package-pinned adopted payload for BDPF authoring. It does not claim that each pin is the latest available edition, and it does not determine project applicability, jurisdictional compliance, evidence sufficiency or contractual authority. Refresh triggers govern any later verification.

### Source-use rules

1. Cite a source by exact identifier, edition/date and source owner when its content changes a pattern, project claim or evaluation row.
2. State the **adopted payload**; do not treat a title or citation as authority for unrelated claims.
3. State the **blocked overread**: what the source does not make true.
4. Separate framework-authoring source use from project evidence use. A standard can inform BDPF wording while a concrete project still needs an applicability/evidence relation.
5. Refresh on exact trigger. «Use latest» without an edition/currentness route is non-conformant.
6. Preserve rival/local sources when they materially change candidate structures, criteria, evidence or decision use; one standard family is not the whole built-asset design domain.

### Framework and architecture source rows

| Source-use id and package pin | Source use in BDPF | Adopted payload | Main loci | Blocked overread | Refresh trigger |
| --- | --- | --- | --- | --- | --- |
| `SRC-BDPF-FPF-JUL2026` — `FPF Core Conceptual Specification@July2026` | Normative dependency for this DPF edition | Holon/context/role/method/work distinctions; P2S; grounded architecture; PAD/ADR/ADA; evidence; gate/readiness; publication; DPF package form; evaluation/improvement/refresh | Entire package | BDPF may not redefine Core or make Core depend backward on BDPF | Any cited Core pattern semantic or edition change |
| `SRC-BDPF-15288-2023` — `ISO/IEC/IEEE 15288:2023` | Systems life-cycle source family | Stakeholder/system concerns, lifecycle processes, verification/validation and information-management pressures; problem/source prompts, not a BDPF workflow | `BDPF.1–5`, `BDPF.7–11` | Process names do not become BDPF stages, performed work or proof of conformance | Edition/corrigendum or adopted-payload change |
| `SRC-BDPF-24748-2-2024` — `ISO/IEC/IEEE 24748-2:2024` | Guidance for applying 15288 | Iterative/recursive life-cycle management and method-description boundary pressure | `BDPF.2`, pilot and refresh guidance | No mandatory project method, WorkPlan or enactment evidence | Edition/corrigendum or relation-to-15288 change |
| `SRC-BDPF-24774-2021` — `ISO/IEC/IEEE 24774:2021` | Process-description source | Purpose/outcome/activity/information-item and process-view discipline for readable method descriptions | `BDPF.2` | Process description is not `U.Method`, WorkPlan, performed Work or authority | Edition/corrigendum or FPF method-owner change |
| `SRC-BDPF-42010-2022` — `ISO/IEC/IEEE 42010:2022` | Architecture-description source | Architecture descriptions, concerns, viewpoints, views, correspondences, rationale and stakeholder reading | `BDPF.5–7`, `BDPF.10`, `BDPF.12` | Description/view is not architecture, PAD or evidence | Edition/corrigendum; FPF `C.30.AD/ASV` change |
| `SRC-BDPF-42030-2019` — `ISO/IEC/IEEE 42030:2019` | Package-pinned architecture-evaluation source | Evaluation framing, stakeholder concerns, criteria and evidence-oriented evaluation pressure | `BDPF.6B`, `BDPF.6C`, `BDPF.12` | No universal score, BDPF gate or project approval | Published-edition or adopted-payload change |

### Built-asset information and exchange source rows

| Source-use id and package pin | Adopted payload | Main loci | Blocked overread | Refresh trigger |
| --- | --- | --- | --- | --- |
| `SRC-BDPF-19650-1-2018` — `ISO 19650-1:2018` | Concepts/principles for information management using BIM; container status/currentness and collaborative information-use pressure | `BDPF.3B`, `BDPF.7B`, `BDPF.10`, `BDPF.11` | Status does not establish engineering truth, PAD or actual state | Edition/corrigendum or project adoption-profile change |
| `SRC-BDPF-19650-2-2018` — `ISO 19650-2:2018` | Delivery-phase information management and exchange/approval-state context | `BDPF.2`, `BDPF.9`, `BDPF.10` | Milestone/status does not become gate, work occurrence or decision adequacy | Edition/corrigendum or project protocol change |
| `SRC-BDPF-19650-3-2020` — `ISO 19650-3:2020` | Operational information-management and source-return pressure | `BDPF.1`, `BDPF.4`, `BDPF.10`, `BDPF.11` | Operational model is not actual state without evidence/observation | Edition/corrigendum; lifecycle-scope change |
| `SRC-BDPF-19650-4-2022` — `ISO 19650-4:2022` | Information-exchange process and decision-point pressure | `BDPF.7B`, `BDPF.9`, `BDPF.10` | Exchange acceptance does not prove design or regulatory compliance | Edition/corrigendum or exchange-requirement change |
| `SRC-BDPF-19650-5-2020` — `ISO 19650-5:2020` | Security-minded information management and access-boundary prompts | `BDPF.7B`, `BDPF.10` | Security/access label does not decide architecture or evidence sufficiency | Edition/corrigendum or security-profile change |
| `SRC-BDPF-19650-6-2025` — `ISO 19650-6:2025` | Health-and-safety information-management prompts | `BDPF.3`, `BDPF.4`, `BDPF.8–11` | Information availability does not prove safe design or safe work | Edition/corrigendum or project-adoption change |
| `SRC-BDPF-16739-1-2024` — `ISO 16739-1:2024` | IFC schema/exchange and typed representation surface | `BDPF.10` | IFC file/schema is not asset, architecture, PAD, evidence sufficiency or complete correspondence | Edition/addendum or exchange-profile change |
| `SRC-BDPF-29481-1-2025` — `ISO 29481-1:2025` | Information Delivery Manual methodology/format for exchange requirements | `BDPF.2`, `BDPF.7B`, `BDPF.10` | IDM/process map is not performed work, PAD or proof of correct information | Edition/corrigendum or project IDM change |
| `SRC-BDPF-7817-1-2024` — `ISO 7817-1:2024` | Level-of-information-need distinctions | `BDPF.7B`, `BDPF.9`, `BDPF.10` | Level label is not universal maturity, adequacy score or evidence | Edition/corrigendum or project information-need change |
| `SRC-BDPF-IDS-1.0` — buildingSMART `IDS v1.0` | Machine-readable information-requirement/checking surface | `BDPF.10`, `BDPF.8`, `BDPF.9` | Pass covers encoded information requirements only; not general compliance, performance, PAD or gate | IDS spec, rule-set or tool-interpretation change |
| `SRC-BDPF-81346-PROJECTPIN` — project-pinned applicable `ISO/IEC 81346` part/edition | Reference-designation and structuring/reference relations | `BDPF.5`, `BDPF.10` | Code/name is not physical structure, architecture or asset identity by label | Project pin or applicable part/edition change |

### Project-specific source families

Every project row needs exact carrier, owner, edition/date, applicability scope and source-return condition. Labels below are source families, not an authoritative universal list.

| Project source family | Typical signal/use | Main receiving patterns | Non-admissible use |
| --- | --- | --- | --- |
| Project brief / design assignment / technical or technological assignment | value/use needs, constraints, capacities, scenario assumptions and required outputs | `BDPF.3/3B`, `BDPF.4`, `BDPF.5` | Does not select architecture or prove demand/performance. |
| Planning/site/land-use and jurisdictional materials | site placement, envelope, access, protected zones, external interfaces and rule applicability questions | `BDPF.3A`, `BDPF.6` | Carrier/list does not settle legal interpretation or spatial solution. |
| Utility connection conditions and operator requirements | capacity, connection point, boundary/interface, reliability or metering constraints | `BDPF.3A`, `BDPF.5`, `BDPF.6` | Does not prove internal engineering configuration adequacy. |
| Engineering surveys and investigations | geotechnical, environmental, geodetic, hydrological and existing-condition signals with uncertainty/currentness | `BDPF.3`, `BDPF.3A`, `BDPF.8`, `BDPF.11` | Investigation report does not select foundation/structural solution or remain current indefinitely. |
| Existing-asset survey/as-built/scan/model | actual-condition evidence candidates, geometry/material/defect signals and representation gaps | `BDPF.3`, `BDPF.8`, `BDPF.10`, `BDPF.11` | As-built label/model is not actual state without scope, method and currentness. |
| Operational, maintenance and user requirements | role/use/mode/maintenance/logistics scenarios and failure consequences | `BDPF.4`, `BDPF.5`, `BDPF.6B` | Stakeholder statement does not by itself prove feasibility or authority. |
| Hazard, fire, security, accessibility and safety sources | affected parties, scenarios, constraints, evidence/assurance/gate exits | `BDPF.3A`, `BDPF.4–9` plus direct safety/ethics/regulatory owners | BDPF record does not certify safety or compliance. |
| Climate/environment/resource sources | external conditions, temporal windows and performance/resource pressures | `BDPF.3`, `BDPF.6B`, `BDPF.8`, `BDPF.11` | Dataset/forecast does not automatically support causal or future-performance claim. |
| Technology/process/equipment data | process functions, loads, flows, space/interface and maintainability signals | `BDPF.4–6`, `BDPF.8` | Vendor data does not choose architecture or prove project-specific performance. |
| Cost/schedule/procurement/construction assumptions | candidate constraints, estimates, phasing and construction-method pressures | `BDPF.6A–7`, `BDPF.8`, `BDPF.11` | Estimate or preferred procurement route is not architectural evidence for all concerns. |
| Review findings, comments, clashes and machine checks | defect/source cues and potential represented-structure conflicts | `BDPF.11`, then exact owner | Comment/check status does not establish root cause or invalidity. |
| Decisions, commitments, approvals and authority acts | source/authority relations with scope/window | `BDPF.7`, `BDPF.9`, direct role/speech-act owners | Organizational effect does not prove technical adequacy. |

### Source admission card

Use this compact form when a source row becomes load-bearing:

```text
BuiltAssetDesignSourceUse@ProjectOrPackage:
  sourceRef:
  sourceKind:
  sourceOwner:
  editionOrDate:
  applicabilityScope:
  exactClaimOrPayloadUsed:
  receivingPatternOrProjectClaimRef:
  adoptedUse:
  rejectedOverread:
  evidenceOrAuthorityStatus:
  sourceCurrentnessWindow:
  sourceReturnCondition:
  refreshTrigger:
```

### Refresh decision

A source change does not automatically invalidate the package or every project decision. Apply:

```text
changed source
→ identify exact adopted payload or project signal
→ find consuming pattern/claim/decision/evidence/projection refs
→ create BDPF.11 impact trace
→ decide noImpact | localRepair | evidenceRefresh | PADReopen | patternRefresh | packageEditionRefresh
→ publish currentness/supersession result through G.11/E.4.PFR
```

---

# First Bounded Pilot And Adoption Boundary

The first pilot tests one substantive decision relation, not completeness of all project documentation and not adoption of every BDPF pattern.

```text
BDPFPilotFrame@Project:
  pilotId:
  projectRef:
  describedHolonRef:
  boundedDecisionScenarioRef:
  declaredPilotUse:
  nonUseBoundary:
  currentDecisionOrIssueRef:
  currentSourceRefs:
  currentCarrierAndProjectionRefs:
  currentRoleAssignmentRefs:
  currentEvidenceRefs:
  selectedBDPFPatternUseRefs:
  expectedFirstResults:
  protectedTradeoffs:
  pilotEvaluationQuestionRef:
  observedWorkAndResultRefs:
  fieldFeedbackRefs:
  packageRepairCandidateRefs:
  stopCondition:
  reopenCondition:
```

## Pilot selection rule

Choose one decision that:

- changes at least two structure relations or disciplines;
- has existing source/evidence/carrier material to reconstruct;
- is important enough that source return and reopen matter;
- is bounded enough to complete one decision/evaluation cycle;
- has named formulation, review and downstream reader roles;
- can be observed without treating the pilot as statutory review or approval.

Good pilot examples:

- vertical-core configuration;
- foundation/basement structural concept under site conditions;
- plantroom/distribution configuration;
- temporary/permanent access and phasing in reconstruction;
- facade system interfaces and maintenance strategy;
- one fire/evacuation/control structure question with direct safety-owner exits.

Bad first pilots:

- «проверить всю ПД»;
- «внедрить BDPF во всей организации»;
- «оценить качество ОКС в целом»;
- purely documentary task with no structure/decision question;
- decision whose evidence or authority cannot be accessed at all.

## Suggested pilot rhythm — conditional, not a universal workflow

| Current pilot condition | First pattern use | Stop/continue condition |
| --- | --- | --- |
| Only carriers and issue wording exist | `BDPF.3/3A` | Stop when source signal and architecture question are reviewable. |
| Existing decision is hidden in drawings/minutes | `BDPF.7`, then `BDPF.10` | Stop when PAD and represented/lost structures are recoverable. |
| Candidate plurality is missing | `BDPF.6A` | Continue only if comparison use is current. |
| Criteria/score is defective | `BDPF.6B/6C` | Stop at a lawful retained set or abstention. |
| PAD exists but handoff fails | `BDPF.12` | Repair strongest blocker; re-evaluate changed version. |
| Source changed or finding arrived | `BDPF.11` | Stop at owner-specific disposition. |

No participant must fill every pattern record. Materialize only the records required by the declared pilot use and delayed/reliance-bearing review.

## Pilot evidence and observations

The pilot may collect the following **method-use observations**. They are not direct measures of built-asset quality.

| Observation id | Question | Evidence basis | Blocked overread |
| --- | --- | --- | --- |
| `decisionReconstructionTime` | How long does a new reviewer need to recover question, basis, structures, losses and reopen? | timed review work + reconstruction result | Lower time does not prove better PAD unless required content remains correct. |
| `independentReconstructionAgreement` | Do two roles recover materially the same decision relation and boundaries? | independent result comparison with discrepancy log | Agreement is not truth or assurance. |
| `sourceToStructureTraceCoverage` | Which load-bearing source signals have a receiving structure/question/owner? | exact trace rows | Percentage does not prove source quality or completeness. |
| `unscopedEvidenceClaimCount` | How many reliance-bearing claims lack scope/evidence path? | review of selected claim set | Count depends on declared claim set and use. |
| `representationLossDetection` | Which selected/expected structures were found absent or distorted in carriers? | BDPF.10 rows and review evidence | More findings can mean better detection, not worse project quality. |
| `sourceChangeImpactLatency` | How quickly can changed source identify suspect decisions/evidence/projections? | dated impact-trace work | Speed does not prove correct impact disposition. |
| `strongestADARepairClosure` | Did the strongest BDPF.12 blocker improve after a named repair and re-evaluation? | two decision versions + coordinate rows | Coordinate movement does not prove engineering result beyond declared use. |
| `operatorBurden` | What time/cognitive/document burden did BDPF add, and what got worse? | role feedback + work/resource evidence | Satisfaction alone does not decide method utility. |

## Pilot completion conditions

A bounded pilot is complete when:

1. one exact decision scenario and declared use are pinned;
2. selected BDPF patterns produce their direct results, not substitute documents;
3. at least two roles can reconstruct the PAD/use boundary or the selected first result;
4. one `BDPF.12` evaluation identifies strongest blockers, or the pilot truthfully stops before PAD adequacy is current;
5. at least one source-return/change or representation-loss question is exercised;
6. operator burden and protected trade-offs are recorded;
7. field feedback is routed to local repair, pattern repair, source refresh or no-change disposition;
8. no pilot result is represented as proof of OКС quality, compliance, approval or enterprise readiness.

## Adoption boundary

Do not mandate BDPF as an enterprise service/regulation after one pilot. Promotion beyond `locallyUsableWithVisibleLimits` requires at minimum:

- two heterogeneous project decisions involving different structure families and reader roles;
- complete `E.21` evaluations for priority patterns and repair of below-floor coordinates;
- evidence that decision reconstruction or repair value exceeds operator burden for the declared uses;
- one exercised source-change/impact route;
- stable local role/authority mappings that remain separate from pattern semantics;
- a refreshed `E.4.DPF.DA` package evaluation;
- an explicit PFAD/supersession decision for the promoted edition.

---

# Repository And Carrier Assembly Guard

This v0.5.1 file remains an all-in-one revision-candidate publication carrier. It is suitable for inspection and bounded pilot use. It should not be split into a source-of-truth package merely because headings exist.

Target assembly after stabilization:

```text
pack/dpf/built-asset-design/
  BuiltAssetDesignPrinciplesFramework.md
  README.md                         # thin first-entry carrier, no new semantics
  package-architecture-decision.md  # PFAD projection; no new framework semantics
  relation-records.md
  source-use-and-refresh-map.md
  acceptance-cases.md
  patterns/
    BDPF.1-built-asset-system-in-context.md
    BDPF.2-design-decision-development-method.md
    BDPF.3-source-signal-use.md
    BDPF.3A-problem-to-structure-flow.md
    BDPF.3B-initial-data-analysis-package.md
    BDPF.4-use-concept.md
    BDPF.5-system-concept.md
    BDPF.6-architecture-question.md
    BDPF.6A-candidate-configurations.md
    BDPF.6B-characteristics-criteria-eval.md
    BDPF.6C-comparison-retained-set.md
    BDPF.7-project-architecture-decision.md
    BDPF.7A-adr-projection.md
    BDPF.7B-minimal-decision-use-package.md
    BDPF.8-claim-specific-evidence.md
    BDPF.9-readiness-boundary-use.md
    BDPF.10-pd-bim-view-projection.md
    BDPF.11-feedback-impact-repair.md
    BDPF.12-decision-adequacy.md
  quality/
    E21-BDPF-3A-v0.5.1.md
    E21-BDPF-7-v0.5.1.md
    E21-BDPF-10-v0.5.1.md
    E21-BDPF-12-v0.5.1.md
    E21-BDPF-remaining-patterns.md
    E4DPFDA-BDPF-v0.5.1.md
  pilots/
    <field-pilot-evidence-carriers>
```

Rules:

- patterns remain the governing action-guidance loci;
- README, cards, templates, databases, skills or assistants are publication/access carriers and may not add semantics;
- project templates are implementations/publication forms, not pattern bodies;
- pilot evidence and work records stay outside `patterns/`;
- source standards and project sources are referenced, not copied as BDPF norms;
- generated schemas, forms or graphs enter through `C.35` admission before reliance;
- moving a file to `pack/` does not make it stable, current, adequate or authoritative.

---

# Package Quality Result

## Package-form subpass (`E.4.DPF.DA` PFM1–PFM11)

| Check | Result for v0.5.1 | Evidence / limitation | Required repair |
| --- | --- | --- | --- |
| `PFM1 Front-door order` | `pass` | ToC, Readme, Preface and Pattern Index precede pattern bodies. | Recheck after any carrier split. |
| `PFM2 Pattern-language primacy` | `pass` | Full action-guiding pattern bodies precede support maps/records. | Keep templates and implementation guidance out of pattern bodies. |
| `PFM3 Map discoverability` | `pass` | ToC, Relations, wording/source/currentness returns point to support maps. | Add route if a new map is introduced. |
| `PFM4 Dependency direction` | `pass` | Explicit dependency toward `FPFCorePatternSet@July2026`; reverse dependency blocked. | Use Core amendment route for any candidate Core change. |
| `PFM5 Publication-and-access-carrier boundary` | `pass` | Carrier, records, future repository and access forms are explicitly non-semantic/non-authoritative. | Re-evaluate when a skill/MCP/access service is created. |
| `PFM6 Public package naming` | `pass` | Domain head `Built Asset Design` is visible; draft/status not embedded as identity. | Use edition/status fields, not title mutation. |
| `PFM7 Development-state absence` | `passForRevisionCarrier` | Durable user-facing content is separated from pilot/work residue; front matter states revision-candidate qualification without process-state contamination. | Keep actual review logs, handoffs and work artifacts outside the package carrier. |
| `PFM8 Cross-DPF relation discipline` | `pass` | Load-bearing framework relations use `E.4.PFR`; no upstream DPF dependency is currently claimed. | Add exact PFR before depending on another DPF. |
| `PFM9 Normal-pattern maturity` | `priorityEvaluationPassForBoundedPilot / remainingCoverageIncomplete` | All public pattern loci have normal `E.8` sections; complete `E.21` records are materialized for `BDPF.3A`, `BDPF.7`, `BDPF.10` and `BDPF.12`. Remaining patterns are not yet individually evaluated. | Evaluate the remaining patterns before broader package qualification; re-evaluate priority patterns after material changes. |
| `PFM10 Access-currentness and callable-use boundary` | `notTriggered` | No skill pack, MCP-backed access service or assistant publication is part of this edition. | Apply before any callable/access carrier is relied on. |
| `PFM11 Carrier structure-account` | `pass` | Package Carrier Structure-Account names readers, denominator, foregrounded/deferred structure, epiplexity value and source-return boundary. | Re-evaluate after package split, substantial coarsening or reader change. |

## `DPFPackageAdequacyEvaluation@BuiltAssetDesignPrinciplesFramework-v0.5.1`

```text
DPFPackageAdequacyEvaluation@BuiltAssetDesignPrinciplesFramework-v0.5.1:
  evaluatedPackageRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  packageKind: all-in-one-publication-carrier for a domain-principle-framework revision candidate
  declaredDomainOrLocalContext: development and expert/technical support of architecture-significant cross-disciplinary built-asset design decisions
  intendedReaderOrOperator: design leads, architects/engineers, reviewers, information coordinators and technical clients
  declaredUse: one bounded project-decision pilot and package inspection
  nonUseBoundary: not regulation, statutory review procedure, BIM standard, proof, approval, WorkPlan or enterprise mandate
  fpfCoreEditionRef: FPFCorePatternSet@July2026
  dependencyAndEditionRefs: Name And Edition Route; PFR-BDPF-CORE-DEP-001
  sourceBasisRefs: Source Use And Refresh Map
  pfadDecisionRefs: PFAD-BDPF-2026-07-13-001
  patternSetRefs: BDPF.1 through BDPF.12 with lettered extensions
  relationRecordRefs: PFR-BDPF-* including PFAD and produced-carrier admission relations
  publicationCarrierRefs: this file
  accessCarrierRefs: none
  qualityEvidenceRefs: PFM subpass; package-coordinate rows; E21-BDPF-3A-v0.5.1; E21-BDPF-7-v0.5.1; E21-BDPF-10-v0.5.1; E21-BDPF-12-v0.5.1; no field-transfer or enterprise-adoption evidence
  refreshRefs: RefreshRoute@BuiltAssetDesignPrinciplesFramework
  status: locallyUsableWithVisibleLimits
  firstRepairOrNoProposalDisposition: run heterogeneous field pilots and complete E.21 evaluations for the remaining pattern set before public/enterprise qualification
  reopenCondition: any Core/source/pattern/relation/carrier/use/field-evidence change
```

### Coordinate results

| Coordinate | Value | Short rationale | Evidence locus | Repair or no-proposal disposition |
| --- | ---: | --- | --- | --- |
| `D1DomainScopeAndUseAdequacy` | `4` | Domain, users, bounded pilot use and extensive non-use boundary are explicit. `5` would require demonstrated transfer across more organizations/jurisdictions. | Front matter, Readme, Framework Context | No immediate content repair; test boundary interpretation in pilots. |
| `D2DidacticEntryAndAdoptionAdequacy` | `4` | Trigger-based front door and first-result guidance allow entry without reading maps. `5` needs observed first-use telemetry. | ToC, Readme, Pattern Index, pilot conditions | Measure first-entry errors and repair the highest-friction route. |
| `D3ScalableFormalityAndAssurancePathAdequacy` | `4` | Plain recognition leads to typed records, evidence/assurance/gate exits and evaluations without forcing all apparatus at once. | Pattern bodies, especially 3A, 7–12 | Verify that low-risk pilot users can stay light without losing boundaries. |
| `D4CoreDependencyAndDomainBoundaryAdequacy` | `4` | Core owners, no-new-U-kind rule and reverse-dependency block are explicit. | Framework Context, dependency record, PFRs | Re-run on every cited Core edition change. |
| `D5PackageFormLayeringAndRelationAdequacy` | `4` | Front door, patterns, acceptance probes, support records, PFAD, source/quality/refresh records are separate and discoverable. | ToC, PFAD, PFM table, reordered acceptance/support sections | Re-evaluate after file/package split or access-carrier creation. |
| `D6DomainLexiconAndKindSettlementAdequacy` | `4` | High-risk built-asset terms route to kinds/owners and blocked overreads. `5` needs evidence across local vocabularies and bilingual use. | Precision Restoration And Owner Map; pattern schemas | Collect lexical failures in at least two project organizations. |
| `D7PracticeUtilityAndProblemResolutionAdequacy` | `4` | Patterns address recognizable design failures with direct results, cases and repair moves. `5` needs repeated field adoption evidence. | BDPF.1–12 and acceptance probes | Run bounded field pilots; compare result value against burden. |
| `D8HeterogeneousCaseAndTransferAdequacy` | `3` | Ten heterogeneous acceptance probes exist, but they are designed cases, not completed field runs. | Acceptance Cases; no field evidence carrier | Complete at least two heterogeneous real/simulated project runs with different roles and structure families. |
| `D9EditionStateAndCurrentnessAdequacy` | `4` | Edition, supersession, source pins, migration boundary and refresh triggers are explicit. `5` needs replayed refresh. | Name/Edition Route, Source Map, PFR, Refresh Route | Exercise one real source/Core edition impact and publish disposition. |
| `D10ImprovementAndRefreshAdequacy` | `4` | BDPF.11, BDPF.12, E.22/E.23 and G.11 routes support smallest repair and versioned re-evaluation. | BDPF.11/12, pilot, refresh route | Run one complete object-version improvement loop and package refresh probe. |
| `D11DomainSoTAAlignmentAdequacy` | `4` | Package-pinned architecture/information sources materially change pattern boundaries, machine-check limits and refresh. `5` requires broader rival practice/source packs and field calibration. | SoTA-Echoing sections and Source Map | Add source rows only where they change a solution/check/boundary; calibrate with project/domain specialists. |

**No average is issued.** `D8=3` is the strongest package blocker. The resulting package status is `locallyUsableWithVisibleLimits` for the declared bounded pilot, not public/enterprise/stable qualification.

## Pattern-maturity register

| Pattern group | E.8 body status | E.21 evaluation status | Current qualification |
| --- | --- | --- | --- |
| `BDPF.1/1A–3` | Complete canonical sections; `BDPF.1A` adds site-start delimitation and placement relation | Not individually materialized | Bounded-pilot use with package limits; direct source/evidence owners required |
| `BDPF.3A` | Complete and revised for exact structure-owner routing | `E21-BDPF-3A-v0.5.1`: `admissibleForDeclaredUse` at floor 4 | Priority pattern suitable as bounded authoring/pilot input; no field-transfer proof |
| `BDPF.3B–6` | Complete canonical sections; `BDPF.6` shadow-kind repair completed | Not individually materialized | Bounded-pilot use; individual E.21 still required |
| `BDPF.6A–6C` | Complete; coherence, criterion-role and owner-routing repairs completed | Not individually materialized | Bounded-pilot use; evaluate before broader reliance |
| `BDPF.7` | Complete PAD specialization | `E21-BDPF-7-v0.5.1`: `admissibleForDeclaredUse` at floor 4 | Bounded decision-authoring/review input; direct evidence/authority still required |
| `BDPF.7A–9` | Complete canonical sections and non-use routing | Not individually materialized | Pilot-only; publication/evidence/gate owners remain mandatory |
| `BDPF.10` | Complete with invariant-coverage/correspondence repair | `E21-BDPF-10-v0.5.1`: `admissibleForDeclaredUse` at floor 4 | Bounded representation-review input; no actual-state/compliance proof |
| `BDPF.11` | Complete with supported impact propagation | Not individually materialized | Pilot feedback/impact use; individual E.21 required |
| `BDPF.12` | Complete ADA specialization with exact Core routing | `E21-BDPF-12-v0.5.1`: `admissibleForDeclaredUse` at floor 4 | Bounded decision-quality evaluation input; never approval/gate |

Section presence alone is not an `E.21` pass. The four records below are package-authoring quality evidence for this edition; they are not field evidence that project use succeeds.

## Priority-pattern E.21 evaluations

### `E21-BDPF-3A-v0.5.1` — `BDPF.3A` Problem pressure to built-asset structure

```text
PatternQualityEvaluation:
  evaluationId: E21-BDPF-3A-v0.5.1
  patternOfConcernRef: BDPF.3A@BuiltAssetDesignPrinciplesFramework-v0.5.1
  declaredScope: pattern body, Readme/ToC/Index entry, named acceptance case, source-use and relation records in this edition
  declaredUse: authoring-quality and bounded-pilot pattern-use input for an ordinary practitioner
  workingReaderScope: design lead, architect/engineer, reviewer or information coordinator familiar with project work but not required to know the whole FPF monolith
  qualificationWindow: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1 and FPFCorePatternSet@July2026
  declaredFloor: every E.21 coordinate >= 4 wellExpressedForDeclaredUse
  evaluationEvidenceBasis:
    - BDPF.3A pattern body and conformance checklist
    - Table of Contents, Readme and Pattern Index entries for BDPF.3A
    - BDPF.3A Archetypal Grounding and AC-BDPF-01
    - Framework Context, PFAD, PFR and Source Use And Refresh Map
  protectedTradeoffs:
    - practical first-use affordability must not be sacrificed for exhaustive formal apparatus
    - domain specificity must not create duplicate Core ontology or authority
    - strong boundary text must not displace positive action guidance
  status: admissibleForDeclaredUse
  nonAdmissibleUse: field-performance proof, release gate, enterprise adoption, project decision approval or evidence of successful pattern enactment
  stopOrReopenCondition: any pattern-body, Core-owner, source-use, reader/use, carrier-entry or acceptance-case change; field contradiction; or a coordinate falling below 4
```

```text
PrecisionRestorationProfile:
  wordHeadAndUsePrecision: repaired for subject-first EntityOfConcern, exact direct owners and bounded local record labels
  phraseApparatus: no material phrase-apparatus blocks first use; bilingual identifiers remain only where they preserve exact FPF/project refs
  repetitionAndDistribution: recognition, Solution, checks and Relations carry different functions; no quality-result material is embedded in the pattern body
  onticAndSlotRelationClarity: DPF-local records are not admitted as U-kinds; slots preserve relation-family owners
  descriptionPublicationSourceBoundary: carrier, source, evidence, decision, gate and actual-work overreads are explicitly blocked
  patternApplicationOntology: the first useful result and receiving owner are recoverable without treating presentation order as workflow
  overallEffect: no material precision-restoration defect lowers the declared-use evaluation in this edition
  affectedCoordinates: none below floor; profile directly supports EntityOfConcernPrimacyAndSemioBiasResistance, SemanticKindAndNameRecoverability and UseAffordabilityAndApparatusProportionality
  restorationAndGoverningRefs: E.10, E.10.ARCH, F.19, E.24.CD, E.24.PUB and the direct Core owners cited by BDPF.3A
```

| Coordinate | Value | ShortRationale |
| --- | ---: | --- |
| `WorkingSituationAndUseBoundaryRecognizability` | `4` | 4 — Problem frame names trigger, first useful move, failure, benefit and explicit non-use. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `EntityOfConcernAndClaimScopeStability` | `4` | 4 — Subject-first Primary EntityOfConcern and project schema keep bearer, context and declared use recoverable. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `PatternApplicationGuidance` | `4` | 4 — Solution gives ordered positive moves, exact first result and conformance checks. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `ClosureAndBoundedNonUseRecoverability` | `4` | 4 — Non-admissible use, stop/return and reopen conditions are explicit in frame, schema and Relations. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `SemanticKindAndNameRecoverability` | `4` | 4 — Record-kind discipline and schema distinguish the governed relation from card, carrier, status and stronger claims. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `NeighborAuthorityAndBoundedUseFit` | `4` | 4 — Relations and direct-owner exits name FPF owners by value without moving their authority into BDPF. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `EntityOfConcernPrimacyAndSemioBiasResistance` | `4` | 4 — Opening leads with the project subject and action; publication, source and quality apparatus remains late and bounded. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `PracticalUseDeltaAndHarmPrevention` | `4` | 4 — Archetypal grounding and anti-pattern table show the changed project use and prevented overread. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `UseAffordabilityAndApparatusProportionality` | `4` | 4 — One thin first record is usable before optional heavy evidence, comparison or package apparatus. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `RepairLocalityAndChangeImpactPredictability` | `4` | 4 — Checklist, anti-pattern repair and Relations point to the smallest repair locus and reopen effect. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `ProxyForValueSubstitutionResistance` | `4` | 4 — The pattern blocks requirement-to-solution and local-carrier-fix substitution by retaining unknown structure and receiving owner. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `ClaimJustificationTraceabilityCurrentnessAndReplayability` | `4` | 4 — Source-signal use refs, exact structure-kind refs or owner-bound cues, structural-information notes and receiving owner support replay. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `CaseCountercaseAndTransferCoverage` | `4` | 4 — BDPF.3A Archetypal Grounding and AC-BDPF-01 plus the anti-pattern table provide one worked case and countercase boundary. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `MaturePatternParityAndSelectedContentSufficiency` | `4` | 4 — Comparator `C.32.P2S`; selected ingredients are governing-pattern-specific exits, structural uncertainty and stop before candidate/PAD work. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `SoTABindingAndCurrentness` | `4` | 4 — `SRC-BDPF-FPF-JUL2026` is adopted through exact `C.32.P2S`; domain source applicability returns to project records and the source map. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `FormalClaimAdmissibilityAndLensFit` | `4` | 4 — Typed structure-kind refs and structural-information states are bounded; no unowned mathematical, measurement or gate claim is made. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `FalsifiabilityAndLoweringCondition` | `4` | 4 — Changed source, affected holon, unknown structure, characteristic pressure or owner explicitly reopens/lowers the result. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `CorpusEntryProjectionAndEcologyFit` | `4` | 4 — ToC trigger, Readme entry, Pattern Index row and acceptance-case routing align with the pattern body. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |
| `EvolutionFrontAndRefreshDiscipline` | `4` | 4 — Reopen conditions and BDPF.11/G.11/E.23 routes identify the smallest evolution locus. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no repeated cross-organization field replay of the flow card exists. |

**Result:** `admissibleForDeclaredUse` at the declared floor of `4` for bounded authoring and pilot-use input. No average is issued. The shared blocker against `5` is absence of repeated heterogeneous field transfer; that absence remains package coordinate `D8=3` rather than being hidden inside the pattern result.

### `E21-BDPF-7-v0.5.1` — `BDPF.7` Project built-asset architecture decision

```text
PatternQualityEvaluation:
  evaluationId: E21-BDPF-7-v0.5.1
  patternOfConcernRef: BDPF.7@BuiltAssetDesignPrinciplesFramework-v0.5.1
  declaredScope: pattern body, Readme/ToC/Index entry, named acceptance case, source-use and relation records in this edition
  declaredUse: authoring-quality and bounded-pilot pattern-use input for an ordinary practitioner
  workingReaderScope: design lead, architect/engineer, reviewer or information coordinator familiar with project work but not required to know the whole FPF monolith
  qualificationWindow: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1 and FPFCorePatternSet@July2026
  declaredFloor: every E.21 coordinate >= 4 wellExpressedForDeclaredUse
  evaluationEvidenceBasis:
    - BDPF.7 pattern body and conformance checklist
    - Table of Contents, Readme and Pattern Index entries for BDPF.7
    - BDPF.7 vertical-core worked slice and AC-BDPF-02
    - Framework Context, PFAD, PFR and Source Use And Refresh Map
  protectedTradeoffs:
    - practical first-use affordability must not be sacrificed for exhaustive formal apparatus
    - domain specificity must not create duplicate Core ontology or authority
    - strong boundary text must not displace positive action guidance
  status: admissibleForDeclaredUse
  nonAdmissibleUse: field-performance proof, release gate, enterprise adoption, project decision approval or evidence of successful pattern enactment
  stopOrReopenCondition: any pattern-body, Core-owner, source-use, reader/use, carrier-entry or acceptance-case change; field contradiction; or a coordinate falling below 4
```

```text
PrecisionRestorationProfile:
  wordHeadAndUsePrecision: repaired for subject-first EntityOfConcern, exact direct owners and bounded local record labels
  phraseApparatus: no material phrase-apparatus blocks first use; bilingual identifiers remain only where they preserve exact FPF/project refs
  repetitionAndDistribution: recognition, Solution, checks and Relations carry different functions; no quality-result material is embedded in the pattern body
  onticAndSlotRelationClarity: DPF-local records are not admitted as U-kinds; slots preserve relation-family owners
  descriptionPublicationSourceBoundary: carrier, source, evidence, decision, gate and actual-work overreads are explicitly blocked
  patternApplicationOntology: the first useful result and receiving owner are recoverable without treating presentation order as workflow
  overallEffect: no material precision-restoration defect lowers the declared-use evaluation in this edition
  affectedCoordinates: none below floor; profile directly supports EntityOfConcernPrimacyAndSemioBiasResistance, SemanticKindAndNameRecoverability and UseAffordabilityAndApparatusProportionality
  restorationAndGoverningRefs: E.10, E.10.ARCH, F.19, E.24.CD, E.24.PUB and the direct Core owners cited by BDPF.7
```

| Coordinate | Value | ShortRationale |
| --- | ---: | --- |
| `WorkingSituationAndUseBoundaryRecognizability` | `4` | 4 — Problem frame names trigger, first useful move, failure, benefit and explicit non-use. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `EntityOfConcernAndClaimScopeStability` | `4` | 4 — Subject-first Primary EntityOfConcern and project schema keep bearer, context and declared use recoverable. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `PatternApplicationGuidance` | `4` | 4 — Solution gives ordered positive moves, exact first result and conformance checks. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `ClosureAndBoundedNonUseRecoverability` | `4` | 4 — Non-admissible use, stop/return and reopen conditions are explicit in frame, schema and Relations. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `SemanticKindAndNameRecoverability` | `4` | 4 — Record-kind discipline and schema distinguish the governed relation from card, carrier, status and stronger claims. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `NeighborAuthorityAndBoundedUseFit` | `4` | 4 — Relations and direct-owner exits name FPF owners by value without moving their authority into BDPF. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `EntityOfConcernPrimacyAndSemioBiasResistance` | `4` | 4 — Opening leads with the project subject and action; publication, source and quality apparatus remains late and bounded. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `PracticalUseDeltaAndHarmPrevention` | `4` | 4 — Archetypal grounding and anti-pattern table show the changed project use and prevented overread. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `UseAffordabilityAndApparatusProportionality` | `4` | 4 — One thin first record is usable before optional heavy evidence, comparison or package apparatus. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `RepairLocalityAndChangeImpactPredictability` | `4` | 4 — Checklist, anti-pattern repair and Relations point to the smallest repair locus and reopen effect. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `ProxyForValueSubstitutionResistance` | `4` | 4 — The pattern blocks record, signature, one calculation, concern coverage or detail depth from substituting for PAD commitment. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `ClaimJustificationTraceabilityCurrentnessAndReplayability` | `4` | 4 — Decision subject, candidate/comparison basis, selected and expected structures, losses, roles, evidence exits, projections and valid window are pinned. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `CaseCountercaseAndTransferCoverage` | `4` | 4 — BDPF.7 vertical-core worked slice and AC-BDPF-02 plus the anti-pattern table provide one worked case and countercase boundary. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `MaturePatternParityAndSelectedContentSufficiency` | `4` | 4 — Comparator `C.32.PAD`; selected ingredients are selected-structure commitment, accepted loss, method docking, architect/developer split and reopen. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `SoTABindingAndCurrentness` | `4` | 4 — `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-42010-2022` and `SRC-BDPF-42030-2019` are adopted with explicit decision/description/evaluation boundaries. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `FormalClaimAdmissibilityAndLensFit` | `4` | 4 — PAD fields and role/evidence/authority exits are kind-explicit; criteria values or votes do not become the decision mechanism. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `FalsifiabilityAndLoweringCondition` | `4` | 4 — Candidate-basis, source, authority, evidence, structure, use or validity-window change explicitly reopens the PAD. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `CorpusEntryProjectionAndEcologyFit` | `4` | 4 — ToC trigger, Readme entry, Pattern Index row and acceptance-case routing align with the pattern body. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |
| `EvolutionFrontAndRefreshDiscipline` | `4` | 4 — Reopen conditions and BDPF.11/G.11/E.23 routes identify the smallest evolution locus. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no cross-team replay showing that a second delivery team can enact the decision without local recovery exists. |

**Result:** `admissibleForDeclaredUse` at the declared floor of `4` for bounded authoring and pilot-use input. No average is issued. The shared blocker against `5` is absence of repeated heterogeneous field transfer; that absence remains package coordinate `D8=3` rather than being hidden inside the pattern result.

### `E21-BDPF-10-v0.5.1` — `BDPF.10` Decision projection into PD, BIM and views

```text
PatternQualityEvaluation:
  evaluationId: E21-BDPF-10-v0.5.1
  patternOfConcernRef: BDPF.10@BuiltAssetDesignPrinciplesFramework-v0.5.1
  declaredScope: pattern body, Readme/ToC/Index entry, named acceptance case, source-use and relation records in this edition
  declaredUse: authoring-quality and bounded-pilot pattern-use input for an ordinary practitioner
  workingReaderScope: design lead, architect/engineer, reviewer or information coordinator familiar with project work but not required to know the whole FPF monolith
  qualificationWindow: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1 and FPFCorePatternSet@July2026
  declaredFloor: every E.21 coordinate >= 4 wellExpressedForDeclaredUse
  evaluationEvidenceBasis:
    - BDPF.10 pattern body and conformance checklist
    - Table of Contents, Readme and Pattern Index entries for BDPF.10
    - BDPF.10 smoke-control/evacuation slice and AC-BDPF-07
    - Framework Context, PFAD, PFR and Source Use And Refresh Map
  protectedTradeoffs:
    - practical first-use affordability must not be sacrificed for exhaustive formal apparatus
    - domain specificity must not create duplicate Core ontology or authority
    - strong boundary text must not displace positive action guidance
  status: admissibleForDeclaredUse
  nonAdmissibleUse: field-performance proof, release gate, enterprise adoption, project decision approval or evidence of successful pattern enactment
  stopOrReopenCondition: any pattern-body, Core-owner, source-use, reader/use, carrier-entry or acceptance-case change; field contradiction; or a coordinate falling below 4
```

```text
PrecisionRestorationProfile:
  wordHeadAndUsePrecision: repaired for subject-first EntityOfConcern, exact direct owners and bounded local record labels
  phraseApparatus: no material phrase-apparatus blocks first use; bilingual identifiers remain only where they preserve exact FPF/project refs
  repetitionAndDistribution: recognition, Solution, checks and Relations carry different functions; no quality-result material is embedded in the pattern body
  onticAndSlotRelationClarity: DPF-local records are not admitted as U-kinds; slots preserve relation-family owners
  descriptionPublicationSourceBoundary: carrier, source, evidence, decision, gate and actual-work overreads are explicitly blocked
  patternApplicationOntology: the first useful result and receiving owner are recoverable without treating presentation order as workflow
  overallEffect: no material precision-restoration defect lowers the declared-use evaluation in this edition
  affectedCoordinates: none below floor; profile directly supports EntityOfConcernPrimacyAndSemioBiasResistance, SemanticKindAndNameRecoverability and UseAffordabilityAndApparatusProportionality
  restorationAndGoverningRefs: E.10, E.10.ARCH, F.19, E.24.CD, E.24.PUB and the direct Core owners cited by BDPF.10
```

| Coordinate | Value | ShortRationale |
| --- | ---: | --- |
| `WorkingSituationAndUseBoundaryRecognizability` | `4` | 4 — Problem frame names trigger, first useful move, failure, benefit and explicit non-use. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `EntityOfConcernAndClaimScopeStability` | `4` | 4 — Subject-first Primary EntityOfConcern and project schema keep bearer, context and declared use recoverable. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `PatternApplicationGuidance` | `4` | 4 — Solution gives ordered positive moves, exact first result and conformance checks. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `ClosureAndBoundedNonUseRecoverability` | `4` | 4 — Non-admissible use, stop/return and reopen conditions are explicit in frame, schema and Relations. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `SemanticKindAndNameRecoverability` | `4` | 4 — Record-kind discipline and schema distinguish the governed relation from card, carrier, status and stronger claims. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `NeighborAuthorityAndBoundedUseFit` | `4` | 4 — Relations and direct-owner exits name FPF owners by value without moving their authority into BDPF. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `EntityOfConcernPrimacyAndSemioBiasResistance` | `4` | 4 — Opening leads with the project subject and action; publication, source and quality apparatus remains late and bounded. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `PracticalUseDeltaAndHarmPrevention` | `4` | 4 — Archetypal grounding and anti-pattern table show the changed project use and prevented overread. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `UseAffordabilityAndApparatusProportionality` | `4` | 4 — One thin first record is usable before optional heavy evidence, comparison or package apparatus. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `RepairLocalityAndChangeImpactPredictability` | `4` | 4 — Checklist, anti-pattern repair and Relations point to the smallest repair locus and reopen effect. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `ProxyForValueSubstitutionResistance` | `4` | 4 — The pattern blocks BIM detail, federation, status, LOD labels and machine-check pass from substituting for structure correspondence or engineering truth. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `ClaimJustificationTraceabilityCurrentnessAndReplayability` | `4` | 4 — Exact decision/structure refs, view/carrier editions, captured/lost relations, correspondence status and source return support replay. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `CaseCountercaseAndTransferCoverage` | `4` | 4 — BDPF.10 smoke-control/evacuation slice and AC-BDPF-07 plus the anti-pattern table provide one worked case and countercase boundary. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `MaturePatternParityAndSelectedContentSufficiency` | `4` | 4 — Comparators `C.30.AD.BA`, `C.33` and `C.34`; selected ingredients are description-use boundary, missing-structure return and directional correspondence. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `SoTABindingAndCurrentness` | `4` | 4 — Source-use table binds `SRC-BDPF-42010-2022`, ISO 19650 pins, IFC, IDM, LOIN, IDS and project-pinned 81346 with adopt/reject boundaries. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `FormalClaimAdmissibilityAndLensFit` | `4` | 4 — Representation states and correspondence status are typed; schema/check claims stay bounded to encoded predicates and declared carriers. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `FalsifiabilityAndLoweringCondition` | `4` | 4 — PAD, viewpoint, carrier/rule edition, correspondence conflict or actual-state evidence change reopens the projection. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `CorpusEntryProjectionAndEcologyFit` | `4` | 4 — ToC trigger, Readme entry, Pattern Index row and acceptance-case routing align with the pattern body. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |
| `EvolutionFrontAndRefreshDiscipline` | `4` | 4 — Reopen conditions and BDPF.11/G.11/E.23 routes identify the smallest evolution locus. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no heterogeneous cold-reader or federated-model field replay demonstrates exceptional transfer and loss recovery. |

**Result:** `admissibleForDeclaredUse` at the declared floor of `4` for bounded authoring and pilot-use input. No average is issued. The shared blocker against `5` is absence of repeated heterogeneous field transfer; that absence remains package coordinate `D8=3` rather than being hidden inside the pattern result.

### `E21-BDPF-12-v0.5.1` — `BDPF.12` Declared-use architecture-decision adequacy

```text
PatternQualityEvaluation:
  evaluationId: E21-BDPF-12-v0.5.1
  patternOfConcernRef: BDPF.12@BuiltAssetDesignPrinciplesFramework-v0.5.1
  declaredScope: pattern body, Readme/ToC/Index entry, named acceptance case, source-use and relation records in this edition
  declaredUse: authoring-quality and bounded-pilot pattern-use input for an ordinary practitioner
  workingReaderScope: design lead, architect/engineer, reviewer or information coordinator familiar with project work but not required to know the whole FPF monolith
  qualificationWindow: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1 and FPFCorePatternSet@July2026
  declaredFloor: every E.21 coordinate >= 4 wellExpressedForDeclaredUse
  evaluationEvidenceBasis:
    - BDPF.12 pattern body and conformance checklist
    - Table of Contents, Readme and Pattern Index entries for BDPF.12
    - BDPF.12 vertical-core evaluation slice and its below-floor handoff result
    - Framework Context, PFAD, PFR and Source Use And Refresh Map
  protectedTradeoffs:
    - practical first-use affordability must not be sacrificed for exhaustive formal apparatus
    - domain specificity must not create duplicate Core ontology or authority
    - strong boundary text must not displace positive action guidance
  status: admissibleForDeclaredUse
  nonAdmissibleUse: field-performance proof, release gate, enterprise adoption, project decision approval or evidence of successful pattern enactment
  stopOrReopenCondition: any pattern-body, Core-owner, source-use, reader/use, carrier-entry or acceptance-case change; field contradiction; or a coordinate falling below 4
```

```text
PrecisionRestorationProfile:
  wordHeadAndUsePrecision: repaired for subject-first EntityOfConcern, exact direct owners and bounded local record labels
  phraseApparatus: no material phrase-apparatus blocks first use; bilingual identifiers remain only where they preserve exact FPF/project refs
  repetitionAndDistribution: recognition, Solution, checks and Relations carry different functions; no quality-result material is embedded in the pattern body
  onticAndSlotRelationClarity: DPF-local records are not admitted as U-kinds; slots preserve relation-family owners
  descriptionPublicationSourceBoundary: carrier, source, evidence, decision, gate and actual-work overreads are explicitly blocked
  patternApplicationOntology: the first useful result and receiving owner are recoverable without treating presentation order as workflow
  overallEffect: no material precision-restoration defect lowers the declared-use evaluation in this edition
  affectedCoordinates: none below floor; profile directly supports EntityOfConcernPrimacyAndSemioBiasResistance, SemanticKindAndNameRecoverability and UseAffordabilityAndApparatusProportionality
  restorationAndGoverningRefs: E.10, E.10.ARCH, F.19, E.24.CD, E.24.PUB and the direct Core owners cited by BDPF.12
```

| Coordinate | Value | ShortRationale |
| --- | ---: | --- |
| `WorkingSituationAndUseBoundaryRecognizability` | `4` | 4 — Problem frame names trigger, first useful move, failure, benefit and explicit non-use. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `EntityOfConcernAndClaimScopeStability` | `4` | 4 — Subject-first Primary EntityOfConcern and project schema keep bearer, context and declared use recoverable. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `PatternApplicationGuidance` | `4` | 4 — Solution gives ordered positive moves, exact first result and conformance checks. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `ClosureAndBoundedNonUseRecoverability` | `4` | 4 — Non-admissible use, stop/return and reopen conditions are explicit in frame, schema and Relations. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `SemanticKindAndNameRecoverability` | `4` | 4 — Record-kind discipline and schema distinguish the governed relation from card, carrier, status and stronger claims. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `NeighborAuthorityAndBoundedUseFit` | `4` | 4 — Relations and direct-owner exits name FPF owners by value without moving their authority into BDPF. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `EntityOfConcernPrimacyAndSemioBiasResistance` | `4` | 4 — Opening leads with the project subject and action; publication, source and quality apparatus remains late and bounded. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `PracticalUseDeltaAndHarmPrevention` | `4` | 4 — Archetypal grounding and anti-pattern table show the changed project use and prevented overread. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `UseAffordabilityAndApparatusProportionality` | `4` | 4 — One thin first record is usable before optional heavy evidence, comparison or package apparatus. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `RepairLocalityAndChangeImpactPredictability` | `4` | 4 — Checklist, anti-pattern repair and Relations point to the smallest repair locus and reopen effect. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `ProxyForValueSubstitutionResistance` | `4` | 4 — The pattern blocks averages, document completeness, reviewer authority and high scores from substituting for weak-coordinate repair or approval. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `ClaimJustificationTraceabilityCurrentnessAndReplayability` | `4` | 4 — Evaluated decision version, use, floor, every coordinate, adjacent-value rationale, evidence locus and repair owner make the evaluation replayable. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `CaseCountercaseAndTransferCoverage` | `4` | 4 — BDPF.12 vertical-core evaluation slice and its below-floor handoff result plus the anti-pattern table provide one worked case and countercase boundary. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `MaturePatternParityAndSelectedContentSufficiency` | `4` | 4 — Comparator `C.32.ADA` with `E.21`; the complete Core coordinate set, labels, no-average law and owner-specific repair routes are preserved. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `SoTABindingAndCurrentness` | `4` | 4 — `SRC-BDPF-FPF-JUL2026`, `SRC-BDPF-42010-2022` and `SRC-BDPF-42030-2019` inform domain prompts without creating external authority. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `FormalClaimAdmissibilityAndLensFit` | `4` | 4 — Ordinal 0..5 values, exact labels, not-triggered guard and no-average policy are used lawfully; the disposition is explicitly evaluation-only. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `FalsifiabilityAndLoweringCondition` | `4` | 4 — Use, decision/projection edition, evidence locus, floor or source/structure/work relation change requires re-evaluation. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `CorpusEntryProjectionAndEcologyFit` | `4` | 4 — ToC trigger, Readme entry, Pattern Index row and acceptance-case routing align with the pattern body. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |
| `EvolutionFrontAndRefreshDiscipline` | `4` | 4 — Reopen conditions and BDPF.11/G.11/E.23 routes identify the smallest evolution locus. A value of 3 would understate the by-value loci and actionable boundaries; 5 would overstate because no independent inter-rater, cross-project or downstream-use replay supports exceptional expression. |

**Result:** `admissibleForDeclaredUse` at the declared floor of `4` for bounded authoring and pilot-use input. No average is issued. The shared blocker against `5` is absence of repeated heterogeneous field transfer; that absence remains package coordinate `D8=3` rather than being hidden inside the pattern result.


# Refresh Route

```text
RefreshRoute@BuiltAssetDesignPrinciplesFramework:
  frameworkEditionRef: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1
  sourceCurrentnessOwnerRef: G.11
  qualityFramingOwnerRef: E.22
  improvementOwnerRef: E.23
  packageAdequacyOwnerRef: E.4.DPF.DA
  patternQualityOwnerRef: E.21
  relationAndEditionOwnerRef: E.4.PFR
  refreshTriggers:
    - cited FPF Core pattern semantic or edition change
    - official/source-map edition or adopted-payload change
    - project pilot contradicts a problem frame, solution move, boundary or check
    - repeated defect not owned by current pattern set
    - E.21 pattern coordinate below declared floor
    - E.4.DPF.DA coordinate below declared package-use floor
    - access/publication carrier introduces loss or authority overread
    - local term repeatedly fails owner restoration
    - generated/tool-assisted use changes admission or evidence boundary
  firstRefreshAction: create smallest impact trace over affected pattern, relation, source row, carrier or quality result
  editionDecision: noChange | sourceRowRefresh | localPatternRepair | relationRecordRepair | carrierRepair | newPackageEdition | deprecateOrSplitPattern | proposeCoreAmendment
  blockedOverread: refresh trigger is not proof that the package or all dependent project records are invalid
  closureCondition: affected claims have owner-specific disposition, changed versions are evaluated, edition/currentness records are published and stale carriers are superseded or bounded
```

## Trigger-to-owner table

| Trigger | First affected object | First action | New edition required when… |
| --- | --- | --- | --- |
| FPF Core change | Dependency/PFR and affected pattern semantics | Compare exact slots/boundaries; create impact trace | governed result kind, relation, scale, value or boundary changes materially |
| Standard/source edition change | Source row and consuming pattern/project claim | Review adopted payload and applicability | pattern solution/check/boundary or package source basis changes |
| One pilot defect | Exact pattern use/project record | Local repair or no-impact disposition | only if defect reveals a recurring package-level gap |
| Repeated cross-case defect | Method/pattern family | E.22 frame + E.23 change/re-evaluation | selected pattern content or relation set changes |
| Low E.21 coordinate | One pattern version | Repair weakest coordinate; re-evaluate | published pattern text/semantics changes |
| Low DPF package coordinate | Carrier/relation/source/pattern set | Repair smallest package locus | selected pattern set, package architecture or qualification changes |
| New access service/assistant | Access/publication carrier | Apply PFM10, C.35, currentness and authority boundaries | new access carrier becomes part of package edition |
| New local vocabulary | Name/bridge/precision map | Recover owner; add local bridge only if recurring | durable public package term/record changes |
| Generated candidate/record use | Produced carrier admission | Apply C.35 and direct owner checks | package begins to govern a new generation/admission problem |

## Improvement loop for one pattern

```text
E.21 result row or field failure
→ E.22 quality-evaluation question frame
→ one exact repair proposal with predicted coordinate change and protected tradeoffs
→ change one pattern/carrier/relation/source row version
→ re-run E.21 or E.4.DPF.DA
→ accept | revise | reject | hold
→ publish edition/supersession/currentness through E.4.PFR/G.11
```

Do not call wording edits, added examples, new checklists or prompt retries improvements until the changed object version is re-evaluated.

## Promotion conditions for the next package edition

A v0.6/stable-candidate decision should not be made until:

1. at least two heterogeneous field pilots are complete;
2. the four priority E.21 records are re-evaluated against field findings, and individual E.21 evaluations exist for the remaining public pattern set required by the promoted use;
3. no triggered pattern has a declared-use blocking coordinate below its floor;
4. one source-change impact and one representation-loss route have been exercised;
5. local role/authority mappings and project regulatory sources remain external/direct-owner records;
6. PFM10 is evaluated if any access/assistant carrier exists;
7. package `D8` reaches at least `4` for the promoted declared use;
8. a new `PrincipleFrameworkArchitectureDecision@Context` states selected pattern set, relation structure, publication/access architecture, evidence, losses and supersession.

## Deprecation and supersession

- Never delete an edition from traceability when project records cite it.
- Mark deprecated pattern/edition, replacement and migration boundary.
- Do not infer compatibility from version numbering; state impact explicitly.
- Existing project records remain governed by their cited edition until migrated or bounded by a currentness/impact decision.
- When a domain discovery appears universal, submit it through an explicit Core amendment decision; do not make FPF Core depend on this DPF.

---

# Recommended Citation

```text
Built Asset Design Principles Framework (BDPF).
Package edition: BuiltAssetDesignPrinciplesFramework@2026-07-13-v0.5.1.
Dependency: First Principles Framework Core Conceptual Specification@July2026.
Status: locallyUsableWithVisibleLimits for bounded pilot use.
```

# End Of Package Carrier
