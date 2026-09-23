# Design Principles

Status: APPROVED

Baseline version: v0.1

Purpose:
Принципы, инварианты и исходные критерии проверки дизайна.

[INDEX](../INDEX.md) · [OPEN questions](../OPEN_QUESTIONS.md)

Ниже — дословно перенесённые разделы baseline. Статус APPROVED фиксирует заданный baseline, но не закрывает OPEN questions и не утверждает недостающие значения. Примеры, ориентиры и будущие варианты сохраняют исходный смысл.

## Уточнение CANON UPDATE 001

[DIV-001–DIV-005](../genetics/GENETIC_DIVERSITY_MODEL.md) добавляют принципы разнообразия: специализация имеет цену, тип не задаёт готовый класс, полезный родитель зависит от цели и команды. Это требования к будущему дизайну, а не доказанный баланс. [COMBAT-001–COMBAT-004](../combat/COMBAT_CORE.md) разрешают документировать основу боя при общем статусе DRAFT; исходный non-goal об RPG не задаёт и не запрещает по предположению конкретные боевые характеристики. Их набор остаётся OPEN.

Основание и ограниченный приоритет: [Update 001](../updates/GENOME_CANON_UPDATE_001.md). Принципы не вводят равную сумму характеристик, скрытые штрафы популярным родителям или гарантированную неожиданность потомка.

Источник: [GENOME_GAME_DESIGN_SPEC_v0.1.md](../source/GENOME_GAME_DESIGN_SPEC_v0.1.md), разделы 2, 3, 41, 43, 44, 45.

<!-- baseline:GDS:2:start -->
## 2. Non-goals
GENOME must not become:
- a Tamagotchi where feeding is the main gameplay;
- an idle clicker;
- an RPG with HP / ATK / DEF progression;
- a Pokémon clone;
- a loot-box game;
- a Common/Rare/Epic/Legendary random-card generator;
- a game where paid genes are objectively stronger;
- an NFT/crypto economy;
- a game where a creature dies because the player did not log in;
- a spreadsheet visible to a new player from minute one.
<!-- baseline:GDS:2:end -->

<!-- baseline:GDS:3:start -->
## 3. Simple outside, deep inside
### 3.1 Casual layer
A new player sees appearance, temperament, 3–5 obvious traits, adaptation icons, family tree and simple breeding probabilities.

Example:
```text
SOLARI #33802
Botanical
Light adapted
Calm
Long leaves
Glow

Possible offspring:
Green / Orange
Long / Short leaves
Glow possible
Rare unknown mutation possible
```

### 3.2 Advanced layer
The Laboratory reveals chromosome pairs, loci, exact alleles, dominant/recessive relationships, linkage, carrier status, quantitative traits, harmful recessives, pedigree coefficient and expected offspring distributions.

Example:
```text
Chr 2 — Locus LF02
Leaf morphology
Genotype: L1 / L3
L1 = Long
L3 = Short
Expression model: incomplete dominance
Phenotype: Medium-long
```
<!-- baseline:GDS:3:end -->

<!-- baseline:GDS:41:start -->
## 41. First playable acceptance criteria
A test player must be able to intentionally:
1. Receive two known-genotype breeders.
2. Understand one desirable allele is recessive.
3. Produce a carrier.
4. Breed carriers to obtain the homozygous visible phenotype.
5. See phenotype match genotype rules.
6. Use pedigree to avoid an overly related cross.
7. Observe linkage/recombination affecting two nearby loci.
8. Observe at least one mutation over a reasonable simulated population.
9. Stabilize a target trait across several generations.
10. Explain why one breeder was selected over another.

If optimal play becomes “breed random pairs until Epic appears”, the design has failed.
<!-- baseline:GDS:41:end -->

<!-- baseline:GDS:43:start -->
## 43. UX principle for complexity
Main UI vocabulary:
```text
Likely
Possible
Hidden carrier
Related
Stable line
New mutation
```

Advanced Lab vocabulary:
```text
heterozygous
homozygous
recessive
linked loci
crossover
allele frequency
```

Teach advanced concepts gradually.
<!-- baseline:GDS:43:end -->

<!-- baseline:GDS:44:start -->
## 44. Design invariants
These rules must not be simplified away:
1. Creatures are diploid.
2. Every inherited locus has two alleles.
3. Offspring come from parental gametes.
4. Chromosomal linkage exists.
5. Recombination exists.
6. Dominant, recessive and incomplete/codominant expression exists.
7. At least some traits are polygenic.
8. Hidden carrier states exist.
9. Pedigree changes expected genetic risk through shared alleles.
10. Mutation is rare and controlled.
11. Genotype and phenotype are separate.
12. Individual level-up never rewrites genotype.
13. Population rarity derives from frequencies.
14. Paid purchases do not create objectively stronger genetic lines.
15. Random breeding cannot be optimal strategy.
<!-- baseline:GDS:44:end -->

<!-- baseline:GDS:45:start -->
## 45. Kill criteria
Redesign/stop if:
- players ignore genotype and only chase rarity colors;
- phenotype gives no clue why breeding decisions matter;
- genetic analysis feels like homework rather than discovery;
- optimal strategy is mass breeding;
- social breeding is unnecessary because public breeders are always better;
- a small allele set dominates all useful expeditions;
- inbreeding penalties feel arbitrary;
- mutations are never seen or become routine;
- seasonal genes obsolete existing lines;
- monetization meaningfully increases genetic power.
<!-- baseline:GDS:45:end -->

Источник: [GENOME_DOMAIN_BIBLE_v0.1.md](../source/GENOME_DOMAIN_BIBLE_v0.1.md), разделы 23.

<!-- baseline:DB:23:start -->
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
<!-- baseline:DB:23:end -->
