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
# K8S

## microk8s enable storage and dns ingress
```bash
microk8s enable storage dns
```

## Persistense Volume
```bash
kubectl apply -f k8s/db/postgres-pvc.yaml
```
## secrets
* pg secret

```bash
kubectl create secret generic pg-user \
--from-literal=PGUSER=<put user name here> \
--from-literal=PGPASSWORD=<put password here>
```

## configmaps
```bash
kubectl create configmap django-config --from-env-file=myproject/myproject/.env
```
## Deployments
* Postgres
```bash
kubectl apply -f k8s/db/postgres-deployment.yaml
```
* django
```bash
kubectl apply -f k8s/django/django-deployment.yaml
```

## Services
* Postgres
```bash
kubectl apply -f k8s/db/postgres-clip.yaml
```

* django
```bash
kubectl apply -f k8s/django/django-clip.yaml
```

## Ingress


check README.md in k8s/certs directory to create valid certificates



### Migrations?
### Static files? [whitenoise](http://whitenoise.evans.io/en/stable/)


## required apt  packages

```bash
sudo apt install python3-setuptools
```

## healthcheks
[django-helath-cheks](https://github.com/KristianOellegaard/django-health-check)
