# Terminology

Status: APPROVED

Baseline version: v0.1

Purpose:
Исходный словарь сущностей; детальные определения находятся в тематических документах.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 2.

<!-- baseline:DB:2:start -->
## 2. Канонические сущности

| Entity | Что это | Основные поля |
|---|---|---|
| Creature | конкретное существо | id, owner, parents, genome, phenotype, state |
| Genome | 6 пар хромосом / 24 loci | две allele copies на locus |
| Phenotype | выраженный внешний/функциональный результат | body, colors, pattern, glow, stats |
| Pedigree | родословная | parent_a, parent_b, generation |
| Line | селекционный проект | target loci, forbidden conditions, generations |
| Morphotype | главное имя типа в UI | rule-derived |
| Ecotype | функциональный тег | BOTANICAL/AQUATIC/... |
| SequenceKnowledge | что игрок знает о genome | per-locus knowledge state |
<!-- baseline:DB:2:end -->

Источник: [Domain Bible](../source/GENOME_DOMAIN_BIBLE_v0.1.md), вводная часть.

<!-- baseline:DB:preamble:start -->
# GENOME — Domain Bible / Canonical Dictionary v0.1

**Назначение:** обязательный reference для реализации вместе с `GENOME_GAME_DESIGN_SPEC_v0.1.md`.

Этот документ отвечает на вопрос **«что именно существует в игре и что означает каждое поле/свойство»**. Если код, UI или тест противоречат этому словарю, сначала меняется словарь, потом реализация.
<!-- baseline:DB:preamble:end -->

Историческое имя Game Design Spec выше указывает на [сохранённый источник](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md). Это вводная baseline, а не отдельное правило разрешения противоречий.
