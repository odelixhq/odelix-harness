# HAR-SKL — trading-skills

**Уточнение scope Research: r12.1 · 2026-09-18.** Пользовательские примеры не определяют встроенную стратегию или обязательный dataset; статус реализации не меняется.

**Owner repo:** `odelix-harness` · **Activation gate:** I1/RES-1 · **Design:** 1.0.1 / 2026-09-28.
**Implementation status:** SPEC_ONLY / requires code inventory. Proposed path: `modules/trading-skills`; this path does not assert an existing crate/package. Reuse existing implementation before introducing files.

## Назначение и предел ответственности

Managed analytical/research procedures для всех standard и custom strategies; parses intent, plans tools, requests criticism, explains results.

## Public ports и контракты

strategy.define, strategy.compare, strategy.explain, experiment.plan/run/explain, portfolio.explain; actions have scope and side-effect metadata.

Имена операций задают semantics, не подтверждают опубликованный API. Producer schema/fixtures и точная версия выпускаются вместе с реализацией; Stack registry содержит discovery/pins. Ошибки типизированы, environment/tenant/asOf/unit fields обязательны там, где применимы.

## Разрешённые зависимости

Product Research/Investigation application ports; Market compiler/pricing; HAR-CTX/CRT; activated Execution only via explicit policy-bound tools.

Private imports и запись в чужие таблицы запрещены. Domain logic получает immutable inputs; infrastructure I/O подключается composition root. При новом общем контракте сначала согласуются producer fixtures и consumer migration.

## Состояние, время и восстановление

One skill id/version semantics across Connect/Desk/Workstation. Draft→validate→compute→critic→result, with questions/abstention as valid outcomes.

Version/config/code/dataset/contract refs связывают результат с исходными условиями. Retry действует в пределах operation id; unknown external state сверяется до повторного side effect. Денежные величины и timestamps не теряют точность при сериализации.

## Инварианты и отказ

Never invent quotes/Greeks/PnL or missing selected inputs; no master key. request_quote may disclose intent externally and is not classified blanket read-only.

## Acceptance и review

Unresolved user-defined threshold or exit policy; unsupported calendar valuation; available raw data but denied rights; low evidence abstention; blind baseline comparison; result cannot be relabelled verified externally.

До Done нужны реальный code map/commit, выполненные meaningful checks, peer review и ссылки в Issue. Здесь тесты описаны как требования, не отмечены выполненными. Проверить публичные exports, allowed dependencies и отсутствие дублирующей реализации. Нет требования создавать новый runtime или deployment для этого модуля.

## Наблюдаемость и знание проекта

Логировать operation/run/strategy refs, duration, typed outcome, coverage и retry count без secrets/скрытых рассуждений. Метрики применяются к своей ответственности: module-specific failures из раздела инвариантов должны отличаться от infrastructure timeouts. Builder обновляет факты этого MODULE с кодом; Coordinator обновляет index/status. Не копировать полный отчёт в несколько документов.


## Приёмка r15

Один Pi + отдельная bounded fixed-question capability за SemanticEvaluatorPort, не второй agent loop. Jev условный заменяемый adapter; transport/semantic quality/forecast три разные проверки. См. [SEMANTIC-EVALUATOR.md](../../docs/AI-HARNESS-AND-INTELLIGENCE-PLATFORM.md#semantic-evaluator) и owner Issue в [общем backlog](../../docs/DEVELOPMENT.md#DEP-b335630551). Новые гарантии требуют tests/evidence; сохранённая спецификация не означает implemented.
<!-- R159 observer-postmortem -->
## Новые процедуры и их источники

Минимальный observation digest используется HAR-012 без обязательной advanced team. HAR-017 формирует post-mortem по разрешённым inputs и явно сообщает coverage IMPORTED/RECONSTRUCTABLE/VERIFIED_AS_SHOWN; это не повышение полноты. HAR-018 переносит bounded specialist/challenge/composer procedure TradingAgents в Pi, а не их LangGraph. Сценарные risk claims не являются решением deterministic policy owner.
