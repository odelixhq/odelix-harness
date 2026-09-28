# HAR-RUN — run-runtime

**Owner repo:** `odelix-harness` · **Activation gate:** C1/I1 · **Design:** 1.0.0 / 2026-09-28.
**Implementation status:** SPEC_ONLY / requires code inventory. Proposed path: `modules/run-runtime`; this path does not assert an existing crate/package. Reuse existing implementation before introducing files.

## Назначение и предел ответственности

Agent loop и task/specialist orchestration внутри Pi. Product PLT-RUN owns durable admission/placement/lease, не reasoning flow.

## Public ports и контракты

StartAgentRun(pinnedManifest, lease), StreamRunEvents, Checkpoint, CancelRun; typed final outcome with evidence/usage refs.

Имена операций задают semantics, не подтверждают опубликованный API. Producer schema/fixtures и точная версия выпускаются вместе с реализацией; Stack registry содержит discovery/pins. Ошибки типизированы, environment/tenant/asOf/unit fields обязательны там, где применимы.

## Разрешённые зависимости

HAR-CTX/SKL/CAP/MDL/CRT/TRC/EVL; Product run-control/usage ports; approved deterministic domain tools.

Private imports и запись в чужие таблицы запрещены. Domain logic получает immutable inputs; infrastructure I/O подключается composition root. При новом общем контракте сначала согласуются producer fixtures и consumer migration.

## Состояние, время и восстановление

Single authoritative executor with fencing token, durable checkpoints and bounded retries. Child tasks belong to one root Run and budget.

Version/config/code/dataset/contract refs связывают результат с исходными условиями. Retry действует в пределах operation id; unknown external state сверяется до повторного side effect. Денежные величины и timestamps не теряют точность при сериализации.

## Инварианты и отказ

No duplicate settlement after resume; expired lease cannot commit; material answer without Critic not procedure-verified. No trading send via generic shell.

## Acceptance и review

Worker crash/fencing; model timeout; budget exhaustion; child task failure; cancel at tool boundary; resumed tool side effect reconciled before retry.

До Done нужны реальный code map/commit, выполненные meaningful checks, peer review и ссылки в Issue. Здесь тесты описаны как требования, не отмечены выполненными. Проверить публичные exports, allowed dependencies и отсутствие дублирующей реализации. Нет требования создавать новый runtime или deployment для этого модуля.

## Наблюдаемость и знание проекта

Логировать operation/run/strategy refs, duration, typed outcome, coverage и retry count без secrets/скрытых рассуждений. Метрики применяются к своей ответственности: module-specific failures из раздела инвариантов должны отличаться от infrastructure timeouts. Builder обновляет факты этого MODULE с кодом; Coordinator обновляет index/status. Не копировать полный отчёт в несколько документов.


## Приёмка r15

Один Pi + отдельная bounded fixed-question capability за SemanticEvaluatorPort, не второй agent loop. Jev условный заменяемый adapter; transport/semantic quality/forecast три разные проверки. См. [SEMANTIC-EVALUATOR.md](../../docs/AI-HARNESS-AND-INTELLIGENCE-PLATFORM.md#semantic-evaluator) и owner Issue в [общем backlog](../../docs/DEVELOPMENT.md#DEP-b335630551). Новые гарантии требуют tests/evidence; сохранённая спецификация не означает implemented.
<!-- R159 mission-leases -->
## Mission attempt discipline

Идентификатор `(mission,trigger,iteration)` обеспечивает идемпотентное wake. Один fenced lease владеет активным attempt; stale worker не коммитит result. Один root budget охватывает children/retries. SLEEPING не вызывает LLM; нет бесконечного polling-loop модели. Terminal Run status не равен подтверждённому внешнему эффекту. HAR-012 generic, HAR-020 advanced binding.
