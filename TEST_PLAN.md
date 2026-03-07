# API Testing – Wishlist Service
## Цель тестирования
Проверить корректность работы REST API сервиса Wishlist:
- корректность HTTP методов
- статус-коды ответов
- структура JSON ответа
- валидация входных данных
- авторизация пользователей
API: https://api.wishlist.otus.kartushin.su
---
# Объекты тестирования
Основные группы эндпоинтов:
1. Authentication
- POST /api/auth/register
- POST /api/auth/login
2. Wishlists
- GET /api/wishlists
- POST /api/wishlists
- GET /api/wishlists/{id}
- PUT /api/wishlists/{id}
- DELETE /api/wishlists/{id}
3. Gifts
- GET /api/gifts/{id}
- PUT /api/gifts/{id}
- DELETE /api/gifts/{id}
- PUT /api/gifts/{id}/reserve
4. Gifts in wishlist
- GET /api/gifts/wishlist/{wishListId}
- POST /api/gifts/wishlist/{wishListId}
---
# Тестовые сценарии
## 1 Регистрация пользователя
### Позитивный
POST /api/auth/register
Body:
{
"username": "testuser123",
"email": "test123@mail.com
",
"password": "12345678"
}
Ожидаемый результат
- Status 200
- пользователь создан
---
### Негативный
1. Пароль меньше 6 символов
2. Пустой username
3. Некорректный email
Ожидаемый результат
- Status 400
---
## 2 Авторизация
POST /api/auth/login
Позитивный:
{
"username": "testuser123",
"password": "12345678"
}
Ожидаемый результат
- Status 200
- возвращается JWT token
---
Негативный
- неправильный пароль
- несуществующий пользователь
Ожидаемый результат
- 401
---
## 3 Создание списка желаний
POST /api/wishlists
Позитивный
{
"title": "Birthday",
"description": "Birthday gifts"
}
Ожидаемый результат
- 200
- возвращается созданный wishlist
---
Негативный
- пустой title
Ожидаемый результат
- 400
---
## 4 Получение списка желаний
GET /api/wishlists
Позитивный
- статус 200
- возвращается массив wishlist
---
Негативный
- отсутствует token
Ожидаемый результат
- 401
---
## 5 Создание подарка
POST /api/gifts/wishlist/{wishListId}
Позитивный
{
"name": "iPhone",
"description": "New phone",
"price": 1000
}
Ожидаемый результат
- 200
- gift создан
---
Негативный
- price отсутствует
- name пустой
Ожидаемый результат
- 200
- gift создан
---
Негативный
- price отсутствует
- name пустой
