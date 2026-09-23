# Open Questions

Status: OPEN

Вопросы обнаружены при организации baseline; ни один не решён этой задачей. Указание APPROVED v0.1 у блока не снимает перечисленные ограничения. GDS и DB означают сохранённые [Game Design Spec](source/GENOME_GAME_DESIGN_SPEC_v0.1.md) и [Domain Bible](source/GENOME_DOMAIN_BIBLE_v0.1.md). Каталог — [data/genome_v1.yaml](../data/genome_v1.yaml). Нужен явный CANON UPDATE; значения и примеры пока сохранены без исправления.

## OQ-001 — Как согласовать примерные ID и генетические сценарии GDS с каталогом v0.1?

Status: OPEN

Context:
GDS §3.2, §5, §17–18, §21, §27, §33–35 используют LF02, LEF1, PAT2, C1/C2, G2, W3, F/f, D/d и D1. DB §5–6 и каталог содержат PAT1, APP1, COL1:c0..c3, GLW1:g0..g3, AQU1:q0..q3, DEF1:M/m; LF02/LEF1/PAT2 отсутствуют. GDS §35 иллюстрирует сцепленные Glow/Water, тогда как GLW1 находится на CHR2, AQU1 — на CHR4. Frost в GDS — рецессивный пример, CLD1 в каталоге — ADDITIVE. GDS §41 требует целенаправленно получить видимый желательный рецессивный признак, но его соответствие контенту v0.1 не задано.

Why decision is required:
Нельзя автоматически переименовывать ID, менять карту, добавлять alleles или считать примеры исполнимыми fixtures. Нужно определить применимость и согласованные примеры для текущего каталога.

Do not implement before resolved.

## OQ-002 — Должны ли примеры вероятностей breeding описывать одно скрещивание?

Status: OPEN

Context:
В GDS §17 casual view показывает Green 50%, Blue 25%, Turquoise 25%; advanced view — COL1:C1/C2 × C1/C1. По примеру incomplete dominance из GDS §5.2 это скрещивание даёт C1/C1 и C1/C2, но не C2/C2. Не уточнено, являются ли casual и advanced примеры одним случаем; их ID также расходятся с каталогом (OQ-001).

Why decision is required:
Нужно согласовать назначение примеров и правила отображения вероятностей при неполном знании genome; нельзя молча корректировать проценты.

Do not implement before resolved.

## OQ-003 — Как полностью определяются derived stats и составляющие формул?

Status: OPEN

Context:
DB §7 и `derived_stats` совпадают, но не определяют `*.effects`, `SIZ1.effect`, `APP1.fins_bonus`, `APP1.leaves_bonus`, `SKN1.fuzzy_bonus`, `SKN1.smooth_bonus`, `SKN1.veined_bonus`, `body_size_cold_modifier`, `body_size_heat_modifier`, `size_modifier`, `health_penalty`, `heterozygosity_bonus`, `metabolism_modifier`, `health_modifier`. В fertility также есть `inbreeding_modifier` (OQ-008). Не заданы правила агрегации двух copies, округления и применения trait_modifiers. В DB §8 / `health_conditions` заданы flats и recovery multipliers, но нет порядка их композиции с формулами и clamp. Поля energy recovery, mood и care effects не имеют полной модели восстановления/границ.

Why decision is required:
Существующие формулы невозможно однозначно вычислить без новых допущений. Подстановка нулей, суммирование или усреднение по догадке изменили бы дизайн.

Do not implement before resolved.

## OQ-004 — Как maturation_hours соотносится с фиксированными стадиями жизни?

Status: OPEN

Context:
DB §4 и `life_stages` задают EGG 120, JUVENILE 120, ADOLESCENT 240 минут: до ADULT суммарно 8 часов. DB §7 / `derived_stats.maturation_hours` задают диапазон 5–14 часов с неопределёнными модификаторами. GDS §14 предполагает постепенное раскрытие pattern, temperament и latent phenotype; расписание раскрытия не задано.

Why decision is required:
Не определено, изменяет ли derived duration стадии, включает ли яйцо и как распределяется время/раскрытие между стадиями.

Do not implement before resolved.

## OQ-005 — Как expression models однозначно переводят две allele copies в phenotype?

Status: OPEN

Context:
DB §5–6 и `loci` называют INCOMPLETE_DOMINANCE_VECTOR, PALETTE_BLEND, CODOMINANT_COMPOSITION, CODOMINANT_PATTERN, DOSAGE_WITH_SPECIAL и ADDITIVE_ROUNDED. Полные правила объединения shape vectors, palettes, appendages, patterns и eye counts отсутствуют. GDS §5 описывает классы expression на примерах; DB §23 требует deterministic phenotype.

Why decision is required:
Названия моделей и allele values не определяют все heterozygous outcomes, способы смешивания, округления, дозировки и разрешения взаимодействий. Нельзя выбирать их при реализации.

Do not implement before resolved.

## OQ-006 — Как определяются glow_intensity и surface для классификации?

