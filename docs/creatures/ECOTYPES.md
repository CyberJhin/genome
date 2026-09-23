# Ecotypes

Status: APPROVED

Baseline version: v0.1

Purpose:
Функциональные ecotypes в рамках Creature Model v0.1.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Machine-readable counterpart: [genome_v1.yaml](../../data/genome_v1.yaml), `ecotypes`, `adaptation_tiers`. Определения display tiers сохранены только в каталоге, новые не добавлены.

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 9.

<!-- baseline:DB:9:start -->
## 9. Ecotypes

- `BOTANICAL`: `photosynthesis >= 70`
- `AQUATIC`: `aquatic >= 70`
- `CRYO`: `cold >= 70`
- `THERMAL`: `heat >= 70`
- `LUMINOUS`: `glow_intensity >= 2`
- `RESILIENT`: `endurance >= 75 and expressed_health_defects == 0`
<!-- baseline:DB:9:end -->
