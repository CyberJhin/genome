# Mutation System

Status: APPROVED

Baseline version: v0.1

Purpose:
Модель мутаций и mutation-only alleles.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Переходы и rates: [genome_v1.yaml](../../data/genome_v1.yaml), `mutation`. Неполнота графа и structural events: OQ-007.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 10.

<!-- baseline:GDS:10:start -->
## 10. Mutation system
Mutation must be rare enough to feel special but common enough to appear during normal play. Real rates are too low for game pacing, so GENOME uses accelerated fictional mutation rates while preserving genetic logic.

### 10.1 Base target
```text
Probability an offspring gets >=1 mutation: ~1–3%
```
Balancing target, not universal constant.

### 10.2 MVP mutation types
- allele mutation;
- novel allele discovery;
- controlled structural cosmetic mutation.

Novel alleles may be absent from the founder population and enter through mutation or seasonal introduction.

### 10.3 Mutation graph
Mutations must follow explicit transitions.
Bad:
```text
any allele -> any allele equally
```
Good:
```text
Green -> Cyan -> Blue
Green -> Yellow
Blue -> Violet
```
<!-- baseline:GDS:10:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 11, 12.

<!-- baseline:DB:11:start -->
## 11. Mutation-only alleles

- `COL1:c3` — Violet
- `PAT1:p3` — Fractal
- `GLW1:g3` — AuroraGlow
- `SKN1:k3` — Prism
- `AQU1:q3` — Abyssal
- `CLD1:c3` — FrostCore
- `PHO1:f3` — Blacklight

Mutation-only alleles отсутствуют у founders. После первого возникновения наследуются как обычные alleles.
<!-- baseline:DB:11:end -->

<!-- baseline:DB:12:start -->
## 12. Mutation model

- per allele-copy mutation rate: `0.00035`
- structural event rate: `0.003`
- target: около 2% offspring с >=1 mutation; итог подтверждается simulation, не предположением.
- mutation переходы data-driven и лежат в YAML `mutation.edges`.
<!-- baseline:DB:12:end -->
