# Creature Model

Status: APPROVED

Baseline version: v0.1

Purpose:
Существо, жизненный цикл, фенотип и исходные формулы характеристик. Эти характеристики не определяют Combat.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Machine-readable counterpart: [genome_v1.yaml](../../data/genome_v1.yaml), `life_stages`, `derived_stats`, `health_conditions`. Неполные формулы сохранены буквально: OQ-003–OQ-005.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 7, 14, 15, 25, 32.

<!-- baseline:GDS:7:start -->
## 7. Individual development is not evolution
Individual creatures mature:
```text
Embryo/Egg -> Juvenile -> Adolescent -> Adult
```

Evolution emerges across generations through selection. Do not use Pokémon-like “evolve individual into species” as the genetic core.
<!-- baseline:GDS:7:end -->

<!-- baseline:GDS:14:start -->
## 14. Creature lifecycle
### Egg
After breeding an egg is created. Genome is fixed at creation.

### Hatch
Visible immediately:
- base morphology;
- basic color;
- obvious structural traits.

### Juvenile/adolescent
Final pattern, temperament and some latent phenotype reveal gradually.

### Adult
Can breed, explore, join research, be lent for breeding, remain active or move to reserve.
<!-- baseline:GDS:14:end -->

<!-- baseline:GDS:15:start -->
## 15. Care system
Care is supportive:
```text
Feed
Play
Rest
Habitat
```

Purpose:
- recover energy;
- temporary mood;
- maturation;
- lightweight daily interaction.

Care must not permanently increase genetic stats or create superior genes. Missing a day never destroys progress.
<!-- baseline:GDS:15:end -->

<!-- baseline:GDS:25:start -->
## 25. Quantitative traits
Recommended initial continuous traits:
- energy capacity;
- maturation speed;
- fertility;
- cold tolerance;
- heat tolerance;
- aquatic adaptation;
- exploration endurance;
- curiosity.

No single allele should dominate an entire stat.
<!-- baseline:GDS:25:end -->

<!-- baseline:GDS:32:start -->
## 32. Visual genetics requirement
Renderer must be compositional:
```text
base body
body proportions
eye set
appendage set
leaf/horn/ear set
pattern mask
primary palette
secondary palette
surface modifier
aura
particles
```

A new allele should preferably modify controlled visual parameters rather than require a totally new hand-drawn creature.
<!-- baseline:GDS:32:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 1, 3, 4, 7, 8, 21.

<!-- baseline:DB:1:start -->
## 1. Ключевая модель мира

В игре одна базовая синтетическая форма — `GENOMORPH`. Нет конечного списка из сотен заранее нарисованных видов. Каждый Creature — уникальный индивидуум: `genotype + pedigree + phenotype + mutable state`. `Solari`, `Aqualis`, `Cryalis` и т.п. — вычисляемые **morphotypes**, а не отдельные species.

Это важно для реализации: frontend не должен получать `solari.png`; он получает phenotype descriptor и собирает внешний вид из компонентов.
<!-- baseline:DB:1:end -->

<!-- baseline:DB:3:start -->
## 3. Creature — полный набор характеристик

### Наследуемые
Только `genome`. Любой наследуемый эффект обязан происходить из allele data.

### Вычисляемые
`phenotype`, `morphotype`, `ecotypes`, `aquatic`, `cold`, `heat`, `photosynthesis`, `energy_capacity`, `endurance`, `curiosity`, `calmness`, `metabolism`, `fertility`, `heterozygosity`, `health_state`, `rarity`.

### Изменяемые в течение жизни
`energy`, `mood`, `life_stage`, `maturity_progress`, `current_activity`, `breeding_ready_at`, `personal_name`, `knowledge_state`. Care никогда не переписывает genotype.

### Метаданные
`public_id`, `owner_id`, `generation`, `founder`, `parent_a_id`, `parent_b_id`, `born_at`, `genome_schema_version`, discovery flags.
<!-- baseline:DB:3:end -->

<!-- baseline:DB:4:start -->
## 4. Life stages

- `EGG` — 120 минут
- `JUVENILE` — 120 минут
- `ADOLESCENT` — 240 минут
- `ADULT` — постоянно

Смерти от старости/неактивности в v0.1 нет. Отсутствие игрока не уничтожает progress.
<!-- baseline:DB:4:end -->

<!-- baseline:DB:7:start -->
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
<!-- baseline:DB:7:end -->

<!-- baseline:DB:8:start -->
## 8. Health / hidden carriers

| Condition | Genotype | Эффект |
|---|---|---|
| `METABOLIC_FRAGILITY` | DEF1 m/m | {'energy_recovery_multiplier': 0.8, 'fertility_flat': -15, 'endurance_flat': -10} |
| `DERMAL_INSTABILITY` | DEF2 p/p | {'cold_flat': -6, 'heat_flat': -6} |
| `IMMUNE_FRAGILITY` | IMM1 i/i | {'energy_recovery_multiplier': 0.9, 'fertility_flat': -5, 'endurance_flat': -8} |

Heterozygous carrier не получает penalty. Носительство может быть скрыто до sequencing.
<!-- baseline:DB:8:end -->

<!-- baseline:DB:21:start -->
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
<!-- baseline:DB:21:end -->
