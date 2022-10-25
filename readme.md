프로젝트용 테스트 홈페이지를 도커 컨테이너로 1 Instance로 운영하게 하는 테스트 git입니다.

[사용환경]

Amazon EC2의 t2.micro 인스턴스

Ubuntu 이미지 사용



[구동조건]

1. run_me.sh에 실행 권한 준 후 실행

2. portainer 폴더에서 sudo docker-compose up -d

3. web 폴더에서 sudo docker build -t django:v2 .

4. web 폴더 sudo docker-compose up -d

5. web_django_1 컨테이너 접속 후

python manage.py makemigrations

python manage.py migrate

python manage.py createsuperuser



[TODO]

Static 폴더 S3으로 이관
