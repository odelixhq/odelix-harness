# HAR-CTX — context

**Owner repo:** `odelix-harness` · **Activation gate:** I1 · **Design:** 1.0.0 / 2026-09-28.
**Implementation status:** SPEC_ONLY / requires code inventory. Proposed path: `modules/context`; this path does not assert an existing crate/package. Reuse existing implementation before introducing files.

## Назначение и предел ответственности

Управляет bounded context каждого product agent: retrieval, budgets, compression и checkpoint handoff. Не авторитет рыночных фактов.

## Public ports и контракты

BuildAgentContext(role, run, task, evidenceRefs, modelBudget); CheckpointContext → HandoffRef; ResumeContext validates digests.

Имена операций задают semantics, не подтверждают опубликованный API. Producer schema/fixtures и точная версия выпускаются вместе с реализацией; Stack registry содержит discovery/pins. Ошибки типизированы, environment/tenant/asOf/unit fields обязательны там, где применимы.

## Разрешённые зависимости

Product INV-CTX/EVD/PLT tenant; HAR-RUN/CAP/MDL; immutable source refs. Secrets broker only returns permitted handles.

Private imports и запись в чужие таблицы запрещены. Domain logic получает immutable inputs; infrastructure I/O подключается composition root. При новом общем контракте сначала согласуются producer fixtures и consumer migration.

## Состояние, время и восстановление

Packet binds role/tenant/session/run/asOf/schema/source hashes; reserves tool/output tokens before admission. Retrieval summaries preserve fact/inference/unknown labels.

Version/config/code/dataset/contract refs связывают результат с исходными условиями. Retry действует в пределах operation id; unknown external state сверяется до повторного side effect. Денежные величины и timestamps не теряют точность при сериализации.

## Инварианты и отказ

Stale/context-cross-tenant packet rejected; critical policy and task scope survive compaction. Reviewer context not contaminated with authoritative Builder verdict.

## Acceptance и review

Small-window compaction; long tool output truncation with artifact ref; revoked evidence; wrong tenant; resume after code/model switch; no loss of unresolved blocker.

До Done нужны реальный code map/commit, выполненные meaningful checks, peer review и ссылки в Issue. Здесь тесты описаны как требования, не отмечены выполненными. Проверить публичные exports, allowed dependencies и отсутствие дублирующей реализации. Нет требования создавать новый runtime или deployment для этого модуля.

## Наблюдаемость и знание проекта

Логировать operation/run/strategy refs, duration, typed outcome, coverage и retry count без secrets/скрытых рассуждений. Метрики применяются к своей ответственности: module-specific failures из раздела инвариантов должны отличаться от infrastructure timeouts. Builder обновляет факты этого MODULE с кодом; Coordinator обновляет index/status. Не копировать полный отчёт в несколько документов.


## Приёмка r15

Один Pi + отдельная bounded fixed-question capability за SemanticEvaluatorPort, не второй agent loop. Jev условный заменяемый adapter; transport/semantic quality/forecast три разные проверки. См. [SEMANTIC-EVALUATOR.md](../../docs/AI-HARNESS-AND-INTELLIGENCE-PLATFORM.md#semantic-evaluator) и owner Issue в [общем backlog](../../docs/DEVELOPMENT.md#DEP-b335630551). Новые гарантии требуют tests/evidence; сохранённая спецификация не означает implemented.

<a id="external-data-layer"></a>
## External provider input eligibility

[Нормативная AI-граница](../../docs/AI-HARNESS-AND-INTELLIGENCE-PLATFORM.md#external-data-context). Compiler проверяет DataBinding/receipt, source and transform versions, known availability, freshness/completeness и AI permissions по каждому слою. No direct OpenBB/vendоr fetch внутри Pi.

Проверки: current revised macro row не считается известным в прошлом; unknown side/book input нельзя заменить нулём; rounded chain field не exact premium; as-shown использует сохранённый snapshot; revoked AI right предотвращает egress даже при разрешённом display/cache.
<!-- R159 known-time-egress -->
## Контекст DecisionRecord и полной data-программы

Context compiler получает InputRef с source event time, knownAt, outcomeKnownAt, source vintage/cut, precision, доступностью bytes и allowed uses. Неизвестные/недоступные refs не разрешаются скрытым сетевым запросом. Право проверяется до hosted inference и при cache reuse; derived feature/narrative сохраняет исходные ограничения. Полный target source не даёт права анализировать его ещё не собранные данные.
