# DjangoAuth — REST API з JWT авторизацією

## Опис

Це бекенд на Django + Django REST Framework з кастомним User, JWT-авторизацією (SimpleJWT) та endpoint-ами для реєстрації, логіну, логауту й отримання інформації про користувача.

---

## Основні можливості

- Реєстрація користувача: `/api/register/`
- Логін (отримання JWT): `/api/login/`
- Логаут (blacklist refresh-токена): `/api/logout/`
- Отримання/оновлення JWT: `/api/token/`, `/api/token/refresh/`
- Перегляд/редагування користувачів: `/api/users/`
- Отримання своїх даних: `/api/users/me/`

---

## Швидкий старт

1. **Клонувати репозиторій та встановити залежності**
    ```bash
    git clone <repo_url>
    cd DjangoAuth
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    ```

2. **Налаштувати .env**
    ```
    DEBUG=True
    DB_NAME=djangoauth
    DB_USER=postgres
    DB_PASSWORD=yourpassword
    DB_HOST=localhost
    DB_PORT=5432
    SECRET_KEY=your-secret-key
    ```

3. **Міграції та запуск**
    ```bash
    python3 manage.py migrate
    python3 manage.py createsuperuser
    python3 manage.py runserver
    ```

---

## Використання API

### Реєстрація
`POST /api/register/`
```json
{
  "email": "user@example.com",
  "name": "User Name",
  "password": "StrongPassword123"
}
```

### Логін
`POST /api/login/`
```json
{
  "email": "user@example.com",
  "password": "StrongPassword123"
}
```
**Відповідь:**
```json
{
  "refresh": "<refresh_token>",
  "access": "<access_token>"
}
```

### Логаут
`POST /api/logout/`
```json
{
  "refresh": "<refresh_token>"
}
```
**Headers:**  
`Authorization: Bearer <access_token>`

### Отримати свої дані
`GET /api/users/me/`  
**Headers:**  
`Authorization: Bearer <access_token>`

---

## Технології

- Django 4+
- Django REST Framework
- SimpleJWT
- PostgreSQL

---

## Для фронтенду

- Авторизація через JWT (Bearer Token)
- Всі відповіді — JSON
- Для доступу до захищених endpoint-ів потрібен access-токен

---

## Ліцензія

MIT
