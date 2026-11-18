# Курсовой проект по предмету ML/DLOps
---
Подготовил: Панфилов Михаил Алексеевич

## Окружение

В проекте используется менеджер пакетов uv. 
Команды инициализации окружения и регистрация ядра для jupyter:
```bash
    uv venv --python 3.11
    source .venv/bin/activate
    uv pip install -r requirements.txt
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

## Ноутбуки

1. 01_read_data.ipynb: чтение CSV из S3
2. 02_training.ipynb: регрессия цены, разбиение, выбираем между Ridge, соседями и деревом по MAE на validation, финальная оценка на test
3. 03_pipeline.ipynb: итоговый Pipeline (ColumnTransformer + Ridge), сохранение в artifacts/model.pkl. Файл model.pkl в git не храним