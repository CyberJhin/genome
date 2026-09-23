# Pacing

Status: DRAFT

Purpose:
Исходные ориентиры длительности сессии и breeding cooldown.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус документа остаётся DRAFT; перенос исходного текста не утверждает решения блока и не закрывает OPEN questions. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 29, 36.

<!-- baseline:GDS:29:start -->
## 29. Breeding cooldown and fertility
Use biological cooldown, e.g. 2–8 hours depending on fertility. Exact values come from balancing.

Purpose:
- preserve breeder value;
- prevent brute-force mutation farming;
- encourage diversity;
- make social breeding meaningful.

Cooldown must not be purchasable away without limit.
<!-- baseline:GDS:29:end -->

<!-- baseline:GDS:36:start -->
## 36. Player session loop
Typical 5–10 minute session:
```text
1. Check eggs/newly matured offspring.
2. Inspect phenotype.
3. Sequence or partially analyze an interesting creature.
4. Compare breeders for a line.
5. Start one breeding.
6. Send another creature on expedition.
7. Review Codex/research progress.
8. Optional: respond to social breeding request.
```

There must be a meaningful decision, not only timers.
<!-- baseline:GDS:36:end -->
