FROM python:3.10  # Берёт базовый образ с Python 3.10.

WORKDIR /app # Создаёт папку /app и делает её рабочей (как cd /app).

RUN pip install gunicorn==20.1.0 # Устанавливает Gunicorn (WSGI-сервер для Django).Django не умеет сам обслуживать HTTP-запросы в продакшене. Gunicorn это делает.

COPY requirements.txt . # Копирует файл requirements.txt из вашей папки в контейнер (в /app).

RUN pip install -r requirements.txt --no-cache-dir # Устанавливает все зависимости из requirements.txt.

COPY . . # Копирует весь код проекта из папки backend/ в контейнер.

RUN python manage.py collectstatic --noinput # Собирает всю статику (CSS, JS) в одну папку.
Зачем: Чтобы Nginx мог отдавать статические файлы напрямую.

CMD ["gunicorn", "--bind", "0.0.0.0:8000", "kittygram_backend.wsgi"] # Запускает Gunicorn при старте контейнера.
