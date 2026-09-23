# Genetic Content Bible

Status: APPROVED

Baseline version: v0.1

Purpose:
Каталог loci/alleles и исходный genetic scope.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Machine-readable counterpart: [genome_v1.yaml](../../data/genome_v1.yaml), `loci`. Сводная карта: [GENOME_MODEL](GENOME_MODEL.md).

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 39.

<!-- baseline:GDS:39:start -->
## 39. MVP genetic scope
Recommended first playable:
```text
6 chromosome pairs
24 loci
12 visual loci
6 adaptation/quantitative loci
3 temperament/metabolism loci
3 recessive/hidden-health loci
2–4 alleles per locus
~60–70 total initial alleles
5–8 mutation-only alleles
```
<!-- baseline:GDS:39:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 6.

<!-- baseline:DB:6:start -->
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
<!-- baseline:DB:6:end -->
