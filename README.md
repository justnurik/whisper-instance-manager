## English

### Description

This project is a component of [tg-bot-voice-to-text](https://github.com/justnurik/tg-bot-voice-to-text). It is designed to quickly launch the Whisper model from OpenAI.

This repository helps you quickly spin up:

* A local Whisper model instance in Docker.

To simplify setup, there's a script to generate all necessary configuration files. You only need to:

* Fill in a global config `config.yml`
* Provide one or more model configs in the `configs/` folder.

### Getting Started

#### 1. Fill out the configuration files

`config.yml` – global project configuration:

```yaml
download_directory: downloads  # Directory for audio file downloads
log_directory: logs             # Directory for storing logs
```

`configs/1.yml` – individual model configuration:

```yaml
type: local               # Type of model (e.g., 'local' for Whisper)
port: 6029                # Port for the model FastAPI server
name: model_1             # Unique name of the instance
log_level: DEBUG          # Logging level for this instance
log_file: model_1.log     # Path to log file
prometheus_port: 8000     # Prometheus metrics endpoint port for this instance
model_size: medium        # Whisper model size (tiny, base, small, medium, large)
```

#### 2. Generate Docker configs

```bash
python generate.py
```

#### 3. Start the model services in the background

```bash
docker-compose up --build -d
```

#### 4. Wait a moment until all services are up

### Advanced: Use custom models

You can integrate your own model by:

1. Subclassing the `Model` interface in `src/model.py`
2. Adding logic to `src/model_factory.py` to support your custom model type (use a `type` field in YAML)
3. Updating your config files accordingly

Then restart the project.

### License

MIT License.

## Русский

### Описание

Этот проект является частью [tg-bot-voice-to-text](https://github.com/justnurik/tg-bot-voice-to-text). Он предназначен для быстрого запуска модели Whisper от OpenAI.

С помощью этого репозитория можно быстро:

* Запустить модель Whisper в Docker-контейнере.

Для удобства есть скрипт генерации конфигурационных файлов. Вам нужно лишь:

* Заполнить глобальный конфиг `config.yml`
* Указать, какие модели запускать – в виде файлов `configs/*.yml`

### Как запустить

#### 1. Заполните конфигурационные файлы

`config.yml` — глобальный конфиг:

```yaml
download_directory: downloads  # Каталог загрузок аудио
log_directory: logs             # Каталог для логов
```

`configs/1.yml` — конфигурация конкретной модели:

```yaml
type: local               # Тип модели (например, local – Whisper)
port: 6029                # Порт для FastAPI-сервера модели
name: model_1             # Имя инстанса
log_level: DEBUG          # Уровень логов
log_file: model_1.log     # Файл логов
prometheus_port: 8000     # Порт для метрик Prometheus
model_size: medium        # Размер модели Whisper (tiny, base, small, medium, large)
```

#### 2. Сгенерируйте файлы конфигурации Docker

```bash
python generate.py
```

#### 3. Запустите сервисы модели в фоне

```bash
docker-compose up --build -d
```

#### 4. Подождите немного — сервисы поднимутся

### Расширение: Свои модели

Вы можете добавить собственную модель:

1. Унаследуйтесь от интерфейса `Model` в `src/model.py`
2. Добавьте обработку нового типа модели в `src/model_factory.py`
3. Укажите свой `type` в YAML-конфиге

После этого обновите конфиги и перезапустите проект.

### Лицензия

Проект распространяется по лицензии MIT.
