# MediaHub uptime

Внешний мониторинг [MediaHub Pro](https://mediahubpro.ru): проверка каждые 5 минут через GitHub Actions.

## Что проверяется

1. **Сайт** — `https://mediahubpro.ru/` отвечает `200` и содержит «MediaHub».
2. **Сервер** — `health.txt` читается напрямую с origin (`171.22.114.76`), в обход Cloudflare.
3. **Бот** — в `health.txt` свежий timestamp (не старше 5 минут) и `"bot":"active"`.

Heartbeat на сервере обновляется раз в минуту через `/etc/cron.d/mediahub-heartbeat`.

## Алерты

Приходят в Telegram от `@MediaHubPro_bot`:

- 🔴 сайт/сервер/бот недоступен;
- 🟢 всё снова работает.

Сообщение отправляется только при смене состояния, без спама. Секреты `TELEGRAM_BOT_TOKEN` и `TELEGRAM_CHAT_ID` хранятся в настройках репозитория.

## Ручной запуск

Actions → **uptime** → Run workflow. Флаг `test_alert` отправляет тестовое сообщение в Telegram.
