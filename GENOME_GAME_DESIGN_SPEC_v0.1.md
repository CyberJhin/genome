# GENOME — Game Design Specification
## Genetics / Breeding / Progression System
**Version:** 0.1  
**Status:** Game-design baseline before technical specification  
**Core principle:** genetics-first collection game, not Tamagotchi and not idle-RPG.

## 0. Purpose
This document defines the game-design system for GENOME: what the player is trying to achieve, how creatures are born, how inheritance works, how lineages are built, how mutations appear, how the player learns the genome, what makes breeding strategic, and what supports long-term retention.

This is **not** a backend/frontend architecture specification. Codex must not replace the rules below with a simpler random-rarity generator.

Central promise:
> The player does not level one pet forever. The player breeds populations, builds lineages, studies inheritance and tries to obtain rare, stable and useful combinations of genes.

The player's real collection is not just pictures. It is living creatures, genotypes, pedigrees, discovered alleles, stable lines and global discoveries.

## 1. Product fantasy
The player is a breeder/researcher of a synthetic life form. They receive a founder organism, learn visible traits, gradually sequence the genome, choose breeding partners, produce offspring and decide which descendants are worth keeping in a line.

The game should enable statements such as:
- “This line has carried the frost allele for six generations.”
- “This creature looks ordinary but is a carrier of a rare recessive mutation.”
- “I need to cross these two lines to combine Water III and Glow II.”
- “This child inherited the father's pattern but the mother's metabolic trait.”
- “I discovered this mutation first on the server.”
- “My line is genetically stable, but I need unrelated blood to reduce the risk of a recessive defect.”

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

## 4. Biological model
Creatures are a fictional **diploid hermaphroditic species**.

This preserves near-real genetics while avoiding male/female matching friction.

### 4.1 MVP genome
- 6 chromosome pairs
- 24 functional loci
- ~4 loci per chromosome
- 2 inherited chromosome copies per pair
- 48 inherited allele copies total

Each locus stores:
```text
chromosome_id
position_cM
locus_id
allele_left
allele_right
```

`position_cM` is a simplified genetic-map position used for linkage/recombination.

Nearby loci must be inherited together more often. Independent random inheritance per locus is not acceptable.

## 5. Alleles and expression models
### 5.1 Complete dominance
```text
G = glow
g = no glow
GG -> glow
Gg -> glow
gg -> no glow
```

### 5.2 Incomplete dominance
```text
C1/C1 -> green
C1/C2 -> turquoise
C2/C2 -> blue
```

### 5.3 Codominance
Both alleles are expressed, useful for markings and dual-color regions.

### 5.4 Recessive traits
```text
F/F -> normal
F/f -> normal carrier
f/f -> frost phenotype
```

### 5.5 Polygenic traits
At least some characteristics use several loci:
- body size;
- energy capacity;
- fertility;
- expedition endurance;
- curiosity;
- heat/cold tolerance.

Formula class:
```text
phenotype = base + sum(allele effects) + bounded environment modifier
```

### 5.6 Epistasis
Some genes suppress or modify others.

Example:
```text
Pigment locus says orange.
Albino locus aa suppresses pigment.
Phenotype is pale/white, genotype still carries orange.
```

## 6. Genotype vs phenotype
Genotype is inherited biological state. Phenotype is expressed result:
```text
genotype + gene interactions + developmental state + environment = phenotype
```

Care, level or habitat must never silently rewrite genotype.

## 7. Individual development is not evolution
Individual creatures mature:
```text
Embryo/Egg -> Juvenile -> Adolescent -> Adult
```

Evolution emerges across generations through selection. Do not use Pokémon-like “evolve individual into species” as the genetic core.

## 8. Meiosis and offspring generation
Offspring are created by simplified meiosis:
1. Each parent has chromosome pairs.
2. A gamete receives one recombined chromosome from each pair.
3. Crossover may exchange segments between homologs.
4. Two gametes combine into a diploid offspring genome.
5. Mutation is applied.
6. Genotype is translated into phenotype.

## 9. Recombination
Nearby loci are linked.

Example parental homologs:
```text
A: [Green] ---- [Spots] -------- [Glow]
B: [Blue ] ---- [Plain] -------- [NoGlow]
```

Without crossover, Green+Spots+Glow or Blue+Plain+NoGlow are common. Crossover can produce Green+Spots+NoGlow.

### 9.1 Simplified algorithm
For each chromosome during gamete production:
1. Randomly choose homolog A or B as starting source.
2. Generate crossover count using a bounded Poisson-like distribution.
3. Pick crossover positions along the map.
4. Switch source homolog after each crossover.
5. Read alleles from the recombinant chromosome.

Initial target distribution:
```text
0 crossovers: ~35%
1 crossover : ~45%
2 crossovers: ~17%
3 crossovers: ~3%
```
Balance later using simulation.

