# Проект Привычек (Atomic Habit Tracker)
Проект "Atomic Habit Tracker" - это бэкенд-часть веб-приложения для отслеживания и управления личными привычками. Приложение позволяет пользователям создавать, просматривать, редактировать и удалять привычки, а также получать напоминания через Telegram.

## Основные Функции

- **Регистрация и аутентификация пользователей:** Пользователи могут регистрироваться и входить в систему.
- **Управление привычками:** Пользователи могут создавать и управлять своими привычками.
- **Пагинация и фильтрация:** Поддерживается пагинация и фильтрация привычек.
- **Интеграция с Telegram:** Пользователи получают напоминания о привычках через Telegram.

## Начало работы 🚀

**Перед началом убедитесь, что у вас установлено следующее:**

    1. Python версии 3.11 или выше
    2. Poetry для управления зависимостями

## Установка и Запуск

1. **Клонируйте репозиторий:**

    ```bash
    git clone https://github.com/exetch/atomic_habbits.git
    ```

2. **Установите зависимости:**

    ```bash
    poetry install
    ```

3. **Настройте файл .env и переменные окружения 🌐**

    Для корректной работы приложения, необходимо создать файл .env с вашими данными. Вставьте следующие переменные и заполните их значениями:

    ```makefile
    DB_NAME=your_DB_name
    DB_USER=your_DB_user
    DB_PASSWORD=your_DB_password
    DB_HOST=your_DB_host
    DB_PORT=your_DB_port
    TELEGRAM_API_TOKEN=your_API_TOKEN
    ```

3. **Примените миграции:**

    ```bash
    python manage.py migrate
    ```

4. **Настройка и создание суперпользователя 👤**

    Для установки параметров суперпользователя, пароля и email, отредактируйте файл `users/management/commands/create_superuser.py`.
    
    Чтобы создать суперпользователя, выполните следующую команду в командной строке:
    
    ```bash
    python manage.py create_superuser
    ```

5. **Добавление тестовых данных в проект (необязательно)**

    Чтобы создать тестовые данные, выполните следующую команду:

    ```bash
    python manage.py create_users
    ```

6. **Запуск сервера Redis 🔄**

    Сервис использует Redis, поэтому убедитесь, что сервер запущен:

    **Пользователям Linux:**

    ```bash
    sudo service redis-server start
    ```
    **Пользователям Windows:**
    
    Установите и используйте WSL (Подсистему Windows для Linux), затем запустите Redis в вашем дистрибутиве Linux:
    
    ```bash
    sudo service redis-server start
    ```

7. **Запуск Celery Worker**

    Чтобы запустить воркера Celery, используйте следующую команду

    **Пользователям Linux:**
    ```bash
    celery -A config worker -l info
    ```
    **Пользователям Windows:**
    
    ```bash
    celery -A config worker -l info -P eventlet
    ```
8. **Запуск Celery Beat**

    Celery Beat используется для запуска периодических задач. Для его запуска выполните команду:
    ```bash
    celery -A config beat -l info --scheduler django_celery_beat.schedulers:DatabaseScheduler
    ```

## Документация API

После запуска сервера перейдите по ссылке http://localhost:8000/redoc/ для просмотра документации ReDoc.

## Тестирование

Перед запуском тестов убедитесь, что в вашей базе данных нет данных, которые могут повлиять на результаты тестов. В идеале, следует использовать отдельную тестовую базу данных, чтобы изолировать тестовые данные от реальных данных приложения.

Используйте следующую команду для запуска тестов:

```bash
 coverage run --source='.' manage.py test
```


