# api_final
## **Описание проекта**
«API для Yatube» представляет собой реализацию API для проекта «Yatube» – социальной сети, где пользователи делятся своими историями и мыслями, общаются в комментариях и имеют возможность отслеживать публикации интересных им авторов.
Проект «Yatube» реализован на Django, в свою очередь «API для Yatube» реализован с использованием библиотеки Django REST Framework (DRF).
DRF мощный и гибкий инструмент для построения Web API, который имеет следующие преимущества:
* Крайне удобная для разработчиков браузерная версия API;
* Наличие пакетов для OAuth1a и OAuth2 авторизации;
* Сериализация, поддерживающая ORM и не-ORM источники данных;
* Возможность полной и детальной настройки - можно использовать обычные представления-функции, если вы не нуждаетесь в мощном функционале;
* Расширенная документация и отличная поддержка сообщества.<br/>

Через API Yatube можно публиковать посты, подписываться на авторов, отслеживать посты авторов, на которых Вы подписаны (и тех, на кого не подписаны – тоже), отслеживаться новые комментарии к своим постам и многое другое.



## **Как запустить проект**
Клонировать репозиторий и перейти в него в командной строке:
```
git clone https://github.com/slapeach/api_final_yatube.git
```
```
cd api_final_yatube
```

Cоздать виртуальное окружение:
```
python3 -m venv env
```
На Windows:
```
python -m venv venv
```
Активировать виртуальное окружение:
```
source env/bin/activate
```
На Windows:
```
source venv/Scripts/activate
```

Установить зависимости из файла requirements.txt:
```
python3 -m pip install --upgrade pip
```
На Windows:
```
python -m pip install --upgrade pip
```
```
pip install -r requirements.txt
```

Выполнить миграции:
```
python3 manage.py migrate
```
На Windows:
```
python manage.py migrate
```

Запустить проект:
```
python3 manage.py runserver
```
На Windows:
```
python manage.py runserver
```


## **Примеры запросов**


**Пример создания нового пользователя**<br/>

Для создания нового пользователя отправьте POST-запрос на …/auth/users/ с указанием имени пользователя и пароля.
```
POST /auth/users/
```
```
{
    "username" : "newuser",
    "password" : "passwordWgr32!3lk"
}
```
<br/>

**Получение JWT-токена**

Для получения JWT-токена необходимо отправить POST-запрос на …/auth/jwt/create/ с именем пользователя и паролем, указанными при создании пользователя.
```
POST /auth/jwt/create/
```
```
{
    "username" : "newuser",
    "password" : "passwordWgr32!3lk"
}
```
Будет получен ответ следующего вида:
```
{
    "refresh": "string",
    "access": "string"
}
```
Токен, необходимый для дальнейшей работы, лежит в поле “access”. Данные из “refresh” потребуется для обновления “access”-токена, если он был утерян или украден. 
<br/>

**Обновление JWT-токен**

Отправьте POST-запрос на …/auth/jwt/refresh/ с указанием данных из поля “refresh”, полученных ранее.

```
POST /auth/jwt/refresh/
```
```
{
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTYyMDk0MTQ3NywianRpIjoiODUzYzE5MTg5NzMwNDQwNTk1ZjI3ZTBmOTAzZDcxZDEiLCJ1c2VyX2lkIjoxfQ.0vJBPIUZG4MjeU_Q-mhr5Gqjx7sFlO6AShlfeINK8nA"
}
```
<br/>

**Проверка JWT-токен**
```
POST /auth/jwt/verify/
```
```
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjIwODU1Mzc3LCJqdGkiOiJkY2EwNmRiYTEzNWQ0ZjNiODdiZmQ3YzU2Y2ZjNGE0YiIsInVzZXJfaWQiOjF9.eZfkpeNVfKLzBY7U0h5gMdTwUnGP3LjRn5g8EIvWlVg"
}
```
<br/>

**Подписка на пользователя**
```
POST /api/v1/follow/
```
```
{
    "following": "testuser"
}
```
<br/>

**Пример поиска по подпискам**
```
GET /api/v1/follow?search=testuser
```
<br/>

**Пример добавления нового поста**
```
POST /api/v1/posts/
```
```
{
    "text": "Тестовый текст",
    "group": 1
}
```
<br/>

**Получение списка всех постов**

```
GET /api/v1/posts/
```
<br/>

**Получение трех записей, с третьей по пятую (или меньше, если в результате запроса менее 5 записей)**
```
GET /api/v1/posts/?limit=3&offset=2
```
<br/>

**Пример добавления нового комментария к посту с id=1**
```
POST /api/v1/posts/1/comments/
```
```
{
    "text": "тест тест"
}
```
<br/>

**Удаление комментария с id=1 к посту c id=2**
```
DELETE /api/v1/posts/2/comments/1/
```
<br/>

**Пример получения информации о группе**
```
GET /api/v1/groups/1/
```
