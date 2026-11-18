# Docker

[[Wiki|← на главную]]

Проект поддерживает запуск в Docker. У каждого сервиса свой `Dockerfile` (многоэтапная сборка: SDK-образ → `dotnet publish` → runtime-образ ASP.NET).

| Сервис | Dockerfile | Образ в локальном Registry |
|---|---|---|
| ApiGateway | `src/RtuItLab.ApiGateway/Dockerfile` | `localhost:5000/rtuitlab/apigateway` |
| Identity | `src/Services/Identity/Identity.API/Dockerfile` | `localhost:5000/rtuitlab/identityapi` |
| Purchases | `src/Services/Purchases/Purchases.API/Dockerfile` | `localhost:5000/rtuitlab/purchasesapi` |
| Shops | `src/Services/Shops/Shops.API/Dockerfile` | `localhost:5000/rtuitlab/shopsapi` |
| Factories | `src/Services/Factories/Factories.API/Dockerfile` | `localhost:5000/rtuitlab/factoriesapi` |

Запуск всего проекта (из каталога `src`):

```
docker-compose pull
docker-compose up
```

`src/docker-compose.yml` поднимает RabbitMQ, SQL Server и пять сервисов. Образы собирает конвейер Drone — см. [[Окружение_разработки]].
