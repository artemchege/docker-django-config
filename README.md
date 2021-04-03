Тут представлены 3 обязательных файла для создания image django проекта и последующего запуска контейнеров. 

Зачем: 
Чтоб каждый раз не писать Dockerfile и docker-compose.yml просто копируем текущий конфиг в готовй django проект, после запускаем docker-compose up и далее проект 
запускается на 8000 порту хоста. 

Комманды: 

    docker-compose up
    docker exec -it web_container_id python manage.py makemigrations
    docker exec -it web_container_id python manage.py migrate
    docker exec -it web_container_id python manage.py createsuperuser

Что надо знать: 
1. В docker-compose.yml сперва поднимается БД postgres, после поднимается сам сервер django (build-in, без gunicorn). 
2. Снабдить актуальным requirements.txt, pip freeze > requirements.txt 
3. В соотвествии с конфигом БД в docker-compose файле, чтоб django корректно работал с БД прописать в settings.py django проекта следующие строки: 

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'postgres',
            'USER': 'postgres',
            'PASSWORD': 'postgres',
            'HOST': 'db',
            'PORT': 5432,
        }
    }

В readme кусок кода выше выглядит расформатированным (поправить в продакшене). 

Было протестировано на базовом django проекте, все сработало. 

Документация: https://docs.docker.com/compose/django/
