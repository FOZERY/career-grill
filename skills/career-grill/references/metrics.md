# Метрики и подробные истории достижений

Метрика в легенде — это история изменения системы или продукта. Короткая строка CV является производной от подробного рассказа: проблема → бизнес-значение → ответственность → решение → измерение → результат.

## Два уровня записи

### Короткая формула

Используй для итоговой строки достижения:

> `<сильный глагол>` + `<что изменил>` + `<технический механизм>` + `<метрика: было → стало>` + `<область результата>`.

Пример:

> Cut checkout API P95 latency from 687 ms to 214 ms by replacing sequential scans with composite indexes and removing an N+1 query from the order summary flow.

Формулировки `Improved API performance significantly` и `Improved API performance by 40%` недостаточны: не названы измеряемый путь, исходное/итоговое состояние и механизм.

### Подробная карточка легенды

Для каждого выбранного достижения создай в `CAREER_LEGEND.md` одну карточку по STAR+:

```markdown
#### Достижение N — <короткое название>

**Situation / проблема.** Как проявлялась проблема, кого затрагивала, насколько часто и почему была важна бизнесу или пользователю.

**Task / моя ответственность.** Какой результат требовался, где начиналась и заканчивалась ответственность пользователя, кто ещё участвовал.

**Action / диагностика и решение.** Как нашли причину; какие варианты рассматривали; что выбрали; какие изменения внесли в код, данные, инфраструктуру и процесс; как выкатывали и страховали риск.

**Result / измерение.** Определение метрики, baseline, result, периоды до/после, инструмент, конкретный dashboard/query/trace/report, дополнительные проверки и влияние на продукт.

**Почему достижение сильное.** Связь с пользователем/бизнесом, инженерная сложность, личный вклад, масштаб и компромисс.

**Источник и ограничения.** Откуда взялось число, какие есть ограничения причинности и что стоило бы измерить дополнительно.

**Короткая английская формула.** <материал для CV>
```

## Глубина измерения

Не принимай формулировку «посмотрели в Grafana». Доведи измерение до воспроизводимой цепочки:

1. Какое событие, запрос или операция измерялись?
2. Где начинался и заканчивался timer?
3. Какой инструмент создавал сигнал: application histogram, OpenTelemetry span, access log, PostgreSQL `EXPLAIN ANALYZE`, `pg_stat_statements`, Kafka lag exporter, CI analytics или продуктовая аналитика?
4. Как называлась метрика, label/filter, endpoint, topic, consumer group или query fingerprint?
5. Какой dashboard или запрос агрегировал данные?
6. Какое окно сравнивали: часы пика, семь дней до/после, одинаковый тип нагрузки?
7. Почему выбран P50/P95/P99, average, rate, count или доля?
8. Как исключили прогрев кэша, изменение трафика, сезонность, другой релиз и ошибку измерения?
9. Как проверили результат после deployment и что считалось сигналом для rollback?
10. Кто имел доступ к данным и почему пользователь видел эту метрику?

В легенде сохрани короткое, конкретное описание. Например:

> P95 брали из Prometheus histogram `http_request_duration_seconds` на endpoint создания заказа, dashboard команды в Grafana. Сравнивали два одинаковых вечерних пика по семь дней до и после rollout, исключив 5xx и внутренние health checks. После релиза дополнительно проверили traces и частоту timeout на клиентском gateway.

## Иерархия метрик по силе влияния

### 1. Деньги и бизнес

Примеры: выручка, GMV, MRR/ARR, инфраструктурные расходы, cost per request/order, стоимость inference, потери от инцидентов.

Это самые сильные показатели, когда инженерное действие действительно связано с денежным результатом. Для всей карьерной легенды выделяй не более 1–2 достижений как прямые денежные кейсы. Они наиболее естественны там, где команда видит P&L или счёт клиента: стартап, SaaS, коммерческая платформа, агентство/аутсорс с измеримой стоимостью проекта. В большой компании прямую выручку часто корректнее описывать как вклад, экономию инфраструктуры или снижение бизнес-потерь.

Пример короткой формулы:

> Reduced monthly LLM inference cost from approximately $15.6K to $9.3K through semantic caching, request batching and model routing, while preserving the agreed response-quality threshold.

В подробной истории нужны billing export, период, объём запросов, изменение unit cost и контроль качества.

### 2. Пользователь и продукт

Это основной класс достижений. Примеры: checkout latency, успешность заказа, время выдачи результата, conversion, cancellation, retention, доставка и свежесть статуса.

Пример:

> Cut checkout P95 from 2.08 s to 436 ms by parallelizing independent validations and caching product availability, reducing client timeouts during evening peaks.

Если conversion или retention менялись одновременно, установи способ измерения причинности. При отсутствии A/B-теста или контролируемого сравнения используй формулировку `contributed to`, а не присваивай всё изменение одному backend-релизу.

### 3. Система и масштаб

Примеры: RPS/QPS, events/s, concurrent connections, consumer lag, размер БД, rows/day, throughput jobs.

