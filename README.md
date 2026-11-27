# AI Relay

Протокол последовательной разработки несколькими AI-агентами.

https://github.com/papa-gadim/AI-relay

## Управление агентом

Логика — в `AGENT.md` (линейные шаги). В чат — только доступ и одна фраза «прочитай AGENT.md…».

| Обращение | В чат |
|-----------|--------|
| Новый проект | URL проекта + токен + URL протокола + токен + ТЗ + «прочитай AGENT.md в протоколе и выполни» |
| Продолжение | URL проекта + токен + «прочитай AGENT.md и STATUS.md в проекте и продолжай» |

Handoff между агентами — файл `STATUS.md` в проекте (точка остановки + следующий шаг).

## Файлы

```
AGENT.md           алгоритм (в протоколе; в проект копируется templates/AGENT.md)
BOOTSTRAP.md       установка правил в пустой проект
rules/             core, workflow, coding, build, communication
templates/         STATUS, PROJECT, README, AGENT
prompts/init-agent.md
```
