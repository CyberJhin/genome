# GENOME — Domain Bible / Canonical Dictionary v0.1

**Назначение:** обязательный reference для реализации вместе с `GENOME_GAME_DESIGN_SPEC_v0.1.md`.

Этот документ отвечает на вопрос **«что именно существует в игре и что означает каждое поле/свойство»**. Если код, UI или тест противоречат этому словарю, сначала меняется словарь, потом реализация.

## 1. Ключевая модель мира

В игре одна базовая синтетическая форма — `GENOMORPH`. Нет конечного списка из сотен заранее нарисованных видов. Каждый Creature — уникальный индивидуум: `genotype + pedigree + phenotype + mutable state`. `Solari`, `Aqualis`, `Cryalis` и т.п. — вычисляемые **morphotypes**, а не отдельные species.

Это важно для реализации: frontend не должен получать `solari.png`; он получает phenotype descriptor и собирает внешний вид из компонентов.

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

## 3. Creature — полный набор характеристик

### Наследуемые
Только `genome`. Любой наследуемый эффект обязан происходить из allele data.

### Вычисляемые
`phenotype`, `morphotype`, `ecotypes`, `aquatic`, `cold`, `heat`, `photosynthesis`, `energy_capacity`, `endurance`, `curiosity`, `calmness`, `metabolism`, `fertility`, `heterozygosity`, `health_state`, `rarity`.

### Изменяемые в течение жизни
`energy`, `mood`, `life_stage`, `maturity_progress`, `current_activity`, `breeding_ready_at`, `personal_name`, `knowledge_state`. Care никогда не переписывает genotype.

### Метаданные
`public_id`, `owner_id`, `generation`, `founder`, `parent_a_id`, `parent_b_id`, `born_at`, `genome_schema_version`, discovery flags.

## 4. Life stages

- `EGG` — 120 минут
- `JUVENILE` — 120 минут
- `ADOLESCENT` — 240 минут
- `ADULT` — постоянно

Смерти от старости/неактивности в v0.1 нет. Отсутствие игрока не уничтожает progress.

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

## 6. Полный каталог loci и alleles

### BDY1

- Chromosome: `CHR1` @ 8 cM
- Category: `VISUAL`
- Expression: `INCOMPLETE_DOMINANCE_VECTOR`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `b0` | Round | 45% | shape_vector={'width': 1.0, 'height': 1.0, 'lower_mass': 0.0} |
| `b1` | Pear | 35% | shape_vector={'width': 0.95, 'height': 1.05, 'lower_mass': 0.15} |
| `b2` | Tall | 20% | shape_vector={'width': 0.85, 'height': 1.15, 'lower_mass': -0.05} |

### SIZ1

- Chromosome: `CHR1` @ 31 cM
- Category: `VISUAL_QUANTITATIVE`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `s0` | Small | 25% | scale_effect=-0.08 |
| `s1` | Medium | 55% | scale_effect=0.0 |
| `s2` | Large | 20% | scale_effect=0.08 |

### APP1

- Chromosome: `CHR1` @ 61 cM
- Category: `VISUAL`
- Expression: `CODOMINANT_COMPOSITION`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `a0` | Antennae | 30% | renderer_asset=appendage_antennae; trait_modifiers={'curiosity_display': 5} |
| `a1` | Leaves | 40% | renderer_asset=appendage_leaves; trait_modifiers={'photosynthesis': 10} |
| `a2` | Fins | 30% | renderer_asset=appendage_fins; trait_modifiers={'aquatic': 10} |

### TAI1

- Chromosome: `CHR1` @ 88 cM
- Category: `VISUAL`
- Expression: `COMPLETE_DOMINANCE`
- Dominance: `t2 > t1 > t0`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `t0` | Nub | 45% | renderer_asset=tail_nub |
| `t1` | Curl | 40% | renderer_asset=tail_curl |
| `t2` | Fork | 15% | renderer_asset=tail_fork |

### COL1

