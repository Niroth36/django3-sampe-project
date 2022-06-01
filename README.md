# Clone and run project
```bash
git clone https://github.com/tsadimas/django3-sampe-project.git
python -m venv myvenv
source myvenv/bin/activate
pip install -r requirements.txt
cd myproject
cp myproject/.env.example myproject/.env
```
edit myproject/.env file to define
```vim
SECRET_KEY='test123'
DATABASE_URL=sqlite:///./db.sqlite3
```
# run development server
```bash
python manage.py runserver
```
test webhook

# run migrations and create superuser with docker-compose
```bash
docker-compose exec django python manage.py makemigrations
docker-compose exec django python manage.py migrate
docker-compose exec django python manage.py createsuperuser
```
hello