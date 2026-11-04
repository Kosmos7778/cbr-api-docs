# cbr-api-docs — документация API курсов валют ЦБ РФ

Образец работы технического писателя: спецификация **OpenAPI 3.1** для живого публичного API
(cbr-xml-daily.ru — JSON-зеркало котировок Банка России) и два рендера этой спецификации.

## Смотреть онлайн (GitHub Pages)

| Рендер | Ссылка |
|---|---|
| Redoc — готовая статичная документация | https://kosmos7778.github.io/cbr-api-docs/redoc.html |
| Swagger UI — интерактивная, запросы можно отправлять | https://kosmos7778.github.io/cbr-api-docs/swagger-ui.html |

## Что внутри

| Файл | Что это |
|---|---|
| `openapi-cbr.yaml` | Спецификация OpenAPI 3.1: 3 эндпоинта, 4 схемы, валидирована openapi-spec-validator |
| `redoc.html` | Готовая документация (Redoc), спека встроена — открывается без сервера |
| `swagger-ui.html` | Интерактивный Swagger UI со встроенной спекой |

## Что показывает этот пример

- **Реальные данные.** Примеры ответов сняты с живого API: USD 81.6699 ₽, EUR 91.601 ₽ (04.11.2026), архивные котировки за 30.10.2026 проверены реальным запросом.
- **Ловушки описаны до того, как о них споткнётся разработчик:** номинал (у йены курс за 100 единиц), строковый `NumCode` с ведущим нулём, обратная котировка в формате money.js.
- **Named examples** — подписанные примеры видны в выпадающем списке Swagger UI.
- **Обход истории** — показано, как через `PreviousURL` идти по архиву котировок день за днём.

## Проверка спецификации

```bash
npx @redocly/cli lint openapi-cbr.yaml
# или
pip install openapi-spec-validator && python -c "
from openapi_spec_validator import validate
import yaml; validate(yaml.safe_load(open('openapi-cbr.yaml')))
print('VALID')"
```

## Swagger UI локально

На GitHub Pages работает сразу. Локально нужен любой HTTP-сервер — резолвер `$ref`
не работает с `file://`:

```bash
python -m http.server 8777
# откройте http://localhost:8777/swagger-ui.html
```

---

> 📂 Демо-проект из портфолио технического писателя: показывает, как может выглядеть документация вашего API. По вашей Postman-коллекции, Swagger-файлу или готовому коду роутов сделаю аналогично. Больше примеров — в профиле [@Kosmos7778](https://github.com/Kosmos7778).