- Chromosome: `CHR2` @ 5 cM
- Category: `VISUAL`
- Expression: `PALETTE_BLEND`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `c0` | Mint | 45% | palette_anchor=#66DDB2 |
| `c1` | Amber | 33% | palette_anchor=#F1B85B |
| `c2` | Azure | 22% | palette_anchor=#62A8E8 |
| `c3` | Violet | 0% | palette_anchor=#9C6FE8; mutation_only=True |

### SEC1

- Chromosome: `CHR2` @ 24 cM
- Category: `VISUAL`
- Expression: `COMPLETE_DOMINANCE`
- Dominance: `d2 > d1 > d0`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `d0` | Cream | 55% | palette_anchor=#F4E8C8 |
| `d1` | Rose | 30% | palette_anchor=#F2A4B8 |
| `d2` | Charcoal | 15% | palette_anchor=#414957 |

### PAT1

- Chromosome: `CHR2` @ 52 cM
- Category: `VISUAL`
- Expression: `CODOMINANT_PATTERN`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `p0` | Clear | 50% | renderer_pattern=None |
| `p1` | Spots | 30% | renderer_pattern=pattern_spots |
| `p2` | Stripes | 20% | renderer_pattern=pattern_stripes |
| `p3` | Fractal | 0% | renderer_pattern=pattern_fractal; mutation_only=True |

### GLW1

- Chromosome: `CHR2` @ 82 cM
- Category: `VISUAL`
- Expression: `DOSAGE_WITH_SPECIAL`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `g0` | None | 70% | glow_weight=0 |
| `g1` | SoftGlow | 25% | glow_weight=1 |
| `g2` | PulseGlow | 5% | glow_weight=2 |
| `g3` | AuroraGlow | 0% | glow_weight=5; mutation_only=True; renderer_shader=aurora |

### EYE1

- Chromosome: `CHR3` @ 12 cM
- Category: `VISUAL`
- Expression: `ADDITIVE_ROUNDED`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `e1` | OneEye | 10% | numeric_value=1 |
| `e2` | TwoEyes | 75% | numeric_value=2 |
| `e3` | ThreeEyes | 15% | numeric_value=3 |

### EYS1

- Chromosome: `CHR3` @ 35 cM
- Category: `VISUAL`
- Expression: `COMPLETE_DOMINANCE`
- Dominance: `y2 > y1 > y0`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `y0` | Round | 55% | renderer_asset=eyes_round |
| `y1` | Almond | 30% | renderer_asset=eyes_almond |
| `y2` | Diamond | 15% | renderer_asset=eyes_diamond |

### SKN1

- Chromosome: `CHR3` @ 63 cM
- Category: `VISUAL`
- Expression: `COMPLETE_DOMINANCE`
- Dominance: `k3 > k2 > k1 > k0`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `k0` | Smooth | 50% | renderer_surface=smooth; trait_modifiers={'heat': 4} |
| `k1` | Fuzzy | 25% | renderer_surface=fuzzy; trait_modifiers={'cold': 8} |
| `k2` | Veined | 25% | renderer_surface=veined; trait_modifiers={'photosynthesis': 5} |
| `k3` | Prism | 0% | renderer_surface=prism; mutation_only=True |

### MRK1

- Chromosome: `CHR3` @ 90 cM
- Category: `VISUAL`
- Expression: `COMPLETE_DOMINANCE`
- Dominance: `m2 > m1 > m0`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `m0` | None | 50% | renderer_marking=None |
| `m1` | Blush | 35% | renderer_marking=marking_blush |
| `m2` | Star | 15% | renderer_marking=marking_star |

### AQU1

- Chromosome: `CHR4` @ 10 cM
- Category: `ADAPTATION`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `q0` | Baseline | 55% | aquatic_effect=0 |
| `q1` | Aquatic | 35% | aquatic_effect=25 |
| `q2` | Specialist | 10% | aquatic_effect=45 |
| `q3` | Abyssal | 0% | aquatic_effect=65; mutation_only=True |

### CLD1

