# Gloud — шаблоны приложений

Репозиторий-источник шаблонов для Gloud. Приложение читает `index.json`, а файлы
шаблонов тянет по raw-URL (`https://raw.githubusercontent.com/<owner>/<repo>/<branch>/<file>`).

В `.env` приложения указывается:

```
TEMPLATES_REPO=<owner>/<repo>@<branch>
```

## Структура

```
index.json              — каталог шаблонов
templates/<id>.json     — файлы шаблонов
```

### index.json

```json
{
  "version": 1,
  "templates": [
    {
      "id": "demo",
      "title": "Название",
      "description": "Короткое описание",
      "icon": "bi-box",
      "version": 1,
      "file": "templates/demo.json",
      "hasSampleData": false
    }
  ]
}
```

- `version` шаблона — увеличивай при изменении содержимого; приложение скачает
  новую версию при синхронизации.
- `hasSampleData: true` — файл содержит и тестовые данные (`schema_records`,
  `schema_values`); при импорте пользователь сможет включить их галочкой.

### Файл шаблона (`templates/<id>.json`)

Это бандл формата Gloud:

```json
{
  "kind": "template",
  "version": 1,
  "tables": { "schema_types": [...], "schema_fields": [...], ... }
}
```

Получить такой файл проще всего через приложение: **Настройки → Система →
Експорт шаблону** (секреты — telegram-токены, webhook-ключи, SMTP — вырезаются
автоматически). Чтобы добавить тестовые данные, экспортируй с данными и проставь
`hasSampleData: true` в `index.json`.

## Как добавить шаблон

1. Положи файл в `templates/<id>.json`.
2. Добавь запись в `index.json`.
3. Закоммить и запушь — приложения подтянут при следующей синхронизации
   (фоново при старте или по кнопке «Обновить»).

> Не клади сюда секреты: репозиторий публичный.
