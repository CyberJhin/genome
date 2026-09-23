# Collection System

Status: DRAFT

Purpose:
Коллекция, reserve, Codex, знания и rarity; полного утверждения отдельного блока в заданном baseline нет.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус документа остаётся DRAFT; перенос исходного текста не утверждает решения блока и не закрывает OPEN questions. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 18, 19, 22, 23, 24.

<!-- baseline:GDS:18:start -->
## 18. Sequencing / Laboratory
Laboratory turns random-looking outcomes into intentional selection.

### 18.1 Knowledge states per locus
```text
Unknown
Phenotype inferred
One allele inferred
Fully sequenced
```

### 18.2 Tests
- Basic phenotype scan: cheap/free, visible traits and likely class.
- Marker panel: selected loci.
- Full sequencing: complete genome.

Full sequencing must be obtainable through gameplay, not paid-only.

### 18.3 Why hidden genotype matters
```text
Parent A: normal, F/f
Parent B: normal, F/f
Expected child:
25% F/F
50% F/f carrier
25% f/f -> Frost
```

Before sequencing, only “latent trait possible” may be known.
<!-- baseline:GDS:18:end -->

<!-- baseline:GDS:19:start -->
## 19. Collection and reserve
### Active collection
Frequently used creatures.

### Genetic reserve
Archived creatures remain alive and keep genome, pedigree, breeding history and discovery status.

Never force permanent destruction of genetic history due to slot pressure.
<!-- baseline:GDS:19:end -->

<!-- baseline:GDS:22:start -->
## 22. Codex
Global/personal genetics encyclopedia.

Sections:
```text
Morphology
Pigments
Patterns
Adaptations
Metabolism
Temperament
Mutations
Hidden disorders
```

Knowledge stages:
```text
Unknown
Observed
Sequenced
Bred successfully
Stabilized in a line
```

The goal is not merely to collect pictures; it is to understand and reproduce the genome.
<!-- baseline:GDS:22:end -->

<!-- baseline:GDS:23:start -->
## 23. Global discoveries
Some alleles begin globally undiscovered.

Record:
- first phenotype observed;
- first allele sequenced;
- first homozygous individual;
- first stable line.

Example:
```text
AURORA GENE
First observed: Dinis — 2026-10-14
First stabilized: Masha — 2026-10-21
```
<!-- baseline:GDS:23:end -->

<!-- baseline:GDS:24:start -->
## 24. Rarity
Primary rarity must derive from actual population frequency.

Example:
```text
Aurora allele frequency: 0.21%
Aurora visible phenotype: 0.07%
Living creatures: 1,283
Exact phenotype combination: 1 in 18,430
```

UI may map this to labels, but underlying truth is frequency-based.
<!-- baseline:GDS:24:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 16, 20.

<!-- baseline:DB:16:start -->
## 16. Knowledge / Laboratory

Per-locus knowledge states: `UNKNOWN`, `PHENOTYPE_INFERRED`, `ONE_ALLELE_INFERRED`, `FULLY_SEQUENCED`. Basic scan не меняет genome. Marker panel стоит 20 Research Points, full sequence — 80 baseline.
<!-- baseline:DB:16:end -->

<!-- baseline:DB:20:start -->
## 20. Rarity

Rarity выводится из мировой population frequency. Нельзя хранить `EPIC` как первичную случайную характеристику существа.
- `COMMON`: {'min_frequency': 0.1}
- `UNCOMMON`: {'min_frequency': 0.03, 'max_frequency': 0.1}
- `RARE`: {'min_frequency': 0.005, 'max_frequency': 0.03}
- `EXCEPTIONAL`: {'min_frequency': 0.0005, 'max_frequency': 0.005}
- `ULTRA_RARE`: {'max_frequency': 0.0005}

До population >=1000 псевдоточная rarity не показывается.
<!-- baseline:DB:20:end -->
