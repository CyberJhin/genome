# Genome Model

Status: APPROVED

Baseline version: v0.1

Purpose:
Модель генома, наследуемое состояние и исходные контракты. Существующие контракты сохранены из baseline; новая техническая архитектура не создаётся.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Текущий путь каталога: [data/genome_v1.yaml](../../data/genome_v1.yaml). Упоминание `genome_v1_catalog.yaml` внутри дословного baseline ниже — историческое имя этого же файла, а не отдельный действующий каталог.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 4, 5, 6, 16.

<!-- baseline:GDS:4:start -->
## 4. Biological model
Creatures are a fictional **diploid hermaphroditic species**.

This preserves near-real genetics while avoiding male/female matching friction.

### 4.1 MVP genome
- 6 chromosome pairs
- 24 functional loci
- ~4 loci per chromosome
- 2 inherited chromosome copies per pair
- 48 inherited allele copies total

Each locus stores:
```text
chromosome_id
position_cM
locus_id
allele_left
allele_right
```

`position_cM` is a simplified genetic-map position used for linkage/recombination.

Nearby loci must be inherited together more often. Independent random inheritance per locus is not acceptable.
<!-- baseline:GDS:4:end -->

<!-- baseline:GDS:5:start -->
## 5. Alleles and expression models
### 5.1 Complete dominance
```text
G = glow
g = no glow
GG -> glow
Gg -> glow
gg -> no glow
```

### 5.2 Incomplete dominance
```text
C1/C1 -> green
C1/C2 -> turquoise
C2/C2 -> blue
```

### 5.3 Codominance
Both alleles are expressed, useful for markings and dual-color regions.

### 5.4 Recessive traits
```text
F/F -> normal
F/f -> normal carrier
f/f -> frost phenotype
```

### 5.5 Polygenic traits
At least some characteristics use several loci:
- body size;
- energy capacity;
- fertility;
- expedition endurance;
- curiosity;
- heat/cold tolerance.

Formula class:
```text
phenotype = base + sum(allele effects) + bounded environment modifier
```

### 5.6 Epistasis
Some genes suppress or modify others.

Example:
```text
Pigment locus says orange.
Albino locus aa suppresses pigment.
Phenotype is pale/white, genotype still carries orange.
```
<!-- baseline:GDS:5:end -->

<!-- baseline:GDS:6:start -->
## 6. Genotype vs phenotype
Genotype is inherited biological state. Phenotype is expressed result:
```text
genotype + gene interactions + developmental state + environment = phenotype
```

Care, level or habitat must never silently rewrite genotype.
<!-- baseline:GDS:6:end -->

<!-- baseline:GDS:16:start -->
## 16. Environment and gene expression
Some loci may be environment-sensitive.

Example:
```text
Seasonal pigment gene:
Cold habitat -> pale expression
Warm habitat -> bright expression
```

Genotype remains unchanged.
<!-- baseline:GDS:16:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 5, 22, 24, 25.

<!-- baseline:DB:5:start -->
## 5. Карта генома

| Chr | cM | Locus | Category | Model |
|---|---:|---|---|---|
| CHR1 | 8 | `BDY1` | VISUAL | INCOMPLETE_DOMINANCE_VECTOR |
| CHR1 | 31 | `SIZ1` | VISUAL_QUANTITATIVE | ADDITIVE |
| CHR1 | 61 | `APP1` | VISUAL | CODOMINANT_COMPOSITION |
| CHR1 | 88 | `TAI1` | VISUAL | COMPLETE_DOMINANCE |
| CHR2 | 5 | `COL1` | VISUAL | PALETTE_BLEND |
| CHR2 | 24 | `SEC1` | VISUAL | COMPLETE_DOMINANCE |
| CHR2 | 52 | `PAT1` | VISUAL | CODOMINANT_PATTERN |
| CHR2 | 82 | `GLW1` | VISUAL | DOSAGE_WITH_SPECIAL |
| CHR3 | 12 | `EYE1` | VISUAL | ADDITIVE_ROUNDED |
| CHR3 | 35 | `EYS1` | VISUAL | COMPLETE_DOMINANCE |
| CHR3 | 63 | `SKN1` | VISUAL | COMPLETE_DOMINANCE |
| CHR3 | 90 | `MRK1` | VISUAL | COMPLETE_DOMINANCE |
| CHR4 | 10 | `AQU1` | ADAPTATION | ADDITIVE |
| CHR4 | 37 | `CLD1` | ADAPTATION | ADDITIVE |
| CHR4 | 66 | `HOT1` | ADAPTATION | ADDITIVE |
| CHR4 | 91 | `PHO1` | ADAPTATION | ADDITIVE |
| CHR5 | 7 | `ENR1` | QUANTITATIVE | ADDITIVE |
| CHR5 | 32 | `END1` | QUANTITATIVE | ADDITIVE |
| CHR5 | 59 | `CUR1` | TEMPERAMENT | ADDITIVE |
| CHR5 | 86 | `CAL1` | TEMPERAMENT | ADDITIVE |
| CHR6 | 9 | `MET1` | METABOLISM | ADDITIVE |
| CHR6 | 34 | `DEF1` | HIDDEN_HEALTH | RECESSIVE |
| CHR6 | 60 | `DEF2` | HIDDEN_HEALTH | RECESSIVE |
| CHR6 | 84 | `IMM1` | HIDDEN_HEALTH | RECESSIVE |
<!-- baseline:DB:5:end -->

<!-- baseline:DB:22:start -->
## 22. Что обязано быть data-driven

Chromosome map, loci, alleles, founder frequencies, mutation edges, trait contributions, morphotype rules, expedition weights и founder genomes берутся из `genome_v1_catalog.yaml`. Не размазывать их по switch/case.
<!-- baseline:DB:22:end -->

<!-- baseline:DB:24:start -->
## 24. Versioning

Любое изменение locus, allele, mutation edge, formula или morphotype threshold повышает `genome_schema_version`. Существующие creatures хранят schema version; генетику старых существ нельзя молча переписать.
<!-- baseline:DB:24:end -->

<!-- baseline:DB:25:start -->
## 25. Implementation contract

```text
CATALOG -> GENOTYPE -> PHENOTYPE ENGINE -> DERIVED STATS -> MORPHOTYPE/ECOTYPES -> UI/GAMEPLAY
```

Breeding:
```text
PARENT A --meiosis/recombination--\
                                  CHILD GENOME -> mutation -> phenotype -> creature
PARENT B --meiosis/recombination--/
```

Игровой принцип, который нельзя потерять: **«I bred this», а не «the game rolled this for me».**
<!-- baseline:DB:25:end -->