Status: OPEN

Context:
DB §9–10 / `ecotypes` / `morphotypes` используют `glow_intensity >= 2`; GLW1 содержит `glow_weight`, но формулы intensity нет. PRISM проверяет `surface == PRISM`, тогда как SKN1:k3 задаёт `renderer_surface: prism`. Контракт render в DB §21 использует `surface.type`. `expressed_health_defects` также не определён отдельной формулой. Процедура расчёта и порядок health/environment effects до классификации не заданы.

Why decision is required:
Нужен согласованный переход от allele data к этим полям. Нельзя предполагать суммирование glow или автоматическое преобразование регистра/имён surface.

Do not implement before resolved.

## OQ-007 — Как применяются mutation rates, неполный граф и structural events?

Status: OPEN

Context:
GDS §10 / DB §12 / `mutation` задают per-copy rate 0.00035, structural event rate 0.003 и target около 2%. Граф есть только для COL1, PAT1, GLW1, SKN1, AQU1, CLD1, PHO1; для остальных 17 loci переходы отсутствуют. Structural cosmetic outcomes не перечислены. Не задано сочетание событий, поведение loci без edges, повторных мутаций и конкретная семантика novel allele discovery.

Why decision is required:
Нельзя вывести реальную частоту из rates без определения множества eligible copies и событий. Нельзя создавать недостающие transitions или structural values для достижения target.

Do not implement before resolved.

## OQ-008 — Как вычисляются relatedness/inbreeding и влияет ли коэффициент на fertility?

Status: OPEN

Context:
GDS §11 показывает Low/Moderate/High; DB §14 — LOW/MODERATE/HIGH/VERY_HIGH и глубину 5 поколений. Пороги отсутствуют. Формула `contribution = (1/2)^(n1+n2) * (1 + F_A)` не определяет полностью n1, n2, F_A, суммирование путей, повторных ancestors и неизвестные pedigrees. DB §7 / `derived_stats.fertility` содержит неопределённый `inbreeding_modifier`, тогда как GDS §11 и DB §14 запрещают произвольный штраф вместо риска общих recessive alleles.

Why decision is required:
Нужно согласовать набор UI tiers, определение коэффициента и смысл modifier без изменения формулы по внешним представлениям о генетике.

Do not implement before resolved.

## OQ-009 — Как выбираются crossover positions и обрабатываются границы?

Status: OPEN

Context:
GDS §9 и DB §13 / `recombination` дают распределение количества crossovers 35/45/17/3%. GDS говорит выбрать positions along map, каталог содержит chromosome length 100 cM и позиции loci, но не задаёт распределение позиций, совпадения, точку на locus и крайние позиции. Формулировка bounded Poisson-like не задаёт иной полный алгоритм.

Why decision is required:
Нельзя считать выбор равномерным или вводить обработку границ по умолчанию. Это влияет на linkage и вероятности offspring.

Do not implement before resolved.

## OQ-010 — Какова environment model и какие loci она изменяет по expression?

Status: OPEN

Context:
GDS §5.5, §6, §16 описывают bounded environment modifier и seasonal pigment example. DB §23 требует deterministic phenotype при одинаковой environment model. Каталог не содержит полного списка environment states, чувствительных loci, границ и взаимодействий эффектов.

Why decision is required:
Нельзя приравнять среду к нулевому modifier или придумать habitat effects. Genotype при любом решении остаётся неизменяемым по принятому принципу.

Do not implement before resolved.

## OQ-011 — Как fertility, energy и care определяют breeding cooldown и доступность действий?

Status: OPEN

Context:
GDS §29 задаёт пример 2–8 часов в зависимости от fertility и оставляет exact values balancing. DB §17 / `actions.BREED` содержит base cooldown 360 минут и min energy 30%, но нет функции cooldown(fertility), правил для обоих родителей, полного расхода/восстановления energy и эффекта care на incubation. GDS §17, §28 описывают social breeding; точный non-power reward и условия использования public/чужого breeder не выбраны.

Why decision is required:
Baseline base value не является полной формулой. Нельзя автоматически выбрать reward, лимиты или поведение cooldown для второго владельца.

Do not implement before resolved.

## OQ-012 — Как expedition weights превращаются в результат и rewards?

Status: OPEN

Context:
GDS §26 и DB §18 / `expeditions` задают длительности, веса и классы rewards. Формула результата, нормализация входов, payouts и ограничения отсутствуют. CAVE использует `glow`, тогда как классификация использует `glow_intensity`; соответствие и шкала не заданы. В примере TUNDRA GDS упоминается Glow bonus, которого нет среди числовых weights DB/YAML.

Why decision is required:
Нужно уточнить статус примерного бонуса, смысл score и rewards; веса сами по себе не задают полную expedition model.

Do not implement before resolved.

## OQ-013 — Каковы границы rarity bands и population frequency?

Status: OPEN

