# Decisions

Status: APPROVED

Реестр уже принятых решений baseline v0.1 и CANON UPDATE 001. Это не новое утверждение спорных деталей. Числовые targets, примеры, DRAFT-блоки и неполные формулы не превращаются здесь в окончательные решения.

| ID | Уже принятое решение | Канонический источник |
|---|---|---|
| DEC-001 | Product thesis: «I bred this»; игрок разводит популяции и строит линии. | [Game Vision](canon/GAME_VISION.md), GDS §0, §46 |
| DEC-002 | Одна синтетическая форма GENOMORPH; morphotypes вычисляются, а не являются закрытыми species. | [Creature Model](creatures/CREATURE_MODEL.md), DB §1 |
| DEC-003 | Диплоидная гермафродитная модель; 6 пар хромосом, 24 локуса, 2 allele copies на locus. | [Genome Model](genetics/GENOME_MODEL.md), GDS §4 |
| DEC-004 | Наследование идёт через родительские гаметы, сцепление и рекомбинацию; независимый roll каждого locus недопустим. | [Breeding](genetics/BREEDING_SYSTEM.md), GDS §8–9, DB §13 |
| DEC-005 | Genotype отделён от phenotype; care и sequencing не переписывают genome. | [Genome Model](genetics/GENOME_MODEL.md), GDS §6; [Principles](canon/DESIGN_PRINCIPLES.md), DB §23 |
| DEC-006 | Genome фиксируется при создании яйца; индивидуальное созревание не является эволюцией через поколения. | [Creature Model](creatures/CREATURE_MODEL.md), GDS §7, §14 |
| DEC-007 | Мутации контролируются явными переходами; mutation-only alleles отсутствуют у founders и далее наследуются. | [Mutation](genetics/MUTATION_SYSTEM.md), GDS §10, DB §11–12 |
| DEC-008 | Рецессивный риск связан с общими скрытыми alleles; нельзя убивать или навсегда обесценивать существо из-за дефекта. | [Lineage](genetics/LINEAGE_SYSTEM.md), GDS §11 |
| DEC-009 | Пропуск входа не уничтожает прогресс; смерти от старости/неактивности в v0.1 нет. | [Creature Model](creatures/CREATURE_MODEL.md), GDS §15, DB §4 |
| DEC-010 | Полная sequencing доступна через gameplay; reserve сохраняет геном и историю. | [Collection](creatures/COLLECTION_SYSTEM.md), GDS §18–19 |
| DEC-011 | Первичная rarity происходит из population frequency, а не случайной карточной редкости. | [Collection](creatures/COLLECTION_SYSTEM.md), GDS §24, DB §20 |
| DEC-012 | Платные покупки не создают объективно более сильные генетические линии. | [Principles](canon/DESIGN_PRINCIPLES.md), GDS §44 |
| DEC-013 | Изменения locus, allele, mutation edge, formula или morphotype threshold повышают genome_schema_version; старые геномы нельзя молча переписывать. | [Genome Model](genetics/GENOME_MODEL.md), DB §24 |

Противоречащие или неполные детали этих принципов остаются в [OPEN_QUESTIONS](OPEN_QUESTIONS.md). Статус отдельных collection/economy/progression документов не повышается записью общего принятого принципа.

## CANON UPDATE 001 — 2026-09-23

Status: APPROVED

Основание: [согласованный Update 001](updates/GENOME_CANON_UPDATE_001.md). APPROVED относится только к перечисленным решениям с их оговорками, Combat в целом — DRAFT. Новые решения имеют приоритет над baseline лишь в явно затронутых пунктах; прежние DEC ID сохраняются. OQ-017 уточнён, но не закрыт; остальные прежние OPEN questions также остаются OPEN.

| ID | Уже принятое решение | Канонический источник |
|---|---|---|
| DEC-014 | COMBAT-001: команды 3v3. | [Combat Core](combat/COMBAT_CORE.md), COMBAT-001 |
| DEC-015 | COMBAT-002: автоматический асинхронный бой, подготовка состава до боя, без ручных действий во время боя. | [Combat Core](combat/COMBAT_CORE.md), COMBAT-002 |
| DEC-016 | COMBAT-003: FRONT/BACK_LEFT/BACK_RIGHT; FRONT — стандартная цель обычной одиночной атаки, позиция, а не класс; после выбытия один задний занимает FRONT. Детали исключений и перемещения OPEN. | [Combat Core](combat/COMBAT_CORE.md), COMBAT-003 |
| DEC-017 | COMBAT-004: дискретные раунды, воспроизводимость при одинаковых начальных данных/версии/RNG seed; анимация не меняет исход. Это не утверждает конкретные случайные события. | [Combat Core](combat/COMBAT_CORE.md), COMBAT-004 |
| DEC-018 | DIV-001: шесть логических семейств генов; это не новые chromosomes и не распределение loci. | [Genetic Diversity Model](genetics/GENETIC_DIVERSITY_MODEL.md), DIV-001 |
| DEC-019 | DIV-002: сильная специализация имеет цену на уровне сборки; не требуется штраф у каждого allele или равная сумма stats. | [Genetic Diversity Model](genetics/GENETIC_DIVERSITY_MODEL.md), DIV-002 |
| DEC-020 | DIV-003: тип не готовый класс, гибрид не получает два полных набора преимуществ бесплатно; morphotype, adaptation и специализация различаются. | [Genetic Diversity Model](genetics/GENETIC_DIVERSITY_MODEL.md), DIV-003 |
| DEC-021 | DIV-004: селекция управляет шансами и закрепляет признаки; мутация — отдельный механизм, повторение пары и дубликаты разрешены, скрытая подмена распределения не разрешена. | [Genetic Diversity Model](genetics/GENETIC_DIVERSITY_MODEL.md), DIV-004 |
| DEC-022 | DIV-005: разные генетические пути к роли и разные контры; компенсация слабости имеет цену, родитель выбирается под задачу/команду, без искусственного штрафа за популярность. | [Genetic Diversity Model](genetics/GENETIC_DIVERSITY_MODEL.md), DIV-005 |
