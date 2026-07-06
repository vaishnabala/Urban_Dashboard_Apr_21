🚀 Quick Start
Prerequisites
Python 3.11+ installed
Docker Desktop installed and running
Git installed
TomTom API key get one free
OpenWeatherMap API key get one free
1. Clone the Repository
2. Set Up Environment Variables
Create a .env file in the project root:

.env

TOMTOM_API_KEY=your_tomtom_api_key_here

OWM_API_KEY=your_openweathermap_api_key_here

DATABASE_URL=postgresql://postgres:postgres@localhost:5432/urban_intel

REDIS_URL=redis://localhost:6379/0

3a. Run with Docker Compose (Recommended) Navigate to docker dir and do that
bash docker compose up -d This starts PostgreSQL+PostGIS, the API server, the data scheduler, and the dashboard.

Dashboard: http://localhost:8501 API Docs: http://localhost:8000/docs or

3b. Run Manually (Development)
bash

Start the database
docker run -d --name urban-postgis
-e POSTGRES_PASSWORD=postgres
-e POSTGRES_DB=urban_intel
-p 5432:5432
postgis/postgis:16-3.4

Create virtual environment
python -m venv venv venv\Scripts\activate # Windows

source venv/bin/activate # macOS/Linux
Install dependencies
pip install -r requirements.txt

Initialize database tables
python -c "from src.database.init_db import init_database; init_database()"

Terminal 1 — API Server
uvicorn src.api.main:app --reload --port 8000

Terminal 2 — Data Scheduler
python src/data_collection/scheduler.py

Terminal 3 — Dashboard
streamlit run src/dashboard/app.py 🔌 API Reference Base URL: http://localhost:8000
