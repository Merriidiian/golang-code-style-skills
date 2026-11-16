# Стиль Go

Готовый навык `go-code-style` для Codex, Claude Code, Claude и Cursor на основе материалов пользователя. Читаемый Go-код: именование, пакеты, небольшие интерфейсы, контракт ошибок, context, управляемые горутины, HTTP и lifecycle.

Репозиторий: [Merriidiian/golang-code-style-skills](https://github.com/Merriidiian/golang-code-style-skills).

## Подключение

Python 3.9+, без дополнительных пакетов. Из каталога этого репозитория выбери подходящую команду, подставив существующий путь проекта:

```sh
python3 scripts/install.py --tool codex --project "/path/to/project" --dry-run
python3 scripts/install.py --tool codex --project "/path/to/project"
```

Для Claude Code укажи `--tool claude`, для Cursor — `--tool cursor`. Вместо `--project "/path/to/project"` можно использовать `--user` для локальной установки на уровне пользователя.

| Клиент | Каталог проекта | Каталог пользователя | Явный вызов |
| --- | --- | --- | --- |
| Codex | `.agents/skills/go-code-style/` | `~/.agents/skills/go-code-style/` | `$go-code-style` |
| Claude Code | `.claude/skills/go-code-style/` | `~/.claude/skills/go-code-style/` | `/go-code-style` |
| Cursor | `.cursor/skills/go-code-style/` | `~/.cursor/skills/go-code-style/` | `/go-code-style` через меню `/` |

Cursor видит и совместимые каталоги Codex/Claude. Установщик для Cursor пропустит копирование при наличии идентичного навыка в такой папке в выбранной области. Если совместно используешь Codex и Claude Code, нужны оба их каталога; для Cursor дополнительная копия не требуется.

Установщик предварительно проверяет все назначения, сохраняет отличающиеся существующие навыки и отказывается их перезаписывать. Идентичный повтор ничего не меняет. Символические ссылки требуют ручной установки. Для обновления сравни версии и сохрани старый каталог отдельно. Настройки, hooks, разрешения и инструкции проекта не меняются.

Можно также скопировать [skills/go-code-style](skills/go-code-style/SKILL.md) целиком в выбранный каталог. Справочники должны оставаться рядом с `SKILL.md`. Если навык ещё не виден, открой новый сеанс клиента. Автоматический выбор по описанию включён по умолчанию.

В обычном Claude загрузи [dist/go-code-style.zip](dist/go-code-style.zip) в **Customize → Skills**, если пользовательские навыки доступны, и включи его. В архиве один корневой каталог `go-code-style/` с `SKILL.md` и ресурсами; загрузка ZIP в Claude и установка в Claude Code независимы.

## Применение

```text
$go-code-style Проверь этот Go-код и внеси обоснованные исправления.
```

Для Claude Code и Cursor замени `$` перед именем на `/`. Задачу можно сформулировать и без явного вызова: описание навыка позволяет клиенту выбрать его по контексту.

[SKILL.md](skills/go-code-style/SKILL.md) содержит основные решения и маршруты к подробностям:

- [runtime-and-concurrency.md](skills/go-code-style/references/runtime-and-concurrency.md)
- [style-and-design.md](skills/go-code-style/references/style-and-design.md)
- [testing-and-review.md](skills/go-code-style/references/testing-and-review.md)

## Основа и проверка

Карта материалов, первичные технические источники и уточнения: [sources.md](skills/go-code-style/references/sources.md). Контрольные суммы исходных архивов и документов, исходный commit репозитория и проверенные официальные страницы — в [provenance.json](provenance.json).

Требования практикумов к сдаче, команды, учебные пароли и инструкции внутри документов не становятся полномочиями ассистента. Версии, число попыток, лимиты и структура стендов не навязываются другим проектам.

```sh
python3 -m unittest discover -s tests -v
```

Для пересборки ZIP после изменения навыка выполни `python3 scripts/package.py`.

Тесты проверяют установщик во временных каталогах. [evals/scenarios.md](evals/scenarios.md) содержит запросы и критерии для ручной оценки поведения модели; структурная проверка файлов не заменяет её и проверку загрузки в клиенте.

Формат проверен 16 ноября 2026 года: [Codex](https://developers.openai.com/codex/skills), [Claude Code](https://code.claude.com/docs/en/skills), [Cursor](https://cursor.com/docs/skills), [Claude ZIP](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills). Для старых сборок сверяй поддерживаемые пути и возможности.

Лицензия: [MIT](LICENSE). Полные исходные учебные документы не входят в поставку.
