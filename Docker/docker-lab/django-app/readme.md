# Deploying the django app with docker compose
```
$ sudo docker-compose run web django-admin.py startproject composeexample .

$ sudo chown -R $USER:$USER .
 
$ docker-compose up
```

# Reference
https://docs.docker.com/compose/django/
