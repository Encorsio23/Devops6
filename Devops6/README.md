# DevOps — лабораторная работа 6 (итоговая)

Dev-окружение **Gitea + Redmine + Drone CI + Docker Registry** в одном `docker-compose`, wiki и задачи в Redmine по проекту [RtuItLab](https://github.com/bezlla/RtuItLab), конвейер Drone для сборки контейнеров.

## Структура

| Путь | Что внутри |
|---|---|
| `devenv/docker-compose.yml` | Окружение: Gitea :3001, Redmine :3000 (+ PostgreSQL), Drone :8000, Drone Runner, Registry :5000 |
| `devenv/docker-compose.override.yml` | Подключение томов из прошлых лабораторных (на новой машине не нужен) |
| `devenv/.env.example` | Шаблон секретов Drone и OAuth Gitea |
| `ci/.drone.yml` | Конвейер для репозитория RtuItLab (в самом репозитории лежит в корне как `.drone.yml`) |
| `redmine/wiki/*.md` | Страницы wiki Redmine, подготовленные по README проекта |
| `redmine/issues.md` | Задачи, заведённые в Redmine |
| `screenshots/` | Скриншоты для отчёта |
| `report/` | Реферат — ссылка на документ (скачать в Word/PDF можно из него) |

## Запуск окружения

```bash
cd devenv
cp .env.example .env        # заполнить DRONE_RPC_SECRET, DRONE_GITEA_CLIENT_ID/SECRET
rm docker-compose.override.yml   # если разворачиваете с нуля
docker compose up -d
```

1. Открыть Gitea http://localhost:3001, пройти установку, создать пользователя.
2. В Gitea: Настройки → Приложения → OAuth2, redirect URI `http://localhost:8000/login`; ID и секрет — в `.env`, затем `docker compose up -d`.
3. Открыть Drone http://localhost:8000, войти через Gitea, активировать репозиторий.
4. Положить `ci/.drone.yml` в корень репозитория как `.drone.yml` — push в `master` запустит сборку.

Если на хосте включён ufw: `sudo ufw allow 3001/tcp && sudo ufw allow 8000/tcp` (Gitea и Drone работают в сети хоста).

## Конвейер

1. `clone` — клонирование из Gitea по адресу шлюза docker-сети;
2. `unit-tests` — `dotnet test` для Purchases.UnitTests и Shops.UnitTests;
3. `build-and-push` — `docker build` пяти сервисов (ApiGateway, Identity, Purchases, Shops, Factories) и `docker push` в `localhost:5000/rtuitlab/<сервис>:<номер сборки>` и `:latest`.

Проверка: `curl http://localhost:5000/v2/_catalog`.
