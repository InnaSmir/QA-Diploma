## План автоматизации тестирования
Провести исследовательское тестирование и тестирование на основе опыта, так как нет спецификации и определенных требований к работе приложения и вводимым данным.

Сценарии покупки тура:
1. Провести положительные тесты при заполнении валидными данными всех полей. 
Ожидаемый результат: Платеж успешно проходит.
2. Провести негативные тесты при заполнении не валидными данными каждого поля в отдельности, в том числе оставить поля пустыми.
 Ожидаемый результат: появляется сообщение об ошибке в каждом поле, куда введены не валидные данные, платеж не проходит.
3. Проверить сохраняет ли приложение информацию в таблицах о том, каким способом был совершен платеж и успешно ли он был совершен. Ожидаемый результат: в таблицах сохранена информация о способе и успешности платежа.

### Положительные тест-кейсы:
#### 1.Заполнить все поля валидными данными для покупки
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Заполнить поля месяц, год, владелец, cvc/cvv
6. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется сообщение "Успешно! Операция одобрена банком". Проверить, что платеж прошел и запись Approved появилась в столбце "status" в таблице "payment_entity"
#### 2.Заполнить все поля валидными данными для покупки в кредит
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить в кредит"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Заполнить поля месяц, год, владелец, cvc/cvv
6. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется сообщение "Успешно! Операция одобрена банком". Проверить, что платеж прошел и запись Approved появилась в столбце "status" в таблице "credit_request_entity"

### Негативные тест-кейсы:
##### 1. Заполнить все поля данными для покупки в кредит
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить в кредит"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4442
5. Заполнить поля месяц, год, владелец, cvc/cvv
6. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется сообщение "Неуспешно! Операция не одобрена банком". Проверить, что в таблице появилась запись Decline в столбце "status" в таблице "credit_request_entity"
##### 2. Заполнить все поля данными для покупки
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4442
5. Заполнить поля месяц, год, владелец, cvc/cvv
6. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется сообщение "Неуспешно! Операция не одобрена банком". Проверить, что в таблице появилась запись Decline в столбце "status" в таблице "payment_entity"
##### 3. Заполнить не полностью номер карты для покупки
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444
5. Заполнить поля месяц, год, владелец, cvc/cvv
6. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется ошибка в поле "Номер карты" и отказ совершить платеж
##### 4. Не заполнять поле месяц при покупке
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Не заполнять поле месяц
6. Заполнить поля год, владелец, cvc/cvv
7. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется ошибка в поле "месяц" и отказ совершить платеж
##### 5. Заполнить несуществующий номер карты при покупке в кредит
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить в кредит"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 1111 1111 1111 1111
5. Заполнить поля месяц, год, владелец, cvc/cvv
6. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется ошибка в поле "номер карты" и отказ совершить платеж
##### 6. Заполнить поле месяц не полностью при покупке
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Заполнить поле месяц: 1
6. Заполнить поля год, владелец, cvc/cvv
Нажать кнопку "Продолжить"
Ожидаемый результат: появляется ошибка в поле "месяц" и отказ совершить платеж
##### 7. Заполнить поле год на 15 лет позже от текущей даты при покупке
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Заполнить поле месяц
6. Заполнить поле год на 15 лет позже от текущей даты
7. Заполнить поля: владелец, cvc/cvv
8. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется ошибка в поле "год" и отказ совершить платеж
##### 8. Заполнить поле на 2 года раньше текущей даты при покупке
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Заполнить поле месяц
6. Заполнить поле на 2 года раньше от текущей даты
7. Заполнить поля: владелец, cvc/cvv
8. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется ошибка в поле "год" и отказ совершить платеж
##### 9. Заполнить только имя при покупке
1. Открыть страницу localhost:8080
2. На странице нажать кнопку " Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Заполнить поля месяц, год
6. Заполнить в поле владелец только имя
7. Заполнить поле cvc/cvv
8. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется ошибка в поле "владелец" и отказ совершить платеж
##### 10. Заполнить поле именем через дефис и фамилией при покупке
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Заполнить поля месяц, год
6. Заполнить в поле Владелец: Иван-Иван Иванов
7. Заполнить поле cvc/cvv
8. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется сообщение "Успешно! Операция одобрена банком"
Проверить, что платеж был успешен и запись Approved появилась в столбце "status" в таблице "payment_entity"
##### 11. Заполнить поле владелец на английском языке при покупке в кредит
1. Открыть страницу localhost:8080
2. На странице нажать кнопку "Купить в кредит"
3. На появившейся странице выбрать "Оплата по карте"
4. Заполнить поле номер карты: 4444 4444 4444 4441
5. Заполнить поля месяц, год
6. Заполнить поле владелец на английском языке: "Ivan Ivanov"
7. Заполнить поле cvc/cvv
8. Нажать кнопку "Продолжить"
Ожидаемый результат: появляется ошибка в поле "Владелец" и отказ совершить платеж

### Перечень используемых инструментов
1. IntelliJ IDEA - среда разработки для написания кода и тестов, платформа ориентирована на Java-кодинг, обладает интуитивным интерфейсом, поддерживает все необходимые для тестирования инструменты.
2. JUnit 5 - платформа для написания авто-тестов и их запуска. Позволяет использовать аннотации для упрощения написания и читаемости кода. JUnit 5 содержит новые аннотации, в том числе позволяет использовать параметризированные тесты (запускаемые несколько раз с различными исходными данными) с помощью аннотации @ParameterizedTest.
3. JDK 11 - используем язык приложения - Java.
4. Gradle - инструмент автоматизации сборки и управления зависимостями (будет сама выкачивать все требуемые нам библиотеки после того, как мы пропишем зависимости).
5. Loombook - упростит написание кода, уменьшит его количество и улучшит читаемость.
6. Selenide - инструмент для автоматизированного тестирования веб-приложений на базе Selenium WebDriver, дающий определенные преимущества:
сам запускает и закрывает браузер, сам делает скриншоты после тестов
поддерживает Ajax
7. Faker - для генерации данных, обладает широким спектром генерируемых данных, не нужно самому выдумывать данные.
8. Git и Github: система контроля версий для хранения кода и автотестов. Позволяет откатить изменения, если произошли какие-нибудь проблемы, можно установить CI для контроля. Удобно делиться кодом для совместной разработки и использования.
9. Allure - инструмент для создания визуально наглядной картины выполнения тестов. Генерирует более подробные отчеты с более конкретной визуализацией, чем Gradle.

### Перечень и описание возможных рисков при автоматизации
1. Проблемы с установкой Docker (проблема совместимости Docker с Windows)
2. Проблемы с запуском SUT и Docker
3. Проблемы с поддержкой двух СУБД
4. Отсутствие документации к сервису
5. Необходимость добавления новых тестов для заказчика, в связи с отсутствием документации и спецификации на приложение.

### Интервальная оценка с учетом рисков (в часах): 60 - 80 часов.

### План сдачи работ
1. Завершение кодирования тестов: 24.12.2019 (написание плана тестирования, настройка окружения, написание и отладка автотестов, само тестирование)
2. Предоставление отчетности: 29.12.2019