- Chromosome: `CHR4` @ 37 cM
- Category: `ADAPTATION`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `c0` | Baseline | 55% | cold_effect=0 |
| `c1` | Adapted | 35% | cold_effect=25 |
| `c2` | Specialist | 10% | cold_effect=45 |
| `c3` | FrostCore | 0% | cold_effect=65; mutation_only=True |

### HOT1

- Chromosome: `CHR4` @ 66 cM
- Category: `ADAPTATION`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `h0` | Baseline | 55% | heat_effect=0 |
| `h1` | Adapted | 35% | heat_effect=25 |
| `h2` | Specialist | 10% | heat_effect=45 |

### PHO1

- Chromosome: `CHR4` @ 91 cM
- Category: `ADAPTATION`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `f0` | None | 45% | photosynthesis_effect=0 |
| `f1` | Photoactive | 40% | photosynthesis_effect=25 |
| `f2` | Specialist | 15% | photosynthesis_effect=45 |
| `f3` | Blacklight | 0% | photosynthesis_effect=65; mutation_only=True |

### ENR1

- Chromosome: `CHR5` @ 7 cM
- Category: `QUANTITATIVE`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `n0` | Low | 25% | energy_capacity_effect=-10 |
| `n1` | Standard | 55% | energy_capacity_effect=0 |
| `n2` | High | 20% | energy_capacity_effect=12 |

### END1

- Chromosome: `CHR5` @ 32 cM
- Category: `QUANTITATIVE`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `d0` | Low | 25% | endurance_effect=-8 |
| `d1` | Standard | 55% | endurance_effect=0 |
| `d2` | High | 20% | endurance_effect=10 |

### CUR1

- Chromosome: `CHR5` @ 59 cM
- Category: `TEMPERAMENT`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `u0` | Reserved | 25% | curiosity_effect=-15 |
| `u1` | Balanced | 50% | curiosity_effect=0 |
| `u2` | Curious | 25% | curiosity_effect=15 |

### CAL1

- Chromosome: `CHR5` @ 86 cM
- Category: `TEMPERAMENT`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `a0` | Reactive | 25% | calmness_effect=-15 |
| `a1` | Balanced | 50% | calmness_effect=0 |
| `a2` | Calm | 25% | calmness_effect=15 |

### MET1

- Chromosome: `CHR6` @ 9 cM
- Category: `METABOLISM`
- Expression: `ADDITIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `r0` | Inefficient | 20% | metabolism_effect=-10 |
| `r1` | Standard | 60% | metabolism_effect=0 |
| `r2` | Efficient | 20% | metabolism_effect=10 |

### DEF1

- Chromosome: `CHR6` @ 34 cM
- Category: `HIDDEN_HEALTH`
- Expression: `RECESSIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `M` | Healthy | 92% |  |
| `m` | MetabolicFragilityRisk | 8% | recessive_condition=METABOLIC_FRAGILITY |

### DEF2

