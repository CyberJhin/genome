# Game Vision

Status: APPROVED

Purpose:
Product thesis и исходные границы первого playable.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

## Уточнение CANON UPDATE 001

[Update 001](../updates/GENOME_CANON_UPDATE_001.md) фиксирует [основу Combat](../combat/COMBAT_CORE.md) и [принципы разнообразия](../genetics/GENETIC_DIVERSITY_MODEL.md), сохраняя genetics-first thesis. Он имеет приоритет только для явно затронутых пунктов. Историческое «PvP вне first playable» ниже не запрещает документирование Combat; точный MVP scope и разрешение реализации остаются OPEN (OQ-017). Combat целиком — DRAFT.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 0, 1, 40, 46.

<!-- baseline:GDS:preamble:start -->
# GENOME — Game Design Specification
## Genetics / Breeding / Progression System
**Version:** 0.1  
**Status:** Game-design baseline before technical specification  
**Core principle:** genetics-first collection game, not Tamagotchi and not idle-RPG.
<!-- baseline:GDS:preamble:end -->

<!-- baseline:GDS:0:start -->
## 0. Purpose
This document defines the game-design system for GENOME: what the player is trying to achieve, how creatures are born, how inheritance works, how lineages are built, how mutations appear, how the player learns the genome, what makes breeding strategic, and what supports long-term retention.

This is **not** a backend/frontend architecture specification. Codex must not replace the rules below with a simpler random-rarity generator.

Central promise:
> The player does not level one pet forever. The player breeds populations, builds lineages, studies inheritance and tries to obtain rare, stable and useful combinations of genes.

The player's real collection is not just pictures. It is living creatures, genotypes, pedigrees, discovered alleles, stable lines and global discoveries.
<!-- baseline:GDS:0:end -->

<!-- baseline:GDS:1:start -->
## 1. Product fantasy
The player is a breeder/researcher of a synthetic life form. They receive a founder organism, learn visible traits, gradually sequence the genome, choose breeding partners, produce offspring and decide which descendants are worth keeping in a line.

The game should enable statements such as:
- “This line has carried the frost allele for six generations.”
- “This creature looks ordinary but is a carrier of a rare recessive mutation.”
- “I need to cross these two lines to combine Water III and Glow II.”
- “This child inherited the father's pattern but the mother's metabolic trait.”
- “I discovered this mutation first on the server.”
- “My line is genetically stable, but I need unrelated blood to reduce the risk of a recessive defect.”
<!-- baseline:GDS:1:end -->

<!-- baseline:GDS:40:start -->
## 40. MVP content scope
Initial biomes:
```text
Forest
Tundra
Cave
```

Initial systems:
```text
Creature
Collection
Breeding
Incubation
Laboratory
Pedigree
Codex
One expedition system
One research-goal system
Social breeding request
```

Not first playable:
```text
marketplace
PvP combat
guilds
complex trading
global auction
paid season pass
dozens of habitats
```
<!-- baseline:GDS:40:end -->

<!-- baseline:GDS:46:start -->
## 46. Product thesis to preserve
The game should make the player feel:
> “I bred this.”

not:
> “The game rolled this for me.”

The player's decisions across generations must be visible in the genome, pedigree and phenotype of descendants.
<!-- baseline:GDS:46:end -->
