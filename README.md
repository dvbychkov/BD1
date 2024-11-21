Домашнее задание к занятию "Базы данных, их типы" - <Бычков Денис Вячеславович>

Задание 1. СУБД
Кейс
Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для каждой предметной области.

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему?

1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков. СУБД должна гарантировать целостность и чёткую структуру данных.
1.1.* Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы?
1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? СУБД должны быть гибкими и быстрыми.
1.2.* Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?
1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.
1.3.* Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это реализовать?
1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать со связями.
1.4.* Можно ли к этой СУБД подключить отдел закупок или для них лучше сформировать свою СУБД в связке с СУБД логистов?
1.5.* Можно ли все перечисленные выше задачи решить, используя одну СУБД? Если да, то какую именно?
Приведите ответ в свободной форме.

1.1. 
СУБД: Реляционная СУБД (PostgreSQL или MySQL).  
Данные СУБД обеспечивают строгую целостность данных и отлично подходят для финансовых отчетов и анализа, благодаря мощным средствам работы с данными (функции агрегации, сложные запросы).
API для хеширования: Если необходимости в ускорении хеширования существует, можно рассмотреть использование API, таких как OpenSSL, которые обладают оптимизированными алгоритмами для обработки.
1.2. 
СУБД: NoSQL СУБД (MongoDB).  
Она обеспечивает гибкость в работе с неструктурированными данными и быстрый доступ к информации, что идеально подходит для лендингов и CRM.
Одна СУБД: MongoDB может справляться с задачами как лендингов, так и CRM, предлагая гибкость и масштабируемость.
1.3. 
СУБД: Реляционная СУБД (PostgreSQL).  
Простая структура и использование реляционных данных легко реализуемы в реляционных СУБД. Существует возможность создания визуально структурированной модели данных.
Использование уже существующей СУБД: Да, можно использовать PostgreSQL, добавив новую схему или новые таблицы для хранения обучающих материалов и норм.
1.4. 
СУБД: Графовая СУБД (Neo4j) или реляционная СУБД.  
Графовые СУБД отлично справляются с задачами, связанными со связями и маршрутизацией. Реляционные СУБД также подходят при правильной нормализации таблиц.
Подключение отдела закупок: Если отдел закупок требует специфической информации о материалах или требует частых операций по связыванию данных, имеет смысл создать отдельную базу, которая может связаться с СУБД логистики через API.
1.5.
СУБД: PostgreSQL.  
Она имеет гибкие возможности; можно использовать реляционные данные для бюджетирования и контроля качества, а JSON-формат для лендингов и CRM. В то же время, сложные отношения и маршрутизации можно реализовать через расширенные функции, такие как PostgreSQL с поддержкой графов.
Заключение
Таким образом, в зависимости от задач по масштабу и сложности данных, можно использовать и реляционную, и NoSQL СУБД, либо же ограничиться одной, такой как PostgreSQL, если требуется обеспечить легкость в управлении и интеграции данных.


Задание 2. Транзакции
2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.
2.1.* Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?
Приведите ответ в свободной форме.


2.1. Пошаговый процесс пополнения баланса счёта телефона
1. Идентификация пользователя: Пользователь инициирует операцию пополнения баланса, входя в приложение или веб-сервис и предоставляя необходимые данные (номер телефона, сумму пополнения).
2. Валидирование данных: Система проверяет, корректны ли введенные данные (например, правильность номера телефона, наличие минимальной суммы пополнения).
3. Авторизация платежа: Пользователь выбирает способ оплаты (например, банковская карта или электронный кошелек) и система инициирует процесс авторизации выбранного способа платежа.
4. Запрос на списание средств: После успешной авторизации система отправляет запрос на списание средств с аккаунта пользователя (банковского счёта или карты).
5. Обработка транзакции: Платежный шлюз обрабатывает запрос, и если средства успешно списаны, он возвращает подтверждение успешной транзакции.
6. Завершение операции: Система обновляет баланс счёта телефона пользователя, отправляет уведомление о пополнении и сохраняет запись о транзакции в базе данных.

2.1.* Процесс пополнения через автоплатёж
1. Настройка автоплатежа: Пользователь ранее настраивает автоплатёж, указывая номер телефона, сумму и периодичность (например, ежемесячно).
2. Планирование транзакции: В установленное время система автоматически инициирует процесс пополнения согласно ранее заданным параметрам.
3. Валидирование данных: Система проверяет, актуальны ли данные (действующий номер счета, указанная сумма, наличие достаточных средств на счете).
4. Авторизация платежа: Модуль автоплатежа автоматически инициирует авторизацию средств с привязанного метода оплаты.
5. Обработка транзакции: Платежный шлюз обрабатывает запрос. В случае успешного списания средств он возвращает подтверждение.
6. Завершение операции: Система автоматически обновляет баланс счёта телефона, уведомляет пользователя о пополнении и сохраняет запись о транзакции в базе данных для финансового мониторинга. 
Таким образом, автоплатёж значительно упрощает процесс для пользователя, автоматизируя действия и минимизируя необходимость ввода данных.


