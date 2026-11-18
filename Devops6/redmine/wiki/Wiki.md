# RtuItLab — wiki проекта

Учебный проект, демонстрирующий работу **микросервисов** на ASP.NET Core, **контейнеров Docker** и **брокера сообщений RabbitMQ**. Документация собрана по `README.md` репозитория.

* Исходный код: http://localhost:3001/student/RtuItLab (Gitea)
* Сборки: http://localhost:8000/student/RtuItLab (Drone CI)
* Образы: `localhost:5000/rtuitlab/*` (Docker Registry)

## Разделы

1. [[Функциональность]] — что умеет клиент
2. [[Микросервисы]] — Identity, Purchases, Shops, Factories
3. [[Базы_данных]] — 4 БД, Entity Framework Core, Code First
4. [[RabbitMQ]] — обмен сообщениями через MassTransit
5. [[API_Gateway]] — Ocelot
6. [[Docker]] — запуск проекта в контейнерах
7. [[Тесты]] — модульные и smoke-тесты
8. [[Окружение_разработки]] — Gitea + Redmine + Drone + Registry, конвейер CI

## Порты сервисов

| Сервис | Порт |
|---|---|
| Identity | 7001 |
| Purchases | 7002 |
| Shops | 7003 |
| Factories | 7004 |
| RabbitMQ | 5672 (AMQP), 15672 (панель управления) |
| ApiGateway | 5000 |

## Стек

* ASP.NET Core Web API (.NET Core 3.1, ApiGateway — .NET 5)
* Entity Framework Core
* xUnit (модульные тесты)
* Docker / docker-compose
* RabbitMQ + MassTransit
* Ocelot API Gateway
