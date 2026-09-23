# Simulation Spec

Status: DRAFT

Purpose:
Существующее требование genetics simulation. Полная спецификация не определена; реализация не начинается.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус документа остаётся DRAFT; перенос исходного текста не утверждает решения блока и не закрывает OPEN questions. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Combat Balance: NOT_STARTED. Требование ниже касается уже существующего genetics baseline. Допуски и сценарии остаются OPEN (OQ-016).

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 42.

<!-- baseline:GDS:42:start -->
## 42. Simulation requirement before product development
Before full Mini App development, create an offline genetics simulator that can generate at least 100,000 offspring and validate:
- Mendelian ratios;
- recombination frequencies;
- mutation frequency;
- carrier rates;
- deleterious recessive rates;
- allele-frequency drift;
- target-line stabilization probability;
- inbreeding consequences;
- population diversity.

Simulator must support fixed RNG seeds.

Balance comes from simulation, not intuition.
<!-- baseline:GDS:42:end -->
