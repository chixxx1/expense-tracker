# Expense Tracker API

RESTful API сервис для учета личных финансов. Позволяет отслеживать доходы и расходы, управлять категориями, устанавливать бюджеты и получать финансовые отчеты.

## 📋 Содержание

- [Технологии](#-технологии)
- [Установка и запуск](#-установка-и-запуск)
- [API Endpoints](#-api-endpoints)
  - [Категории](#категории)
  - [Транзакции](#транзакции)
  - [Бюджеты](#бюджеты)
  - [Отчеты](#отчеты)

## 🚀 Технологии

- **Go 1.25.4** - основной язык разработки
- **Gin Web Framework** - HTTP роутинг и middleware
- **JSON файлы** - хранение данных (встроенное решение)
- **Встроенная синхронизация** - потокобезопасные операции с данными

## 🔧 Установка и запуск

### Предварительные требования

- Go 1.21 или выше
- Git

### Установка

1. Клонируйте репозиторий:

```bash
git clone https://github.com/chixxx1/expense-tracker.git
cd expense-tracker
```

Установите зависимости:

```bash
go mod download
```

Запустите приложение:

```bash
go run cmd/api/main.go
```

Сервер запустится на http://localhost:8080

## 📚 API Endpoints

### Категории

Получить все категории

```http
GET /categories
```

Получить категорию по ID

```http
GET /categories/:id
```

Создать категорию

```http
POST /categories
Content-Type: application/json
{
"name": "Продукты",
"type": "expense",
"color": "#FF6B6B",
"icon": "🛒"
}
```

Обновить категорию

```http
PUT /categories/:id
Content-Type: application/json
{
"name": "Супермаркеты",
"type": "expense",
"color": "#FF6B6B",
"icon": "🏪"
}
```

Удалить категорию

```http
DELETE /categories/:id
```

### Транзакции

Получить транзакции с фильтрацией

```http
GET /transactions?start_date=2024-01-01&end_date=2024-01-31&type=expense&category_id=1&limit=10&offset=0
```

Параметры фильтрации:

    start_date - начало периода (YYYY-MM-DD)

    end_date - конец периода (YYYY-MM-DD)

    category_id - ID категории

    type - тип транзакции (income или expense)

    payment_method - метод оплаты (cash, card, transfer)

    limit - количество записей

    offset - смещение для пагинации

Получить транзакцию по ID

```http
GET /transactions/:id
```

Создать транзакцию

```http
POST /transactions
Content-Type: application/json
{
"amount": 1500.50,
"type": "expense",
"category_id": 1,
"date": "2024-01-15T10:30:00Z",
"description": "Продукты в супермаркете",
"payment_method": "card"
}
```

Обновить транзакцию

```http
PUT /transactions/:id
Content-Type: application/json
{
"amount": 1600.00,
"type": "expense",
"category_id": 1,
"date": "2024-01-15T10:30:00Z",
"description": "Продукты и бытовая химия",
"payment_method": "card"
}
```

Удалить транзакцию

```http
DELETE /transactions/:id
```

### Бюджеты

Получить бюджеты с фильтрацией

```http
GET /budgets?category_id=1&period=monthly&month=2024-01
```

Получить бюджет по ID

```http
GET /budgets/:id
```

Создать бюджет

```http
POST /budgets
Content-Type: application/json
{
"category_id": 1,
"amount": 30000,
"period": "monthly",
"month": "2024-01-01T00:00:00Z"
}
```

Обновить бюджет

```http
PUT /budgets/:id
Content-Type: application/json
{
"category_id": 1,
"amount": 35000,
"period": "monthly",
"month": "2024-01-01T00:00:00Z"
}
```

Удалить бюджет

```http
DELETE /budgets/:id
```

### Отчеты

Финансовый отчет за период

```http
GET /reports/financial?start_date=2024-01-01&end_date=2024-01-31
```

Отчет по категориям за период

```http
GET /reports/categories?start_date=2024-01-01&end_date=2024-01-31
```

Отчет по бюджету

```http
GET /reports/budgets/:id
```
