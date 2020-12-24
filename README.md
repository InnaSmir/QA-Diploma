# Дипломный проект профессии «Тестировщик»
## Дипломный проект представляет собой автоматизацию тестирования комплексного сервиса, взаимодействующего с СУБД и API Банка.
Приложение представляет из себя веб-сервис, который предоставляет возможность купить тур по определённой цене с помощью двух способов: 
1. Обычная оплата по дебетовой карте
2. Уникальная технология: выдача кредита по данным банковской карты

## Документация проекта:
* [План автоматизации тестирования](https://github.com/InnaSmir/QA-Diploma/blob/main/docs/Plan.md)
* Отчет по итогам тестирования
* Отчет по итогам автоматизации

## Необходимое программное обеспечение:
* Java11
* IntelliJ IDEA
* Docker

## Инструкция по запуску авто-тестов:
* Склонируйте репозиторий https://github.com/InnaSmir/QA-Diploma
* Запустите контейнер в терминале InteliJ Idea, в котором разворачивается база данных docker-compose up -d --force-recreate
* Запустите SUT командой:
#### Запуск в MySQL:
1. Запустить машину: docker-machine start default
2. Запустить контейнеры: docker-compose -f docker-compose-mysql.yml up –d
3. Запустить SUT: java -jar artifacts/aqa-shop.jar
4. Запустить тесты: gradlew test -Dtest.db.url=jdbc:mysql://192.168.99.100:3306/app
5. Остановить контейнеры: docker-compose -f docker-compose-mysql.yml down
6. Остановить машину: docker-machine stop default
#### Запуск для Postgres:
1. Запустить машину: docker-machine start default
2. Запустить контейнеры: docker-compose -f docker-compose-postgres.yml up -d
3. Запустить SUT: java -Dspring.datasource.url=jdbc:postgresql://192.168.99.100:5432/app -jar artifacts/aqa-shop.jar
4. Запустить тесты: gradlew test -Dtest.db.url=jdbc:postgresql://192.168.99.100:5432/app
5. Остановить контейнеры: docker-compose -f docker-compose-postgres.yml down
6. Остановить машину: docker-machine stop default
        
        
      