## 10. Mutation system
Mutation must be rare enough to feel special but common enough to appear during normal play. Real rates are too low for game pacing, so GENOME uses accelerated fictional mutation rates while preserving genetic logic.

### 10.1 Base target
```text
Probability an offspring gets >=1 mutation: ~1–3%
```
Balancing target, not universal constant.

### 10.2 MVP mutation types
- allele mutation;
- novel allele discovery;
- controlled structural cosmetic mutation.

Novel alleles may be absent from the founder population and enter through mutation or seasonal introduction.

### 10.3 Mutation graph
Mutations must follow explicit transitions.
Bad:
```text
any allele -> any allele equally
```
Good:
```text
Green -> Cyan -> Blue
Green -> Yellow
Blue -> Violet
```

## 11. Recessive defects and inbreeding
Model inbreeding through shared hidden recessive alleles, not arbitrary “inbreeding -20%”.

Example:
```text
D = healthy
d = recessive metabolic defect
DD -> healthy
Dd -> healthy carrier
dd -> metabolic weakness
```

Possible consequences:
- lower expedition endurance;
- lower fertility;
- slower maturation;
- lower energy recovery.

Never kill or permanently invalidate a creature.

UI shows relatedness as Low / Moderate / High. Advanced view may show a coefficient.

The game teaches a trade-off:
> Pure lines become more predictable, but excessive homozygosity increases recessive risk.

## 12. Genetic health
Derived indicators may include:
- heterozygosity;
- known deleterious homozygotes;
- known carrier loci;
- genetic diversity score.

These are explanatory statistics, not arbitrary power scores.

## 13. Starter population
New player receives:
```text
1 personal founder
+ access to 6–10 public laboratory breeders
```

Founder design requirements:
- no genetically doomed starts;
- common alleles represented;
- some rare alleles possible but not guaranteed;
- sufficient unrelatedness;
- player can breed without recruiting a human immediately.

Public breeders exist to bootstrap the game; player-owned social lines should become more valuable later.

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

## 16. Environment and gene expression
Some loci may be environment-sensitive.

Example:
```text
Seasonal pigment gene:
Cold habitat -> pale expression
Warm habitat -> bright expression
```

Genotype remains unchanged.

## 17. Breeding flow
### Step 1 — choose Parent A
Adult from own collection.

### Step 2 — choose Parent B
Sources:
- own collection;
- public laboratory pool;
- friend's creature;
- breeding marketplace later.

### Step 3 — compatibility analysis
Casual view:
```text
Color: Green 50%, Blue 25%, Turquoise 25%
Leaves: Long 75%, Short 25%
Glow: Possible
Health risk: Low
```

Advanced view:
```text
COL1: C1/C2 × C1/C1
PAT2: P0/P3 × P3/P3
DEF1: D/d × D/D
```

Also show:
- relatedness;
- known carrier overlap;
- expected diversity;
- known phenotype probabilities;
- hidden outcomes;
- mutation baseline.

### Step 4 — confirm breeding
Consumes biological cooldown/time, not a casino ticket.

### Step 5 — gamete generation
Run recombination + inheritance + mutation.

### Step 6 — incubation
Egg exists; genome fixed.

### Step 7 — hatch
Reveal phenotype.

### Step 8 — analysis
Player chooses:
```text
Keep active
Move to reserve
Sequence
Add to breeding line
Use in expedition
Offer as breeding partner
```

## 18. Sequencing / Laboratory
Laboratory turns random-looking outcomes into intentional selection.

### 18.1 Knowledge states per locus
```text
Unknown
Phenotype inferred
One allele inferred
Fully sequenced
```

### 18.2 Tests
- Basic phenotype scan: cheap/free, visible traits and likely class.
- Marker panel: selected loci.
- Full sequencing: complete genome.

Full sequencing must be obtainable through gameplay, not paid-only.

### 18.3 Why hidden genotype matters
```text
Parent A: normal, F/f
Parent B: normal, F/f
Expected child:
25% F/F
50% F/f carrier
25% f/f -> Frost
```

Before sequencing, only “latent trait possible” may be known.

## 19. Collection and reserve
### Active collection
Frequently used creatures.

### Genetic reserve
Archived creatures remain alive and keep genome, pedigree, breeding history and discovery status.

Never force permanent destruction of genetic history due to slot pressure.

## 20. Pedigree
Every non-founder records:
```text
parent_a_id
parent_b_id
generation
birth_timestamp
breeder_id
```

Pedigree supports relatedness, recessive-risk reasoning and lineage prestige.

## 21. Lines
A line is a player-defined breeding project.

Examples:
```text
Aurora Line — stabilize Aurora Glow + Frost resistance
Pure Botanical — homozygous Botanical traits
Deep Water — Water III + endurance + bioluminescence
```

