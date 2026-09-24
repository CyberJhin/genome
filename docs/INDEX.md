# GENOME — Design Index

Status: APPROVED

Статус этого индекса относится к организации baseline. Он не утверждает DRAFT/OPEN/NOT_STARTED блоки.

## Product thesis

«I bred this.» Игрок разводит популяции, строит линии, изучает наследование и получает редкие, стабильные и полезные сочетания генов. Его решения через поколения видны в геноме, родословной и фенотипе потомков. Источник: [Game Vision](canon/GAME_VISION.md), GDS §0, §46.

## Baseline design blocks

Статус и версия разделены: используются только APPROVED, DRAFT, OPEN, NOT_STARTED. APPROVED v0.1 не означает, что пробелы исходников решены. Подразделы наследуют только уже заданный scope одобрения; новые согласованные решения зафиксированы отдельно в CANON UPDATE 001–007; APPROVED не распространяется на неописанную детализацию.

| Design block | Status | Baseline version | Canonical docs |
|---|---|---|---|
| Game Vision | APPROVED | — | [Vision](canon/GAME_VISION.md), [Principles](canon/DESIGN_PRINCIPLES.md) |
| Core Genetics | APPROVED | v0.1 | [Genome](genetics/GENOME_MODEL.md), [Content Bible](genetics/GENETIC_CONTENT_BIBLE.md), [Terminology](canon/TERMINOLOGY.md) |
| Creature Model | APPROVED | v0.1 | [Creature](creatures/CREATURE_MODEL.md), [Morphotypes](creatures/MORPHOTYPES.md), [Ecotypes](creatures/ECOTYPES.md) |
| Breeding principles | APPROVED | v0.1 | [Breeding](genetics/BREEDING_SYSTEM.md), [Lineage](genetics/LINEAGE_SYSTEM.md) |
| Mutation model | APPROVED | v0.1 | [Mutation](genetics/MUTATION_SYSTEM.md) |
| Genetic diversity principles | APPROVED | DIV-001–DIV-005 only | [Diversity Model](genetics/GENETIC_DIVERSITY_MODEL.md) |
| Combat | DRAFT | COMBAT-001–COMBAT-021, только согласованные границы | [Core](combat/COMBAT_CORE.md), [Stats](combat/COMBAT_STATS.md), [Roles](combat/ROLES.md), [Counters](combat/COUNTERS.md), [Genetic Abilities](combat/GENETIC_ABILITIES.md) |
| Combat Stats | DRAFT | COMBAT-005–COMBAT-010: функции/понятия/качественные правила APPROVED; Precision DRAFT | [Stats](combat/COMBAT_STATS.md) |
| Counters | DRAFT | COMBAT-011–COMBAT-018: только качественные взаимодействия APPROVED | [Counters](combat/COUNTERS.md) |
| Genetic Abilities | DRAFT | COMBAT-019–COMBAT-021: только качественная модель APPROVED; каталог OPEN | [Genetic Abilities](combat/GENETIC_ABILITIES.md) |
| Roles | NOT_STARTED | — | [Roles](combat/ROLES.md) |
| Combat Balance | NOT_STARTED | — | [Combat Balance stub](balance/BALANCE_MODEL.md#combat-balance) |
| Progression | DRAFT | — | [Progression](progression/PROGRESSION.md), [Pacing](progression/PACING.md), [Collection](creatures/COLLECTION_SYSTEM.md) |
| Economy | DRAFT | — | [Economy](economy/ECONOMY.md) |
| Monetization | DRAFT | — | [Monetization](economy/MONETIZATION.md) |
| Seasonal content | DRAFT | — | [Seasons](progression/SEASONS.md) |
| Genetics balance documentation | DRAFT | — | [Existing targets](balance/BALANCE_MODEL.md), [Existing simulation requirements](balance/SIMULATION_SPEC.md) |

## Работа с каноном

- [DECISIONS](DECISIONS.md) — решения baseline и COMBAT/DIV из CANON UPDATE 001–007.
- [CANON UPDATE 001](updates/GENOME_CANON_UPDATE_001.md) — основание новых решений; имеет приоритет только для явно затронутых пунктов.
- [CANON UPDATE 002](updates/GENOME_CANON_UPDATE_002.md) — функции семи характеристик, различие Charge/Charge Generation и направления цены; не полный Combat.
- [CANON UPDATE 003](updates/GENOME_CANON_UPDATE_003.md) — качественные правила производительности, корпуса и нервной системы; численная модель и баланс не утверждены.
- [CANON UPDATE 004](updates/GENOME_CANON_UPDATE_004.md) — первые взаимодействия оболочки, резонанса, восстановления и импульса; не полный каталог и не численная модель.
- [CANON UPDATE 005](updates/GENOME_CANON_UPDATE_005.md) — Помеха будущему поступлению Charge и защитная связь через перенос потери здоровья; только качественные взаимодействия и ограничения.
- [CANON UPDATE 006](updates/GENOME_CANON_UPDATE_006.md) — цена массового охвата и временное подавление лечения выбранной цели; только качественные взаимодействия и ограничения.
- [CANON UPDATE 007](updates/GENOME_CANON_UPDATE_007.md) — наследуемая композиция поведения, объяснимые инстинкты, реактивные связки и мутации регуляции; Genetic Abilities DRAFT, каталог и алгоритмы OPEN.
- [OPEN_QUESTIONS](OPEN_QUESTIONS.md) — противоречия, неполные правила и будущие решения; все имеют Status: OPEN.
- [CHANGELOG](CHANGELOG.md) — организационные изменения и consistency review.
- [CONTRIBUTING_DESIGN](../CONTRIBUTING_DESIGN.md) — правила CANON UPDATE.
- [README / Source of Truth](../README.md#source-of-truth) — иерархия источников истины.

## Machine-readable catalogs

- [genome_v1.yaml](../data/genome_v1.yaml) — исходный `genome_v1_catalog.yaml`, перенесён без изменения байтов. Содержит также исходные actions, resources и expeditions; они не дублируются в другом каталоге.
- [combat_v1.yaml](../data/combat_v1.yaml) — DRAFT: только team size, auto/async, три позиции и round-based model. Не исполнимый каталог.
- [abilities_v1.yaml](../data/abilities_v1.yaml) — NOT_STARTED, stub; качественная модель Genetic Abilities DRAFT не создаёт машинный каталог.
- [progression_v1.yaml](../data/progression_v1.yaml) — DRAFT, навигационная заготовка без новых значений.

## Точка плана и следующий design block

- Шаг 1: baseline документации завершён.
- Шаг 2A: COMBAT-001–COMBAT-004 зафиксированы; Combat целиком DRAFT. Round/targeting/victory details остаются OPEN. Roles и Combat Balance сохраняют NOT_STARTED; Genetic Abilities по Update 007 — DRAFT; Combat Stats по Update 002 — DRAFT, Counters по Update 004 — DRAFT.
- Шаг 2B: DIV-001–DIV-005 APPROVED только как принципы; Content Bible и баланс не завершены.
- Шаг 2C: функции характеристик зафиксированы Update 002, качественная цена специализации согласована в COMBAT-008–COMBAT-010 (Update 003). Combat и Combat Stats остаются DRAFT; Precision — DRAFT-кандидат. Численные формулы, коэффициенты, связь с генетическим каталогом и проверка баланса остаются OPEN; численная модель 2C не завершена.
- Шаг 2D частично согласован: Update 004 фиксирует первые две группы взаимодействий — оболочка/резонанс и восстановление/импульс; Update 005 добавляет COMBAT-015 (Помеха будущему поступлению Charge) и COMBAT-016 (защитная связь через перенос потери здоровья); Update 006 добавляет COMBAT-017 (цена массового охвата) и COMBAT-018 (подавление лечения выбранной цели). Это не исчерпывающий каталог направлений, не готовые Roles/Genetic Abilities и не завершённый 2D. Combat, Combat Stats и Counters остаются DRAFT; Precision — DRAFT-кандидат.
- Update 007 добавляет COMBAT-019–COMBAT-021: основу наследуемых связок и инстинктов для совместимости внутри 2D и как зависимость будущего блока Genetic Abilities. Genetic Abilities DRAFT; это не завершение 2D, запуск полного каталога 2E или шага 4.
- После проверки фиксации и переноса в main следующий вопрос внутри 2D — конкретные правила выбора действия при конкурирующих условиях, ожидание окна и запасное действие; на них проверяется совместная работа механизмов. Численные формулы 2C и связь с генетическим каталогом остаются открытыми зависимостями; Precision решается с таргетингом. В этой задаче следующие этапы не начинаются.
- Шаг 3: полное независимое ревью Combat ещё не начинается.
- Шаг 4: полный Genetic Content Bible и расширение генома позже. APPROVED у существующего каталога v0.1 не означает утверждения будущего полного каталога.

OQ-017 остаётся OPEN: Combat разрешено документировать, но точная комплектация first playable и разрешение писать код не согласованы. Прежнее «PvP вне first playable» не запрещает design-работу. OQ-020–OQ-024 описывают недостающие детали основы и разнообразия. Update 002 частично уточнил OQ-021–OQ-023; Update 003 уточнил качественную часть OQ-023; Update 004 частично уточняет OQ-023–OQ-024 и добавляет в OQ-022 ссылку на тайминг взаимодействий, без закрытия вопросов. Update 005 частично уточняет OQ-022–OQ-024 и различие переноса потери здоровья/перехвата атаки в OQ-021; формулы, пределы, длительности, доля переноса и порядок массовых атак остаются OPEN. Update 006 частично уточняет OQ-021–OQ-024: охват и допустимые цели, очередь массовых событий, цена концентрации и ограниченное подавление лечения; схема охвата, расчёты и связь подавления с Control/Stability не утверждены. Update 007 частично уточняет OQ-022 и OQ-024: качественная основа инстинктов и связок согласована, алгоритмы, генетические источники и каталог OPEN; OQ-021/OQ-023 сохраняются как зависимости. OQ-003, OQ-016, OQ-017, OQ-024 и все остальные вопросы сохраняются OPEN. OQ-001–OQ-016, OQ-018–OQ-019 остаются OPEN; update не задаёт вероятности, формулы, expression, pedigree или новые размеры каталога. Экономические ограничения и конкурентный эффект мест/инкубаторов также не доказаны (OQ-018).

## Baseline sources и карта переноса

- [GDS — GENOME_GAME_DESIGN_SPEC_v0.1.md](source/GENOME_GAME_DESIGN_SPEC_v0.1.md)
- [DB — GENOME_DOMAIN_BIBLE_v0.1.md](source/GENOME_DOMAIN_BIBLE_v0.1.md)

Оба исходника сохранены без изменения байтов. Номера, формулы, примеры, рекомендации и оговорки в перенесённых разделах сохранены дословно; редакционные пояснения находятся вне них. Старые имена файлов внутри baseline — исторические ссылки. При конфликте baseline нет автоматического приоритета GDS над DB или наоборот: вопрос остаётся OPEN до CANON UPDATE.

Каждый нумерованный раздел имеет ровно одно тематическое место. Повторы, уже существовавшие между GDS и DB, сохранены с указанием источника и не объявляются новыми независимыми решениями.

| Canonical document | GDS sections | DB sections |
|---|---|---|
| [Game Vision](canon/GAME_VISION.md) | 0, 1, 40, 46 | — |
| [Design Principles](canon/DESIGN_PRINCIPLES.md) | 2, 3, 41, 43, 44, 45 | 23 |
| [Terminology](canon/TERMINOLOGY.md) | — | 2 |
| [Genome Model](genetics/GENOME_MODEL.md) | 4, 5, 6, 16 | 5, 22, 24, 25 |
| [Breeding System](genetics/BREEDING_SYSTEM.md) | 8, 9, 13, 17, 28, 33, 34, 35 | 13, 15 |
| [Mutation System](genetics/MUTATION_SYSTEM.md) | 10 | 11, 12 |
| [Lineage System](genetics/LINEAGE_SYSTEM.md) | 11, 12, 20, 21 | 14 |
| [Genetic Content Bible](genetics/GENETIC_CONTENT_BIBLE.md) | 39 | 6 |
| [Creature Model](creatures/CREATURE_MODEL.md) | 7, 14, 15, 25, 32 | 1, 3, 4, 7, 8, 21 |
| [Morphotypes](creatures/MORPHOTYPES.md) | — | 10 |
| [Ecotypes](creatures/ECOTYPES.md) | — | 9 |
| [Collection System](creatures/COLLECTION_SYSTEM.md) | 18, 19, 22, 23, 24 | 16, 20 |
| [Progression](progression/PROGRESSION.md) | 26, 27, 37 | 17, 18 |
| [Pacing](progression/PACING.md) | 29, 36 | — |
| [Seasonal Content](progression/SEASONS.md) | 38 | — |
| [Economy](economy/ECONOMY.md) | 30 | 19 |
| [Monetization](economy/MONETIZATION.md) | 31 | — |
| [Simulation Spec](balance/SIMULATION_SPEC.md) | 42 | — |

Вводная GDS сохранена в Game Vision; вводная DB — в Terminology. BALANCE_MODEL содержит ссылки на существующие определения. COMBAT_CORE содержит основу Update 001 и ссылки на Update 002–007; COMBAT_STATS сохраняет определения Update 002 и качественные правила Update 003; COUNTERS фиксирует взаимодействия Update 004–006. Roles остаётся stub; GENETIC_ABILITIES фиксирует COMBAT-019–COMBAT-021 из Update 007 и имеет статус DRAFT. Новый GENETIC_DIVERSITY_MODEL содержит DIV-001–DIV-005; это дополнение к карте исходного baseline, а не перенос или изменение исходных разделов.