Задание 3. SQL vs NoSQL
3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL.
3.1.* Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.

3.1. Преимущества SQL-систем по отношению к NoSQL
1. Строгая структура данных: SQL-системы используют заранее определенные схемы, что обеспечивает строгую целостность и организованность данных. Это особенно важно для финансовых и бизнес-приложений.
2. Сложные запросы: SQL позволяет выполнять сложные запросы с использованием JOIN, подзапросов и агрегаций, что упрощает извлечение и анализ взаимосвязанных данных.
3. Транзакционная надежность: SQL-базы данных обеспечивают поддержку ACID-принципов (атомарность, целостность, изоляция, долговечность), что гарантирует надежность транзакций и защиту данных от сбоев.
4. Стандартный язык: SQL является общепринятым языком, что обеспечивает высокую степень совместимости между различными СУБД и снижает порог входа для разработчиков и аналитиков.
5. Подробное управление пользователями: SQL-системы позволяют гибко настраивать уровни доступа и управление правами пользователей, что важно для обеспечения безопасности данных.

3.1.* Преимущества NewSQL перед SQL и NoSQL
1. Масштабируемость как у NoSQL: NewSQL предоставляет возможность горизонтального масштабирования, что позволяет эффективно работать с объемами данных, превышающим возможности традиционных реляционных СУБД.
2. Поддержка ACID: NewSQL сохраняет преимущества строгих транзакционных характеристик SQL-систем (надежность и целостность данных), что является критически важным для многих приложений.
3. Высокая производительность: Новый подход к архитектуре БД и использование распределенных вычислений обеспечивают большую скорость обработки запросов по сравнению с традиционными реляционными системами.
4. Гибкость схемы: NewSQL часто предлагает более гибкие схемы, чем традиционные SQL, что позволяет лучше адаптироваться к изменениям в бизнес-требованиях без необходимости полностью перерабатывать структуру базы данных.
5. Интеграция с современными технологиями: NewSQL системы легко интегрируются с современными облачными архитектурами, микросервисами и большими данными, что делает их актуальными для современных приложений.

Таким образом, NewSQL сочетает в себе лучшие качества SQL и NoSQL, обеспечивая высокую производительность, масштабируемость и надежность при работе с данными.


Приведите ответ в свободной форме.

Задание 4. Кластеры
Необходимо производить большое количество вычислений при работе с огромным количеством данных, под эту задачу выделено 1000 машин.
На основе какого критерия будете выбирать тип СУБД и какая модель распределённых вычислений здесь справится лучше всего и почему?
Приведите ответ в свободной форме.


Критерии выбора СУБД:
1. Объем и тип данных: 
   - Если данные структурированы с четкими схемами, целесообразно использовать распределённые реляционные СУБД (например, Google Spanner или CockroachDB).
   - Для неструктурированных или полуструктурированных данных лучше подойдут NoSQL решения (например, Apache Cassandra или MongoDB).
2. Требования к производительности: 
   - Системы, которые обеспечивают высокую скорость записи и чтения данных, будут предпочтительными. Например, Cassandra отлично справляется с высокими требованиями к записи данных.
3. Масштабируемость:
   - Выбор системы, способной легко масштабироваться горизонтально, является важным аспектом. NoSQL базы данных, такие как HBase или Couchbase, могут эффективно использовать 1000 машин, обеспечивая гибкую архитек­туру.
4. Поддержка транзакций и целостности данных: 
   - Если критична поддержка ACID-транзакций, тогда стоит выбирать NewSQL или распределённые реляционные СУБД, что обеспечит надежность работы с критически важными данными.
5. Инструменты аналитики: 
   - Для задач, требующих анализа больших данных, система должна поддерживать интеграцию с инструментами обработки, такими как Apache Spark или Hadoop.

Модель распределённых вычислений:
Для обработки больших объемов данных на 1000 машинах лучше всего подойдёт модель MapReduce: 
- Параллелизм: MapReduce позволяет распределять задачу на множество машин, обрабатывая данные параллельно, что значительно увеличивает скорость вычислений.
- Обработка больших объемов данных: Модель эффективно работает с большими наборами данных, что делает её идеальной для анализа больших данных.
- Толерантность к сбоям: MapReduce автоматически повторяет задачи в случае сбоя, что важно при работе с большим количеством узлов.
- Хорошая интеграция с популярными хранилищами данных: MapReduce прекрасно работает в связке с HDFS (Hadoop Distributed File System) и различными NoSQL СУБД, что позволяет хранить и обрабатывать данные эффективно.

Заключение

Выбор СУБД и модели распределённых вычислений будет зависеть от природы данных и требований к обработке. Для заданной конфигурации можно рассмотреть комбинирование NoSQL СУБД (например, Cassandra) с моделью MapReduce для максимального использования вычислительных ресурсов и обработки больших объемов данных.