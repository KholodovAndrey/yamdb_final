# API для Yamdb
Проект API для Yamdb является учебным, в рамках курса Яндекс "Python-разработчик"


![example workflow](https://github.com/KholodovAndrey/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

### Описание проекта API для Yamdb

Проект YaMDb собирает отзывы пользователей на различные произведения.
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка».
Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»).
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.
Пользователи могут оставлять комментарии к отзывам.
Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.

В данном проекте реализован REST API для проекта Yamdb, данные передаются в формате JSON.
Аутентификация по JWT-токену.

### Стек технологий

- проект написан на Python с использованием Django REST Framework
- библиотека Simple JWT - работа с JWT-токеном
- библиотека django-filter - фильтрация запросов
- базы данных - SQLite3, PostgresSQL
- система управления версиями - git
- система контейнеризации - Docker

## Развертывание проекта

Клонировать репозиторий и перейти в него в командной строке:

```
git clone git@github.com:KholodovAndrey/infra_sp2.git
```

```
cd api_yamdb
```

Создайте .env файл в директории infra/, в котором должны содержаться следующие переменные:
```
DB_ENGINE=django.db.backends.postgresql
DB_NAME= # название БД\ POSTGRES_USER= # ваше имя пользователя
POSTGRES_PASSWORD= # пароль для доступа к БД
DB_HOST=db
DB_PORT=5432\
SECRET_KEY= # секретный код от проекта из settings.py
```

### Как запустить проект локально:

Cоздать и активировать виртуальное окружение:

```
py -3.9 -m venv env - создание виртуального окружения(Windows)
python3 -m venv venv - создание виртуального окружения(linux, macOS)
```

```
source env/Scripts/activate - активация виртуального окружения(Windows)
source venv/bin/activate - активация виртуального окружения(linux, macOS)
```

Установить зависимости из файла requirements.txt:

```
python -m pip install --upgrade pip - Обновление менеджера пакетов PIP(Windows)
python3 -m pip install --upgrade pip - Обновление менеджера пакетов PIP(linux, macOS)
```

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python manage.py migrate (Windows)
python3 manage.py migrate (linux, macOS)
```

Импортировать базу данных:

```
python manage.py csv_to_bd (Windows)
python3 manage.py csv_to_bd (linux, macOS)
```

Запустить проект:

```
python manage.py runserver - Запуск локального сервера(Windows)
python3 manage.py runserver - Запуск локального сервера(linux, macOS)
```

Создать суперпользователя для управления узлом администрирования:

```
python manage.py createsuperuser - (Windows)
python3 manage.py createsuperuser - (linux, macOS)
```

#### Примеры запросов
Пример POST-запроса на регистрацию нового пользователя: POST .../api/v1/auth/signup/
```
{
"email": "user@example.com",
"username": "string"
}
```
Пример ответа на GET-запрос на получение списка всех произведений: GET .../api/v1/titles/
```
{
"count": 0,
"next": "string",
"previous": "string",
"results": [
{
"id": 0,
"name": "string",
"year": 0,
"rating": 0,
"description": "string",
"genre": [
{
"name": "string",
"slug": "string"
}
],
"category": {
"name": "string",
"slug": "string"
}
}
]
}
```


Ресурсы API YaMDb
- auth: аутентификация.
- users: пользователи.
- titles: произведения, к которым пишут отзывы.
- categories: категории (типы) произведений («Фильмы», «Книги», «Музыка»). Одно произведение может быть привязано только к одной категории.
- genres: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.
- reviews: отзывы на произведения. Отзыв привязан к определённому произведению.
- comments: комментарии к отзывам. Комментарий привязан к определённому отзыву.


### Запуск проекта через сервер

Перейдите в папку проекта и выполните команду:

docker-compose up -d --build
При первом запуске для функционирования проекта выполните команды:

docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input

Заполните базу начальными данными

docker-compose exec web python manage.py loaddata fixtures.json


Более подробно информацию об эндпоинтах и примерах запросов и ответов можно посмотреть в
```
/api_yamdb/api_yamdb/static/redoc.yaml
```
