# Курсовой проект по предмету ML/DLOps.
---
Подготовил: Панфилов Михаил Алексеевич

## Окружение

В проекте используется менеджер пакетов uv. 
Команды инициализации окружения и регистрация ядра для jupyter:
```bash
    uv venv --python 3.11
    source .venv/bin/activate
    uv pip install jupyterlab ipykernel pandas boto3
    python -m ipykernel install --user --name mlops26
```

## Данные

Источник: Inside Airbnb Лондон  снимок за март 2026
Файл: s3://mlops26-course-bucket/prepared/train.csv
Хранилище: Yandex Object Storage, endpoint https://storage.yandexcloud.net, регион ru-central1.

## Ключи доступа

1. Создайть в корне репозитория файл secretkeys.py с двумя переменными
    
    ```python
    KEY_ID = "..."
    ACCESS_KEY = "..."
    ```
Файл указан в .gitignore

## Локальная копия данных

Запасная копия того же CSV должна лежать в data/train.csv. В git ее нет.
Скачать ее можно в ноутбуке, если добавить временную ячейку после ячейки с настройками:

    LOCAL_PATH.parent.mkdir(exist_ok=True)
    s3.download_file(S3_BUCKET, S3_KEY, str(LOCAL_PATH))

## Запуск

```bash
    source .venv/bin/activate
    jupyter lab
```

1. Открыть 01_read_data.ipynb
2. Выбрать ядро mlops26
3. Выполните ячейки сверху вниз
