# Bootstrap

Выполнять **только** если в корне проекта нет `AGENT.md`.

1. Возьми файлы из репозитория протокола `https://github.com/papa-gadim/AI-relay`:
   - корень: скопируй `templates/AGENT.md` → в проект как `AGENT.md`
   - скопируй папку `rules/` целиком
   - `templates/STATUS.md` → `STATUS.md`
   - `templates/PROJECT.md` → `PROJECT.md`
   - `templates/README.md` → `README.md`

2. Заполни из ТЗ человека:
   - `README.md` — название, назначение, функции
   - `PROJECT.md` — стек (если есть), versionName `0.1`, versionCode `1`
   - `STATUS.md` — этап 1, чек-листы из ТЗ, **конкретный** «Следующий шаг»

3. Коммит: `Bootstrap AI Relay protocol`

4. Сообщение в чат (и стоп):

```
Готов к работе.
Проект: <название>
Этап: <из STATUS.md>
Следующий шаг: <из STATUS.md>
```
