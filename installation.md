# Earthworks PM
A geotechnical data management platform for engineers

This repository contains both the API server and the frontend website for Earthworks PM.

## Installation requirements
* **Python 3**, with ability to create virtual environments
* **PostgreSQL** (tested with 9.4, 9.6, 10.1)
* **PostGIS** extension for postgresql
* **npm** package manager

## Installation instructions
### Environment setup
* Create a Python 3 virtual environment and activate it (see [Python docs](https://docs.python.org/3/library/venv.html))
* Clone this repository
* From the root directory (containing ```manage.py``` and ```requirements.txt```), run ```pip install -r requirements.txt``` 
### PostgreSQL setup
* Create a new postgres user (see [PostgreSQL docs](https://www.postgresql.org/docs/9.1/static/sql-createrole.html)) 
* Create a new postgres database
* Enter the command line for your database with ```psql -d your_database_name``` and run the command ```CREATE EXTENSION POSTGIS;```
* Start the database server (on systemd Linux systems, run ```sudo systemctl enable postgresql``` and ```sudo systemctl start postgresql```)
### API server (Django) setup
* Edit ```eqc/settings_secret.py.template``` with your database credentials. Generate a random secret key. You can generate a key with Python with:
```
>>> import random
>>> ''.join([random.SystemRandom().choice('abcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*(-_=+)') for i in range(50)])
``` 
* You must **copy** the generated string into the constant. Rename the file to ```settings_secret.py``` (remove 'template' from filename)
* Go to the root directory of the repo and setup database tables with ```python manage.py migrate```
* Use ```python manage.py createsuperuser``` to create an admin account for the backend API.
* Start the Django development server with ```python manage.py runserver```. You should see a message that your application is running on localhost:8000. Try logging in with your admin account at localhost:8000/admin/ and see the API at localhost:8000/projects/api/
* For production systems, use gunicorn and nginx.
### Web app (Vue.JS) setup
* Enter the epm-web folder from the repository root
* run ```npm install``` to install dependencies
* run ```npm run dev``` to run the development server
* If you have trouble logging in or connecting to the API, make sure that ```CORS_WHITELIST``` in ```eqc/settings.py``` contains the localhost:8080 frontend dev server and that ```api``` and ```loginApi``` in ```epm-web/src/store/index.js``` are pointing to the local API server (localhost:8000).
