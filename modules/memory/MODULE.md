# HAR-MEM — memory

**Owner repo:** `odelix-harness` · **Activation gate:** I1/Expansion · **Design:** 1.0.0 / 2026-09-28.
**Implementation status:** SPEC_ONLY / requires code inventory. Proposed path: `modules/memory`; this path does not assert an existing crate/package. Reuse existing implementation before introducing files.

## Назначение и предел ответственности

Извлекает и предлагает полезные memory candidates из runs. Долговременными пользовательскими объектами и consent владеет Product INV-MEM.

## Public ports и контракты

ProposeMemory(evidenceRefs, proposedFact, scope, ttl); ValidateMemoryReference; request Product commit/delete through public port.

Имена операций задают semantics, не подтверждают опубликованный API. Producer schema/fixtures и точная версия выпускаются вместе с реализацией; Stack registry содержит discovery/pins. Ошибки типизированы, environment/tenant/asOf/unit fields обязательны там, где применимы.

## Разрешённые зависимости

INV-MEM and INV-EVD APIs, HAR-CRT quality, PLT-DG retention/rights. No direct Product database writes.

Private imports и запись в чужие таблицы запрещены. Domain logic получает immutable inputs; infrastructure I/O подключается composition root. При новом общем контракте сначала согласуются producer fixtures и consumer migration.

## Состояние, время и восстановление

Candidate→reviewed→accepted/rejected; durable revision and TTL in Product. Model preference hypothesis not silently rewritten as user fact.

Version/config/code/dataset/contract refs связывают результат с исходными условиями. Retry действует в пределах operation id; unknown external state сверяется до повторного side effect. Денежные величины и timestamps не теряют точность при сериализации.

## Инварианты и отказ

No raw chain-of-thought, secrets, privileged prompts or cross-tenant memory. Operator trading use of customer intelligence forbidden by policy.

## Acceptance и review

Consent revoked; expired market fact; deletion/export propagated; source correction; speculative claim rejected; same fact dedup by semantic/source refs.

До Done нужны реальный code map/commit, выполненные meaningful checks, peer review и ссылки в Issue. Здесь тесты описаны как требования, не отмечены выполненными. Проверить публичные exports, allowed dependencies и отсутствие дублирующей реализации. Нет требования создавать новый runtime или deployment для этого модуля.

## Наблюдаемость и знание проекта

Логировать operation/run/strategy refs, duration, typed outcome, coverage и retry count без secrets/скрытых рассуждений. Метрики применяются к своей ответственности: module-specific failures из раздела инвариантов должны отличаться от infrastructure timeouts. Builder обновляет факты этого MODULE с кодом; Coordinator обновляет index/status. Не копировать полный отчёт в несколько документов.


## Приёмка r15

Один Pi + отдельная bounded fixed-question capability за SemanticEvaluatorPort, не второй agent loop. Jev условный заменяемый adapter; transport/semantic quality/forecast три разные проверки. См. [SEMANTIC-EVALUATOR.md](../../docs/AI-HARNESS-AND-INTELLIGENCE-PLATFORM.md#semantic-evaluator) и owner Issue в [общем backlog](../../docs/DEVELOPMENT.md#DEP-b335630551). Новые гарантии требуют tests/evidence; сохранённая спецификация не означает implemented.
<!-- R159 decision-memory -->
## Поздний импорт и reflections

Retrieval отдельно фильтрует момент знания записи и исхода. Старый eventAt у позднего импорта не делает outcome доступным прошлому Run. Reflection — новая версия с собственным знанием и consent, не замена события. Отсутствие Critic отмечается NOT_RUN. Rejected/abstained records входят в разрешённую выборку наряду с удачными; memory policy и dataset retention применяются перед чтением.

<a id="memory-permission"></a>
## Отдельное право памяти

Jev user_memory проверяется независимо от audit, eval и training. Retrieval учитывает source namespace, consent, known_at/outcome_known_at и отмену разрешения. Личная копия данных не превращается в продуктовую память; запрещённый derived text не снимает provenance ограничения.
