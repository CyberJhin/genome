# Lineage System

Status: APPROVED

Baseline version: v0.1

Purpose:
Родословные, линии и принципы генетического риска.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 11, 12, 20, 21.

<!-- baseline:GDS:11:start -->
## 11. Recessive defects and inbreeding
Model inbreeding through shared hidden recessive alleles, not arbitrary “inbreeding -20%”.

Example:
```text
D = healthy
d = recessive metabolic defect
DD -> healthy
Dd -> healthy carrier
dd -> metabolic weakness
```

Possible consequences:
- lower expedition endurance;
- lower fertility;
- slower maturation;
- lower energy recovery.

Never kill or permanently invalidate a creature.

UI shows relatedness as Low / Moderate / High. Advanced view may show a coefficient.

The game teaches a trade-off:
> Pure lines become more predictable, but excessive homozygosity increases recessive risk.
<!-- baseline:GDS:11:end -->

<!-- baseline:GDS:12:start -->
## 12. Genetic health
Derived indicators may include:
- heterozygosity;
- known deleterious homozygotes;
- known carrier loci;
- genetic diversity score.

These are explanatory statistics, not arbitrary power scores.
<!-- baseline:GDS:12:end -->

<!-- baseline:GDS:20:start -->
## 20. Pedigree
Every non-founder records:
```text
parent_a_id
parent_b_id
generation
birth_timestamp
breeder_id
```

Pedigree supports relatedness, recessive-risk reasoning and lineage prestige.
<!-- baseline:GDS:20:end -->

<!-- baseline:GDS:21:start -->
## 21. Lines
A line is a player-defined breeding project.

Examples:
```text
Aurora Line — stabilize Aurora Glow + Frost resistance
Pure Botanical — homozygous Botanical traits
Deep Water — Water III + endurance + bioluminescence
```

Player can pin target alleles, target phenotype and forbidden defects.

Progress example:
```text
Aurora Line — Generation 7
Target loci stabilized: 4/6
Aurora: homozygous ✓
Frost: heterozygous
Endurance: 72%
Defect D1: carrier ⚠
```
<!-- baseline:GDS:21:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 14.

<!-- baseline:DB:14:start -->
## 14. Relatedness / inbreeding

Pedigree анализируется до 5 поколений. UI tiers: `LOW`, `MODERATE`, `HIGH`, `VERY_HIGH`. Основной смысл риска — более высокая вероятность встретить одинаковый скрытый recessive allele, а не произвольный штраф.

Для общего ancestor A:
```text
contribution = (1/2)^(n1+n2) * (1 + F_A)
```
<!-- baseline:DB:14:end -->
