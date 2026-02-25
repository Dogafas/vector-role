# Ansible Role: Vector

Роль для установки и настройки [Vector](https://vector.dev/) - высокопроизводительного инструмента для сбора, преобразования и маршрутизации логов и метрик.

## Описание

Роль выполняет следующие действия:
- Скачивает и устанавливает Vector указанной версии
- Создает необходимые директории для конфигурации и данных
- Разворачивает конфигурационный файл из шаблона
- Настраивает systemd unit для управления сервисом
- Запускает и включает Vector в автозагрузку

## Требования

- Ansible >= 2.9
- ОС: Ubuntu (все версии)
- Архитектура: x86_64

## Параметры роли

### Основные параметры

| Параметр | Значение по умолчанию | Описание |
|----------|----------------------|----------|
| `vector_version` | `0.30.0` | Версия Vector для установки |
| `vector_archive_url` | `https://github.com/vectordotdev/vector/releases/download/v{{ vector_version }}/vector-{{ vector_version }}-x86_64-unknown-linux-gnu.tar.gz` | URL для скачивания архива Vector |
| `vector_archive_path` | `/tmp/vector.tar.gz` | Путь для временного хранения архива |
| `vector_extract_path` | `/opt/vector` | Путь для распаковки архива |
| `vector_bin_path` | `/usr/local/bin/vector` | Путь к исполняемому файлу Vector |
| `vector_config_dir` | `/etc/vector` | Директория для конфигурационных файлов |
| `vector_data_dir` | `/var/lib/vector` | Директория для данных Vector |

## Зависимости

Роль не имеет зависимостей от других ролей.

## Пример использования

### Базовое использование

```yaml
- hosts: vector_servers
  roles:
    - vector-role
```

### С переопределением параметров

```yaml
- hosts: vector_servers
  roles:
    - role: vector-role
      vars:
        vector_version: "0.31.0"
        vector_data_dir: "/data/vector"
```

### Playbook с явными параметрами

```yaml
- hosts: vector_servers
  vars:
    vector_version: "0.30.0"
    vector_config_dir: "/etc/vector"
  roles:
    - vector-role
```

## Конфигурация Vector

По умолчанию роль разворачивает базовую конфигурацию Vector:
- **Source**: сбор логов из journald
- **Sink**: вывод в консоль в формате JSON

Для изменения конфигурации отредактируйте шаблон `templates/vector.yml.j2`.

## Handlers

Роль включает handler `Restart vector`, который перезапускает сервис Vector при изменении конфигурации.

## Лицензия

MIT

## Автор

ByteBard
