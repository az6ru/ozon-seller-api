# Ozon Seller API

API для получения информации о товарах и продавцах на Ozon.

## Установка

```bash
# Клонирование репозитория
git clone https://github.com/az6ru/ozon-seller-api.git
cd ozon-seller-api

# Создание виртуального окружения
python -m venv venv
source venv/bin/activate  # для Linux/Mac
# или
venv\Scripts\activate  # для Windows

# Установка зависимостей
pip install -r requirements.txt
```

## Запуск

```bash
uvicorn app.main:app --reload
```

API будет доступно по адресу: http://localhost:8000

Документация API: http://localhost:8000/docs

## Документация

Подробная документация доступна в файле [docs/api_documentation.md](docs/api_documentation.md)

## Структура проекта

```
ozon-seller-api/
├── app/
│   ├── __init__.py
│   ├── main.py          # Основной файл FastAPI приложения
│   ├── parser.py        # Парсер Ozon
│   ├── models.py        # Pydantic модели
│   ├── config.py        # Конфигурация приложения
│   └── dependencies.py  # Зависимости FastAPI
├── docs/
│   └── api_documentation.md  # Документация API
├── tests/
│   └── __init__.py
├── .env.example         # Пример файла с переменными окружения
├── .gitignore          # Игнорируемые файлы Git
├── requirements.txt    # Зависимости проекта
└── README.md          # Документация проекта
```

## Переменные окружения

Создайте файл `.env` на основе `.env.example` и укажите необходимые значения:

```bash
# API Keys (через запятую)
API_KEYS=your_api_key_1,your_api_key_2

# Redis configuration
REDIS_URL=redis://localhost:6379

# Rate limiting
RATE_LIMIT=100

# Cache TTL in seconds (5 minutes)
CACHE_TTL=300
```

## Использование

### Python

```python
import requests

API_KEY = "your_api_key_here"
BASE_URL = "http://localhost:8000"

# Получение списка товаров продавца
response = requests.get(
    f"{BASE_URL}/sellers/1179237/products",
    params={"page": 1, "page_size": 12},
    headers={"X-API-Key": API_KEY}
)
products = response.json()

# Получение информации о товаре
response = requests.get(
    f"{BASE_URL}/products/123456789",
    params={"include_description": True},
    headers={"X-API-Key": API_KEY}
)
product = response.json()
```

### cURL

```bash
# Получение списка товаров продавца
curl -X GET "http://localhost:8000/sellers/1179237/products?page=1&page_size=12" \
     -H "X-API-Key: your_api_key_here"

# Получение информации о товаре
curl -X GET "http://localhost:8000/products/123456789?include_description=true" \
     -H "X-API-Key: your_api_key_here"
```

## Лицензия

MIT