# Берёт базовый образ с Python 3.10.
FROM python:3.10

# Создаёт папку /app и делает её рабочей (как cd /app).
WORKDIR /app

# Устанавливает Gunicorn (WSGI-сервер для Django).Django не умеет сам обслуживать HTTP-запросы в продакшене. Gunicorn это делает.
RUN pip install gunicorn==20.1.0

# Копирует файл requirements.txt из вашей папки в контейнер (в /app).
COPY requirements.txt .

# Устанавливает все зависимости из requirements.txt.
RUN pip install -r requirements.txt --no-cache-dir

# Копирует весь код проекта из папки backend/ в контейнер.
COPY . .

# Собирает всю статику (CSS, JS) в одну папку.
#Зачем: Чтобы Nginx мог отдавать статические файлы напрямую.
RUN python manage.py collectstatic --noinput

# Запускает Gunicorn при старте контейнера.
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "kittygram_backend.wsgi"]
