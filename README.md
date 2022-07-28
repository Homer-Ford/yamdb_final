# api_yamdb
![example workflow](https://github.com/Homer-Ford/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

### Описание проекта:

Проект интерфейса API для сайта, который собирает отзывы пользователей на произведения.
Произведения делятся на предустановленные категории и список категорий может быть расширен администратором.
В каждой категории есть произведения и произведению может быть присвоен жанр из списка предустановленных.
Пользователи оставляют к произведениям отзывы и ставят оценку.
Данный проект позволяет с помощью API запросов от разных типов пользователей: получать, создавать, редактировать или удалять отзывы и комментарии к произведениям.
Польза данного проекта заключается в быстроте и удобстве во взаимодействии с информацией на сайте, не заходя на его web страницу.

### Шаблон наполнения env-файла:

DB_ENGINE-в какой СУБД работаем
DB_NAME-имя базы данных
POSTGRES_USER-логин для подключения к базе данных
POSTGRES_PASSWORD-пароль для подключения к БД
DB_HOST-название сервиса (контейнера)
DB_PORT-порт для подключения к БД 
SECRET_KEY-секретный ключ приложения Django

### Описание запуска приложения:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/Homer-Ford/infra_sp2.git
```

```
cd ./infra_sp2/infra
```

Запускаем сборку контейнеров:

```
docker-compose up -d --build 
```

Выполнить миграции:

```
docker-compose exec web python manage.py migrate
```

Создать суперюзера:

```
docker-compose exec web python manage.py createsuperuser
```

Собрать статику:

```
docker-compose exec web python manage.py collectstatic --no-input
```

Для создания резервной копии базы данных:

```
docker-compose exec web python manage.py dumpdata > fixtures.json
```

Для заполнения базы данных из резервной копии:

```
docker-compose exec web python manage.py loaddata dump.json 
```

### Примеры: 

запросы к API начинаются с /api/v1/

Получение списка всех категорий

http://127.0.0.1/api/v1/categories/

Добавление нового отзыва

http://127.0.0.1/api/v1/titles/{title_id}/reviews/

{
"text": "Плохое произведение",
"score": 1
}

Полуение отзыва по id

http://127.0.0.1/api/v1/titles/{title_id}/reviews/{review_id}/

Добавление комментария к отзыву

http://127.0.0.1/api/v1/titles/{title_id}/reviews/{review_id}/comments/

{
"text": "Не советую"
}