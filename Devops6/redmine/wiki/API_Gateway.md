# API Gateway (Ocelot)

[[Wiki|← на главную]]

Адрес: **http://localhost:5000**

API Gateway — единая точка входа для клиентов: принимает запросы и перенаправляет их нужному микросервису. В проекте используется **Ocelot** (`src/RtuItLab.ApiGateway`, .NET 5).

Маршруты и правила переадресации описаны в файле `ocelot.json`. Документация по формату: https://ocelot.readthedocs.io/en/latest/features/configuration.html
