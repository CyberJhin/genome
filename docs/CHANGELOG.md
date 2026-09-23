# Changelog

Status: APPROVED

## 2026-09-23 — Establish canonical design baseline

Организация документации по запросу владельца проекта; game-design решения не менялись.

- Созданы INDEX, тематические canonical docs, DECISIONS, OPEN_QUESTIONS и CONTRIBUTING_DESIGN.
- Все 47 нумерованных разделов GDS и 25 разделов DB, а также обе вводные части перенесены дословно. Карта переноса находится в [INDEX](INDEX.md#baseline-sources-и-карта-переноса).
- Оба MD baseline перенесены из корня в docs/source без изменения байтов; сохраняются как исходники.
- `genome_v1_catalog.yaml` перенесён в [data/genome_v1.yaml](../data/genome_v1.yaml) без изменения байтов, значений, ID или genome_schema_version.
- Combat и abilities представлены только NOT_STARTED stubs. progression_v1.yaml содержит DRAFT-указатели на существующие данные, без дублирования значений и без нового runtime-контракта.
- В README добавлена Source of Truth hierarchy. Исходные упоминания старого имени каталога сохранены внутри цитируемого baseline и пояснены текущими ссылками.
- Combat, technical architecture, backend/frontend и simulator не проектировались и не реализовывались.

## Consistency review

Проверяется документальный baseline, а не корректность будущей реализации или генетической симуляции.

| Категория | Результат |
|---|---|
| Broken links | Локальные Markdown-ссылки и используемые anchors проверены; отсутствующих целей нет. Исторические имена в дословных исходниках — не активные пути текущего каталога. |
| Missing docs / content | Все запрошенные документы и четыре YAML присутствуют. Все 72 нумерованных раздела и обе вводные имеют ровно одно дословное тематическое размещение. Git object hashes обоих source MD и основного YAML совпадают с исходным commit; учтено стандартное для checkout преобразование LF/CRLF. |
| Duplicate definitions | Исходные повторы сохранены с provenance: GDS §4 / DB §5 (геном), GDS §9 / DB §13 (рекомбинация), GDS §10 / DB §11–12 (мутации), GDS §14 / DB §4 (жизненный цикл), GDS §11 / DB §14 (relatedness), GDS §18 / DB §16 (lab), GDS §24 / DB §20 (rarity), GDS §26 / DB §18 (экспедиции), GDS §30 / DB §19 (ресурсы). Карта DB §5 и каталог DB §6 повторяют metadata loci по назначению. Тематический текст и docs/source — управляемое дублирование baseline, а не два независимых новых канона. Числа основного YAML не размножены в progression_v1.yaml. |
| YAML / MD values | Проверены chromosome map, все 76 allele rows (names, frequencies, properties), 13 derived formulas, ecotype/morphotype rules, action/rarity values и expedition durations/weights: DB соответствует YAML. Это не означает полноту формул. |
| YAML structure | Все четыре YAML разбираются без duplicate keys. Проверены 6 chromosomes, 24 loci, существование ссылок на alleles, founder frequency sums, восемь diploid founder genomes, отсутствие mutation-only alleles у founders, mutation edges/weight sums, crossover distribution и expedition weight sums. |
| YAML / MD divergence | Примеры GDS используют ID вне каталога и другое размещение Glow/Water: OQ-001. Пример casual probabilities не соответствует указанному cross, если это один случай: OQ-002. PRISM/prism и glow field mapping: OQ-006. TUNDRA example Glow bonus отсутствует в числовых weights: OQ-012. |
| Противоречия / неоднозначности | Фиксированные 8 часов стадий и maturation_hours 5–14: OQ-004. Три/четыре relatedness tiers и inbreeding_modifier при запрете произвольного штрафа: OQ-008. 76 total / 69 founder-eligible alleles и приблизительный initial scope, а также polygenic body size / SIZ1: OQ-019. Часть случаев может оказаться намеренным примером или уточнением, но это не решено автоматически. |
| Неполные определения и скрытые предположения | Derived stats, expression, mutation, crossover positions, environment, cooldown, expedition result, rarity boundaries, knowledge/line stability, founder phase/selfing, simulation criteria и DRAFT-блоки вынесены в OQ-003–OQ-016, OQ-018. Значения для заполнения пробелов не добавлялись. |
| Scope | Шесть biome examples в GDS §26 не объявлены противоречием: GDS §40 явно ограничивает MVP Forest/Tundra/Cave, как DB/YAML. 6–10 public breeders и восемь в каталоге согласуются. Будущий Combat требует отдельного CANON UPDATE (OQ-017). |

Все 19 записей [OPEN_QUESTIONS](OPEN_QUESTIONS.md) остаются OPEN. Баланс, probabilities simulation и игровая реализация не проверялись исполнением: это вне текущей задачи, а правила имеют открытые вопросы. Проверки выше относятся к сохранности, структуре, ссылкам и согласованности существующих данных.

Проверки выполнены временным скриптом вне репозитория с Python/PyYAML; зависимости проекта не добавлялись. При независимом review устранено двусмысленное редакционное пояснение APPROVED в DRAFT-документах: их статус явно остаётся DRAFT. Исходный текст разделов при этом не менялся.

Стандартный `git diff --cached --check` отмечает две исходные Markdown hard-break последовательности (два пробела после Version и Status в перенесённой вводной GDS). Они намеренно сохранены для дословного переноса. Проверка с отключением только `blank-at-eol` проходит; конфигурация репозитория не менялась.