Context:
GDS §24 приводит частоты allele, phenotype и combination. DB §20 / `rarity_bands` задают min/max, но не включительность общих границ 0.1, 0.03, 0.005, 0.0005, объект измерения, состав population, момент пересчёта и точное отображение до population 1000. `adaptation_tiers` имеет целочисленные интервалы 0–29, 30–49 и т.д., при этом правила округления дробных derived values не заданы.

Why decision is required:
Нельзя предположить диапазоны с открытой/закрытой границей, округление или знаменатель статистики.

Do not implement before resolved.

## OQ-014 — Как определяется стабильная линия, знание и discovery milestone?

Status: OPEN

Context:
GDS §18, §21–23 описывают состояния знания, stabilized loci, first stable line и illustrative progress. Нет точных критериев стабилизации, обновления inferred knowledge, обработки hidden outcomes, одновременных global discoveries или объёма доступного другому игроку знания. Marker panel не определяет конкретные наборы loci; basic scan назван cheap/free без выбора цены.

Why decision is required:
Нельзя превращать пример progress в алгоритм, автоматически назначать discoveries или раскрывать полный скрытый genotype при показе вероятностей.

Do not implement before resolved.

## OQ-015 — Как создаётся personal founder, задаётся haplotype phase и допускается ли selfing?

Status: OPEN

Context:
GDS §4, §13, §17 задают diploid hermaphroditic species, personal founder и public breeders. DB §15 / `founders` задают восемь полных генотипов и focus labels. Не описаны генерация личного founder с гарантиями, соответствие левой/правой allele copy единому homolog по chromosome, ancestry/unrelatedness founders и допустимость Parent A = Parent B. Не уточнено, focus — цель breeder или гарантированный вычисляемый morphotype; имена GENERALIS_DIVERSE и GENERALIS_CARRIER_TUTORIAL не являются morphotype IDs.

Why decision is required:
Нельзя трактовать focus как результат классификации, считать список alleles фазированным без правила или самостоятельно разрешить/запретить selfing. Эти решения меняют breeding outcomes.

Do not implement before resolved.

## OQ-016 — Какие сценарии, допуски и balance criteria должна проверять simulation?

Status: OPEN

Context:
GDS §42 требует минимум 100,000 offspring, fixed RNG seeds и перечень проверяемых свойств. Не заданы test populations, tolerances, target stabilization probability, допустимый drift и критерии результата; GDS §41 говорит о reasonable simulated population без численного определения. Полной simulation specification нет.

Why decision is required:
Нельзя объявить validation успешной только по sample size или подбирать правила для получения желаемых targets. Здесь сохраняется требование, simulator не разрабатывается.

Do not implement before resolved.

## OQ-017 — Как будущий Combat соотносится с утверждёнными границами baseline?

Status: OPEN

Context:
Текущий заданный статус Combat и Combat Balance — NOT_STARTED. GDS §2 исключает RPG с HP/ATK/DEF progression, §26 говорит No combat system required, §40 исключает PvP из first playable; DB §18 задаёт MVP expeditions без боёв. Запрошены только stubs для будущего блока.

Why decision is required:
До отдельного CANON UPDATE нельзя вывести из структуры папок разрешение менять MVP scope, проектировать Combat или переносить существующие derived stats в боевые.

Do not implement before resolved.

## OQ-018 — Как конкретизируются progression, economy, monetization и seasonal content?

Status: OPEN

Context:
Эти блоки имеют DRAFT. GDS §27–31, §37–38 и DB §19 описывают направления, границы, примеры и некоторые baseline costs, но не полные unlocks, income/reward amounts, lab upgrades, pacing progression, размеры active/reserve, условия additional incubator, сезонный контент и правила его ввода. ABYSS — пример, а не утверждённый каталог сезона; marketplace и paid season pass исключены из первого playable в GDS §40.

Why decision is required:
Нужны отдельные явные решения по конкретным значениям и scope без превращения разрешённой категории монетизации или сезонного примера в утверждённый продукт. Заготовка progression_v1.yaml не заполняет эти пробелы.

Do not implement before resolved.

## OQ-019 — Что входит в initial allele count и как категории scope сопоставляются каталогу?

Status: OPEN

Context:
GDS §39 рекомендует ~60–70 total initial alleles, 5–8 mutation-only и разбивку 12 visual / 6 adaptation-quantitative / 3 temperament-metabolism / 3 hidden-health loci. Каталог содержит 76 alleles, включая 7 mutation-only (69 с ненулевой founder frequency). Категория SIZ1 — VISUAL_QUANTITATIVE; ENR1/END1 и адаптации дополняют остальные группы. Входит ли mutation-only в initial total и как учитывать пересекающиеся категории — явно не сказано. GDS §5.5 приводит body size как polygenic, а `body_scale` в DB §7 зависит только от SIZ1.

Why decision is required:
76 против ~60–70 нельзя автоматически объявить ошибкой или исправить удалением alleles. Нужно уточнить scope и статус рекомендаций о polygenic traits относительно конкретного каталога.

Do not implement before resolved.
