# MVP Blog

## Цель:

Написать API для приложения блог, где пользователи могут писать статьи и делиться со своими подписчиками.

## Основные Требования:

- Python 3.10
- Django 4.1.1
- DRF 3.12.4
- SQLite

## Этап 1. Models.

### Создать модели:

1. Кастомную модель `User` [(link)](https://docs.djangoproject.com/en/4.1/topics/auth/customizing/#auth-custom-user)
2. `Post` _с отношением (User - Post)_
3. `Like` _с отношениями (User - Like - Post)_
4. `Comment` _с отношением (User - Comment - Post)_

### Поля моделей:

#### User:
- `email: str` *
- `password: str` *
- `username: str`

_Сделать `username` не обязательным, а `email` обязательным._

#### Post:
- `user: foregin-key to User` *
- `title: str` *
- `description: str` *
- `text: text` *

#### Like:
- `user: foregin-key to User` *
- `post: foregin-key to Post` *

#### Comment:
- `user: foregin-key to User` *
- `post: foregin-key to Post` *
- `text: text` *

**!!! Не забудь про миграции.**

## Этап 2. Endpoints.

1. Сделать **Сериализаторы** для созданых моделей [(link)](https://www.django-rest-framework.org/api-guide/serializers/)
2. Сделать **CRUD** для созданых моделей с использованием **ViewSets** [(link)](https://www.django-rest-framework.org/api-guide/viewsets/)
3. Сделать **JWT** авторизацию [(link)](https://www.django-rest-framework.org/api-guide/authentication/#json-web-token-authentication)
4. Ограничить доступ на добавление лайка к посту, коммента не авторизованым юзерам.
5. Добавить ограничения, чтобы юзер не мог изменить данные другого юзера.

## Этап 3. Improvements.

- Добавить возможность **автоудаления поста** с использованием `Celery`
- Добавить возможность **отложеного поста** с использованием `Celery`
- Написать `Middleware` которая при возникновении ошибки в приложении будет отправлять ошибку в телеграм админу(ам), и на почту. [link](https://docs.djangoproject.com/en/4.1/topics/http/middleware/)
- Добавить **пагинацию** для постов, комментов. [link](https://www.django-rest-framework.org/api-guide/pagination/)
- Добавить **фильтрацию** для постов, комментов. [link](https://www.django-rest-framework.org/api-guide/filtering/)
- Сделать ендпоинты в виде `/api/v1/posts` или `/api/v1/comments` и т.д.

## Этап 4. Docker.

1. Сделать `Dockerfile` для API приложения
2. Сделать `docker-compose.yml` в котором должны жить api, postgres, redis, celery.
