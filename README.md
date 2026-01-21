# DjangoAuth
# Django Auth API

REST API для аутентифікації користувачів з JWT токенами.

## Технології

- Python 3.13
- Django 6.0
- Django REST Framework
- PyJWT
- SQLite

## Встановлення

```bash
# Клонувати репозиторій
git clone https://github.com/your-username/DjangoAuth.git
cd DjangoAuth

# Створити віртуальне середовище
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Встановити залежності
pip install -r requirements.txt

# Застосувати міграції
python manage.py migrate

# Запустити сервер
python manage.py runserver
```

## API Endpoints

| Метод | URL | Опис |
|-------|-----|------|
| POST | `/api/register/` | Реєстрація нового користувача |
| POST | `/api/login/` | Вхід (повертає JWT токен) |
| GET | `/api/user/` | Отримати поточного користувача |
| POST | `/api/logout/` | Вийти з системи |

## Приклади запитів

### Реєстрація

```bash
curl -X POST http://localhost:8000/api/register/ \
  -H "Content-Type: application/json" \
  -d '{
    "username": "john",
    "email": "john@example.com",
    "password": "securepassword123"
  }'
```

**Відповідь:**
```json
{
  "id": 1,
  "username": "john",
  "email": "john@example.com"
}
```

### Вхід

```bash
curl -X POST http://localhost:8000/api/login/ \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "securepassword123"
  }'
```

**Відповідь:**
```json
{
  "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### Отримати користувача

```bash
curl http://localhost:8000/api/user/ \
  --cookie "jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

**Відповідь:**
```json
{
  "id": 1,
  "username": "john",
  "email": "john@example.com"
}
```

## Структура проєкту

```
DjangoAuth/
├── auth/                   # Налаштування Django
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── users/                  # Додаток користувачів
│   ├── models.py          # Кастомна модель User
│   ├── serializers.py     # Серіалізатори DRF
│   ├── views.py           # API views
│   └── urls.py            # URL маршрути
├── manage.py
├── requirements.txt
└── README.md
```

## Модель користувача

Використовується кастомна модель `User` з аутентифікацією по email:

```python
class User(AbstractUser):
    email = models.EmailField(unique=True)
    
    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = ['username']
```

## Автор

MatviiT

## Ліцензія

MIT