Player can pin target alleles, target phenotype and forbidden defects.

Progress example:
```text
Aurora Line — Generation 7
Target loci stabilized: 4/6
Aurora: homozygous ✓
Frost: heterozygous
Endurance: 72%
Defect D1: carrier ⚠
```

## 22. Codex
Global/personal genetics encyclopedia.

Sections:
```text
Morphology
Pigments
Patterns
Adaptations
Metabolism
Temperament
Mutations
Hidden disorders
```

Knowledge stages:
```text
Unknown
Observed
Sequenced
Bred successfully
Stabilized in a line
```

The goal is not merely to collect pictures; it is to understand and reproduce the genome.

## 23. Global discoveries
Some alleles begin globally undiscovered.

Record:
- first phenotype observed;
- first allele sequenced;
- first homozygous individual;
- first stable line.

Example:
```text
AURORA GENE
First observed: Dinis — 2026-10-14
First stabilized: Masha — 2026-10-21
```

## 24. Rarity
Primary rarity must derive from actual population frequency.

Example:
```text
Aurora allele frequency: 0.21%
Aurora visible phenotype: 0.07%
Living creatures: 1,283
Exact phenotype combination: 1 in 18,430
```

UI may map this to labels, but underlying truth is frequency-based.

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

## 27. Research objectives
Examples:
- produce homozygous Glow G2/G2;
- produce Water W3 without linked D1 defect;
- create Botanical + Cold II + Calm;
- increase heterozygosity of Aurora line;
- breed out a recessive defect within three generations.

Research objectives teach genetics through goals.

## 28. Social breeding
Players can expose selected adults as breeding partners.

Request example:
```text
Use Nebula #82144 as Parent B?
Your creature: SOLARI #33802
Estimated offspring:
Water possible
Glow 62%
Botanical 50%
[Accept]
```

Second owner receives a non-power reward such as breeding credit, research points or a genetic sample. Offspring belongs to initiating player in MVP.

## 29. Breeding cooldown and fertility
Use biological cooldown, e.g. 2–8 hours depending on fertility. Exact values come from balancing.

Purpose:
- preserve breeder value;
- prevent brute-force mutation farming;
- encourage diversity;
- make social breeding meaningful.

Cooldown must not be purchasable away without limit.

## 30. Economy
Keep soft currencies minimal.

### Research Points
Earned from sequencing, discoveries, objectives and expeditions. Used for lab upgrades and research unlocks.

### Nutrients
Earned passively/expeditions. Used for care and incubation support.

Do not introduce a pile of currencies.

## 31. Monetization boundaries
Allowed:
- cosmetic phenotype overlays;
- habitat themes;
- profile frames;
- creature nameplates;
- collection presentation;
- extra saved line templates;
- extra convenient active slots;
- capped additional parallel incubator;
- cosmetic season pass;
- gifts;
- visual particles/effects.

Forbidden:
- paid stronger alleles;
- guaranteed rare mutation purchase;
- unlimited breeding bypass;
- paid rerolls;
- loot boxes;
- dominant stat boosts;
- paid immunity to genetic defects.

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

## 33. Example genome fragment
Creature A:
```text
COL1: C1/C2 -> turquoise
PAT2: P1/P1 -> stripes
LEF1: L2/L3 -> medium leaves
GLW1: G1/g  -> glow
CLD1: K2/K1 -> cold tolerance 2
DEF1: D/d   -> healthy carrier
```

Creature B:
```text
COL1: C2/C2 -> blue
PAT2: P1/P3 -> stripes + dots
LEF1: L1/L3 -> short-medium leaves
GLW1: g/g   -> no glow
CLD1: K1/K1 -> cold tolerance 1
DEF1: D/D   -> healthy
```

Child genotype comes from recombined parental gametes, never by independently rolling each displayed trait.

## 34. Example hidden recessive decision
Player wants frost phenotype.

Known:
```text
Parent A: F/f
Parent B: unknown
```
After sequencing B:
```text
Parent B: F/f
25% F/F
50% F/f
25% f/f -> Frost
```
Now the player can intentionally pursue the trait.

## 35. Example linkage decision
Two desired alleles are on the same chromosome in repulsion:
```text
copy A: G2 --- w0
copy B: g0 --- W3
```
Player wants:
```text
G2 --- W3
```
This requires crossover between the loci. Producing the line may take several generations.

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

## 38. Seasonal content
A season adds a small genetic expansion and never invalidates old populations.

Example:
```text
Season: ABYSS
Bioluminescence
Pressure resistance
Deep pigment
Tentacle morphology
Void pattern
```

After the season, alleles remain in world population through descendants.

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

## 46. Product thesis to preserve
The game should make the player feel:
> “I bred this.”

not:
> “The game rolled this for me.”

The player's decisions across generations must be visible in the genome, pedigree and phenotype of descendants.
