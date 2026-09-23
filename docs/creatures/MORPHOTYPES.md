# Morphotypes

Status: APPROVED

Baseline version: v0.1

Purpose:
Вычисляемые morphotypes в рамках Creature Model v0.1.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

Machine-readable counterpart: [genome_v1.yaml](../../data/genome_v1.yaml), `morphotypes`. Неопределённая интерпретация surface/glow: OQ-006.

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 10.

<!-- baseline:DB:10:start -->
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
<!-- baseline:DB:10:end -->
