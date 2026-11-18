# RabbitMQ

[[Wiki|← на главную]]

Порты: **5672** (AMQP) и **15672** (панель управления).

RabbitMQ используется вместе с библиотекой **MassTransit** для обмена запросами между микросервисами. Каждый запрос попадает в очередь и обрабатывается, когда до него доходит очередь; сообщения не теряются.

В `Startup` каждого сервиса регистрируются обработчики (consumer'ы) и настраиваются очереди, например для Identity:

```csharp
x.AddConsumer<Authenticate>();
x.AddConsumer<CreateUser>();
x.AddConsumer<GetUserByToken>();

cfg.ReceiveEndpoint("identityQueue", e =>
{
    e.PrefetchCount = 20;
    e.UseMessageRetry(r => r.Interval(2, 100));
    e.Consumer<Authenticate>(context);
    e.Consumer<CreateUser>(context);
    e.Consumer<GetUserByToken>(context);
});
```

Подключение к брокеру — `rabbitmq://host.docker.internal/`. Для сериализации используется Newtonsoft.Json с `PreserveReferencesHandling.Objects`.
