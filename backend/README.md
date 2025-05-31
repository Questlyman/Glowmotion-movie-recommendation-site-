# 🎬 Онлайн кинотеатр – FastAPI backend

REST API для современного онлайн-кинотеатра: управление пользователями, фильмами, рецензиями, избранным, просмотренным, списком "буду смотреть" и персональными рекомендациями (в том числе с помощью LLM).

---

## 🛠️ Стек технологий

- **FastAPI** — фреймворк Python для создания REST API
- **SQLAlchemy** — ORM для работы с базой данных
- **Pydantic** — валидация данных и схемы
- **SQLite** — СУБД по умолчанию 
- **CORS** — поддержка кросс-доменных запросов
- **APScheduler** — задачи по расписанию
- **python-dotenv** — переменные окружения
- **passlib[bcrypt]** — для хеширования паролей
- **langchain-gigachat** — интеграция с LLM для генерации рекомендаций

---

## 🚀 Быстрый старт

### 1. Клонируйте репозиторий и перейдите в папку проекта

```bash
git clone <URL-репозитория>
cd <папка проекта>
```

### 2. Создайте виртуальное окружение и установите зависимости

#### Linux / macOS:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

#### Windows (CMD):

```cmd
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

#### Windows (PowerShell):

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### 3. Запустите сервер FastAPI

```bash
uvicorn main:app --reload
```

Приложение будет доступно по адресу: [http://127.0.0.1:8000](http://127.0.0.1:8000)

- Swagger UI: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- ReDoc: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## 📦 Структура проекта

```bash
backend/
│
├── routes/
│   ├── movies/
│   │   ├── movie.py
│   │   ├── other_tables.py
│   │   └── rec_movie.py
│   ├── reviews/
│   │   └── review.py
│   └── users/
│       └── user.py
│
├── schemas/
│   ├── movie.py
│   ├── review.py
│   └── user.py
│
├── services/
│   ├── errors/
│   │   ├── movie.py
│   │   ├── review.py
│   │   └── user.py
│   └── movies/
│       ├── fav_watch_and_ed.py
│       ├── find_movie.py
│       ├── giga.py
│       ├── kinopoisk_client.py
│       ├── movie_logic.py
│       ├── movie_repository.py
│       ├── premieres.py
│       ├── rec_movies.py
│       └── top_movies_loader.py
│
├── reviews/
│   ├── another_review_service.py
│   └── reviewCRUD.py
│
├── scheduled_scripts/ (в разработке)
│
├── users/
│   ├── users_service.py
│   └── util_password.py
│
├── database.py
├── film.json
├── main.py
├── models.py
├── README.md
├── requirements.txt
```

---

## 🧭 Описание основных папок и файлов

- **routes/** — роутеры FastAPI: обработчики запросов пользователей, фильмов, рецензий и др.
- **schemas/** — Pydantic-схемы для сериализации и валидации входящих/исходящих данных
- **services/** — бизнес-логика приложения, интеграция с внешними сервисами, база данных
  - **services/errors/** — кастомные классы ошибок
  - **services/movies/** — логика по работе с фильмами, топами, рекомендациями, интеграция с LLM
  - **services/reviews/** — сервисы и логика для работы с рецензиями
  - **services/users/** — сервисы и утилиты для пользователей
  - **services/scheduled_scripts/** — скрипты для выполнения по расписанию (в разработке)
- **database.py** — подключение и инициализация базы данных
- **models.py** — SQLAlchemy-модели для таблиц БД
- **main.py** — точка входа FastAPI приложения
- **requirements.txt** — список зависимостей проекта

---

## 🔗 Основные возможности API

- **/api/users/** — регистрация, логин, логаут, обновление, удаление пользователя, получение информации о себе и других
- **/api/movies/** — просмотр информации о фильмах, топ фильмов, новинки, расширенный поиск, подробная информация по id
- **/api/reviews/** — добавление, просмотр, обновление, удаление отзывов
- **/api/tables/** — управление своими списками: "Избранное", "Просмотрено", "Буду смотреть"
- **/api/recommendations/** — персональные рекомендации на основе жанров и предпочтений пользователя, поддержка LLM

---

## 💡 Примеры запросов

### Регистрация пользователя

```http
POST /api/users
Content-Type: application/json

{
  "email": "user@example.com",
  "username": "newuser",
  "password": "yourpassword"
}
```

### Получение топ-10 фильмов

```http
GET /api/movies/top/?count=10
```

### Добавление фильма в избранное

```http
POST /api/tables/{movie_id}/favorite_movies
```

### Получение персональных рекомендаций

```http
GET /api/recommendations/me
```

---

## ⚠️ Примечания

- Для взаимодействия с фронтендом (например, React + Vite) рекомендуется запускать фронт на порте 4000 или 5173.
- По умолчанию используется SQLite (можно заменить на PostgreSQL/MySQL и т.д.)
- В файле `.env` храните свои секретные ключи и настройки
- Для LLM (gigachat/LLM-рекомендаций) требуется отдельный API-ключ, который указывается в `.env`
- Для неофициального KinoPoisk API требуется отдельный API-ключ, которые указывается в `.env`

---

## 📢 Обратная связь

Если у вас есть вопросы, баги или предложения — создавайте issue или открывайте pull request!

**Разработка: студенты МАИ**
| Студент                      | Роль                        | Задачи в проекте                                  |
|------------------------------|-----------------------------|---------------------------------------------------|
| Волков Алексей Александрович | Team Lead / Backend developer | Маршруты (Routes), остальная backend-логика        |
| Рахматуллин Айдар Рамильевич | Backend developer           | Интеграция с API Кинопоиска, LLM GigaChat, отзывы |
| Митрофанов Олег Русланович   | Frontend developer          | Полный Frontend стек (разработка интерфейса)      |