Такая метрика показывает масштаб и инженерную способность, но сама по себе не объясняет пользу. Свяжи её с необходимостью: выдержать пик, убрать очередь, снизить задержку пользователя или обеспечить рост продукта.

Пример:

> Raised sustained location-ingestion capacity from 11.7K to 38.4K events/s by batching Kafka writes and parallelizing consumers by courier ID, keeping processing lag below 3.6 s in load tests.

### 4. Активность

Примеры: число endpoints, миграций, сервисов, интеграций, PR, тестов или участников команды. Это контекст объёма работы, а не доказательство результата. Используй редко и рядом с более сильным эффектом.

Слабая формулировка:

> Developed 18 REST endpoints across 7 microservices.

Усиленная контекстом:

> Owned delivery-status workflows across 7 services and consolidated 18 client endpoints behind a versioned API, reducing breaking mobile changes during staged releases.

## Пять технических типов метрик

Распределяй их по карьерной легенде, выбирая те, которые естественно следуют из проектов.

| Тип | Что измерять | Примеры |
|---|---|---|
| Скорость | P95/P99 latency, response/build/deploy time, job duration, cold start, MTTR | `P95 687 → 214 ms`, `deploy 18.4 → 7.2 min` |
| Объём | RPS/QPS, events/s, rows, database size, processed TB, users/tenants/devices, concurrent connections | `38.4K events/s`, `7.8M rows/day` |
| Надёжность | availability, error rate, incidents, change failure rate, successful deploys, recovery rate | `error rate 1.8% → 0.37%`, `MTTR 71 → 24 min` |
| Деньги | infrastructure bill, cost/request, cost/order, savings, revenue protected, incident cost | `$15.6K → $9.3K/month` |
| Процессы и люди | release frequency, review/onboarding/lead time, team/service scope | `lead time 4.6 → 1.9 days` |

Test coverage относится к качеству процесса и является косвенным сигналом надёжности. Не выдавай рост coverage за снижение production-дефектов без отдельного измерения.

## Продуктовые и бизнес-метрики

| Категория | Метрики | Что показывают |
|---|---|---|
| Revenue | Revenue, MRR, ARR, ARPU, AOV, GMV | Денежный объём продукта |
| Conversion | Conversion Rate, funnel conversion | Доля пользователей, дошедших до целевого действия |
| Acquisition | New Users, CAC, CPA | Привлечение и его стоимость |
| Retention | D1/D7/D30 retention, churn, repeat rate | Возврат и удержание пользователей |
| Engagement | DAU, WAU, MAU, DAU/MAU | Частота использования продукта |
| Unit economics | LTV, CAC, LTV/CAC, payback period, cost per order | Экономика пользователя или операции |
| Transactional | Orders, bookings, transactions, AOV | Объём основного бизнес-процесса |
| Failures | Cancellation, payment failure, refund, unsuccessful delivery | Точки потери денег и доверия |

DAU и MAU описывают продуктовый масштаб; сами по себе они не являются личным достижением инженера. Retention становится инженерным достижением, когда известна связь: какую пользовательскую проблему устранили, какой cohort/период измеряли и чем отделили эффект от маркетинга, сезонности и других продуктовых изменений.

### Food delivery / dispatch / real-time

- Бизнес: orders/day, order conversion, cancellation rate, delivery completion, average delivery time, courier acceptance, orders per courier-hour, GMV, cost per delivery.
- Продукт: DAU/MAU, repeat order rate, D7/D30 retention, checkout funnel, доля заказов с live tracking.
- Технические: RPS, P95/P99 latency, error rate, availability, concurrent WebSockets, events/s, consumer lag, dispatch latency, location freshness.

Пример цепочки влияния:

> Снизили P95 dispatch latency с 1.46 s до 382 ms → сократили долю assignment timeout с 2.1% до 0.54% → выросла успешность автоматического назначения. Влияние на среднее время доставки описывается отдельно и только при наличии продуктовой аналитики.

### Production AI / RAG / voice

- Пользовательские: task success rate, answer acceptance, grounded-answer rate, citation coverage, search-to-action conversion, containment rate, escalation rate, time-to-first-audio, completion rate.
- Retrieval/evals: Recall@K, Precision@K, MRR/NDCG, reranker lift, faithfulness/groundedness, golden-set pass rate, human-review score.
- Производительность: time to first token/byte/audio, end-to-end P95/P99, tokens/s, requests/min, documents/hour, queue/processing lag.
- Объём: documents/chunks/vectors, tokens/day, conversations, audio minutes, concurrent streams.
- Надёжность: provider error/timeout rate, fallback success, retry rate, malformed-output rate, hallucination/unsafe-answer rate.
- Деньги: cost per request/conversation/audio minute, cache savings, monthly inference/embedding bill, human-review cost avoided.

Одна AI-история должна сочетать минимум техническую метрику и результат workflow. Например:

> Снизили P95 ответа RAG-ассистента с 4.82 s до 2.17 s за счёт parallel retrieval, semantic cache и streaming; доля сессий, где оператор принимал предложенный ответ без редактирования, выросла с 41% до 58% по данным CMS analytics.

