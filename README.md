# alx_travel_app

## Django Project Setup with API Documentation and Database Configuration

### 📌 Features
- Django project `alx_travel_app` with app `listings`
- REST API powered by Django REST Framework (DRF)
- CORS enabled (via django-cors-headers)
- MySQL database configured using .env variables
- Swagger / Redoc API documentation (drf-yasg) at `/swagger/` and `/redoc/`
- Celery configured with RabbitMQ for background jobs
- Ready for containerization / deployment

---

### 📂 Project Structure
```
alx_travel_app/
├── alx_travel_app/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── celery.py
│   └── wsgi.py
├── listings/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   └── urls.py
├── venv/
├── .env
├── .gitignore
├── manage.py
├── requirement.txt
└── README.md
```

---

### ⚙️ Setup Instructions

#### 1. Clone Repository
```bash
git clone https://github.com/<your-username>/alx_travel_app.git
cd alx_travel_app
```

#### 2. Create & Activate Virtual Environment
```bash
python -m venv venv
source venv/bin/activate    # Linux/macOS
venv\Scripts\Activate     # Windows PowerShell
```

#### 3. Install Dependencies
```bash
pip install --upgrade pip
pip install -r requirement.txt
```

#### 4. Configure Environment Variables (`.env` file)
```
SECRET_KEY=change-me-to-a-secure-value
DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost

DB_NAME=alx_travel
DB_USER=alx_user
DB_PASSWORD=alx_pass
DB_HOST=127.0.0.1
DB_PORT=3306
USE_PYMYSQL=True

CELERY_BROKER_URL=amqp://guest:guest@localhost:5672//
CORS_ALLOW_ALL_ORIGINS=True
```

#### 5. Database Setup (MySQL)
```sql
CREATE DATABASE alx_travel CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'alx_user'@'localhost' IDENTIFIED BY 'alx_pass';
GRANT ALL PRIVILEGES ON alx_travel.* TO 'alx_user'@'localhost';
FLUSH PRIVILEGES;
```

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

---

### 🐇 RabbitMQ Setup
```bash
docker run -d --hostname my-rabbit --name some-rabbit   -p 5672:5672 -p 15672:15672 rabbitmq:3-management
```
Management UI: [http://localhost:15672](http://localhost:15672)  
(default user/pass: guest / guest)

---

### 🚀 Running the Project

Start Django server:
```bash
python manage.py runserver
```

Access:
- API: [http://127.0.0.1:8000/api/](http://127.0.0.1:8000/api/)
- Swagger: [http://127.0.0.1:8000/swagger/](http://127.0.0.1:8000/swagger/)
- Redoc: [http://127.0.0.1:8000/redoc/](http://127.0.0.1:8000/redoc/)

Start Celery worker:
```bash
celery -A alx_travel_app worker -l info
```

---

### 🛠 Useful Commands
```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
celery -A alx_travel_app worker -l info
```

---

### 📝 Git Setup
```bash
git init
git add .
git commit -m "Initial project setup: Django, DRF, Swagger, Celery, MySQL"
git branch -M main
git remote add origin git@github.com:<your-username>/alx_travel_app.git
git push -u origin main
```

---

### 🧰 Common Issues & Fixes
- **mysqlclient errors on Windows** → use PyMySQL  
- **Swagger not loading** → ensure `drf_yasg` is in `INSTALLED_APPS` and `urls.py`  
- **CORS blocked** → check `corsheaders.middleware` order in `MIDDLEWARE`  
- **Celery not connecting** → verify RabbitMQ is running  
- **.env not loading** → confirm path and `env.read_env()`  

---

### 📌 Next Steps
- Implement listings models, serializers, and viewsets  
- Add JWT authentication (`djangorestframework-simplejwt`)  
- Write unit tests  
- Dockerize (Django + MySQL + RabbitMQ + Celery)  
- Setup GitHub Actions for CI/CD  
