# YaMDb

![example workflow](https://github.com/v-holodov/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
![example workflow](https://github.com/v-holodov/foodgram-project/actions/workflows/fg_workflow.yml/badge.svg)


## Описание
**YaMDb** - это REST API для проекта по сбору отзывов пользователей на произведения в категориях "Книги", "Фильмы" и "Музыка". Пользователи оставляют к произведениям текстовые отзывы и выставляют произведению рейтинг (оценку в диапазоне от одного до десяти). Из множества оценок автоматически высчитывается средняя оценка произведения.

## Технологии
В проекте используются следующие основные пакеты:
- Python 3.7
- Django 3.0.5
- Django REST framework 3.11.0  
- Djangorestframework-simplejwt 4.6.0
- Gunicorn 20.0.4
- Psycopg2-binary 2.8.5
- Docker  20.10.5
- Nginx 1.19.9
- PostgreSQL 12.6


## Установка
Проект YaMDb развертывается в трёх docker-контейнерах с использованием WSGI-сервера Gunicorn и HTTP-сервера Nginx.


Для начала склонируйте репозиторий командой 
```bash
git clone https://github.com/V-Holodov/infra_sp2.git
```
Создайте файл .env с переменными окружения для работы с базой данных:
```
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД 
```
Для запуска приложения выполните развертывание контейнеров в фоновом режиме командой:
```bash
docker-compose up -d --build 
```
Для запуска миграций выполните команды:
```bash
docker-compose exec web python manage.py makemigrations
docker-compose exec web python manage.py migrate --noinput
```
Создать суперпользователя необходимо командой:
```bash
docker-compose exec web python manage.py createsuperuser
```
После этого необходимо собрать статику командой:
```bash
docker-compose exec web python manage.py collectstatic --no-input
```
Проверьте развертывание, перейдя по адресу:
[http://127.0.0.1/admin/](http://127.0.0.1/admin/)

Для применения фикстур для заполнения базы начальными данными можно выполнить команду:
```bash
docker-compose exec web python manage.py loaddata fixtures.json
```
## Документация API
Документация API доступна по адресу [http://127.0.0.1/redoc/](http://127.0.0.1/redoc/)

## Об авторе
Проект подготовлен выпускником бэкенд-факультета Яндекс-Практикума [Виталием Холодовым ](https://www.linkedin.com/in/v-holodov/).