Проверь dataset, rubric и выборку evals. Рост acceptance не равен автоматической экономии денег; экономию рассчитай через обработанное время и стоимость часа.

### Процессы, люди и AI-автоматизация

- lead time задачи, время code review, время onboarding до первого production change;
- deploy frequency, change failure rate, rollback rate, время подготовки release notes;
- число повторных инцидентов, MTTR, доля выполненных postmortem actions;
- доля команды, использующая новый процесс, completion rate и время ручной работы;
- время daily/weekly reporting, полнота статусов, доля пропущенных blockers, время менеджеров на сбор отчёта.

Пример AI-автоматизации:

> Внедрил internal status bot, который собирал структурированные async updates и формировал daily/weekly summaries; сократил ручную подготовку статусов с ~4.3 до ~1.1 manager-hours в неделю и достиг 86% weekly response rate за первые восемь недель.

В подробной истории объясни channels/permissions, расписание, prompt/schema, обработку пропусков, human review, хранение данных, качество summary и способ расчёта сэкономленного времени.

## Происхождение метрики

Используй четыре уровня:

1. **Публичная:** опубликована компанией для продукта или платформы; служит контекстом масштаба.
2. **Измеренная:** dashboard, tracing, логи, query plan, CI/CD analytics, load test или incident report.
3. **Рассчитанная:** выводится из известных входных значений по показанной формуле.
4. **Оценочная:** инженерная оценка с диапазоном, assumptions и sensitivity check.

Публичная, рассчитанная и оценочная метрики не становятся личным результатом кандидата автоматически. В `Паспорте для CV` помечай метрику как `подтверждено` только когда пользователь подтвердил сам результат и правдоподобный способ, которым он знал это значение. Остальные уровни остаются контекстом или материалом для тренировки.

Для каждой метрики сохрани:

| Поле | Содержание |
|---|---|
| Определение | Что считается, единица, scope и точка измерения |
| Период | Окно наблюдения, среднее или пик |
| Baseline / result | Значения в сопоставимых условиях |
| Источник | Ссылка, dashboard, query, trace, test/report или формула |
| Расчёт | Входные данные и операции |
| Диапазон | Разумный минимум, рекомендуемое значение, максимум |
| Причинность | Действие пользователя и другие изменения |
| Источник и воспроизводимость | Как получено число и как повторить измерение |

## Построение оценки

Начинай с наблюдаемой бизнес-величины и спускайся к сервису:

- активные курьеры × частота координат → location events/s;
- заказы/день × число смен состояния → order events/day;
- пользователи пикового часа × запросы за сессию → средний поток;
- replicas × лимит pool → возможные подключения PostgreSQL;
- объекты/день × размер записи × retention → размер таблицы;
- commits/week × доля релизов → deploy frequency.

Покажи консервативный и верхний сценарии, затем предложи рекомендуемое значение. Среднее за сутки не называй пиком: добавь обоснованный коэффициент пиковости. Проверь согласованность с публичным масштабом компании, числом инстансов, partitions, connection pools и возможностями хранилища.

Не форсируй числовой результат. Если значение нельзя естественно связать с наблюдаемым сигналом, способом измерения и доступом пользователя, предложи качественный эффект: устранённый класс ошибок, сокращённый ручной шаг, появившуюся возможность, более предсказуемый релиз или снижение риска. Конкретное, но необоснованное число слабее честного качественного результата.

## Арифметика

- снижение длительности: `(до − после) / до × 100%`;
- ускорение: `до / после`;
- изменение доли в процентных пунктах: `после − до`;
- error rate: ошибки / все попытки за одинаковое окно;
- availability требует определения успешного ответа и периода.

Пятикратное ускорение соответствует снижению времени на 80%. P95 SQL-запроса, P95 HTTP endpoint и end-to-end задержка до клиента — разные показатели. Перцентили отдельных этапов не складываются как end-to-end P95.

## Естественность чисел

Не используй заоблачные порядки вроде `1 000 000 RPS` без источника и соответствующей архитектуры. Избегай серии круглых значений и одинаково красивых процентов. Одновременно не создавай ложную точность: `37,284%` не соответствует грубой оценке.

Сначала получи диапазон и точность измерения:

- точный dashboard: `P95 487 ms → 163 ms`;
- приблизительная память: `~500 ms → ~170 ms`;
- расчётная нагрузка: `примерно 8–12K events/s в пике`;
- процент из измеренных значений: `снижение примерно на 66%`.

Неровная цифра сама по себе не делает показатель правдоподобным. Она должна следовать из измерения или расчёта.

## Финальная фиксация метрики

Подготовь запись:

> «Проблема влияла на `<пользователь/бизнес>` так: `<эффект>`. Мы измеряли `<показатель>` в `<инструмент>` на уровне `<endpoint/сервис/продукт>`. Сравнивали `<период до>` и `<период после>` при `<условия>`. Было `<baseline>`, стало `<result>`. Я сделал `<действие>`; параллельно менялось `<другие факторы>`, поэтому результат описан как `<причина/вклад>`».

Если невозможно внятно назвать источник, точку измерения и период, оставь диапазон, capacity/load-test result или качественный эффект.
