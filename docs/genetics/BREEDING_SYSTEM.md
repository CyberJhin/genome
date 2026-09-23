# Breeding System

Status: APPROVED

Baseline version: v0.1

Purpose:
Принципы скрещивания, рекомбинация и исходные примеры.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Founder genomes: [genome_v1.yaml](../../data/genome_v1.yaml), `founders`. [Cooldown](../progression/PACING.md). Примеры исходника с другими ID не являются разрешением добавлять alleles; см. OQ-001 и OQ-002.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 8, 9, 13, 17, 28, 33, 34, 35.

<!-- baseline:GDS:8:start -->
## 8. Meiosis and offspring generation
Offspring are created by simplified meiosis:
1. Each parent has chromosome pairs.
2. A gamete receives one recombined chromosome from each pair.
3. Crossover may exchange segments between homologs.
4. Two gametes combine into a diploid offspring genome.
5. Mutation is applied.
6. Genotype is translated into phenotype.
<!-- baseline:GDS:8:end -->

<!-- baseline:GDS:9:start -->
## 9. Recombination
Nearby loci are linked.

Example parental homologs:
```text
A: [Green] ---- [Spots] -------- [Glow]
B: [Blue ] ---- [Plain] -------- [NoGlow]
```

Without crossover, Green+Spots+Glow or Blue+Plain+NoGlow are common. Crossover can produce Green+Spots+NoGlow.

### 9.1 Simplified algorithm
For each chromosome during gamete production:
1. Randomly choose homolog A or B as starting source.
2. Generate crossover count using a bounded Poisson-like distribution.
3. Pick crossover positions along the map.
4. Switch source homolog after each crossover.
5. Read alleles from the recombinant chromosome.

Initial target distribution:
```text
0 crossovers: ~35%
1 crossover : ~45%
2 crossovers: ~17%
3 crossovers: ~3%
```
Balance later using simulation.
<!-- baseline:GDS:9:end -->

<!-- baseline:GDS:13:start -->
## 13. Starter population
New player receives:
```text
1 personal founder
+ access to 6–10 public laboratory breeders
```

Founder design requirements:
- no genetically doomed starts;
- common alleles represented;
- some rare alleles possible but not guaranteed;
- sufficient unrelatedness;
- player can breed without recruiting a human immediately.

Public breeders exist to bootstrap the game; player-owned social lines should become more valuable later.
<!-- baseline:GDS:13:end -->

<!-- baseline:GDS:17:start -->
## 17. Breeding flow
### Step 1 — choose Parent A
Adult from own collection.

### Step 2 — choose Parent B
Sources:
- own collection;
- public laboratory pool;
- friend's creature;
- breeding marketplace later.

### Step 3 — compatibility analysis
Casual view:
```text
Color: Green 50%, Blue 25%, Turquoise 25%
Leaves: Long 75%, Short 25%
Glow: Possible
Health risk: Low
```

Advanced view:
```text
COL1: C1/C2 × C1/C1
PAT2: P0/P3 × P3/P3
DEF1: D/d × D/D
```

Also show:
- relatedness;
- known carrier overlap;
- expected diversity;
- known phenotype probabilities;
- hidden outcomes;
- mutation baseline.

### Step 4 — confirm breeding
Consumes biological cooldown/time, not a casino ticket.

### Step 5 — gamete generation
Run recombination + inheritance + mutation.

### Step 6 — incubation
Egg exists; genome fixed.

### Step 7 — hatch
Reveal phenotype.

### Step 8 — analysis
Player chooses:
```text
Keep active
Move to reserve
Sequence
Add to breeding line
Use in expedition
Offer as breeding partner
```
<!-- baseline:GDS:17:end -->

<!-- baseline:GDS:28:start -->
## 28. Social breeding
Players can expose selected adults as breeding partners.

Request example:
```text
Use Nebula #82144 as Parent B?
Your creature: SOLARI #33802
Estimated offspring:
Water possible
Glow 62%
Botanical 50%
[Accept]
```

Second owner receives a non-power reward such as breeding credit, research points or a genetic sample. Offspring belongs to initiating player in MVP.
<!-- baseline:GDS:28:end -->

<!-- baseline:GDS:33:start -->
## 33. Example genome fragment
Creature A:
```text
COL1: C1/C2 -> turquoise
PAT2: P1/P1 -> stripes
LEF1: L2/L3 -> medium leaves
GLW1: G1/g  -> glow
CLD1: K2/K1 -> cold tolerance 2
DEF1: D/d   -> healthy carrier
```

Creature B:
```text
COL1: C2/C2 -> blue
PAT2: P1/P3 -> stripes + dots
LEF1: L1/L3 -> short-medium leaves
GLW1: g/g   -> no glow
CLD1: K1/K1 -> cold tolerance 1
DEF1: D/D   -> healthy
```

Child genotype comes from recombined parental gametes, never by independently rolling each displayed trait.
<!-- baseline:GDS:33:end -->

<!-- baseline:GDS:34:start -->
## 34. Example hidden recessive decision
Player wants frost phenotype.

Known:
```text
Parent A: F/f
Parent B: unknown
```
After sequencing B:
```text
Parent B: F/f
25% F/F
50% F/f
25% f/f -> Frost
```
Now the player can intentionally pursue the trait.
<!-- baseline:GDS:34:end -->

<!-- baseline:GDS:35:start -->
## 35. Example linkage decision
Two desired alleles are on the same chromosome in repulsion:
```text
copy A: G2 --- w0
copy B: g0 --- W3
```
Player wants:
```text
G2 --- W3
```
This requires crossover between the loci. Producing the line may take several generations.
<!-- baseline:GDS:35:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 13, 15.

<!-- baseline:DB:13:start -->
## 13. Recombination

Каждая хромосома рекомбинируется как единый haplotype. Локусы нельзя наследовать независимо. Baseline crossover count:
- 0: 35%
- 1: 45%
- 2: 17%
- 3: 3%
<!-- baseline:DB:13:end -->

<!-- baseline:DB:15:start -->
## 15. Starter public founders

| ID | Focus | Назначение |
|---|---|---|
| `LAB-F01` | VERDANT | ботанические genes |
| `LAB-F02` | SOLARI | photosynthesis + glow |
| `LAB-F03` | AQUALIS | aquatic line |
| `LAB-F04` | CRYALIS | cold line |
| `LAB-F05` | PYRA | heat line |
| `LAB-F06` | LUNARI | glow/face diversity |
| `LAB-F07` | GENERALIS_DIVERSE | unrelated diverse blood |
| `LAB-F08` | GENERALIS_CARRIER_TUTORIAL | tutorial hidden carriers |

Полные 24-locus genotypes каждого founder находятся в YAML и должны использоваться в tests/fixtures.
<!-- baseline:DB:15:end -->
