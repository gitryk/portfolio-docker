# portfolio-docker #

프로젝트용 테스트 홈페이지를 도커 컨테이너로 1 Instance로 운영하게 하는 테스트 git입니다.

[사용환경]

Amazon EC2의 t2.micro 인스턴스

Ubuntu 이미지 사용

git clone https://github.com/tryklab/portfolio-docker.git



[구동조건]

1. run_me.sh에 실행 권한 준 후 실행

2. portainer 폴더에서 sudo docker-compose up -d #생략 가능함 시각적으로 관리하기 쉬운 도커 관리 툴임

3. web 폴더에서 sudo docker build -t django:v2 .

4. web/django/Univ/config/settings.py 편집하여 RDS와 RedisCluster에 대한 설정값 기입하기(해당 부분 수정)
```
DATABASES = {
    "default": {
        "ENGINE": 'django.db.backends.mysql',
        "NAME": '[DB Database Name]',
        "USER": '[DB USER Name]',
        "PASSWORD": '[DB PASSWORD]',
        "HOST": '[Master DB address]',
        "PORT": '3306',
    },
    'replica': {
        "ENGINE": 'django.db.backends.mysql',
        "NAME": '[DB Database Name]',
        "USER": '[DB USER Name]',
        "PASSWORD": '[DB PASSWORD]',
        "HOST": '[Replica DB address]',
        "PORT": '3306',
    },
}
CACHES = { 
    "default": { 
        "BACKEND": "django_redis.cache.RedisCache", 
        "LOCATION": [ 
            "redis://[Master RedisCache Server address]:6379", 
            "redis://[Secondary RedisCache Server address]:6379", ], 
        "OPTIONS": { 
            "CLIENT_CLASS": "django_redis.client.DefaultClient", 
            "MASTER_CACHE": "redis://[[Master RedisCache Server address]:6379", 
        }, 
    }
}
```
5. web 폴더 sudo docker-compose up -d

6. web_django_1 컨테이너 접속 후
``` 
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```
