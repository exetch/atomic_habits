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


2. **Настройте файл .env и переменные окружения 🌐**

    Для корректной работы приложения, необходимо создать файл .env с вашими данными. Вставьте следующие переменные и заполните их значениями:

    ```makefile
      DB_NAME=postgres
      DB_USER=postgres
      DB_PASSWORD=mysecretpassword
      DB_HOST=db
      DB_PORT=5432
      TELEGRAM_API_TOKEN=your_API_TOKEN
    ```


## Запуск с использованием Docker 🐳

1. **Создание Docker образа**:
   Для начала создайте Docker образ вашего приложения. Выполните следующую команду в терминале, находясь в корневой директории проекта:
   ```bash
   docker-compose build
   ```
   
2. **Запуск приложения**:
   Теперь можно запустить приложение. Выполните команду:
   ```bash
   docker-compose up
   ```
3. **Настройка и создание суперпользователя 👤**

    Для установки параметров суперпользователя, пароля и email, отредактируйте файл `users/management/commands/create_superuser.py`.
    
    Чтобы создать суперпользователя, выполните следующую команду в командной строке:
    
    ```bash
    docker-compose exec web python manage.py create_superuser
    ```

## Интеграция с Telegram

### Настройка Telegram Бота

Для получения напоминаний о привычках через Telegram, выполните следующие шаги:

1. **Создайте Telegram бота**:
   - Перейдите в Telegram и начните чат с [BotFather](https://t.me/botfather).
   - Следуйте инструкциям BotFather для создания нового бота. По завершении вы получите токен бота, добавьте этот токен в .env

2. **Получите ссылку на своего бота**:
   - После создания бота BotFather предоставит вам ссылку на вашего бота, например: `https://t.me/your_bot_name`.

3. **Поделитесь ссылкой на бота с пользователями**:
   - Предоставьте пользователям ссылку на вашего бота, чтобы они могли начать использовать его для получения напоминаний.

### Использование Бота

1. **Запуск бота**:
   - Перейдите по ссылке бота и нажмите "Start" (Запустить).

2. **Отправка email для связи аккаунта**:
   - Отправьте боту email, который вы использовали для регистрации в приложении "Atomic Habit Tracker". Это позволит боту идентифицировать вас и связать ваш Telegram аккаунт с аккаунтом в приложении.

### Получение Напоминаний

- После успешной связи аккаунта, бот будет автоматически отправлять вам напоминания о ваших привычках.
- Напоминания будут отправляться за 5 минут до назначенного времени выполнения каждой привычки.
   
## Документация API

После запуска сервера перейдите по ссылке http://localhost:8001/redoc/ для просмотра документации ReDoc.

## Тестирование

Перед запуском тестов убедитесь, что в вашей базе данных нет данных, которые могут повлиять на результаты тестов. В идеале, следует использовать отдельную тестовую базу данных, чтобы изолировать тестовые данные от реальных данных приложения.

Используйте следующую команду для запуска тестов в уже запущеном контейнере:

```bash
docker-compose exec web coverage run --source='.' manage.py test

```
Создайте отчет в консоли:
```bash
docker-compose exec web coverage report
```
Генерируйте HTML-отчет для более детального анализа:

```bash
docker-compose exec web coverage html
```