- Chromosome: `CHR6` @ 60 cM
- Category: `HIDDEN_HEALTH`
- Expression: `RECESSIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `P` | Stable | 94% |  |
| `p` | DermalInstabilityRisk | 6% | recessive_condition=DERMAL_INSTABILITY |

### IMM1

- Chromosome: `CHR6` @ 84 cM
- Category: `HIDDEN_HEALTH`
- Expression: `RECESSIVE`

| Allele | Name | Founder freq | Особенности |
|---|---|---:|---|
| `I` | Resilient | 93% |  |
| `i` | ImmuneFragilityRisk | 7% | recessive_condition=IMMUNE_FRAGILITY |

## 7. Derived Stats — что означает каждая характеристика

### `body_scale`

```text
clamp(1.0 + SIZ1.effect(a1) + SIZ1.effect(a2), 0.84, 1.16)
```

### `aquatic`

```text
clamp(20 + AQU1.effects + APP1.fins_bonus, 0, 100)
```

### `cold`

```text
clamp(20 + CLD1.effects + SKN1.fuzzy_bonus + body_size_cold_modifier, 0, 100)
```

### `heat`

```text
clamp(20 + HOT1.effects + SKN1.smooth_bonus + body_size_heat_modifier, 0, 100)
```

### `photosynthesis`

```text
clamp(PHO1.effects + APP1.leaves_bonus + SKN1.veined_bonus, 0, 100)
```

### `metabolism`

```text
clamp(50 + MET1.effects, 0, 100)
```

### `curiosity`

```text
clamp(50 + CUR1.effects, 0, 100)
```

### `calmness`

```text
clamp(50 + CAL1.effects, 0, 100)
```

### `heterozygosity`

```text
heterozygous_loci / 24
```

### `energy_capacity`

```text
100 + ENR1.effects + round((metabolism-50)*0.20) + size_modifier - health_penalty
```

### `endurance`

```text
clamp(50 + END1.effects + 0.10*(energy_capacity-100) + heterozygosity_bonus - health_penalty, 0, 100)
```

### `fertility`

```text
clamp(70 + (metabolism-50)*0.30 + heterozygosity_bonus - health_penalty - inbreeding_modifier, 10, 100)
```

### `maturation_hours`

```text
clamp(8 - metabolism_modifier + size_modifier + health_modifier, 5, 14)
```

Ключевые display ranges: adaptations/temperament `0..100`; energy capacity обычно ~70..140. `heterozygosity` — доля heterozygous loci из 24, это не power score.

## 8. Health / hidden carriers

| Condition | Genotype | Эффект |
|---|---|---|
| `METABOLIC_FRAGILITY` | DEF1 m/m | {'energy_recovery_multiplier': 0.8, 'fertility_flat': -15, 'endurance_flat': -10} |
| `DERMAL_INSTABILITY` | DEF2 p/p | {'cold_flat': -6, 'heat_flat': -6} |
| `IMMUNE_FRAGILITY` | IMM1 i/i | {'energy_recovery_multiplier': 0.9, 'fertility_flat': -5, 'endurance_flat': -8} |

Heterozygous carrier не получает penalty. Носительство может быть скрыто до sequencing.

## 9. Ecotypes

- `BOTANICAL`: `photosynthesis >= 70`
- `AQUATIC`: `aquatic >= 70`
- `CRYO`: `cold >= 70`
- `THERMAL`: `heat >= 70`
- `LUMINOUS`: `glow_intensity >= 2`
- `RESILIENT`: `endurance >= 75 and expressed_health_defects == 0`

## 10. Morphotypes

Morphotype выбирается первым совпавшим правилом по priority. Это UI-классификация, а не генетически закрытый вид.

- `PRISM`: `surface == PRISM`
- `AURORA`: `cold >= 70 and glow_intensity >= 2`
- `SOLARI`: `photosynthesis >= 70 and glow_intensity >= 2`
- `AMPHION`: `photosynthesis >= 60 and aquatic >= 60`
- `AQUALIS`: `aquatic >= 70`
- `CRYALIS`: `cold >= 70`
- `PYRA`: `heat >= 70`
- `VERDANT`: `photosynthesis >= 70`
- `LUNARI`: `glow_intensity >= 2`
- `GENERALIS`: `true`

## 11. Mutation-only alleles

- `COL1:c3` — Violet
- `PAT1:p3` — Fractal
- `GLW1:g3` — AuroraGlow
- `SKN1:k3` — Prism
- `AQU1:q3` — Abyssal
- `CLD1:c3` — FrostCore
- `PHO1:f3` — Blacklight

Mutation-only alleles отсутствуют у founders. После первого возникновения наследуются как обычные alleles.

## 12. Mutation model

- per allele-copy mutation rate: `0.00035`
- structural event rate: `0.003`
- target: около 2% offspring с >=1 mutation; итог подтверждается simulation, не предположением.
- mutation переходы data-driven и лежат в YAML `mutation.edges`.

## 13. Recombination

Каждая хромосома рекомбинируется как единый haplotype. Локусы нельзя наследовать независимо. Baseline crossover count:
- 0: 35%
- 1: 45%
- 2: 17%
- 3: 3%

## 14. Relatedness / inbreeding

Pedigree анализируется до 5 поколений. UI tiers: `LOW`, `MODERATE`, `HIGH`, `VERY_HIGH`. Основной смысл риска — более высокая вероятность встретить одинаковый скрытый recessive allele, а не произвольный штраф.

Для общего ancestor A:
```text
contribution = (1/2)^(n1+n2) * (1 + F_A)
```

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

## 16. Knowledge / Laboratory

Per-locus knowledge states: `UNKNOWN`, `PHENOTYPE_INFERRED`, `ONE_ALLELE_INFERRED`, `FULLY_SEQUENCED`. Basic scan не меняет genome. Marker panel стоит 20 Research Points, full sequence — 80 baseline.

## 17. Actions

- `FEED`: {'nutrient_cost': 5, 'energy_gain': 25}
- `PLAY`: {'energy_cost': 10, 'mood_gain': 20}
- `BREED`: {'min_energy_percent': 30, 'base_cooldown_minutes': 360}
- `FULL_SEQUENCE`: {'research_points_cost': 80}
- `MARKER_PANEL`: {'research_points_cost': 20}

Центр игры — `BREED`, не `FEED`. Care actions поддерживают creature state, но не создают permanent genetic power.

## 18. Expeditions

- `FOREST` — 30 min, weights={'photosynthesis': 0.4, 'curiosity': 0.25, 'endurance': 0.35}
- `TUNDRA` — 60 min, weights={'cold': 0.5, 'endurance': 0.35, 'metabolism': 0.15}
- `CAVE` — 90 min, weights={'glow': 0.3, 'calmness': 0.25, 'endurance': 0.45}

MVP expeditions не имеют боёв. Они дают функциональный смысл разным genetic builds.

## 19. Resources

- `NUTRIENTS` — care/incubation resource.
- `RESEARCH_POINTS` — sequencing/lab progression resource.
Не добавлять третью soft currency без отдельного design decision.

## 20. Rarity

Rarity выводится из мировой population frequency. Нельзя хранить `EPIC` как первичную случайную характеристику существа.
- `COMMON`: {'min_frequency': 0.1}
- `UNCOMMON`: {'min_frequency': 0.03, 'max_frequency': 0.1}
- `RARE`: {'min_frequency': 0.005, 'max_frequency': 0.03}
- `EXCEPTIONAL`: {'min_frequency': 0.0005, 'max_frequency': 0.005}
- `ULTRA_RARE`: {'max_frequency': 0.0005}

До population >=1000 псевдоточная rarity не показывается.

## 21. Что frontend получает для render

```text
body.shape
body.scale
appendages[]
tail.type
palette.primary
palette.secondary
pattern.layers[]
glow.type + intensity
eyes.count + shape
surface.type
marking.type
```

Никакого `creatureImage=solari.png` как источника истины.

## 22. Что обязано быть data-driven

Chromosome map, loci, alleles, founder frequencies, mutation edges, trait contributions, morphotype rules, expedition weights и founder genomes берутся из `genome_v1_catalog.yaml`. Не размазывать их по switch/case.

## 23. Core invariants for tests

- Creature всегда имеет ровно 2 alleles для каждого из 24 loci.
- Mutation-only alleles отсутствуют у founders.
- Child получает один recombinant chromosome от каждого parent.
- Новый allele появляется только от parent или mutation event.
- M/m не выражает DEF1; m/m всегда выражает DEF1.
- Sequencing и care никогда не меняют genome.
- Morphotype выводится из phenotype/derived stats.
- Rarity не является вручную заданной permanent характеристикой.
- Одинаковый genotype + одинаковая environment model => deterministic phenotype.
- RNG влияет на inheritance/mutation, но не на interpretation уже созданного genome.

## 24. Versioning

Любое изменение locus, allele, mutation edge, formula или morphotype threshold повышает `genome_schema_version`. Существующие creatures хранят schema version; генетику старых существ нельзя молча переписать.

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