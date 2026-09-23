# Progression

Status: DRAFT

Purpose:
Исходные действия, экспедиции, исследовательские цели и долгосрочный цикл.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус документа остаётся DRAFT; перенос исходного текста не утверждает решения блока и не закрывает OPEN questions. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Значения действий и экспедиций сохранены в [genome_v1.yaml](../../data/genome_v1.yaml), `actions`, `expeditions`; [progression_v1.yaml](../../data/progression_v1.yaml) пока содержит только указатели на них.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 26, 27, 37.

<!-- baseline:GDS:26:start -->
## 26. Expeditions
Biomes:
```text
Forest
Desert
Ocean
Cave
Tundra
Ruins
```

Each expedition values different genetic traits.

Example:
```text
TUNDRA
Cold tolerance: high priority
Endurance: medium
Glow: bonus
Heat adaptation: irrelevant
```

Rewards:
- research samples;
- nutrients;
- sequencing materials;
- cosmetic fragments;
- habitat items;
- rare non-paid catalysts.

No combat system required.
<!-- baseline:GDS:26:end -->

<!-- baseline:GDS:27:start -->
## 27. Research objectives
Examples:
- produce homozygous Glow G2/G2;
- produce Water W3 without linked D1 defect;
- create Botanical + Cold II + Calm;
- increase heterozygosity of Aurora line;
- breed out a recessive defect within three generations.

Research objectives teach genetics through goals.
<!-- baseline:GDS:27:end -->

<!-- baseline:GDS:37:start -->
## 37. Long-term loop
```text
discover genes
-> build lines
-> stabilize traits
-> solve breeding problems
-> introduce unrelated blood
-> discover mutations
-> spread useful alleles across lines
-> complete research goals
-> seasonal genetic expansion
```
<!-- baseline:GDS:37:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 17, 18.

<!-- baseline:DB:17:start -->
## 17. Actions

- `FEED`: {'nutrient_cost': 5, 'energy_gain': 25}
- `PLAY`: {'energy_cost': 10, 'mood_gain': 20}
- `BREED`: {'min_energy_percent': 30, 'base_cooldown_minutes': 360}
- `FULL_SEQUENCE`: {'research_points_cost': 80}
- `MARKER_PANEL`: {'research_points_cost': 20}

Центр игры — `BREED`, не `FEED`. Care actions поддерживают creature state, но не создают permanent genetic power.
<!-- baseline:DB:17:end -->

<!-- baseline:DB:18:start -->
## 18. Expeditions

- `FOREST` — 30 min, weights={'photosynthesis': 0.4, 'curiosity': 0.25, 'endurance': 0.35}
- `TUNDRA` — 60 min, weights={'cold': 0.5, 'endurance': 0.35, 'metabolism': 0.15}
- `CAVE` — 90 min, weights={'glow': 0.3, 'calmness': 0.25, 'endurance': 0.45}

MVP expeditions не имеют боёв. Они дают функциональный смысл разным genetic builds.
<!-- baseline:DB:18:end -->
