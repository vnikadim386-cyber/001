# Build & Release

## Сборка

- Все приложения собираются **только через GitHub Actions**.
- Локальную сборку для проверки можно делать, но артефакты для человека и магазинов — из Actions (Artifacts / Releases).
- В workflow задавай имя выходного файла явно. Не оставляй дефолтные `app-debug.apk` / `app-release.apk`.

## Именование артефактов

Имя файла = **имя репозитория** + версия.

Примеры (репозиторий `analog-clock-learn`):

| Тип | versionName | Имя файла |
|-----|-------------|-----------|
| Debug / разработка | `0.1`, `0.2`, `0.3`… | `analog-clock-learn-0.3.apk` |
| Release | `1.0`, `1.1`… | `analog-clock-learn-1.0.apk` (или `.aab`) |

- Debug-версии **всегда** начинаются с `0.` (0.1, 0.2, …).
- Release **только** после явной просьбы человека («сделай релиз», «версия 1.0»).
- `versionCode` — целое число, строго растёт с каждой сборкой (и debug, и release).

В `build.gradle` / `build.gradle.kts` (или аналоге):

- `versionName` и имя артефакта должны совпадать со схемой выше.
- Имя приложения в UI может отличаться; **файл** и **versionName** — по репозиторию и схеме версий.

## Debug vs Release

| | Debug (0.x) | Release (1.0+) |
|--|-------------|----------------|
| Когда | По умолчанию, пока идёт разработка | Только по запросу человека |
| Подпись | debug keystore (стандартный) | release keystore |
| Магазины | Не публиковать | RuStore и др. |

## Keystore (release)

- Keystore **не коммитить** в репозиторий.
- Хранить в GitHub Secrets, например:
  - `KEYSTORE_BASE64` (или файл через secret)
  - `KEYSTORE_PASSWORD`
  - `KEY_ALIAS`
  - `KEY_PASSWORD`
- Один и тот же keystore использовать для всех последующих обновлений в RuStore / других маркетах (смена ключа ломает обновления).
- При первом релизе:
  1. Если keystore ещё нет — сгенерировать, отдать человеку пароли/файл **вне репозитория**, записать secrets в GitHub.
  2. Настроить signingConfigs в Gradle и шаг подписи в Actions.
  3. Собрать release-артефакт с versionName `1.0` (или указанной человеком).
- Не писать пароли keystore в чат, в код, в README, в STATUS.

## GitHub Actions

- Workflow в `.github/workflows/` (например `build.yml`).
- Триггеры: push в основную ветку и/или `workflow_dispatch`.
- Результат: Artifact с правильным именем файла; при релизе — по желанию GitHub Release.
- В `PROJECT.md` кратко фиксируй: как называется workflow, какая текущая versionName / versionCode.

## Версии в STATUS / PROJECT

- Текущую `versionName` и `versionCode` держи в `PROJECT.md` (или в STATUS, если удобнее человеку).
- После каждой значимой сборки обновляй номер (0.1 → 0.2 → …).
