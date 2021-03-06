## ClickHouse release 18.14.17, 2018-11-30

### Исправления ошибок:
* Исправлена ситуация, при которой ODBC Bridge продолжал работу после завершения работы сервера ClickHouse. Теперь ODBC Bridge всегда завершает работу вместе с сервером. [#3642](https://github.com/yandex/ClickHouse/pull/3642)
* Исправлена синхронная вставка в `Distributed` таблицу в случае явного указания неполного списка столбцов или списка столбцов в измененном порядке. [#3673](https://github.com/yandex/ClickHouse/pull/3673)
* Исправлен редкий race condition, который мог привести к падению сервера при удалении MergeTree-таблиц. [#3680](https://github.com/yandex/ClickHouse/pull/3680)
* Исправлен deadlock при выполнении запроса, возникающий если создание новых потоков выполнения невозможно из-за ошибки `Resource temporarily unavailable`. [#3643](https://github.com/yandex/ClickHouse/pull/3643)
* Исправлена ошибка парсинга `ENGINE` при создании таблицы с синтаксисом `AS table` в случае, когда `AS table` указывался после `ENGINE`, что приводило к игнорированию указанного движка. [#3692](https://github.com/yandex/ClickHouse/pull/3692)

## ClickHouse release 18.14.15, 2018-11-21

### Исправления ошибок:
* При чтении столбцов типа `Array(String)`, размер требуемого куска памяти оценивался слишком большим, что приводило к исключению "Memory limit exceeded" при выполнении запроса. Ошибка появилась в версии 18.12.13. [#3589](https://github.com/yandex/ClickHouse/issues/3589)

## ClickHouse release 18.14.14, 2018-11-20

### Исправления ошибок:
* Исправлена работа запросов `ON CLUSTER` в случае, когда в конфигурации кластера включено шифрование (флаг `<secure>`). [#3599](https://github.com/yandex/ClickHouse/pull/3599)

### Улучшения процесса сборки ClickHouse:
* Исправлены проблемы сборки (llvm-7 из системы, macos) [#3582](https://github.com/yandex/ClickHouse/pull/3582)

## ClickHouse release 18.14.13, 2018-11-08

### Исправления ошибок:
* Исправлена ошибка `Block structure mismatch in MergingSorted stream`. [#3162](https://github.com/yandex/ClickHouse/issues/3162)
* Исправлена работа запросов `ON CLUSTER` в случае, когда в конфигурации кластера включено шифрование (флаг `<secure>`). [#3465](https://github.com/yandex/ClickHouse/pull/3465)
* Исправлена ошибка при использовании `SAMPLE`, `PREWHERE` и столбцов-алиасов. [#3543](https://github.com/yandex/ClickHouse/pull/3543)
* Исправлена редкая ошибка `unknown compression method` при использовании настройки `min_bytes_to_use_direct_io`. [3544](https://github.com/yandex/ClickHouse/pull/3544)

### Улучшения производительности:
* Исправлена деградация производительности запросов с `GROUP BY` столбцов типа Int16, Date на процессорах AMD EPYC. [Игорь Лапко](https://github.com/yandex/ClickHouse/pull/3512)
* Исправлена деградация производительности при обработке длинных строк. [#3530](https://github.com/yandex/ClickHouse/pull/3530)

### Улучшения процесса сборки ClickHouse:
* Доработки для упрощения сборки в Arcadia. [#3475](https://github.com/yandex/ClickHouse/pull/3475), [#3535](https://github.com/yandex/ClickHouse/pull/3535)

## ClickHouse release 18.14.12, 2018-11-02

### Исправления ошибок:

* Исправлена ошибка при join-запросе двух неименованных подзапросов. [#3505](https://github.com/yandex/ClickHouse/pull/3505)
* Исправлена генерация пустой `WHERE`-части при запросах к внешним базам. [hotid](https://github.com/yandex/ClickHouse/pull/3477)
* Исправлена ошибка использования неправильной настройки таймаута в ODBC-словарях. [Marek Vavruša](https://github.com/yandex/ClickHouse/pull/3511)

## ClickHouse release 18.14.11, 2018-10-29

### Исправления ошибок:

* Исправлена ошибка `Block structure mismatch in UNION stream: different number of columns` в запросах с LIMIT. [#2156](https://github.com/yandex/ClickHouse/issues/2156)
* Исправлены ошибки при слиянии данных в таблицах, содержащих массивы внутри Nested структур. [#3397](https://github.com/yandex/ClickHouse/pull/3397)
* Исправлен неправильный результат запросов при выключенной настройке `merge_tree_uniform_read_distribution` (включена по умолчанию). [#3429](https://github.com/yandex/ClickHouse/pull/3429)
* Исправлена ошибка при вставке в Distributed таблицу в формате Native. [#3411](https://github.com/yandex/ClickHouse/issues/3411)

## ClickHouse release 18.14.10, 2018-10-23

* Настройка `compile_expressions` (JIT компиляция выражений) выключена по умолчанию. [#3410](https://github.com/yandex/ClickHouse/pull/3410)
* Настройка `enable_optimize_predicate_expression` выключена по умолчанию.

## ClickHouse release 18.14.9, 2018-10-16

### Новые возможности:

* Модификатор `WITH CUBE` для `GROUP BY` (также доступен синтаксис: `GROUP BY CUBE(...)`). [#3172](https://github.com/yandex/ClickHouse/pull/3172)
* Добавлена функция `formatDateTime`. [Alexandr Krasheninnikov](https://github.com/yandex/ClickHouse/pull/2770)
* Добавлен движок таблиц `JDBC` и табличная функция `jdbc` (для работы требуется установка clickhouse-jdbc-bridge). [Alexandr Krasheninnikov](https://github.com/yandex/ClickHouse/pull/3210)
* Добавлены функции для работы с ISO номером недели: `toISOWeek`, `toISOYear`, `toStartOfISOYear`, а также `toDayOfYear`. [#3146](https://github.com/yandex/ClickHouse/pull/3146)
* Добавлена возможность использования столбцов типа `Nullable` для таблиц типа `MySQL`, `ODBC`. [#3362](https://github.com/yandex/ClickHouse/pull/3362)
* Возможность чтения вложенных структур данных как вложенных объектов в формате `JSONEachRow`. Добавлена настройка `input_format_import_nested_json`. [Veloman Yunkan](https://github.com/yandex/ClickHouse/pull/3144)
* Возможность параллельной обработки многих `MATERIALIZED VIEW` при вставке данных. Настройка `parallel_view_processing`. [Marek Vavruša](https://github.com/yandex/ClickHouse/pull/3208)
* Добавлен запрос `SYSTEM FLUSH LOGS` (форсированный сброс логов в системные таблицы, такие как например, `query_log`) [#3321](https://github.com/yandex/ClickHouse/pull/3321)
* Возможность использования предопределённых макросов `database` и `table` в объявлении `Replicated` таблиц. [#3251](https://github.com/yandex/ClickHouse/pull/3251)
* Добавлена возможность чтения значения типа `Decimal` в инженерной нотации (с указанием десятичной экспоненты). [#3153](https://github.com/yandex/ClickHouse/pull/3153)

### Экспериментальные возможности:

* Оптимизация GROUP BY для типов данных `LowCardinality` [#3138](https://github.com/yandex/ClickHouse/pull/3138)
* Оптимизации вычисления выражений для типов данных `LowCardinality` [#3200](https://github.com/yandex/ClickHouse/pull/3200)

### Улучшения:

* Существенно уменьшено потребление памяти для запросов с `ORDER BY` и `LIMIT`. Настройка `max_bytes_before_remerge_sort`. [#3205](https://github.com/yandex/ClickHouse/pull/3205)
* При отсутствии указания типа `JOIN` (`LEFT`, `INNER`, ...), подразумевается `INNER JOIN`. [#3147](https://github.com/yandex/ClickHouse/pull/3147)
* Корректная работа квалифицированных звёздочек в запросах с `JOIN`. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/3202)
* Движок таблиц `ODBC` корректно выбирает способ квотирования идентификаторов в SQL диалекте удалённой СУБД. [Alexandr Krasheninnikov](https://github.com/yandex/ClickHouse/pull/3210)
* Настройка `compile_expressions` (JIT компиляция выражений) включена по-умолчанию.
* Исправлено поведение при одновременном DROP DATABASE/TABLE IF EXISTS и CREATE DATABASE/TABLE IF NOT EXISTS. Ранее запрос `CREATE DATABASE ... IF NOT EXISTS` мог выдавать сообщение об ошибке вида "File ... already exists", а запросы `CREATE TABLE ... IF NOT EXISTS` и `DROP TABLE IF EXISTS` могли выдавать сообщение `Table ... is creating or attaching right now`. [#3101](https://github.com/yandex/ClickHouse/pull/3101)
* Выражения LIKE и IN с константной правой частью пробрасываются на удалённый сервер при запросах из таблиц типа MySQL и ODBC. [#3182](https://github.com/yandex/ClickHouse/pull/3182)
* Сравнения с константными выражениями в секции WHERE пробрасываются на удалённый сервер при запросах из таблиц типа MySQL и ODBC. Ранее пробрасывались только сравнения с константами. [#3182](https://github.com/yandex/ClickHouse/pull/3182)
* Корректное вычисление ширины строк в терминале для `Pretty` форматов, в том числе для строк с иероглифами. [Amos Bird](https://github.com/yandex/ClickHouse/pull/3257).
* Возможность указания `ON CLUSTER` для запросов `ALTER UPDATE`.
* Увеличена производительность чтения данных в формате `JSONEachRow`. [#3332](https://github.com/yandex/ClickHouse/pull/3332)
* Добавлены синонимы функций `LENGTH`, `CHARACTER_LENGTH` для совместимости. Функция `CONCAT` стала регистронезависимой. [#3306](https://github.com/yandex/ClickHouse/pull/3306)
* Добавлен синоним `TIMESTAMP` для типа `DateTime`. [#3390](https://github.com/yandex/ClickHouse/pull/3390)
* В логах сервера всегда присутствует место для query_id, даже если строчка лога не относится к запросу. Это сделано для более простого парсинга текстовых логов сервера сторонними инструментами.
* Логгирование потребления памяти запросом при превышении очередной отметки целого числа гигабайт. [#3205](https://github.com/yandex/ClickHouse/pull/3205)
* Добавлен режим совместимости для случая, когда клиентская библиотека, работающая по Native протоколу, по ошибке отправляет меньшее количество столбцов, чем сервер ожидает для запроса INSERT. Такой сценарий был возможен при использовании библиотеки clickhouse-cpp. Ранее этот сценарий приводил к падению сервера. [#3171](https://github.com/yandex/ClickHouse/pull/3171)
* В `clickhouse-copier`, в задаваемом пользователем выражении WHERE, появилась возможность использовать алиас `partition_key` (для дополнительной фильтрации по партициям исходной таблицы). Это полезно, если схема партиционирования изменяется при копировании, но изменяется незначительно. [#3166](https://github.com/yandex/ClickHouse/pull/3166)
* Рабочий поток движка `Kafka` перенесён в фоновый пул потоков для того, чтобы автоматически уменьшать скорость чтения данных при большой нагрузке. [Marek Vavruša](https://github.com/yandex/ClickHouse/pull/3215).
* Поддержка чтения значений типа `Tuple` и `Nested` структур как `struct` в формате `Cap'n'Proto` [Marek Vavruša](https://github.com/yandex/ClickHouse/pull/3216).
* В список доменов верхнего уровня для функции `firstSignificantSubdomain` добавлен домен `biz` [decaseal](https://github.com/yandex/ClickHouse/pull/3219).
* В конфигурации внешних словарей, пустое значение `null_value` интерпретируется, как значение типа данных по-умоланию. [#3330](https://github.com/yandex/ClickHouse/pull/3330)
* Поддержка функций `intDiv`, `intDivOrZero` для `Decimal`. [b48402e8](https://github.com/yandex/ClickHouse/commit/b48402e8712e2b9b151e0eef8193811d433a1264)
* Поддержка типов `Date`, `DateTime`, `UUID`, `Decimal` в качестве ключа для агрегатной функции `sumMap`. [#3281](https://github.com/yandex/ClickHouse/pull/3281)
* Поддержка типа данных `Decimal` во внешних словарях. [#3324](https://github.com/yandex/ClickHouse/pull/3324)
* Поддержка типа данных `Decimal` в таблицах типа `SummingMergeTree`. [#3348](https://github.com/yandex/ClickHouse/pull/3348)
* Добавлена специализация для `UUID` в функции `if`. [#3366](https://github.com/yandex/ClickHouse/pull/3366)
* Уменьшено количество системных вызовов `open`, `close` при чтении из таблиц семейства `MergeTree` [#3283](https://github.com/yandex/ClickHouse/pull/3283).
* Возможность выполнения запроса `TRUNCATE TABLE` на любой реплике (запрос пробрасывается на реплику-лидера). [Kirill Shvakov](https://github.com/yandex/ClickHouse/pull/3375)

### Исправление ошибок:

* Исправлена ошибка в работе таблиц типа `Dictionary` для словарей типа `range_hashed`. Ошибка возникла в версии 18.12.17. [#1702](https://github.com/yandex/ClickHouse/pull/1702)
* Исправлена ошибка при загрузке словарей типа `range_hashed` (сообщение `Unsupported type Nullable(...)`). Ошибка возникла в версии 18.12.17. [#3362](https://github.com/yandex/ClickHouse/pull/3362)
* Исправлена некорректная работа функции `pointInPolygon` из-за накопления погрешности при вычислениях для полигонов с большим количеством близко расположенных вершин. [#3331](https://github.com/yandex/ClickHouse/pull/3331) [#3341](https://github.com/yandex/ClickHouse/pull/3341)
* Если после слияния кусков данных, у результирующего куска чексумма отличается от результата того же слияния на другой реплике, то результат слияния удаляется, и вместо этого кусок скачивается с другой реплики (это правильное поведение). Но после скачивания куска, он не мог добавиться в рабочий набор из-за ошибки, что кусок уже существует (так как кусок после слияния удалялся не сразу, а с задержкой). Это приводило к циклическим попыткам скачивания одних и тех же данных. [#3194](https://github.com/yandex/ClickHouse/pull/3194)
* Исправлен некорректный учёт общего потребления оперативной памяти запросами (что приводило к неправильной работе настройки `max_memory_usage_for_all_queries` и неправильному значению метрики `MemoryTracking`). Ошибка возникла в версии 18.12.13. [Marek Vavruša](https://github.com/yandex/ClickHouse/pull/3344)
* Исправлена работоспособность запросов `CREATE TABLE ... ON CLUSTER ... AS SELECT ...` Ошибка возникла в версии 18.12.13. [#3247](https://github.com/yandex/ClickHouse/pull/3247)
* Исправлена лишняя подготовка структуры данных для `JOIN` на сервере-инициаторе запроса, если `JOIN` выполняется только на удалённых серверах. [#3340](https://github.com/yandex/ClickHouse/pull/3340)
* Исправлены ошибки в движке `Kafka`: неработоспособность после исключения при начале чтения данных; блокировка при завершении [Marek Vavruša](https://github.com/yandex/ClickHouse/pull/3215).
* Для таблиц `Kafka` не передавался опциональный параметр `schema` (схема формата `Cap'n'Proto`). [Vojtech Splichal](https://github.com/yandex/ClickHouse/pull/3150)
* Если ансамбль серверов ZooKeeper содержит серверы, которые принимают соединение, но сразу же разрывают его вместо ответа на рукопожатие, то ClickHouse выбирает для соединения другой сервер. Ранее в этом случае возникала ошибка `Cannot read all data. Bytes read: 0. Bytes expected: 4.` и сервер не мог стартовать. [8218cf3a](https://github.com/yandex/ClickHouse/commit/8218cf3a5f39a43401953769d6d12a0bb8d29da9)
* Если ансамбль серверов ZooKeeper содержит серверы, для которых DNS запрос возвращает ошибку, то такие серверы пропускаются. [17b8e209](https://github.com/yandex/ClickHouse/commit/17b8e209221061325ad7ba0539f03c6e65f87f29)
* Исправлено преобразование типов между `Date` и `DateTime` при вставке данных в формате `VALUES` (в случае, когда `input_format_values_interpret_expressions = 1`). Ранее преобразование производилось между числовым значением количества дней с начала unix эпохи и unix timestamp, что приводило к неожиданным результатам. [#3229](https://github.com/yandex/ClickHouse/pull/3229)
* Исправление преобразования типов между `Decimal` и целыми числами. [#3211](https://github.com/yandex/ClickHouse/pull/3211)
* Исправлены ошибки в работе настройки `enable_optimize_predicate_expression`. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/3231)
* Исправлена ошибка парсинга формата CSV с числами с плавающей запятой, если используется разделитель CSV не по-умолчанию, такой как например, `;` [#3155](https://github.com/yandex/ClickHouse/pull/3155).
* Исправлена функция `arrayCumSumNonNegative` (она не накапливает отрицательные значения, если аккумулятор становится меньше нуля). [Aleksey Studnev](https://github.com/yandex/ClickHouse/pull/3163)
* Исправлена работа `Merge` таблицы поверх `Distributed` таблиц при использовании `PREWHERE`. [#3165](https://github.com/yandex/ClickHouse/pull/3165)
* Исправления ошибок в запросе `ALTER UPDATE`.
* Исправления ошибок в табличной функции `odbc`, которые возникли в версии 18.12. [#3197](https://github.com/yandex/ClickHouse/pull/3197)
* Исправлена работа агрегатных функций с комбинаторами `StateArray`. [#3188](https://github.com/yandex/ClickHouse/pull/3188)
* Исправлено падение при делении значения типа `Decimal` на ноль. [69dd6609](https://github.com/yandex/ClickHouse/commit/69dd6609193beb4e7acd3e6ad216eca0ccfb8179)
* Исправлен вывод типов для операций с использованием аргументов типа `Decimal` и целых чисел. [#3224](https://github.com/yandex/ClickHouse/pull/3224)
* Исправлен segfault при `GROUP BY` по `Decimal128`. [3359ba06](https://github.com/yandex/ClickHouse/commit/3359ba06c39fcd05bfdb87d6c64154819621e13a)
* Настройка `log_query_threads` (логгирование информации о каждом потоке исполнения запроса) теперь имеет эффект только если настройка `log_queries` (логгирование информации о запросах) выставлена в 1. Так как настройка `log_query_threads` включена по-умолчанию, ранее информация о потоках логгировалась даже если логгирование запросов выключено. [#3241](https://github.com/yandex/ClickHouse/pull/3241)
* Исправлена ошибка в распределённой работе агрегатной функции quantiles (сообщение об ошибке вида `Not found column quantile...`). [292a8855](https://github.com/yandex/ClickHouse/commit/292a885533b8e3b41ce8993867069d14cbd5a664)
* Исправлена проблема совместимости при одновременной работе на кластере серверов версии 18.12.17 и более старых, приводящая к тому, что при распределённых запросах с GROUP BY по ключам одновременно фиксированной и не фиксированной длины, при условии, что количество данных в процессе агрегации большое, могли возвращаться не до конца агрегированные данные (одни и те же ключи агрегации в двух разных строках). [#3254](https://github.com/yandex/ClickHouse/pull/3254)
* Исправлена обработка подстановок в `clickhouse-performance-test`, если запрос содержит только часть из объявленных в тесте подстановок. [#3263](https://github.com/yandex/ClickHouse/pull/3263)
* Исправлена ошибка при использовании `FINAL` совместно с `PREWHERE`. [#3298](https://github.com/yandex/ClickHouse/pull/3298)
* Исправлена ошибка при использовании `PREWHERE` над столбцами, добавленными при `ALTER`. [#3298](https://github.com/yandex/ClickHouse/pull/3298)
* Добавлена проверка отсутствия `arrayJoin` для `DEFAULT`, `MATERIALIZED` выражений. Ранее наличие `arrayJoin` приводило к ошибке при вставке данных. [#3337](https://github.com/yandex/ClickHouse/pull/3337)
* Добавлена проверка отсутствия `arrayJoin` в секции `PREWHERE`. Ранее это приводило к сообщениям вида `Size ... doesn't match` или `Unknown compression method` при выполнении запросов. [#3357](https://github.com/yandex/ClickHouse/pull/3357)
* Исправлен segfault, который мог возникать в редких случаях после оптимизации - замены цепочек AND из равенства выражения константам на соответствующее выражение IN. [liuyimin-bytedance](https://github.com/yandex/ClickHouse/pull/3339).
* Мелкие исправления `clickhouse-benchmark`: ранее информация о клиенте не передавалась на сервер; более корректный подсчёт числа выполненных запросов при завершении работы и для ограничения числа итераций. [#3351](https://github.com/yandex/ClickHouse/pull/3351) [#3352](https://github.com/yandex/ClickHouse/pull/3352)

### Обратно несовместимые изменения:

* Удалена настройка `allow_experimental_decimal_type`. Тип данных `Decimal` доступен для использования по-умолчанию. [#3329](https://github.com/yandex/ClickHouse/pull/3329)


## ClickHouse release 18.12.17, 2018-09-16

### Новые возможности:

* `invalidate_query` (возможность задать запрос для проверки необходимости обновления внешнего словаря) реализована для источника `clickhouse`. [#3126](https://github.com/yandex/ClickHouse/pull/3126)
* Добавлена возможность использования типов данных `UInt*`, `Int*`, `DateTime` (наравне с типом `Date`) в качестве ключа внешнего словаря типа `range_hashed`, определяющего границы диапазонов. Возможность использования `NULL` в качестве обозначения открытого диапазона. [Vasily Nemkov](https://github.com/yandex/ClickHouse/pull/3123)
* Для типа `Decimal` добавлена поддержка агрегатных функций `var*`, `stddev*`. [#3129](https://github.com/yandex/ClickHouse/pull/3129)
* Для типа `Decimal` добавлена поддержка математических функций (`exp`, `sin` и т. п.) [#3129](https://github.com/yandex/ClickHouse/pull/3129)
* В таблицу `system.part_log` добавлен столбец `partition_id`. [#3089](https://github.com/yandex/ClickHouse/pull/3089)

### Исправление ошибок:

* Исправлена работа `Merge` таблицы поверх `Distributed` таблиц. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/3159)
* Исправлена несовместимость (лишняя зависимость от версии `glibc`), приводящая к невозможности запуска ClickHouse на `Ubuntu Precise` и более старых. Несовместимость возникла в версии 18.12.13. [#3130](https://github.com/yandex/ClickHouse/pull/3130)
* Исправлены ошибки в работе настройки `enable_optimize_predicate_expression`. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/3107)
* Исправлено незначительное нарушение обратной совместимости, проявляющееся при одновременной работе на кластере реплик версий до 18.12.13 и создании новой реплики таблицы на сервере более новой версии (выдаётся сообщение `Can not clone replica, because the ... updated to new ClickHouse version`, что полностью логично, но не должно было происходить). [#3122](https://github.com/yandex/ClickHouse/pull/3122)

### Обратно несовместимые изменения:

* Настройка `enable_optimize_predicate_expression` включена по-умолчанию, что конечно очень оптимистично. При возникновении ошибок анализа запроса, связанных с поиском имён столбцов, следует выставить `enable_optimize_predicate_expression` в 0. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/3107)


## ClickHouse release 18.12.14, 2018-09-13

### Новые возможности:

* Добавлена поддержка запросов `ALTER UPDATE`. [#3035](https://github.com/yandex/ClickHouse/pull/3035)
* Добавлена настройка `allow_ddl`, упраляющая доступом пользователя к DDL-запросам. [#3104](https://github.com/yandex/ClickHouse/pull/3104)
* Добавлена настройка `min_merge_bytes_to_use_direct_io` для движков семейства `MergeTree`, позволяющая задать порог на суммарный размер слияния после которого работа с файлами кусков будет происходить с O_DIRECT. [#3117](https://github.com/yandex/ClickHouse/pull/3117)
* В системную таблицу `system.merges` добавлен столбец `partition_id`. [#3099](https://github.com/yandex/ClickHouse/pull/3099)

### Улучшения

* Если в процессе мутации кусок остался неизменённым, он не будет скачан репликами. [#3103](https://github.com/yandex/ClickHouse/pull/3103)
* При работе с `clickhouse-client` добавлено автодополнение для имён настроек. [#3106](https://github.com/yandex/ClickHouse/pull/3106)

### Исправление ошибок

* Добавлена проверка размеров массивов, которые являются элементами полей типа `Nested`, при вставке. [#3118](https://github.com/yandex/ClickHouse/pull/3118)
* Исправлена ошибка обновления внешних словарей с источником `ODBC` и форматом хранения `hashed`. Ошибка возникла в версии 18.12.13.
* Исправлено падение при создании временной таблицы таблицы из запроса с условием `IN`. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/3098)
* Исправлена ошибка в работе агрегатных функций для массивов, элементами которых может быть `NULL`. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/3097)


## ClickHouse release 18.12.13, 2018-09-10

### Новые возможности:

* Добавлен тип данных `DECIMAL(digits, scale)` (`Decimal32(scale)`, `Decimal64(scale)`, `Decimal128(scale)`). Возможность доступна под настройкой `allow_experimental_decimal_type`. [#2846](https://github.com/yandex/ClickHouse/pull/2846) [#2970](https://github.com/yandex/ClickHouse/pull/2970) [#3008](https://github.com/yandex/ClickHouse/pull/3008) [#3047](https://github.com/yandex/ClickHouse/pull/3047)
* Модификатор `WITH ROLLUP` для `GROUP BY` (также доступен синтаксис: `GROUP BY ROLLUP(...)`). [#2948](https://github.com/yandex/ClickHouse/pull/2948)
* В запросах с JOIN, звёздочка раскрывается в список столбцов всех таблиц, в соответствии со стандартом SQL. Вернуть старое поведение можно, выставив настройку (уровня пользователя) `asterisk_left_columns_only` в значение 1. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2787)
* Добавлена поддержка JOIN с табличной функцией. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2907)
* Автодополнение по нажатию Tab в clickhouse-client. [Sergey Shcherbin](https://github.com/yandex/ClickHouse/pull/2447)
* Нажатие Ctrl+C в clickhouse-client очищает запрос, если он был введён. [#2877](https://github.com/yandex/ClickHouse/pull/2877)
* Добавлена настройка `join_default_strictness` (значения `''`, `'any'`, `'all'`). Её использование позволяет не указывать `ANY` или `ALL` для `JOIN`. [#2982](https://github.com/yandex/ClickHouse/pull/2982)
* В каждой строчке лога сервера, относящейся к обработке запроса, выводится идентификатор запроса. [#2482](https://github.com/yandex/ClickHouse/pull/2482)
* Возможность получения логов выполнения запроса в clickhouse-client (настройка `send_logs_level`). При распределённой обработке запроса, логи отправляются каскадно со всех серверов. [#2482](https://github.com/yandex/ClickHouse/pull/2482)
* В таблицах `system.query_log` и `system.processes` (`SHOW PROCESSLIST`) появилась информация о всех изменённых настройках при выполнении запроса (вложенная структура данных `Settings`). Добавлена настройка `log_query_settings`. [#2482](https://github.com/yandex/ClickHouse/pull/2482)
* В таблицах `system.query_log` и `system.processes` появилась информация о номерах потоков, участвующих в исполнении запроса (столбец `thread_numbers`). [#2482](https://github.com/yandex/ClickHouse/pull/2482)
* Добавлены счётчики `ProfileEvents`, измеряющие время, потраченное на чтение и запись по сети; чтение и запись на диск; количество сетевых ошибок; время потраченное на ожидании при ограничении сетевой полосы. [#2482](https://github.com/yandex/ClickHouse/pull/2482)
* Добавлены счётчики `ProfileEvents`, содержащие системные метрики из rusage (позволяющие получить информацию об использовании CPU в userspace и ядре, page faults, context switches) а также метрики taskstats (позволяющие получить информацию о времени ожидания IO, CPU, а также количество прочитанных и записанных данных с учётом и без учёта page cache). [#2482](https://github.com/yandex/ClickHouse/pull/2482)
* Счётчики `ProfileEvents` учитываются не только глобально, но и на каждый запрос, а также на каждый поток выполнения запроса, что позволяет детально профилировать потребление ресурсов отдельными запросами. [#2482](https://github.com/yandex/ClickHouse/pull/2482)
* Добавлена таблица `system.query_thread_log`, содержащая информацию о каждом потоке выполнения запроса. Добавлена настройка `log_query_threads`. [#2482](https://github.com/yandex/ClickHouse/pull/2482)
* В таблицах `system.metrics` и `system.events` появилась встроенная документация. [#3016](https://github.com/yandex/ClickHouse/pull/3016)
* Добавлена функция `arrayEnumerateDense`. [Amos Bird](https://github.com/yandex/ClickHouse/pull/2975)
* Добавлены функции `arrayCumSumNonNegative` и `arrayDifference`. [Aleksey Studnev](https://github.com/yandex/ClickHouse/pull/2942)
* Добавлена агрегатная функция `retention`. [Sundy Li](https://github.com/yandex/ClickHouse/pull/2887)
* Возможность сложения (слияния) состояний агрегатных функций с помощью оператора плюс, а также умножения состояний агрегатных функций на целую неотрицательную константу. [#3062](https://github.com/yandex/ClickHouse/pull/3062) [#3034](https://github.com/yandex/ClickHouse/pull/3034)
* В таблицах семейства MergeTree добавлен виртуальный столбец `_partition_id`. [#3089](https://github.com/yandex/ClickHouse/pull/3089)

### Экспериментальные возможности:

* Добавлен тип данных `LowCardinality(T)`. Тип данных автоматически создаёт локальный словарь значений и позволяет обрабатывать данные без распаковки словаря. [#2830](https://github.com/yandex/ClickHouse/pull/2830)
* Добавлен кэш JIT-скомпилированных функций, а также счётчик числа использований перед компиляцией. Возможность JIT-компиляции выражений включается настройкой `compile_expressions`. [#2990](https://github.com/yandex/ClickHouse/pull/2990) [#3077](https://github.com/yandex/ClickHouse/pull/3077)

### Улучшения:

* Исправлена проблема неограниченного накопления лога репликации в случае наличия заброшенных реплик. Добавлен режим эффективного восстановления реплик после длительного отставания.
* Увеличена производительность при выполнении `GROUP BY` в случае, если есть несколько полей агрегации, одно из которых строковое, а другие - фиксированной длины.
* Увеличена производительность при использовании `PREWHERE` и при неявном переносе выражений в `PREWHERE`.
* Увеличена производительность парсинга текстовых форматов (`CSV`, `TSV`). [Amos Bird](https://github.com/yandex/ClickHouse/pull/2977) [#2980](https://github.com/yandex/ClickHouse/pull/2980)
* Увеличена производительность чтения строк и массивов в бинарных форматах. [Amos Bird](https://github.com/yandex/ClickHouse/pull/2955)
* Увеличена производительность и уменьшено потребление памяти в запросах к таблицам `system.tables` и `system.columns` в случае наличия очень большого количества таблиц на одном сервере. [#2953](https://github.com/yandex/ClickHouse/pull/2953)
* Исправлена проблема низкой производительности в случае наличия большого потока запросов, для которых возвращается ошибка (в `perf top` видна функция `_dl_addr`, при этом сервер использует мало CPU). [#2938](https://github.com/yandex/ClickHouse/pull/2938)
* Прокидывание условий внутрь View (при включенной настройке `enable_optimize_predicate_expression`) [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2907)
* Доработки недостающей функциональности для типа данных `UUID`. [#3074](https://github.com/yandex/ClickHouse/pull/3074) [#2985](https://github.com/yandex/ClickHouse/pull/2985)
* Тип данных `UUID` поддержан в словарях The-Alchemist. [#2822](https://github.com/yandex/ClickHouse/pull/2822)
* Функция `visitParamExtractRaw` корректно работает с вложенными структурами. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2974)
* При использовании настройки `input_format_skip_unknown_fields` корректно работает пропуск значений-объектов в формате `JSONEachRow`. [BlahGeek](https://github.com/yandex/ClickHouse/pull/2958)
* Для выражения `CASE` с условиями, появилась возможность не указывать `ELSE`, что эквивалентно `ELSE NULL`. [#2920](https://github.com/yandex/ClickHouse/pull/2920)
* Возможность конфигурирования operation timeout при работе с ZooKeeper. [urykhy](https://github.com/yandex/ClickHouse/pull/2971)
* Возможность указания смещения для `LIMIT n, m` в виде `LIMIT n OFFSET m`. [#2840](https://github.com/yandex/ClickHouse/pull/2840)
* Возможность использования синтаксиса `SELECT TOP n` в качестве альтернативы для `LIMIT`. [#2840](https://github.com/yandex/ClickHouse/pull/2840)
* Увеличен размер очереди записи в системные таблицы, что позволяет уменьшить количество ситуаций `SystemLog queue is full`.
* В агрегатной функции `windowFunnel` добавлена поддержка событий, подходящих под несколько условий. [Amos Bird](https://github.com/yandex/ClickHouse/pull/2801)
* Возможность использования дублирующихся столбцов в секции `USING` для `JOIN`. [#3006](https://github.com/yandex/ClickHouse/pull/3006)
* Для форматов `Pretty` введено ограничение выравнивания столбцов по ширине. Настройка `output_format_pretty_max_column_pad_width`. В случае более широкого значения, оно всё ещё будет выведено целиком, но остальные ячейки таблицы не будут излишне широкими. [#3003](https://github.com/yandex/ClickHouse/pull/3003)
* В табличной функции `odbc` добавлена возможность указания имени базы данных/схемы. [Amos Bird](https://github.com/yandex/ClickHouse/pull/2885)
* Добавлена возможность использования имени пользователя, заданного в конфигурационном файле `clickhouse-client`. [Vladimir Kozbin](https://github.com/yandex/ClickHouse/pull/2909)
* Счётчик `ZooKeeperExceptions` разделён на три счётчика `ZooKeeperUserExceptions`, `ZooKeeperHardwareExceptions`, `ZooKeeperOtherExceptions`.
* Запросы `ALTER DELETE` работают для материализованных представлений.
* Добавлена рандомизация во времени периодического запуска cleanup thread для таблиц типа `ReplicatedMergeTree`, чтобы избежать периодических всплесков нагрузки в случае очень большого количества таблиц типа `ReplicatedMergeTree`.
* Поддержка запроса `ATTACH TABLE ... ON CLUSTER`. [#3025](https://github.com/yandex/ClickHouse/pull/3025)

### Исправление ошибок:

* Исправлена ошибка в работе таблиц типа `Dictionary` (кидается исключение `Size of offsets doesn't match size of column` или `Unknown compression method`). Ошибка появилась в версии 18.10.3. [#2913](https://github.com/yandex/ClickHouse/issues/2913)
* Исправлена ошибка при мерже данных таблиц типа `CollapsingMergeTree`, если один из кусков данных пустой (такие куски, в свою очередь, образуются при слиянии или при `ALTER DELETE` в случае удаления всех данных), и для слияния был выбран алгоритм `vertical`. [#3049](https://github.com/yandex/ClickHouse/pull/3049)
* Исправлен race condition при `DROP` или `TRUNCATE` таблиц типа `Memory` при одновременном `SELECT`, который мог приводить к падениям сервера. Ошибка появилась в версии 1.1.54388. [#3038](https://github.com/yandex/ClickHouse/pull/3038)
* Исправлена возможность потери данных при вставке в `Replicated` таблицы в случае получения ошибки `Session expired` (потеря данных может быть обнаружена по метрике `ReplicatedDataLoss`). Ошибка возникла в версии 1.1.54378. [#2939](https://github.com/yandex/ClickHouse/pull/2939) [#2949](https://github.com/yandex/ClickHouse/pull/2949) [#2964](https://github.com/yandex/ClickHouse/pull/2964)
* Исправлен segfault при `JOIN ... ON`. [#3000](https://github.com/yandex/ClickHouse/pull/3000)
* Исправлена ошибка поиска имён столбцов в случае, если выражение `WHERE` состоит целиком из квалифицированного имени столбца, как например `WHERE table.column`. [#2994](https://github.com/yandex/ClickHouse/pull/2994)
* Исправлена ошибка вида "Not found column" при выполнении распределённых запросов в случае, если с удалённого сервера запрашивается единственный столбец, представляющий собой выражение IN с подзапросом. [#3087](https://github.com/yandex/ClickHouse/pull/3087)
* Исправлена ошибка `Block structure mismatch in UNION stream: different number of columns`, возникающая при распределённых запросах, если один из шардов локальный, а другой - нет, и если при этом срабатывает оптимизация переноса в `PREWHERE`. [#2226](https://github.com/yandex/ClickHouse/pull/2226) [#3037](https://github.com/yandex/ClickHouse/pull/3037) [#3055](https://github.com/yandex/ClickHouse/pull/3055) [#3065](https://github.com/yandex/ClickHouse/pull/3065) [#3073](https://github.com/yandex/ClickHouse/pull/3073) [#3090](https://github.com/yandex/ClickHouse/pull/3090) [#3093](https://github.com/yandex/ClickHouse/pull/3093)
* Исправлена работа функции `pointInPolygon` для некоторого случая невыпуклых полигонов. [#2910](https://github.com/yandex/ClickHouse/pull/2910)
* Исправлен некорректный результат при сравнении `nan` с целыми числами. [#3024](https://github.com/yandex/ClickHouse/pull/3024)
* Исправлена ошибка в библиотеке `zlib-ng`, которая могла приводить к segfault в редких случаях. [#2854](https://github.com/yandex/ClickHouse/pull/2854)
* Исправлена утечка памяти при вставке в таблицу со столбцами типа `AggregateFunction`, если состояние агрегатной функции нетривиальное (выделяет память отдельно), и если в одном запросе на вставку получается несколько маленьких блоков. [#3084](https://github.com/yandex/ClickHouse/pull/3084)
* Исправлен race condition при одновременном создании и удалении одной и той же таблицы типа `Buffer` или `MergeTree`.
* Исправлена возможность segfault при сравнении кортежей из некоторых нетривиальных типов, таких как, например, кортежей. [#2989](https://github.com/yandex/ClickHouse/pull/2989)
* Исправлена возможность segfault при выполнении некоторых запросов `ON CLUSTER`. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2960)
* Исправлена ошибка в функции `arrayDistinct` в случае `Nullable` элементов массивов. [#2845](https://github.com/yandex/ClickHouse/pull/2845) [#2937](https://github.com/yandex/ClickHouse/pull/2937)
* Возможность `enable_optimize_predicate_expression` корректно поддерживает случаи с `SELECT *`. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2929)
* Исправлена возможность segfault при переинициализации сессии с ZooKeeper. [#2917](https://github.com/yandex/ClickHouse/pull/2917)
* Исправлена возможность блокировки при взаимодействии с ZooKeeper.
* Исправлен некорректный код суммирования вложенных структур данных в `SummingMergeTree`.
* При выделении памяти для состояний агрегатных функций, корректно учитывается выравнивание, что позволяет использовать при реализации состояний агрегатных функций операции, для которых выравнивание является необходимым. [chenxing-xc](https://github.com/yandex/ClickHouse/pull/2808)

### Исправления безопасности:

* Безопасная работа с ODBC источниками данных. Взаимодействие с ODBC драйверами выполняется через отдельный процесс `clickhouse-odbc-bridge`. Ошибки в сторонних ODBC драйверах теперь не приводят к проблемам со стабильностью сервера или уязвимостям. [#2828](https://github.com/yandex/ClickHouse/pull/2828) [#2879](https://github.com/yandex/ClickHouse/pull/2879) [#2886](https://github.com/yandex/ClickHouse/pull/2886) [#2893](https://github.com/yandex/ClickHouse/pull/2893) [#2921](https://github.com/yandex/ClickHouse/pull/2921)
* Исправлена некорректная валидация пути к файлу в табличной функции `catBoostPool`. [#2894](https://github.com/yandex/ClickHouse/pull/2894)
* Содержимое системных таблиц (`tables`, `databases`, `parts`, `columns`, `parts_columns`, `merges`, `mutations`, `replicas`, `replication_queue`) фильтруется согласно конфигурации доступа к базам данных для пользователя (`allow_databases`) [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2856)

### Обратно несовместимые изменения:

* В запросах с JOIN, звёздочка раскрывается в список столбцов всех таблиц, в соответствии со стандартом SQL. Вернуть старое поведение можно, выставив настройку (уровня пользователя) `asterisk_left_columns_only` в значение 1.

### Изменения сборки:

* Добавлен покоммитный запуск большинства интеграционных тестов.
* Добавлен покоммитный запуск проверки стиля кода.
* Корректный выбор реализации `memcpy` при сборке на CentOS7 / Fedora. [Etienne Champetier](https://github.com/yandex/ClickHouse/pull/2912)
* При сборке с помощью clang добавлены некоторые warnings из `-Weverything` в дополнение к обычным `-Wall -Wextra -Werror`. [#2957](https://github.com/yandex/ClickHouse/pull/2957)
* При debug сборке используется debug вариант `jemalloc`.
* Абстрагирован интерфейс библиотеки для взаимодействия с ZooKeeper. [#2950](https://github.com/yandex/ClickHouse/pull/2950)


## ClickHouse release 18.10.3, 2018-08-13

### Новые возможности:
* Возможность использования HTTPS для репликации. [#2760](https://github.com/yandex/ClickHouse/pull/2760)
* Добавлены функции `murmurHash2_64`, `murmurHash3_32`, `murmurHash3_64`, `murmurHash3_128` в дополнение к имеющемуся `murmurHash2_32`. [#2791](https://github.com/yandex/ClickHouse/pull/2791)
* Поддержка Nullable типов в ODBC драйвере ClickHouse (формат вывода `ODBCDriver2`) [#2834](https://github.com/yandex/ClickHouse/pull/2834)
* Поддержка `UUID` в ключевых столбцах.

### Улучшения:
* Удаление кластеров без перезагрузки сервера при их удалении из конфигурационных файлов. [#2777](https://github.com/yandex/ClickHouse/pull/2777)
* Удаление внешних словарей без перезагрузки сервера при их удалении из конфигурационных файлов. [#2779](https://github.com/yandex/ClickHouse/pull/2779)
* Добавлена поддержка `SETTINGS` для движка таблиц `Kafka`. [Alexander Marshalov](https://github.com/yandex/ClickHouse/pull/2781)
* Доработки для типа данных `UUID` (не полностью) Šimon Podlipský. [#2618](https://github.com/yandex/ClickHouse/pull/2618)
* Поддежка пустых кусков после мержей в движках `SummingMergeTree`, `CollapsingMergeTree` and `VersionedCollapsingMergeTree`. [#2815](https://github.com/yandex/ClickHouse/pull/2815)
* Удаление старых записей о полностью выполнившихся мутациях (`ALTER DELETE`) [#2784](https://github.com/yandex/ClickHouse/pull/2784)
* Добавлена таблица `system.merge_tree_settings`. [Kirill Shvakov](https://github.com/yandex/ClickHouse/pull/2841)
* В таблицу `system.tables` добавлены столбцы зависимостей: `dependencies_database` и `dependencies_table`. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2851)
* Добавлена опция конфига `max_partition_size_to_drop`. [#2782](https://github.com/yandex/ClickHouse/pull/2782)
* Добавлена настройка `output_format_json_escape_forward_slashes`. [Alexander Bocharov](https://github.com/yandex/ClickHouse/pull/2812)
* Добавлена настройка `max_fetch_partition_retries_count`. [#2831](https://github.com/yandex/ClickHouse/pull/2831)
* Добавлена настройка `prefer_localhost_replica`, позволяющая отключить предпочтение локальной реплики и хождение на локальную реплику без межпроцессного взаимодействия. [#2832](https://github.com/yandex/ClickHouse/pull/2832)
* Агрегатная функция `quantileExact` возвращает `nan` в случае агрегации по пустому множеству `Float32`/`Float64` типов. [Sundy Li](https://github.com/yandex/ClickHouse/pull/2855)

### Исправление ошибок:
* Убрано излишнее экранирование параметров connection string для ODBC, котрое приводило к невозможности соединения. Ошибка возникла в версии 18.6.0.
* Исправлена логика обработки команд на `REPLACE PARTITION` в очереди репликации. Неправильная логика могла приводить к тому, что при наличии двух `REPLACE` одной и той же партиции, один из них оставался в очереди репликации и не мог выполниться. [#2814](https://github.com/yandex/ClickHouse/pull/2814)
* Исправлена ошибка при мерже, если все куски были пустыми (такие куски, в свою очередь, образуются при слиянии или при `ALTER DELETE` в случае удаления всех данных). Ошибка появилась в версии 18.1.0. [#2930](https://github.com/yandex/ClickHouse/pull/2930)
* Исправлена ошибка при параллельной записи в таблицы типа `Set` или `Join`. [Amos Bird](https://github.com/yandex/ClickHouse/pull/2823)
* Исправлена ошибка `Block structure mismatch in UNION stream: different number of columns`, возникающая при запросах с `UNION ALL` внутри подзапроса, в случае, если один из `SELECT` запросов содержит дублирующиеся имена столбцов. [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2094)
* Исправлена утечка памяти в случае исключения при соединении с MySQL сервером.
* Исправлен некорректный код возврата clickhouse-client в случае ошибочного запроса
* Исправлен некорректная работа materialized views, содержащих DISTINCT. [#2795](https://github.com/yandex/ClickHouse/issues/2795)

### Обратно несовместимые изменения
* Убрана поддержка запросов CHECK TABLE для Distributed таблиц.

### Изменения сборки:
* Заменен аллокатор, теперь используется `jemalloc` вместо `tcmalloc`. На некоторых сценариях ускорение достигает 20%. В то же время, существуют запросы, замедлившиеся до 20%. Потребление памяти на некоторых сценариях примерно на 10% меньше и более стабильно. При высококонкурентной нагрузке, потребление CPU в userspace и в system незначительно вырастает. [#2773](https://github.com/yandex/ClickHouse/pull/2773)
* Использование libressl из submodule. [#1983](https://github.com/yandex/ClickHouse/pull/1983) [#2807](https://github.com/yandex/ClickHouse/pull/2807)
* Использование unixodbc из submodule. [#2789](https://github.com/yandex/ClickHouse/pull/2789)
* Использование mariadb-connector-c из submodule. [#2785](https://github.com/yandex/ClickHouse/pull/2785)
* В репозиторий добавлены файлы функциональных тестов, рассчитывающих на наличие тестовых данных (пока без самих тестовых данных).


## ClickHouse release 18.6.0, 2018-08-02

### Новые возможности:
* Добавлена поддержка ON выражений для JOIN ON синтаксиса:
`JOIN ON Expr([table.]column, ...) = Expr([table.]column, ...) [AND Expr([table.]column, ...) = Expr([table.]column, ...) ...]`
Выражение должно представлять из себя цепочку равенств, объединенных оператором AND. Каждая часть равенства может являться произвольным выражением над столбцами одной из таблиц. Поддержана возможность использования fully qualified имен столбцов (`table.name`, `database.table.name`, `table_alias.name`, `subquery_alias.name`) для правой таблицы. [#2742](https://github.com/yandex/ClickHouse/pull/2742)
* Добавлена возможность включить HTTPS для репликации. [#2760](https://github.com/yandex/ClickHouse/pull/2760)

### Улучшения:
* Сервер передаёт на клиент также patch-компонент своей версии. Данные о patch компоненте версии добавлены в `system.processes` и `query_log`. [#2646](https://github.com/yandex/ClickHouse/pull/2646)


## ClickHouse release 18.5.1, 2018-07-31

### Новые возможности:
* Добавлена функция хеширования `murmurHash2_32`. [#2756](https://github.com/yandex/ClickHouse/pull/2756).

### Улучшения:
* Добавлена возможность указывать значения в конфигурационных файлах из переменных окружения с помощью атрибута `from_env`. [#2741](https://github.com/yandex/ClickHouse/pull/2741).
* Добавлены регистронезависимые версии функций `coalesce`, `ifNull`, `nullIf`. [#2752](https://github.com/yandex/ClickHouse/pull/2752).

### Исправление ошибок:
* Исправлена возможная ошибка при старте реплики. [#2759](https://github.com/yandex/ClickHouse/pull/2759).


## ClickHouse release 18.4.0, 2018-07-28

### Новые возможности:
* Добавлены системные таблицы `formats`, `data_type_families`, `aggregate_function_combinators`, `table_functions`, `table_engines`, `collations` [#2721](https://github.com/yandex/ClickHouse/pull/2721).
* Добавлена возможность использования табличной функции вместо таблицы в качестве аргумента табличной функции `remote` и `cluster` [#2708](https://github.com/yandex/ClickHouse/pull/2708).
* Поддержка `HTTP Basic` аутентификации в протоколе репликации [#2727](https://github.com/yandex/ClickHouse/pull/2727).
* В функции `has` добавлена возможность поиска в массиве значений типа `Enum` по числовому значению [Maxim Khrisanfov](https://github.com/yandex/ClickHouse/pull/2699).
* Поддержка добавления произвольных разделителей сообщений в процессе чтения из `Kafka` [Amos Bird](https://github.com/yandex/ClickHouse/pull/2701).

### Улучшения:
* Запрос `ALTER TABLE t DELETE WHERE` не перезаписывает куски данных, которые не были затронуты условием WHERE [#2694](https://github.com/yandex/ClickHouse/pull/2694).
* Настройка `use_minimalistic_checksums_in_zookeeper` таблиц семейства `ReplicatedMergeTree` включена по-умолчанию. Эта настройка была добавлена в версии 1.1.54378, 2018-04-16. Установка версий, более старых, чем 1.1.54378, становится невозможной.
* Поддерживается запуск запросов `KILL` и `OPTIMIZE` с указанием `ON CLUSTER` [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2689).

### Исправление ошибок:
* Исправлена ошибка `Column ... is not under aggregate function and not in GROUP BY` в случае агрегации по выражению с оператором IN. Ошибка появилась в версии 18.1.0. ([bbdd780b](https://github.com/yandex/ClickHouse/commit/bbdd780be0be06a0f336775941cdd536878dd2c2))
* Исправлена ошибка в агрегатной функции `windowFunnel` [Winter Zhang](https://github.com/yandex/ClickHouse/pull/2735).
* Исправлена ошибка в агрегатной функции `anyHeavy` ([a2101df2](https://github.com/yandex/ClickHouse/commit/a2101df25a6a0fba99aa71f8793d762af2b801ee))
* Исправлено падение сервера при использовании функции `countArray()`.

### Обратно несовместимые изменения:

* Список параметров для таблиц `Kafka` был изменён с `Kafka(kafka_broker_list, kafka_topic_list, kafka_group_name, kafka_format[, kafka_schema, kafka_num_consumers])` на `Kafka(kafka_broker_list, kafka_topic_list, kafka_group_name, kafka_format[, kafka_row_delimiter, kafka_schema, kafka_num_consumers])`. Если вы использовали параметры `kafka_schema` или `kafka_num_consumers`, вам необходимо вручную отредактировать файлы с метаданными `path/metadata/database/table.sql`, добавив параметр `kafka_row_delimiter` со значением `''` в соответствующее место.


## ClickHouse release 18.1.0, 2018-07-23

### Новые возможности:
* Поддержка запроса `ALTER TABLE t DELETE WHERE` для нереплицированных MergeTree-таблиц ([#2634](https://github.com/yandex/ClickHouse/pull/2634)).
* Поддержка произвольных типов для семейства агрегатных функций `uniq*` ([#2010](https://github.com/yandex/ClickHouse/issues/2010)).
* Поддержка произвольных типов в операторах сравнения ([#2026](https://github.com/yandex/ClickHouse/issues/2026)).
* Возможность в `users.xml` указывать маску подсети в формате `10.0.0.1/255.255.255.0`. Это необходимо для использования "дырявых" масок IPv6 сетей ([#2637](https://github.com/yandex/ClickHouse/pull/2637)).
* Добавлена функция `arrayDistinct` ([#2670](https://github.com/yandex/ClickHouse/pull/2670)).
* Движок SummingMergeTree теперь может работать со столбцами типа AggregateFunction ([Constantin S. Pan](https://github.com/yandex/ClickHouse/pull/2566)).

### Улучшения:
* Изменена схема версионирования релизов. Теперь первый компонент содержит год релиза (A.D.; по московскому времени; из номера вычитается 2000), второй - номер крупных изменений (увеличивается для большинства релизов), третий - патч-версия. Релизы по-прежнему обратно совместимы, если другое не указано в changelog.
* Ускорено преобразование чисел с плавающей точкой в строку ([Amos Bird](https://github.com/yandex/ClickHouse/pull/2664)).
* Теперь, если при вставке из-за ошибок парсинга пропущено некоторое количество строк (такое возможно про включённых настройках `input_allow_errors_num`, `input_allow_errors_ratio`), это количество пишется в лог сервера ([Leonardo Cecchi](https://github.com/yandex/ClickHouse/pull/2669)).

### Исправление ошибок:
* Исправлена работа команды TRUNCATE для временных таблиц ([Amos Bird](https://github.com/yandex/ClickHouse/pull/2624)).
* Исправлен редкий deadlock в клиентской библиотеке ZooKeeper, который возникал при сетевой ошибке во время вычитывания ответа ([c315200](https://github.com/yandex/ClickHouse/commit/c315200e64b87e44bdf740707fc857d1fdf7e947)).
* Исправлена ошибка при CAST в Nullable типы ([#1322](https://github.com/yandex/ClickHouse/issues/1322)).
* Исправлен неправильный результат функции `maxIntersection()` в случае совпадения границ отрезков ([Michael Furmur](https://github.com/yandex/ClickHouse/pull/2657)).
* Исправлено неверное преобразование цепочки OR-выражений в аргументе функции ([chenxing-xc](https://github.com/yandex/ClickHouse/pull/2663)).
* Исправлена деградация производительности запросов, содержащих выражение `IN (подзапрос)` внутри другого подзапроса ([#2571](https://github.com/yandex/ClickHouse/issues/2571)).
* Исправлена несовместимость серверов разных версий при распределённых запросах, использующих функцию `CAST` не в верхнем регистре ([fe8c4d6](https://github.com/yandex/ClickHouse/commit/fe8c4d64e434cacd4ceef34faa9005129f2190a5)).
* Добавлено недостающее квотирование идентификаторов при запросах к внешним СУБД ([#2635](https://github.com/yandex/ClickHouse/issues/2635)).

### Обратно несовместимые изменения:
* Не работает преобразование строки, содержащей число ноль, в DateTime. Пример: `SELECT toDateTime('0')`. По той же причине не работает `DateTime DEFAULT '0'` в таблицах, а также `<null_value>0</null_value>` в словарях. Решение: заменить `0` на `0000-00-00 00:00:00`.


## ClickHouse release 1.1.54394, 2018-07-12

### Новые возможности:
* Добавлена агрегатная функция `histogram` ([Михаил Сурин](https://github.com/yandex/ClickHouse/pull/2521)).
* Возможность использования `OPTIMIZE TABLE ... FINAL` без указания партиции для `ReplicatedMergeTree` ([Amos Bird](https://github.com/yandex/ClickHouse/pull/2600)).

### Исправление ошибок:
* Исправлена ошибка - выставление слишком маленького таймаута у сокетов (одна секунда) для чтения и записи при отправке и скачивании реплицируемых данных, что приводило к невозможности скачать куски достаточно большого размера при наличии некоторой нагрузки на сеть или диск (попытки скачивания кусков циклически повторяются). Ошибка возникла в версии 1.1.54388.
* Исправлена работа при использовании chroot в ZooKeeper, в случае вставки дублирующихся блоков данных в таблицу.
* Исправлена работа функции `has` для случая массива с Nullable элементами ([#2115](https://github.com/yandex/ClickHouse/issues/2521)).
* Исправлена работа таблицы `system.tables` при её использовании в распределённых запросах; столбцы `metadata_modification_time` и `engine_full` сделаны невиртуальными; исправлена ошибка в случае, если из таблицы были запрошены только эти столбцы.
* Исправлена работа пустой таблицы типа `TinyLog` после вставки в неё пустого блока данных ([#2563](https://github.com/yandex/ClickHouse/issues/2563)).
* Таблица `system.zookeeper` работает в случае, если значение узла в ZooKeeper равно NULL.


## ClickHouse release 1.1.54390, 2018-07-06

### Новые возможности:
* Возможность отправки запроса в формате `multipart/form-data` (в поле `query`), что полезно, если при этом также отправляются внешние данные для обработки запроса ([Ольга Хвостикова](https://github.com/yandex/ClickHouse/pull/2490)).
* Добавлена возможность включить или отключить обработку одинарных или двойных кавычек при чтении данных в формате CSV. Это задаётся настройками `format_csv_allow_single_quotes` и `format_csv_allow_double_quotes` ([Amos Bird](https://github.com/yandex/ClickHouse/pull/2574))
* Возможность использования `OPTIMIZE TABLE ... FINAL` без указания партиции для не реплицированных вариантов`MergeTree` ([Amos Bird](https://github.com/yandex/ClickHouse/pull/2599)).

### Улучшения:
* Увеличена производительность, уменьшено потребление памяти, добавлен корректный учёт потребления памяти, при использовании оператора IN в случае, когда для его работы может использоваться индекс таблицы ([#2584](https://github.com/yandex/ClickHouse/pull/2584)).
* Убраны избыточные проверки чексумм при добавлении куска. Это важно в случае большого количества реплик, так как в этом случае суммарное количество проверок было равно N^2.
* Добавлена поддержка аргументов типа `Array(Tuple(...))` для функции `arrayEnumerateUniq` ([#2573](https://github.com/yandex/ClickHouse/pull/2573)).
* Добавлена поддержка `Nullable` для функции `runningDifference`. ([#2594](https://github.com/yandex/ClickHouse/pull/2594))
* Увеличена производительность анализа запроса в случае очень большого количества выражений ([#2572](https://github.com/yandex/ClickHouse/pull/2572)).
* Более быстрый выбор кусков для слияния в таблицах типа `ReplicatedMergeTree`. Более быстрое восстановление сессии с ZooKeeper. ([#2597](https://github.com/yandex/ClickHouse/pull/2597)).
* Файл `format_version.txt` для таблиц семейства `MergeTree` создаётся заново при его отсутствии, что имеет смысл в случае запуска ClickHouse после копирования структуры директорий без файлов ([Ciprian Hacman](https://github.com/yandex/ClickHouse/pull/2593)).

### Исправление ошибок:
* Исправлена ошибка при работе с ZooKeeper, которая могла приводить к невозможности восстановления сессии и readonly состояниям таблиц до перезапуска сервера.
* Исправлена ошибка при работе с ZooKeeper, которая могла приводить к неудалению старых узлов при разрыве сессии.
* Исправлена ошибка в функции `quantileTDigest` для Float аргументов (ошибка появилась в версии 1.1.54388) ([Михаил Сурин](https://github.com/yandex/ClickHouse/pull/2553)).
* Исправлена ошибка работы индекса таблиц типа MergeTree, если в условии, столбец первичного ключа расположен внутри функции преобразования типов между знаковым и беззнаковым целым одного размера ([#2603](https://github.com/yandex/ClickHouse/pull/2603)).
* Исправлен segfault, если в конфигурационном файле нет `macros`, но они используются ([#2570](https://github.com/yandex/ClickHouse/pull/2570)).
* Исправлено переключение на базу данных по-умолчанию при переподключении клиента ([#2583](https://github.com/yandex/ClickHouse/pull/2583)).
* Исправлена ошибка в случае отключенной настройки `use_index_for_in_with_subqueries`.

### Исправления безопасности:
* При соединениях с MySQL удалена возможность отправки файлов (`LOAD DATA LOCAL INFILE`).


## ClickHouse release 1.1.54388, 2018-06-28

### Новые возможности:
* Добавлена поддержка запроса `ALTER TABLE t DELETE WHERE` для реплицированных таблиц и таблица `system.mutations`.
* Добавлена поддержка запроса `ALTER TABLE t [REPLACE|ATTACH] PARTITION` для *MergeTree-таблиц.
* Добавлена поддержка запроса `TRUNCATE TABLE` ([Winter Zhang](https://github.com/yandex/ClickHouse/pull/2260))
* Добавлено несколько новых `SYSTEM`-запросов для реплицированных таблиц (`RESTART REPLICAS`, `SYNC REPLICA`, `[STOP|START] [MERGES|FETCHES|REPLICATED SENDS|REPLICATION QUEUES]`).
* Добавлена возможность записи в таблицу с движком MySQL и соответствующую табличную функцию ([sundy-li](https://github.com/yandex/ClickHouse/pull/2294)).
* Добавлена табличная функция `url()` и движок таблиц `URL` ([Александр Сапин](https://github.com/yandex/ClickHouse/pull/2501)).
* Добавлена агрегатная функция `windowFunnel` ([sundy-li](https://github.com/yandex/ClickHouse/pull/2352)).
* Добавлены функции `startsWith` и `endsWith` для строк ([Вадим Плахтинский](https://github.com/yandex/ClickHouse/pull/2429)).
* В табличной функции `numbers()` добавлена возможность указывать offset ([Winter Zhang](https://github.com/yandex/ClickHouse/pull/2535)).
* Добавлена возможность интерактивного ввода пароля в `clickhouse-client`.
* Добавлена возможность отправки логов сервера в syslog ([Александр Крашенинников](https://github.com/yandex/ClickHouse/pull/2459)).
* Добавлена поддержка логирования в словарях с источником shared library ([Александр Сапин](https://github.com/yandex/ClickHouse/pull/2472)).
* Добавлена поддержка произвольного разделителя в формате CSV ([Иван Жуков](https://github.com/yandex/ClickHouse/pull/2263))
* Добавлена настройка `date_time_input_format`. Если переключить эту настройку в значение `'best_effort'`, значения DateTime будут читаться в широком диапазоне форматов.
* Добавлена утилита `clickhouse-obfuscator` для обфускации данных. Пример использования: публикация данных, используемых в тестах производительности.

### Экспериментальные возможности:
* Добавлена возможность вычислять аргументы функции `and` только там, где они нужны ([Анастасия Царькова](https://github.com/yandex/ClickHouse/pull/2272))
* Добавлена возможность JIT-компиляции в нативный код некоторых выражений ([pyos](https://github.com/yandex/ClickHouse/pull/2277)).

### Исправление ошибок:
* Исправлено появление дублей в запросе с `DISTINCT` и `ORDER BY`.
* Запросы с `ARRAY JOIN` и `arrayFilter` раньше возвращали некорректный результат.
* Исправлена ошибка при чтении столбца-массива из Nested-структуры ([#2066](https://github.com/yandex/ClickHouse/issues/2066)).
* Исправлена ошибка при анализе запросов с секцией HAVING вида `HAVING tuple IN (...)`.
* Исправлена ошибка при анализе запросов с рекурсивными алиасами.
* Исправлена ошибка при чтении из ReplacingMergeTree с условием в PREWHERE, фильтрующим все строки ([#2525](https://github.com/yandex/ClickHouse/issues/2525)).
* Настройки профиля пользователя не применялись при использовании сессий в HTTP-интерфейсе.
* Исправлено применение настроек из параметров командной строки в программе clickhouse-local.
* Клиентская библиотека ZooKeeper теперь использует таймаут сессии, полученный от сервера.
* Исправлена ошибка в клиентской библиотеке ZooKeeper, из-за которой ожидание ответа от сервера могло длиться дольше таймаута.
* Исправлено отсечение ненужных кусков при запросе с условием на столбцы ключа партиционирования ([#2342](https://github.com/yandex/ClickHouse/issues/2342)).
* После `CLEAR COLUMN IN PARTITION` в соответствующей партиции теперь возможны слияния ([#2315](https://github.com/yandex/ClickHouse/issues/2315)).
* Исправлено соответствие типов в табличной функции ODBC ([sundy-li](https://github.com/yandex/ClickHouse/pull/2268)).
* Исправлено некорректное сравнение типов `DateTime` с таймзоной и без неё ([Александр Бочаров](https://github.com/yandex/ClickHouse/pull/2400)).
* Исправлен синтаксический разбор и форматирование оператора `CAST`.
* Исправлена вставка в материализованное представление в случае, если движок таблицы представления - Distributed ([Babacar Diassé](https://github.com/yandex/ClickHouse/pull/2411)).
* Исправлен race condition при записи данных из движка `Kafka` в материализованные представления ([Yangkuan Liu](https://github.com/yandex/ClickHouse/pull/2448)).
* Исправлена SSRF в табличной функции remote().
* Исправлен выход из `clickhouse-client` в multiline-режиме ([#2510](https://github.com/yandex/ClickHouse/issues/2510)).

### Улучшения:
* Фоновые задачи в реплицированных таблицах теперь выполняются не в отдельных потоках, а в пуле потоков ([Silviu Caragea](https://github.com/yandex/ClickHouse/pull/1722))
* Улучшена производительность разжатия LZ4.
* Ускорен анализ запроса с большим числом JOIN-ов и подзапросов.
* DNS-кэш теперь автоматически обновляется при большом числе сетевых ошибок.
* Вставка в таблицу теперь не происходит, если вставка в одно из её материализованных представлений невозможна из-за того, что в нём много кусков.
* Исправлено несоответствие в значениях счётчиков событий `Query`, `SelectQuery`, `InsertQuery`.
* Разрешены выражения вида `tuple IN (SELECT tuple)`, если типы кортежей совпадают.
* Сервер с реплицированными таблицами теперь может стартовать, даже если не сконфигурирован ZooKeeper.
* При расчёте количества доступных ядер CPU теперь учитываются ограничения cgroups ([Atri Sharma](https://github.com/yandex/ClickHouse/pull/2325)).
* Добавлен chown директорий конфигов в конфигурационном файле systemd ([Михаил Ширяев](https://github.com/yandex/ClickHouse/pull/2421)).

### Изменения сборки:
* Добавлена возможность сборки компилятором gcc8.
* Добавлена возможность сборки llvm из submodule.
* Используемая версия библиотеки librdkafka обновлена до v0.11.4.
* Добавлена возможность использования библиотеки libcpuid из системы, используемая версия библиотеки обновлена до 0.4.0.
* Исправлена сборка с использованием библиотеки vectorclass ([Babacar Diassé](https://github.com/yandex/ClickHouse/pull/2274)).
* Cmake теперь по умолчанию генерирует файлы для ninja (как при использовании `-G Ninja`).
* Добавлена возможность использования библиотеки libtinfo вместо libtermcap ([Георгий Кондратьев](https://github.com/yandex/ClickHouse/pull/2519)).
* Исправлен конфликт заголовочных файлов в Fedora Rawhide ([#2520](https://github.com/yandex/ClickHouse/issues/2520)).

### Обратно несовместимые изменения:
* Убран escaping в форматах `Vertical` и `Pretty*`, удалён формат `VerticalRaw`.
* Если в распределённых запросах одновременно участвуют серверы версии 1.1.54388 или новее и более старые, то при использовании выражения `cast(x, 'Type')`, записанного без указания `AS`, если слово `cast` указано не в верхнем регистре, возникает ошибка вида `Not found column cast(0, 'UInt8') in block`. Решение: обновить сервер на всём кластере.


## ClickHouse release 1.1.54385, 2018-06-01
### Исправление ошибок:
* Исправлена ошибка, которая в некоторых случаях приводила к блокировке операций с ZooKeeper.

## ClickHouse release 1.1.54383, 2018-05-22
### Исправление ошибок:
* Исправлена деградация скорости выполнения очереди репликации при большом количестве реплик

## ClickHouse release 1.1.54381, 2018-05-14

### Исправление ошибок:
* Исправлена ошибка, приводящая к "утеканию" метаданных в ZooKeeper при потере соединения с сервером ZooKeeper.

## ClickHouse release 1.1.54380, 2018-04-21

### Новые возможности:
* Добавлена табличная функция `file(path, format, structure)`. Пример, читающий байты из `/dev/urandom`: `ln -s /dev/urandom /var/lib/clickhouse/user_files/random` `clickhouse-client -q "SELECT * FROM file('random', 'RowBinary', 'd UInt8') LIMIT 10"`.

### Улучшения:
* Добавлена возможность оборачивать подзапросы скобками `()` для повышения читаемости запросов. Например: `(SELECT 1) UNION ALL (SELECT 1)`.
* Простые запросы `SELECT` из таблицы `system.processes` не учитываются в ограничении `max_concurrent_queries`.

### Исправление ошибок:
* Исправлена неправильная работа оператора `IN` в `MATERIALIZED VIEW`.
* Исправлена неправильная работа индекса по ключу партиционирования в выражениях типа `partition_key_column IN (...)`.
* Исправлена невозможность выполнить `OPTIMIZE` запрос на лидирующей реплике после выполнения `RENAME` таблицы.
* Исправлены ошибки авторизации возникающие при выполнении запросов `OPTIMIZE` и `ALTER` на нелидирующей реплике.
* Исправлены зависания запросов `KILL QUERY`.
* Исправлена ошибка в клиентской библиотеке ZooKeeper, которая при использовании непустого префикса `chroot` в конфигурации приводила к потере watch'ей, остановке очереди distributed DDL запросов и замедлению репликации.

### Обратно несовместимые изменения:
* Убрана поддержка выражений типа `(a, b) IN (SELECT (a, b))` (можно использовать эквивалентные выражение `(a, b) IN (SELECT a, b)`). Раньше такие запросы могли приводить к недетерминированной фильтрации в `WHERE`.


## ClickHouse release 1.1.54378, 2018-04-16

### Новые возможности:

* Возможность изменения уровня логгирования без перезагрузки сервера.
* Добавлен запрос `SHOW CREATE DATABASE`.
* Возможность передать `query_id` в `clickhouse-client` (elBroom).
* Добавлена настройка `max_network_bandwidth_for_all_users`.
* Добавлена поддержка `ALTER TABLE ... PARTITION ... ` для `MATERIALIZED VIEW`.
* Добавлена информация о размере кусков данных в несжатом виде в системные таблицы.
* Поддержка межсерверного шифрования для distributed таблиц (`<secure>1</secure>` в конфигурации реплики в `<remote_servers>`).
* Добавлена настройка уровня таблицы семейства `ReplicatedMergeTree` для уменьшения объема данных, хранимых в zookeeper: `use_minimalistic_checksums_in_zookeeper = 1`
* Возможность настройки приглашения `clickhouse-client`. По-умолчанию добавлен вывод имени сервера в приглашение. Возможность изменить отображаемое имя сервера. Отправка его в HTTP заголовке `X-ClickHouse-Display-Name` (Kirill Shvakov).
* Возможность указания нескольких `topics` через запятую для движка `Kafka` (Tobias Adamson)
* При остановке запроса по причине `KILL QUERY` или `replace_running_query`, клиент получает исключение `Query was cancelled` вместо неполного результата.

### Улучшения:

* Запросы вида `ALTER TABLE ... DROP/DETACH PARTITION` выполняются впереди очереди репликации.
* Возможность использовать `SELECT ... FINAL` и `OPTIMIZE ... FINAL` даже в случае, если данные в таблице представлены одним куском.
* Пересоздание таблицы `query_log` налету в случае если было произведено её удаление вручную (Kirill Shvakov).
* Ускорение функции `lengthUTF8` (zhang2014).
* Улучшена производительность синхронной вставки в `Distributed` таблицы (`insert_distributed_sync = 1`) в случае очень большого количества шардов.
* Сервер принимает настройки `send_timeout` и `receive_timeout` от клиента и применяет их на своей стороне для соединения с клиентом (в переставленном порядке: `send_timeout` у сокета на стороне сервера выставляется в значение `receive_timeout` принятое от клиента, и наоборот).
* Более надёжное восстановление после сбоев при асинхронной вставке в `Distributed` таблицы.
* Возвращаемый тип функции `countEqual` изменён с `UInt32` на `UInt64` (谢磊)

### Исправление ошибок:

* Исправлена ошибка c `IN` где левая часть выражения `Nullable`.
* Исправлен неправильный результат при использовании кортежей с `IN` в случае, если часть компоненнтов кортежа есть в индексе таблицы.
* Исправлена работа ограничения `max_execution_time` с распределенными запросами.
* Исправлены ошибки при вычислении размеров составных столбцов в таблице `system.columns`.
* Исправлена ошибка при создании временной таблицы `CREATE TEMPORARY TABLE IF NOT EXISTS`
* Исправлены ошибки в `StorageKafka` (#2075)
* Исправлены падения сервера от некорректных аргументов некоторых аггрегатных функций.
* Исправлена ошибка, из-за которой запрос `DETACH DATABASE` мог не приводить к остановке фоновых задач таблицы типа `ReplicatedMergeTree`.
* Исправлена проблема с появлением `Too many parts` в агрегирующих материализованных представлениях (#2084).
* Исправлена рекурсивная обработка подстановок в конфиге, если после одной подстановки, требуется другая подстановка на том же уровне.
* Исправлена ошибка с неправильным синтаксисом в файле с метаданными при создании `VIEW`, использующих запрос с `UNION ALL`.
* Исправлена работа `SummingMergeTree` в случае суммирования вложенных структур данных с составным ключом.
* Исправлена возможность возникновения race condition при выборе лидера таблиц `ReplicatedMergeTree`.

### Изменения сборки:

* Поддержка `ninja` вместо `make` при сборке. `ninja` используется по-умолчанию при сборке релизов.
* Переименованы пакеты `clickhouse-server-base` в `clickhouse-common-static`; `clickhouse-server-common` в `clickhouse-server`; `clickhouse-common-dbg` в `clickhouse-common-static-dbg`. Для установки используйте `clickhouse-server clickhouse-client`. Для совместимости, пакеты со старыми именами продолжают загружаться в репозиторий.

### Обратно несовместимые изменения:

* Удалена специальная интерпретация выражения IN, если слева указан массив. Ранее выражение вида `arr IN (set)` воспринималось как "хотя бы один элемент `arr` принадлежит множеству `set`". Для получения такого же поведения в новой версии, напишите `arrayExists(x -> x IN (set), arr)`.
* Отключено ошибочное использование опции сокета `SO_REUSEPORT` (которая по ошибке включена по-умолчанию в библиотеке Poco). Стоит обратить внимание, что на Linux системах теперь не имеет смысла указывать одновременно адреса `::` и `0.0.0.0` для listen - следует использовать лишь адрес `::`, который (с настройками ядра по-умолчанию) позволяет слушать соединения как по IPv4 так и по IPv6. Также вы можете вернуть поведение старых версий, указав в конфиге `<listen_reuse_port>1</listen_reuse_port>`.


## ClickHouse release 1.1.54370, 2018-03-16

### Новые возможности:

* Добавлена системная таблица `system.macros` и автоматическое обновление макросов при изменении конфигурационного файла.
* Добавлен запрос `SYSTEM RELOAD CONFIG`.
* Добавлена агрегатная функция `maxIntersections(left_col, right_col)`, возвращающая максимальное количество одновременно пересекающихся интервалов `[left; right]`. Функция `maxIntersectionsPosition(left, right)` возвращает начало такого "максимального" интервала. ([Michael Furmur](https://github.com/yandex/ClickHouse/pull/2012)).

### Улучшения:

* При вставке данных в `Replicated`-таблицу делается меньше обращений к `ZooKeeper` (также из лога `ZooKeeper` исчезло большинство user-level ошибок).
* Добавлена возможность создавать алиасы для множеств. Пример: `WITH (1, 2, 3) AS set SELECT number IN set FROM system.numbers LIMIT 10`.

### Исправление ошибок:

* Исправлена ошибка `Illegal PREWHERE` при чтении из Merge-таблицы над `Distributed`-таблицами.
* Добавлены исправления, позволяющие запускать clickhouse-server в IPv4-only docker-контейнерах.
* Исправлен race condition при чтении из системной таблицы `system.parts_columns`
* Убрана двойная буферизация при синхронной вставке в `Distributed`-таблицу, которая могла приводить к timeout-ам соединений.
* Исправлена ошибка, вызывающая чрезмерно долгое ожидание недоступной реплики перед началом выполнения `SELECT`.
* Исправлено некорректное отображение дат в таблице `system.parts`.
* Исправлена ошибка, приводящая к невозможности вставить данные в `Replicated`-таблицу, если в конфигурации кластера `ZooKeeper` задан непустой `chroot`.
* Исправлен алгоритм вертикального мержа при пустом ключе `ORDER BY` таблицы.
* Возвращена возможность использовать словари в запросах к удаленным таблицам, даже если этих словарей нет на сервере-инициаторе. Данная функциональность была потеряна в версии 1.1.54362.
* Восстановлено поведение, при котором в запросах типа `SELECT * FROM remote('server2', default.table) WHERE col IN (SELECT col2 FROM default.table)` в правой части `IN` должна использоваться удаленная таблица `default.table`, а не локальная. данное поведение было нарушено в версии 1.1.54358.
* Устранено ненужное Error-level логирование `Not found column ... in block`.


## Релиз ClickHouse 1.1.54362, 2018-03-11

### Новые возможности:

* Агрегация без `GROUP BY` по пустому множеству (как например, `SELECT count(*) FROM table WHERE 0`) теперь возвращает результат из одной строки с нулевыми значениями агрегатных функций, в соответствии со стандартом SQL. Вы можете вернуть старое поведение (возвращать пустой результат), выставив настройку `empty_result_for_aggregation_by_empty_set` в значение 1.
* Добавлено приведение типов при `UNION ALL`. Допустимо использование столбцов с разными алиасами в соответствующих позициях `SELECT` в `UNION ALL`, что соответствует стандарту SQL.
* Поддержка произвольных выражений в секции `LIMIT BY`. Ранее было возможно лишь использование столбцов - результата `SELECT`.
* Использование индекса таблиц семейства `MergeTree` при наличии условия `IN` на кортеж от выражений от столбцов первичного ключа. Пример `WHERE (UserID, EventDate) IN ((123, '2000-01-01'), ...)` (Anastasiya Tsarkova).
* Добавлен инструмент `clickhouse-copier` для межкластерного копирования и перешардирования данных (бета).
* Добавлены функции консистентного хэширования `yandexConsistentHash`, `jumpConsistentHash`, `sumburConsistentHash`. Их можно использовать в качестве ключа шардирования для того, чтобы уменьшить объём сетевого трафика при последующих перешардированиях.
* Добавлены функции `arrayAny`, `arrayAll`, `hasAny`, `hasAll`, `arrayIntersect`, `arrayResize`.
* Добавлена функция `arrayCumSum` (Javi Santana).
* Добавлена функция `parseDateTimeBestEffort`, `parseDateTimeBestEffortOrZero`, `parseDateTimeBestEffortOrNull`, позволяющая прочитать DateTime из строки, содержащей текст в широком множестве возможных форматов.
* Возможность частичной перезагрузки данных внешних словарей при их обновлении (загрузка лишь записей со значением заданного поля большим, чем при предыдущей загрузке) (Arsen Hakobyan).
* Добавлена табличная функция `cluster`. Пример: `cluster(cluster_name, db, table)`. Табличная функция `remote` может принимать имя кластера в качестве первого аргумента, если оно указано в виде идентификатора.
* Возможность использования табличных функций `remote`, `cluster` в `INSERT` запросах.
* Добавлены виртуальные столбцы `create_table_query`, `engine_full` в таблице `system.tables`. Столбец `metadata_modification_time` сделан виртуальным.
* Добавлены столбцы `data_path`, `metadata_path` в таблицы `system.tables` и` system.databases`, а также столбец `path` в таблицы `system.parts` и `system.parts_columns`.
* Добавлена дополнительная информация о слияниях в таблице `system.part_log`.
* Возможность использования произвольного ключа партиционирования для таблицы `system.query_log` (Kirill Shvakov).
* Запрос `SHOW TABLES` теперь показывает также и временные таблицы. Добавлены временные таблицы и столбец `is_temporary` в таблице `system.tables` (zhang2014).
* Добавлен запрос `DROP TEMPORARY TABLE`, `EXISTS TEMPORARY TABLE` (zhang2014).
* Поддержка `SHOW CREATE TABLE` для временных таблиц (zhang2014).
* Добавлен конфигурационный параметр `system_profile` для настроек, используемых внутренними процессами.
* Поддержка загрузки `object_id` в качестве атрибута в словарях с источником `MongoDB` (Павел Литвиненко).
* Возможность читать `null` как значение по-умолчанию при загрузке данных для внешнего словаря с источником `MongoDB` (Павел Литвиненко).
* Возможность чтения значения типа `DateTime` в формате `Values` из unix timestamp без одинарных кавычек.
* Поддержан failover в табличной функции `remote` для случая, когда на части реплик отсутствует запрошенная таблица.
* Возможность переопределять параметры конфигурации в параметрах командной строки при запуске `clickhouse-server`, пример: `clickhouse-server -- --logger.level=information`.
* Реализована функция `empty` от аргумента типа `FixedString`: функция возвращает 1, если строка состоит полностью из нулевых байт (zhang2014).
* Добавлен конфигурационный параметр `listen_try`, позволяющий слушать хотя бы один из listen адресов и не завершать работу, если некоторые адреса не удаётся слушать (полезно для систем с выключенной поддержкой IPv4 или IPv6).
* Добавлен движок таблиц `VersionedCollapsingMergeTree`.
* Поддержка строк и произвольных числовых типов для источника словарей `library`.
* Возможность использования таблиц семейства `MergeTree` без первичного ключа (для этого необходимо указать `ORDER BY tuple()`).
* Добавлена возможность выполнить преобразование (`CAST`) `Nullable` типа в не `Nullable` тип, если аргумент не является `NULL`.
* Возможность выполнения `RENAME TABLE` для `VIEW`.
* Добавлена функция `throwIf`.
* Добавлена настройка `odbc_default_field_size`, позволяющая расширить максимальный размер значения, загружаемого из ODBC источника (по-умолчанию - 1024).
* В таблицу `system.processes` и в `SHOW PROCESSLIST` добавлены столбцы `is_cancelled` и `peak_memory_usage`.

### Улучшения:

* Ограничения на результат и квоты на результат теперь не применяются к промежуточным данным для запросов `INSERT SELECT` и для подзапросов в `SELECT`.
* Уменьшено количество ложных срабатываний при проверке состояния `Replicated` таблиц при запуске сервера, приводивших к необходимости выставления флага `force_restore_data`.
* Добавлена настройка `allow_distributed_ddl`.
* Запрещено использование недетерминированных функций в выражениях для ключей таблиц семейства `MergeTree`.
* Файлы с подстановками из `config.d` директорий загружаются в алфавитном порядке.
* Увеличена производительность функции `arrayElement` в случае константного многомерного массива с пустым массивом в качестве одного из элементов. Пример: `[[1], []][x]`.
* Увеличена скорость запуска сервера при использовании конфигурационных файлов с очень большими подстановками (например, очень большими списками IP-сетей).
* При выполнении запроса, табличные функции выполняются один раз. Ранее табличные функции `remote`, `mysql` дважды делали одинаковый запрос на получение структуры таблицы с удалённого сервера.
* Используется генератор документации `MkDocs`.
* При попытке удалить столбец таблицы, от которого зависят `DEFAULT`/`MATERIALIZED` выражения других столбцов, кидается исключение (zhang2014).
* Добавлена возможность парсинга пустой строки в текстовых форматах как числа 0 для `Float` типов данных. Эта возможность присутствовала раньше, но была потеряна в релизе 1.1.54342.
* Значения типа `Enum` можно использовать в функциях `min`, `max`, `sum` и некоторых других - в этих случаях используются соответствующие числовые значения. Эта возможность присутствовала ранее, но была потеряна в релизе 1.1.54337.
* Добавлено ограничение `max_expanded_ast_elements` действующее на размер AST после рекурсивного раскрытия алиасов.

### Исправление ошибок:

* Исправлены случаи ошибочного удаления ненужных столбцов из подзапросов, а также отсутствие удаления ненужных столбцов из подзапросов, содержащих `UNION ALL`.
* Исправлена ошибка в слияниях для таблиц типа `ReplacingMergeTree`.
* Исправлена работа синхронного режима вставки в `Distributed` таблицы (`insert_distributed_sync = 1`).
* Исправлены segfault при некоторых случаях использования `FULL` и `RIGHT JOIN` с дублирующимися столбцами в подзапросах.
* Исправлены segfault, которые могут возникать при использовании функциональности `replace_running_query` и `KILL QUERY`.
* Исправлен порядок столбцов `source` и `last_exception` в таблице `system.dictionaries`.
* Исправлена ошибка - запрос `DROP DATABASE` не удалял файл с метаданными.
* Исправлен запрос `DROP DATABASE` для базы данных типа `Dictionary`.
* Исправлена неоправданно низкая точность работы функций `uniqHLL12` и `uniqCombined` для кардинальностей больше 100 млн. элементов (Alex Bocharov).
* Исправлено вычисление неявных значений по-умолчанию при необходимости одновременного вычисления явных выражений по-умолчанию в запросах `INSERT` (zhang2014).
* Исправлен редкий случай, в котором запрос к таблице типа `MergeTree` мог не завершаться (chenxing-xc).
* Исправлено падение при выполнении запроса `CHECK` для `Distributed` таблиц, если все шарды локальные (chenxing.xc).
* Исправлена незначительная регрессия производительности при работе функций, использующих регулярные выражения.
* Исправлена регрессия производительности при создании многомерных массивов от сложных выражений.
* Исправлена ошибка, из-за которой в `.sql` файл с метаданными может записываться лишняя секция `FORMAT`.
* Исправлена ошибка, приводящая к тому, что ограничение `max_table_size_to_drop` действует при попытке удаления `MATERIALIZED VIEW`, смотрящего на явно указанную таблицу.
* Исправлена несовместимость со старыми клиентами (на старые клиенты могли отправляться данные с типом `DateTime('timezone')`, который они не понимают).
* Исправлена ошибка при чтении столбцов-элементов `Nested` структур, которые были добавлены с помощью `ALTER`, но являются пустыми для старых партиций, когда условия на такие столбцы переносятся в `PREWHERE`.
* Исправлена ошибка при фильтрации таблиц по условию на виртуальных столбец `_table` в запросах к таблицам типа `Merge`.
* Исправлена ошибка при использовании `ALIAS` столбцов в `Distributed` таблицах.
* Исправлена ошибка, приводящая к невозможности динамической компиляции запросов с агрегатными функциями из семейства `quantile`.
* Исправлен race condition в конвейере выполнения запроса, который мог проявляться в очень редких случаях при использовании `Merge` таблиц над большим количеством таблиц, а также при использовании `GLOBAL` подзапросов.
* Исправлено падение при передаче массивов разных размеров в функцию `arrayReduce` при использовании агрегатных функций от нескольких аргументов.
* Запрещено использование запросов с `UNION ALL` в `MATERIALIZED VIEW`.
* Исправлена ошибка, которая может возникать при инициализации системной таблицы `part_log` при старте сервера (по-умолчанию `part_log` выключен).

### Обратно несовместимые изменения:

* Удалена настройка `distributed_ddl_allow_replicated_alter`. Соответствующее поведение включено по-умолчанию.
* Удалена настройка `strict_insert_defaults`. Если вы использовали эту функциональность, напишите на `clickhouse-feedback@yandex-team.com`.
* Удалён движок таблиц `UnsortedMergeTree`.

## Релиз ClickHouse 1.1.54343, 2018-02-05

* Добавлена возможность использовать макросы при задании имени кластера в распределенных DLL запросах и создании Distributed-таблиц: `CREATE TABLE distr ON CLUSTER '{cluster}' (...) ENGINE = Distributed('{cluster}', 'db', 'table')`.
* Теперь при вычислении запросов вида `SELECT ... FROM table WHERE expr IN (subquery)` используется индекс таблицы `table`.
* Улучшена обработка дубликатов при вставке в Replicated-таблицы, теперь они не приводят к излишнему замедлению выполнения очереди репликации.

## Релиз ClickHouse 1.1.54342, 2018-01-22

Релиз содержит исправление к предыдущему релизу 1.1.54337:
* Исправлена регрессия в версии 1.1.54337: если пользователь по-умолчанию имеет readonly доступ, то сервер отказывался стартовать с сообщением `Cannot create database in readonly mode`.
* Исправлена регрессия в версии 1.1.54337: на системах под управлением systemd, логи по ошибке всегда записываются в syslog; watchdog скрипт по ошибке использует init.d.
* Исправлена регрессия в версии 1.1.54337: неправильная конфигурация по-умоланию в Docker образе.
* Исправлена недетерминированная работа GraphiteMergeTree (в логах видно по сообщениям `Data after merge is not byte-identical to data on another replicas`).
* Исправлена ошибка, в связи с которой запрос OPTIMIZE к Replicated таблицам мог приводить к неконсистентным мержам (в логах видно по сообщениям `Part ... intersects previous part`).
* Таблицы типа Buffer теперь работают при наличии MATERIALIZED столбцов в таблице назначения (by zhang2014).
* Исправлена одна из ошибок в реализации NULL.

## Релиз ClickHouse 1.1.54337, 2018-01-18

### Новые возможности:

* Добавлена поддержка хранения многомерных массивов и кортежей (тип данных `Tuple`) в таблицах.
* Поддержка табличных функций для запросов `DESCRIBE` и `INSERT`. Поддержка подзапроса в запросе `DESCRIBE`. Примеры: `DESC TABLE remote('host', default.hits)`; `DESC TABLE (SELECT 1)`; `INSERT INTO TABLE FUNCTION remote('host', default.hits)`. Возможность писать `INSERT INTO TABLE` вместо `INSERT INTO`.
* Улучшена поддержка часовых поясов. В типе `DateTime` может быть указана таймзона, которая используется для парсинга и отображения данных в текстовом виде. Пример: `DateTime('Europe/Moscow')`. При указании таймзоны в функциях работы с `DateTime`, тип возвращаемого значения будет запоминать таймзону, для того, чтобы значение отображалось ожидаемым образом.
* Добавлены функции `toTimeZone`, `timeDiff`, `toQuarter`, `toRelativeQuarterNum`. В функцию `toRelativeHour`/`Minute`/`Second` можно передать аргумент типа `Date`. Имя функции `now` воспринимается без учёта регистра.
* Добавлена функция `toStartOfFifteenMinutes` (Kirill Shvakov).
* Добавлена программа `clickhouse format` для переформатирования запросов.
* Добавлен конфигурационный параметр `format_schema_path` (Marek Vavruša). Он используется для задания схемы для формата `Cap'n'Proto`. Файлы со схемой могут использоваться только из указанной директории.
* Добавлена поддержка `incl` и `conf.d` подстановок для конфигурации словарей и моделей (Pavel Yakunin).
* В таблице `system.settings` появилось описание большинства настроек (Kirill Shvakov).
* Добавлена таблица `system.parts_columns`, содержащая информацию о размерах столбцов в каждом куске данных `MergeTree` таблиц.
* Добавлена таблица `system.models`, содержащая информацию о загруженных моделях `CatBoost`.
* Добавлены табличные функции `mysql` и `odbc` и соответствующие движки таблиц `MySQL`, `ODBC` для обращения к удалённым базам данных. Функциональность в состоянии "бета".
* Для функции `groupArray` разрешено использование аргументов типа `AggregateFunction` (можно создать массив из состояний агрегатных функций).
* Удалены ограничения на использование разных комбинаций комбинаторов агрегатных функций. Для примера, вы можете использовать как функцию `avgForEachIf`, так и `avgIfForEach`, которые имеют разный смысл.
* Комбинатор агрегатных функций `-ForEach` расширен для случая агрегатных функций с более чем одним аргументом.
* Добавлена поддержка агрегатных функций от `Nullable` аргументов, для случаев, когда функция всегда возвращает не `Nullable` результат (реализовано с участием Silviu Caragea). Пример: `groupArray`, `groupUniqArray`, `topK`.
* Добавлен параметр командной строки `max_client_network_bandwidth` для `clickhouse-client` (Kirill Shvakov).
* Пользователям с доступом `readonly = 2` разрешено работать с временными таблицами (CREATE, DROP, INSERT...) (Kirill Shvakov).
* Добавлена возможность указания количества consumers для `Kafka`.  Расширена возможность конфигурации движка `Kafka` (Marek Vavruša).
* Добавлены функции `intExp2`, `intExp10`.
* Добавлена агрегатная функция `sumKahan`.
* Добавлены функции to*Number*OrNull, где *Number* - числовой тип.
* Добавлена поддержка секции `WITH` для запроса `INSERT SELECT` (автор: zhang2014).
* Добавлены настройки `http_connection_timeout`, `http_send_timeout`, `http_receive_timeout`. Настройки используются, в том числе, при скачивании кусков для репликации. Изменение этих настроек позволяет сделать более быстрый failover в случае перегруженной сети.
* Добавлена поддержка `ALTER` для таблиц типа `Null` (Anastasiya Tsarkova).
* Функция `reinterpretAsString` расширена на все типы данных, значения которых хранятся в памяти непрерывно.
* Для программы `clickhouse-local` добавлена опция `--silent` для подавления вывода информации о выполнении запроса в stderr.
* Добавлена поддержка чтения `Date` в текстовом виде в формате, где месяц и день месяца могут быть указаны одной цифрой вместо двух (Amos Bird).

### Увеличение производительности:

* Увеличена производительность агрегатных функций `min`, `max`, `any`, `anyLast`, `anyHeavy`, `argMin`, `argMax` от строковых аргументов.
* Увеличена производительность функций `isInfinite`, `isFinite`, `isNaN`, `roundToExp2`.
* Увеличена производительность форматирования в текстовом виде и парсинга из текста значений типа `Date` и `DateTime`.
* Увеличена производительность и точность парсинга чисел с плавающей запятой.
* Уменьшено потребление памяти при `JOIN`, если левая и правая часть содержали столбцы с одинаковым именем, не входящие в `USING`.
* Увеличена производительность агрегатных функций `varSamp`, `varPop`, `stddevSamp`, `stddevPop`, `covarSamp`, `covarPop`, `corr` за счёт уменьшения стойкости к вычислительной погрешности. Старые версии функций добавлены под именами `varSampStable`, `varPopStable`, `stddevSampStable`, `stddevPopStable`, `covarSampStable`, `covarPopStable`, `corrStable`.

### Исправления ошибок:

* Исправлена работа дедупликации блоков после `DROP` или `DETATH PARTITION`. Раньше удаление партиции и вставка тех же самых данных заново не работала, так как вставленные заново блоки считались дубликатами.
* Исправлена ошибка, в связи с которой может неправильно обрабатываться `WHERE` для запросов на создание `MATERIALIZED VIEW` с указанием `POPULATE`.
* Исправлена ошибка в работе параметра `root_path` в конфигурации `zookeeper_servers`.
* Исправлен неожиданный результат при передаче аргумента типа `Date` в функцию `toStartOfDay`.
* Исправлена работа функции `addMonths`, `subtractMonths`, арифметика с `INTERVAL n MONTH`, если в результате получается предыдущий год.
* Добавлена недостающая поддержка типа данных `UUID` для `DISTINCT`, `JOIN`, в агрегатных функциях `uniq` и во внешних словарях (Иванов Евгений). Поддержка `UUID` всё ещё остаётся не полной.
* Исправлено поведение `SummingMergeTree` для строк, в которых все значения после суммирования равны нулю.
* Многочисленные доработки для движка таблиц `Kafka` (Marek Vavruša).
* Исправлена некорректная работа движка таблиц `Join` (Amos Bird).
* Исправлена работа аллокатора под FreeBSD и OS X.
* Функция `extractAll` теперь может доставать пустые вхождения.
* Исправлена ошибка, не позволяющая подключить при сборке `libressl` вместо `openssl`.
* Исправлена работа `CREATE TABLE AS SELECT` из временной таблицы.
* Исправлена неатомарность обновления очереди репликации. Эта проблема могла приводить к рассинхронизации реплик и чинилась при перезапуске.
* Исправлено переполнение в функциях `gcd`, `lcm`, `modulo` (оператор `%`) (Maks Skorokhod).
* Файлы `-preprocessed` теперь создаются после изменения `umask` (`umask` может быть задан в конфигурационном файле).
* Исправлена ошибка фоновой проверки кусков (`MergeTreePartChecker`) при использовании партиционирования по произвольному ключу.
* Исправлен парсинг кортежей (значений типа `Tuple`) в текстовых форматах.
* Исправлены сообщения о неподходящих типах аргументов для функций `multiIf`, `array` и некоторых других.
* Переработана поддержка `Nullable` типов. Исправлены ошибки, которые могут приводить к падению сервера. Исправлено подавляющее большинство других ошибок, связанных с поддержкой `NULL`: неправильное приведение типов при INSERT SELECT, недостаточная поддержка Nullable в HAVING и в PREWHERE, режим `join_use_nulls`, Nullable типы в операторе `OR` и т. п.
* Исправлена работа с внутренними свойствами типов данных, что позволило исправить проблемы следующего вида: ошибочное суммирование полей типа `Enum` в `SummingMergeTree`; значения типа `Enum` ошибочно выводятся с выравниванием по правому краю в таблицах в `Pretty` форматах, и т. п.
* Более строгие проверки для допустимых комбинаций составных столбцов - это позволило исправить ошибок, которые могли приводить к падениям.
* Исправлено переполнение при задании очень большого значения параметра для типа `FixedString`.
* Исправлена работа агрегатной функции `topK` для generic случая.
* Добавлена отсутствующая проверка на совпадение размеров массивов для n-арных вариантов агрегатных функций с комбинатором `-Array`.
* Исправлена работа `--pager` для `clickhouse-client` (автор: ks1322).
* Исправлена точность работы функции `exp10`.
* Исправлено поведение функции `visitParamExtract` согласно документации.
* Исправлено падение при объявлении некорректных типов данных.
* Исправлена работа `DISTINCT` при условии, что все столбцы константные.
* Исправлено форматирование запроса в случае наличия функции `tupleElement` со сложным константным выражением в качестве номера элемента.
* Исправлена работа `Dictionary` таблиц для словарей типа `range_hashed`.
* Исправлена ошибка, приводящая к появлению лишних строк при `FULL` и `RIGHT JOIN` (Amos Bird).
* Исправлено падение сервера в случае создания и удаления временных файлов в `config.d` директориях в момент перечитывания конфигурации.
* Исправлена работа запроса `SYSTEM DROP DNS CACHE`: ранее сброс DNS кэша не приводил к повторному резолвингу имён хостов кластера.
* Исправлено поведение `MATERIALIZED VIEW` после `DETACH TABLE` таблицы, на которую он смотрит (Marek Vavruša).

### Улучшения сборки:

* Для сборки используется `pbuilder`. Сборка максимально независима от окружения на сборочной машине.
* Для разных версий систем выкладывается один и тот же пакет, который совместим с широким диапазоном Linux систем.
* Добавлен пакет `clickhouse-test`, который может быть использован для запуска функциональных тестов.
* Добавлена выкладка в репозиторий архива с исходниками. Этот архив может быть использован для воспроизведения сборки без использования GitHub.
* Добавлена частичная интеграция с Travis CI. В связи с ограничениями на время сборки в Travis, запускается только ограниченный набор тестов на Debug сборке.
* Добавлена поддержка `Cap'n'Proto` в сборку по-умолчанию.
* Документация переведена с `Restructured Text` на `Markdown`.
* Добавлена поддержка `systemd` (Vladimir Smirnov). В связи с несовместимостью с некоторыми образами, она выключена по-умолчанию и может быть включена вручную.
* Для динамической компиляции запросов, `clang` и `lld` встроены внутрь `clickhouse`. Они также могут быть вызваны с помощью `clickhouse clang` и `clickhouse lld`.
* Удалено использование расширений GNU из кода и включена опция `-Wextra`. При сборке с помощью `clang` по-умолчанию используется `libc++` вместо `libstdc++`.
* Выделены библиотеки `clickhouse_parsers` и `clickhouse_common_io` для более быстрой сборки утилит.

### Обратно несовместимые изменения:

* Формат засечек (marks) для таблиц типа `Log`, содержащих `Nullable` столбцы, изменён обратно-несовместимым образом. В случае наличия таких таблиц, вы можете преобразовать их в `TinyLog` до запуска новой версии сервера. Для этого в соответствующем таблице файле `.sql` в директории `metadata`, замените `ENGINE = Log` на `ENGINE = TinyLog`. Если в таблице нет `Nullable` столбцов или тип таблицы не `Log`, то ничего делать не нужно.
* Удалена настройка `experimental_allow_extended_storage_definition_syntax`. Соответствующая функциональность включена по-умолчанию.
* Функция `runningIncome` переименована в `runningDifferenceStartingWithFirstValue` во избежание путаницы.
* Удалена возможность написания `FROM ARRAY JOIN arr` без указания таблицы после FROM (Amos Bird).
* Удалён формат `BlockTabSeparated`, использовавшийся лишь для демонстрационных целей.
* Изменён формат состояния агрегатных функций `varSamp`, `varPop`, `stddevSamp`, `stddevPop`, `covarSamp`, `covarPop`, `corr`. Если вы использовали эти состояния для хранения в таблицах (тип данных `AggregateFunction` от этих функций или материализованные представления, хранящие эти состояния), напишите на clickhouse-feedback@yandex-team.com.
* В предыдущих версиях существовала недокументированная возможность: в типе данных AggregateFunction можно было не указывать параметры для агрегатной функции, которая зависит от параметров. Пример: `AggregateFunction(quantiles, UInt64)` вместо `AggregateFunction(quantiles(0.5, 0.9), UInt64)`. Эта возможность потеряна. Не смотря на то, что возможность не документирована, мы собираемся вернуть её в ближайших релизах.
* Значения типа данных Enum не могут быть переданы в агрегатные функции min/max. Возможность будет возвращена обратно в следующем релизе.

### На что обратить внимание при обновлении:
* При обновлении кластера, на время, когда на одних репликах работает новая версия сервера, а на других - старая, репликация будет приостановлена и в логе появятся сообщения вида `unknown parameter 'shard'`. Репликация продолжится после обновления всех реплик кластера.
* Если на серверах кластера работают разные версии ClickHouse, то возможен неправильный результат распределённых запросов, использующих функции `varSamp`, `varPop`, `stddevSamp`, `stddevPop`, `covarSamp`, `covarPop`, `corr`. Необходимо обновить все серверы кластера.

## Релиз ClickHouse 1.1.54327, 2017-12-21

Релиз содержит исправление к предыдущему релизу 1.1.54318:
* Исправлена проблема с возможным race condition при репликации, которая может приводить к потере данных. Проблеме подвержены версии 1.1.54310 и 1.1.54318. Если вы их используете и у вас есть Replicated таблицы, то обновление обязательно. Понять, что эта проблема существует, можно по сообщениям в логе Warning вида `Part ... from own log doesn't exist.` Даже если таких сообщений нет, проблема всё-равно актуальна.

## Релиз ClickHouse 1.1.54318, 2017-11-30

Релиз содержит изменения к предыдущему релизу 1.1.54310 с исправлением следующих багов:
* Исправлено некорректное удаление строк при слияниях в движке SummingMergeTree
* Исправлена утечка памяти в нереплицированных MergeTree-движках
* Исправлена деградация производительности при частых вставках в MergeTree-движках
* Исправлена проблема, приводящая к остановке выполнения очереди репликации
* Исправлено ротирование и архивация логов сервера

## Релиз ClickHouse 1.1.54310, 2017-11-01

### Новые возможности:
* Произвольный ключ партиционирования для таблиц семейства MergeTree.
* Движок таблиц [Kafka](https://clickhouse.yandex/docs/en/single/index.html#document-table_engines/kafka).
* Возможность загружать модели [CatBoost](https://catboost.yandex/) и применять их к данным, хранящимся в ClickHouse.
* Поддержка часовых поясов с нецелым смещением от UTC.
* Поддержка операций с временными интервалами.
* Диапазон значений типов Date и DateTime расширен до 2105 года.
* Запрос `CREATE MATERIALIZED VIEW x TO y` (позволяет указать существующую таблицу для хранения данных материализованного представления).
* Запрос `ATTACH TABLE` без аргументов.
* Логика обработки Nested-столбцов в SummingMergeTree, заканчивающихся на -Map, вынесена в агрегатную функцию sumMap. Такие столбцы теперь можно задавать явно.
* Максимальный размер IP trie-словаря увеличен до 128М записей.
* Функция getSizeOfEnumType.
* Агрегатная функция sumWithOverflow.
* Поддержка входного формата Cap’n Proto.
* Возможность задавать уровень сжатия при использовании алгоритма zstd.

### Обратно несовместимые изменения:
* Запрещено создание временных таблиц с движком, отличным от Memory.
* Запрещено явное создание таблиц с движком View и MaterializedView.
* При создании таблицы теперь проверяется, что ключ сэмплирования входит в первичный ключ.

### Исправления ошибок:
* Исправлено зависание при синхронной вставке в Distributed таблицу.
* Исправлена неатомарность при добавлении/удалении кусков в реплицированных таблицах.
* Данные, вставляемые в материализованное представление, теперь не подвергаются излишней дедупликации.
* Запрос в Distributed таблицу, для которого локальная реплика отстаёт, а удалённые недоступны, теперь не падает.
* Для создания временных таблиц теперь не требуется прав доступа к БД `default`.
* Исправлено падение при указании типа Array без аргументов.
* Исправлено зависание при недостатке места на диске в разделе с логами.
* Исправлено переполнение в функции toRelativeWeekNum для первой недели Unix-эпохи.

### Улучшения сборки:
* Несколько сторонних библиотек (в частности, Poco) обновлены и переведены на git submodules.

## Релиз ClickHouse 1.1.54304, 2017-10-19
### Новые возможности:
* Добавлена поддержка TLS в нативном протоколе (включается заданием `tcp_ssl_port` в `config.xml`)

### Исправления ошибок:
* `ALTER` для реплицированных таблиц теперь пытается начать выполнение как можно быстрее
* Исправлены падения при чтении данных с настройкой `preferred_block_size_bytes=0`
* Исправлено падение `clickhouse-client` при нажатии `Page Down`
* Корректная интепретация некоторых сложных запросов с `GLOBAL IN` и `UNION ALL`
* Операция `FREEZE PARTITION` теперь работает всегда атомарно
* Исправлено зависание пустых POST-запросов (теперь возвращается код 411)
* Исправлены ошибки при интепретации выражений типа `CAST(1 AS Nullable(UInt8))`
* Исправлена ошибка при чтении колонок типа `Array(Nullable(String))` из `MergeTree` таблиц
* Исправлено падение при парсинге запросов типа `SELECT dummy AS dummy, dummy AS b`
* Корректное обновление пользователей при невалидном `users.xml`
* Корректная обработка случаев, когда executable-словарь возвращает ненулевой код ответа

## Релиз ClickHouse 1.1.54292, 2017-09-20

### Новые возможности:
* Добавлена функция `pointInPolygon` для работы с координатами на плоскости.
* Добавлена агрегатная функция `sumMap`, обеспечивающая суммирование массивов аналогично `SummingMergeTree`.
* Добавлена функция `trunc`. Увеличена производительность функций округления `round`, `floor`, `ceil`, `roundToExp2`. Исправлена логика работы функций округления. Изменена логика работы функции `roundToExp2` для дробных и отрицательных чисел.
* Ослаблена зависимость исполняемого файла ClickHouse от версии libc. Один и тот же исполняемый файл ClickHouse может запускаться и работать на широком множестве Linux систем. Замечание: зависимость всё ещё присутствует при использовании скомпилированных запросов (настройка `compile = 1`, по-умолчанию не используется).
* Уменьшено время динамической компиляции запросов.

### Исправления ошибок:
* Исправлена ошибка, которая могла приводить к сообщениям `part ... intersects previous part` и нарушению консистентности реплик.
* Исправлена ошибка, приводящая к блокировке при завершении работы сервера, если в это время ZooKeeper недоступен.
* Удалено избыточное логгирование при восстановлении реплик.
* Исправлена ошибка в реализации UNION ALL.
* Исправлена ошибка в функции concat, возникающая в случае, если первый столбец блока имеет тип Array.
* Исправлено отображение прогресса в таблице system.merges.

## Релиз ClickHouse 1.1.54289, 2017-09-13

### Новые возможности:
* Запросы `SYSTEM` для административных действий с сервером: `SYSTEM RELOAD DICTIONARY`, `SYSTEM RELOAD DICTIONARIES`, `SYSTEM DROP DNS CACHE`, `SYSTEM SHUTDOWN`, `SYSTEM KILL`.
* Добавлены функции для работы с массивами: `concat`, `arraySlice`, `arrayPushBack`, `arrayPushFront`, `arrayPopBack`, `arrayPopFront`.
* Добавлены параметры `root` и `identity` для конфигурации ZooKeeper. Это позволяет изолировать разных пользователей одного ZooKeeper кластера.
* Добавлены агрегатные функции `groupBitAnd`, `groupBitOr`, `groupBitXor` (для совместимости доступны также под именами `BIT_AND`, `BIT_OR`, `BIT_XOR`).
* Возможность загрузки внешних словарей из MySQL с указанием сокета на файловой системе.
* Возможность загрузки внешних словарей из MySQL через SSL соединение (параметры `ssl_cert`, `ssl_key`, `ssl_ca`).
* Добавлена настройка `max_network_bandwidth_for_user` для ограничения общего потребления сети для всех запросов одного пользователя.
* Поддержка `DROP TABLE` для временных таблиц.
* Поддержка чтения значений типа `DateTime` в формате unix timestamp из форматов `CSV` и `JSONEachRow`.
* Включено по-умолчанию отключение отстающих реплик при распределённых запросах (по-умолчанию порог равен 5 минутам).
* Используются FIFO блокировки при ALTER: выполнение ALTER не будет неограниченно блокироваться при непрерывно выполняющихся запросах.
* Возможность задать `umask` в конфигурационном файле.
* Увеличена производительность запросов с `DISTINCT`.

### Исправления ошибок:
* Более оптимальная процедура удаления старых нод в ZooKeeper. Ранее в случае очень частых вставок, старые ноды могли не успевать удаляться, что приводило, в том числе, к очень долгому завершению сервера.
* Исправлена рандомизация при выборе хостов для соединения с ZooKeeper.
* Исправлено отключение отстающей реплики при распределённых запросах, если реплика является localhost.
* Исправлена ошибка, в связи с которой кусок данных таблицы типа `ReplicatedMergeTree` мог становиться битым после выполнения `ALTER MODIFY` элемента `Nested` структуры.
* Исправлена ошибка приводящая к возможному зависанию SELECT запросов.
* Доработки распределённых DDL запросов.
* Исправлен запрос `CREATE TABLE ... AS <materialized view>`.
* Исправлен дедлок при запросе `ALTER ... CLEAR COLUMN IN PARTITION` для `Buffer` таблиц.
* Исправлено использование неправильного значения по-умолчанию для `Enum`-ов (0 вместо минимального) при использовании форматов `JSONEachRow` и `TSKV`.
* Исправлено появление zombie процессов при работе со словарём с источником `executable`.
* Исправлен segfault при запросе HEAD.

### Улучшения процесса разработки и сборки ClickHouse:
* Возможность сборки с помощью `pbuilder`.
* Возможность сборки с использованием `libc++` вместо `libstdc++` под Linux.
* Добавлены инструкции для использования статических анализаторов кода `Coverity`, `clang-tidy`, `cppcheck`.

### На что обратить внимание при обновлении:
* Увеличено значение по-умолчанию для настройки MergeTree `max_bytes_to_merge_at_max_space_in_pool` (максимальный суммарный размер кусков в байтах для мержа) со 100 GiB до 150 GiB. Это может привести к запуску больших мержей после обновления сервера, что может вызвать повышенную нагрузку на дисковую подсистему. Если же на серверах, где это происходит, количество свободного места менее чем в два раза больше суммарного объёма выполняющихся мержей, то в связи с этим перестанут выполняться какие-либо другие мержи, включая мержи мелких кусков. Это приведёт к тому, что INSERT-ы будут отклоняться с сообщением "Merges are processing significantly slower than inserts". Для наблюдения, используйте запрос `SELECT * FROM system.merges`. Вы также можете смотреть на метрику `DiskSpaceReservedForMerge` в таблице `system.metrics` или в Graphite. Для исправления этой ситуации можно ничего не делать, так как она нормализуется сама после завершения больших мержей. Если же вас это не устраивает, вы можете вернуть настройку `max_bytes_to_merge_at_max_space_in_pool` в старое значение, прописав в config.xml в секции `<merge_tree>` `<max_bytes_to_merge_at_max_space_in_pool>107374182400</max_bytes_to_merge_at_max_space_in_pool>` и перезапустить сервер.

## Релиз ClickHouse 1.1.54284, 2017-08-29

* Релиз содержит изменения к предыдущему релизу 1.1.54282, которые исправляют утечку записей о кусках в ZooKeeper

## Релиз ClickHouse 1.1.54282, 2017-08-23

Релиз содержит исправления к предыдущему релизу 1.1.54276:
* Исправлена ошибка `DB::Exception: Assertion violation: !_path.empty()` при вставке в Distributed таблицу.
* Исправлен парсинг при вставке в формате RowBinary, если входные данные начинаются с ';'.
* Исправлена ошибка при рантайм-компиляции некоторых агрегатных функций (например, `groupArray()`).

## Релиз ClickHouse 1.1.54276, 2017-08-16

### Новые возможности:
* Добавлена опциональная секция WITH запроса SELECT. Пример запроса: `WITH 1+1 AS a SELECT a, a*a`
* Добавлена возможность синхронной вставки в Distributed таблицу: выдается Ok только после того как все данные записались на все шарды. Активируется настройкой insert_distributed_sync=1
* Добавлен тип данных UUID для работы с 16-байтовыми идентификаторами
* Добавлены алиасы типов CHAR, FLOAT и т.д. для совместимости с Tableau
* Добавлены функции toYYYYMM, toYYYYMMDD, toYYYYMMDDhhmmss для перевода времени в числа
* Добавлена возможность использовать IP адреса (совместно с hostname) для идентификации сервера при работе с кластерными DDL запросами
* Добавлена поддержка неконстантных аргументов и отрицательных смещений в функции `substring(str, pos, len)`
* Добавлен параметр max_size для агрегатной функции `groupArray(max_size)(column)`, и оптимизирована её производительность

### Основные изменения:
* Улучшение безопасности: все файлы сервера создаются с правами 0640 (можно поменять, через параметр <umask> в конфиге).
* Улучшены сообщения об ошибках в случае синтаксически неверных запросов
* Значительно уменьшен расход оперативной памяти и улучшена производительность слияний больших MergeTree-кусков данных
* Значительно увеличена производительность слияний данных для движка ReplacingMergeTree
* Улучшена производительность асинхронных вставок из Distributed таблицы за счет объединения нескольких исходных вставок. Функциональность включается настройкой distributed_directory_monitor_batch_inserts=1.

### Обратно несовместимые изменения:
* Изменился бинарный формат агрегатных состояний функции `groupArray(array_column)` для массивов

### Полный список изменений:
* Добавлена настройка `output_format_json_quote_denormals`, включающая вывод nan и inf значений в формате JSON
* Более оптимальное выделение потоков при чтении из Distributed таблиц
* Разрешено задавать настройки в режиме readonly, если их значение не изменяется
* Добавлена возможность считывать нецелые гранулы движка MergeTree для выполнения ограничений на размер блока, задаваемый настройкой preferred_block_size_bytes - для уменьшения потребления оперативной памяти и увеличения кэш-локальности при обработке запросов из таблиц со столбцами большого размера
* Эффективное использование индекса, содержащего выражения типа `toStartOfHour(x)`, для условий вида `toStartOfHour(x) op сonstexpr`
* Добавлены новые настройки для MergeTree движков (секция merge_tree в config.xml):
  - replicated_deduplication_window_seconds позволяет задать интервал дедупликации вставок в Replicated-таблицы в секундах
  - cleanup_delay_period - периодичность запуска очистки неактуальных данных
  - replicated_can_become_leader - запретить реплике становиться лидером (и назначать мержи)
* Ускорена очистка неактуальных данных из ZooKeeper
* Множественные улучшения и исправления работы кластерных DDL запросов. В частности, добавлена настройка distributed_ddl_task_timeout, ограничивающая время ожидания ответов серверов кластера.
* Улучшено отображение стэктрейсов в логах сервера
* Добавлен метод сжатия none
* Возможность использования нескольких секций dictionaries_config в config.xml
* Возможность подключения к MySQL через сокет на файловой системе
* В таблицу system.parts добавлен столбец с информацией о размере marks в байтах

### Исправления багов:
* Исправлена некорректная работа Distributed таблиц, использующих Merge таблицы, при SELECT с условием на поле _table
* Исправлен редкий race condition в ReplicatedMergeTree при проверке кусков данных
* Исправлено возможное зависание процедуры leader election при старте сервера
* Исправлено игнорирование настройки max_replica_delay_for_distributed_queries при использовании локальной реплики в качестве источника данных
* Исправлено некорректное поведение `ALTER TABLE CLEAR COLUMN IN PARTITION` при попытке очистить несуществующую колонку
* Исправлено исключение в функции multiIf при использовании пустых массивов или строк
* Исправлено чрезмерное выделение памяти при десериализации формата Native
* Исправлено некорректное автообновление Trie словарей
* Исправлено исключение при выполнении запросов с GROUP BY из Merge-таблицы при использовании SAMPLE
* Исправлено падение GROUP BY при использовании настройки distributed_aggregation_memory_efficient=1
* Добавлена возможность указывать database.table в правой части IN и JOIN
* Исправлено использование слишком большого количества потоков при параллельной агрегации
* Исправлена работа функции if с аргументами FixedString
* Исправлена некорректная работа SELECT из Distributed-таблицы для шардов с весом 0
* Исправлено падение запроса `CREATE VIEW IF EXISTS`
* Исправлено некорректное поведение при input_format_skip_unknown_fields=1 в случае отрицательных чисел
* Исправлен бесконечный цикл в функции `dictGetHierarchy()` в случае некоторых некорректных данных словаря
* Исправлены ошибки типа `Syntax error: unexpected (...)` при выполнении распределенных запросов с подзапросами в секции IN или JOIN, в случае использования совместно с Merge таблицами
* Исправлена неправильная интерпретация SELECT запроса из таблиц типа Dictionary
* Исправлена ошибка "Cannot mremap" при использовании множеств в секциях IN, JOIN, содержащих более 2 млрд. элементов
* Исправлен failover для словарей с источником MySQL

### Улучшения процесса разработки и сборки ClickHouse:
* Добавлена возмозможность сборки в Arcadia
* Добавлена возможность сборки с помощью gcc 7
* Ускорена параллельная сборка с помощью ccache+distcc


## Релиз ClickHouse 1.1.54245, 2017-07-04

### Новые возможности:
* Распределённые DDL (например, `CREATE TABLE ON CLUSTER`)
* Реплицируемый запрос `ALTER TABLE CLEAR COLUMN IN PARTITION`
* Движок таблиц Dictionary (доступ к данным словаря в виде таблицы)
* Движок баз данных Dictionary (в такой базе автоматически доступны Dictionary-таблицы для всех подключённых внешних словарей)
* Возможность проверки необходимости обновления словаря путём отправки запроса в источник
* Qualified имена столбцов
* Квотирование идентификаторов двойными кавычками
* Сессии в HTTP интерфейсе
* Запрос OPTIMIZE для Replicated таблицы теперь можно выполнять не только на лидере

### Обратно несовместимые изменения:
* Убрана команда SET GLOBAL

### Мелкие изменения:
* Теперь после получения сигнала в лог печатается полный стектрейс
* Ослаблена проверка на количество повреждённых/лишних кусков при старте (было слишком много ложных срабатываний)

### Исправления багов:
* Исправлено залипание плохого соединения при вставке в Distributed таблицу
* GLOBAL IN теперь работает при запросе из таблицы Merge, смотрящей в Distributed
* Теперь правильно определяется количество ядер на виртуалках Google Compute Engine
* Исправления в работе executable источника кэшируемых внешних словарей
* Исправлены сравнения строк, содержащих нулевые символы
* Исправлено сравнение полей первичного ключа типа Float32 с константами
* Раньше неправильная оценка размера поля могла приводить к слишком большим аллокациям
* Исправлено падение при запросе Nullable столбца, добавленного в таблицу ALTER-ом
* Исправлено падение при сортировке по Nullable столбцу, если количество строк меньше LIMIT
* Исправлен ORDER BY подзапроса, состоящего только из константных значений
* Раньше Replicated таблица могла остаться в невалидном состоянии после неудавшегося DROP TABLE
* Алиасы для скалярных подзапросов с пустым результатом теперь не теряются
* Теперь запрос, в котором использовалась компиляция, не завершается ошибкой, если .so файл повреждается
