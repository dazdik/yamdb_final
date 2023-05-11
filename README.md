# yamdb_final
[![Django-app workflow](https://github.com/dazdik/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)](https://github.com/dazdik/yamdb_final/actions/workflows/yamdb_workflow.yml)

## Автор:

💻 [dazdik](https://github.com/dazdik)

![Alt-текст](https://boxboat.com/2017/06/28/whats-new-in-docker-17-06/featured.png "Кит по имени Docker")



## Описание проекта REST API для YaMDb

Создан на основе фреймворка [Django REST Framework (DRF)](https://github.com/ilyachch/django-rest-framework-rusdoc)


Проект YaMDb собирает отзывы пользователей о произведениях. Работы разделены на категории: «Книги», «Фильмы», «Музыка». [Ссылка](https://github.com/dazdik/api_yamdb) на репозиторий с проектом.

____

## Технологии:

- Python 3
- DRF (Django REST framework)
- Django ORM
- Docker
- Gunicorn
- Nginx
- Django 3.2
- PostgreSQL
- GIT
___
## Запуск проекта 🚀

1. Клонировать репозиторий и сделать его ***fork***:

```
https://github.com/dazdik/yamdb_final
```

![Alt-текст](https://arduinoplus.ru/wp-content/uploads/2020/10/git-fork-1.jpg)

2. Перейти в директорию  ```cd infra``` и создать файл .env, заполнить его по следующему примеру:

```
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД
```
3. Выполнить вход на удаленный сервер
```bash
ssh <username>@<ip_сервера>
```
4. Устанавливаем на сервере docker-compose:
```
sudo curl -SL https://github.com/docker/compose/releases/download/v2.17.2/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
```

```bash
chmod +x /usr/local/bin/docker-compose
```

5. Скопировать на сервер файлы docker-compose.yaml и default.conf:
```
scp docker-compose.yaml <username>@<ip_сервера>:/home/<username>/
```
```
scp default.conf <username>@<ip_сервера>:/home/<username>/nginx/
```
 6. Создать secrets в своем репозитории:
   - Перейдите в настройки репозитория **Settings**, выберите на панели слева **Secrets**, нажмите **New secret**
   - Сохраните переменные из таблицы ниже с необходимыми значениями: задайте имя секрета и его значение, затем нажмите **Add secret**:
![Alt-текст](https://docs.github.com/assets/cb-28266/mw-1440/images/help/repository/repo-actions-settings.webp)
![Alt-текст](https://docs.github.com/assets/cb-62141/mw-1440/images/help/repository/actions-secrets-tab.webp)


| Имя секрета| Значение |
| ------------- | ------------- |
| DB_ENGINE  |django.db.backends.postgresql  |
| DB_NAME  | DB_NAME  |
| POSTGRES_USER  | postgres  |
| POSTGRES_PASSWORD  | postgres  |
| DB_HOST  | db  |
| DB_PORT  | 5432 |
|  DOCKER_PASSWORD  | Пароль от аккаунта на DockerHub |  
|  DOCKER_USERNAME  | Username в аккаунте на DockerHub |  
|  HOST  | IP удалённого сервера |      
|    USER | Логин на удалённом сервере |
|    SSH_KEY | SSH-key компьютера, с которого будет происходить подключение к удалённому серверу|
|    PASSPHRASE| *Если для ssh используется фраза-пароль* |
|    TELEGRAM_TO| ID пользователя в Telegram |
|    TELEGRAM_TOKEN | ID бота в Telegram |
____

7. Выполнить команды:
```
git add .
git commit -m 'здесь должна быть ваша реклама'
git push
```

После этого будут запущены процессы **workflow**:

 - проверка кода на соответствие стандарту PEP8 (с помощью пакета flake8) - запуск pytest
 - сборка и доставка докер-образа для контейнера web на Docker Hub
 - автоматический деплой проекта на боевой сервер
 - отправка уведомления в Telegram о том, что процесс деплоя успешно завершился


