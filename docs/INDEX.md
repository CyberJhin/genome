# GENOME — Design Index

Status: APPROVED

Статус этого индекса относится к организации baseline. Он не утверждает DRAFT/OPEN/NOT_STARTED блоки.

## Product thesis

«I bred this.» Игрок разводит популяции, строит линии, изучает наследование и получает редкие, стабильные и полезные сочетания генов. Его решения через поколения видны в геноме, родословной и фенотипе потомков. Источник: [Game Vision](canon/GAME_VISION.md), GDS §0, §46.

## Baseline design blocks

Статус и версия разделены: используются только APPROVED, DRAFT, OPEN, NOT_STARTED. APPROVED v0.1 не означает, что пробелы исходников решены. Подразделы наследуют только уже заданный scope одобрения; новые согласованные решения зафиксированы отдельно в CANON UPDATE 001; APPROVED не распространяется на неописанную детализацию.

| Design block | Status | Baseline version | Canonical docs |
|---|---|---|---|
| Game Vision | APPROVED | — | [Vision](canon/GAME_VISION.md), [Principles](canon/DESIGN_PRINCIPLES.md) |
| Core Genetics | APPROVED | v0.1 | [Genome](genetics/GENOME_MODEL.md), [Content Bible](genetics/GENETIC_CONTENT_BIBLE.md), [Terminology](canon/TERMINOLOGY.md) |
| Creature Model | APPROVED | v0.1 | [Creature](creatures/CREATURE_MODEL.md), [Morphotypes](creatures/MORPHOTYPES.md), [Ecotypes](creatures/ECOTYPES.md) |
| Breeding principles | APPROVED | v0.1 | [Breeding](genetics/BREEDING_SYSTEM.md), [Lineage](genetics/LINEAGE_SYSTEM.md) |
| Mutation model | APPROVED | v0.1 | [Mutation](genetics/MUTATION_SYSTEM.md) |
| Genetic diversity principles | APPROVED | DIV-001–DIV-005 only | [Diversity Model](genetics/GENETIC_DIVERSITY_MODEL.md) |
| Combat | DRAFT | COMBAT-001–COMBAT-004 | [Core](combat/COMBAT_CORE.md), [Stats](combat/COMBAT_STATS.md), [Roles](combat/ROLES.md), [Counters](combat/COUNTERS.md), [Genetic Abilities](combat/GENETIC_ABILITIES.md) |
| Combat Balance | NOT_STARTED | — | [Combat Balance stub](balance/BALANCE_MODEL.md#combat-balance) |
| Progression | DRAFT | — | [Progression](progression/PROGRESSION.md), [Pacing](progression/PACING.md), [Collection](creatures/COLLECTION_SYSTEM.md) |
| Economy | DRAFT | — | [Economy](economy/ECONOMY.md) |
| Monetization | DRAFT | — | [Monetization](economy/MONETIZATION.md) |
| Seasonal content | DRAFT | — | [Seasons](progression/SEASONS.md) |
| Genetics balance documentation | DRAFT | — | [Existing targets](balance/BALANCE_MODEL.md), [Existing simulation requirements](balance/SIMULATION_SPEC.md) |

## Работа с каноном

- [DECISIONS](DECISIONS.md) — решения baseline и COMBAT/DIV из CANON UPDATE 001.
- [CANON UPDATE 001](updates/GENOME_CANON_UPDATE_001.md) — основание новых решений; имеет приоритет только для явно затронутых пунктов.
- [OPEN_QUESTIONS](OPEN_QUESTIONS.md) — противоречия, неполные правила и будущие решения; все имеют Status: OPEN.
- [CHANGELOG](CHANGELOG.md) — организационные изменения и consistency review.
- [CONTRIBUTING_DESIGN](../CONTRIBUTING_DESIGN.md) — правила CANON UPDATE.
- [README / Source of Truth](../README.md#source-of-truth) — иерархия источников истины.

## Machine-readable catalogs

- [genome_v1.yaml](../data/genome_v1.yaml) — исходный `genome_v1_catalog.yaml`, перенесён без изменения байтов. Содержит также исходные actions, resources и expeditions; они не дублируются в другом каталоге.
- [combat_v1.yaml](../data/combat_v1.yaml) — DRAFT: только team size, auto/async, три позиции и round-based model. Не исполнимый каталог.
- [abilities_v1.yaml](../data/abilities_v1.yaml) — NOT_STARTED, stub.
- [progression_v1.yaml](../data/progression_v1.yaml) — DRAFT, навигационная заготовка без новых значений.

## Точка плана и следующий design block

- Шаг 1: baseline документации завершён.
- Шаг 2A: COMBAT-001–COMBAT-004 зафиксированы; Combat целиком DRAFT. Round/targeting/victory details остаются OPEN. Детальные stubs и Combat Balance сохраняют NOT_STARTED, поскольку их дизайн не утверждён.
- Шаг 2B: DIV-001–DIV-005 APPROVED только как принципы; Content Bible и баланс не завершены.
- Следующий обсуждаемый блок — 2C: боевые характеристики, отдельные функции и trade-off, затем ecotypes/counters.
- Шаг 3: полное независимое ревью Combat ещё не начинается.
- Шаг 4: полный Genetic Content Bible и расширение генома позже. APPROVED у существующего каталога v0.1 не означает утверждения будущего полного каталога.

OQ-017 остаётся OPEN: Combat разрешено документировать, но точная комплектация first playable и разрешение писать код не согласованы. Прежнее «PvP вне first playable» не запрещает design-работу. Новые OQ-020–OQ-024 описывают недостающие детали основы и разнообразия. OQ-001–OQ-016, OQ-018–OQ-019 остаются OPEN; update не задаёт вероятности, формулы, expression, pedigree или новые размеры каталога. Экономические ограничения и конкурентный эффект мест/инкубаторов также не доказаны (OQ-018).

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

Вводная GDS сохранена в Game Vision; вводная DB — в Terminology. BALANCE_MODEL содержит ссылки на существующие определения. COMBAT_CORE обновлён по Update 001; остальные combat-документы сохраняются как stubs. Новый GENETIC_DIVERSITY_MODEL содержит DIV-001–DIV-005; это дополнение к карте исходного baseline, а не перенос или изменение исходных разделов.
