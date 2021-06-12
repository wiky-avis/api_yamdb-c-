# REST API Yamdb – база отзывов пользователей о произведениях.

## Описание:
Реализован пользовательский функционал дающий возможность пользоваться приложением не посещая сайт:
1.	Пользовательские роли:
  * Аноним — может просматривать описания произведений, читать отзывы и комментарии.
  * Аутентифицированный пользователь (user)— может читать всё, как и Аноним, дополнительно может публиковать отзывы и ставить рейтинг произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы и ставить им оценки; может редактировать и удалять свои отзывы и комментарии.
  * Модератор (moderator) — те же права, что и у Аутентифицированного пользователя плюс право удалять и редактировать любые отзывы и комментарии.
  * Администратор (admin) — полные права на управление проектом и всем его содержимым. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям.
  * Администратор Django — те же права, что и у роли Администратор.
2.	Система регистрации пользователей
  * Пользователь отправляет POST-запрос с параметром email на /api/v1/auth/email/.
  * YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на адрес email.
  * Пользователь отправляет POST-запрос с параметрами email и confirmation_code на /api/v1/auth/token/, в ответе на запрос ему приходит token(JWT-токен).
  * После регистрации и получения токена пользователь может отправить PATCH-запрос на /api/v1/users/me/ и заполнить поля в своём профайле.
3.	Ресурсы API YaMDb
  * Ресурс AUTH: аутентификация.
  * Ресурс USERS: пользователи.
  * Ресурс TITLES: произведения, к которым можно написать отзыв.
  * Ресурс CATEGORIES: категории (типы) произведений («Фильмы», «Книги», «Музыка»).
  * Ресурс GENRES: жанры произведений.
  * Ресурс REVIEWS: отзывы на произведения.
  * Ресурс COMMENTS: комментарии к отзывам.
4.	Рейтинги произведений.

Документация к API доступна по адресу http://localhost:8000/redoc/

## Установка:
Клонируем репозиторий на локальную машину:
```$ git clone https://github.com/netshy/api_final_yatube.git```

Создаем виртуальное окружение:
```$ python -m venv venv```

Устанавливаем зависимости:
```$ pip install -r requirements.txt```

Создание и применение миграций:
```$ python manage.py makemigrations``` и ```$ python manage.py migrate```

Создаем суперпользователя:
```$ python manage.py createsuperuser --email admin@test.com --username admin```

Запускаем django сервер:
```$ python manage.py runserver```

## Примеры запросов к API:
Для формирования ответов и запросов будет использовано расширение для VS Code [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client).

Расширение REST Client позволяет прямо из VS Code отправлять HTTP-запросы, и в этом же интерфейсе просматривать ответы на них. Установка расширения стандартна: в строке поиска панели "Extensions" нужно ввести название плагина "REST Client" и нажать кнопку "Install" («Установить»).

Запросы в REST Client нужно сохранять в файле с расширением .http. После установки создайте в VS Code новый файл (например requests.http). Запросы в файле отделяются друг от друга строками, содержащими три символа #.

Для отправки любого запроса нажмите над ним ссылку "SendRequest". В правой части экрана вы увидите ответ сервера:

![GitHub Logo](/images/окно_вскод.jpg)

