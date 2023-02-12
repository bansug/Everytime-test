# Dockerfile

### 도커파일 작성하기

html과 css 기반으로 간단한 웹페이지를 만들었고, localhost:8000에 80번 포트를 연결시켜야 하기 때문에 Dockerfile을 다음과 같이 작성했다.

```docker
FROM ubuntu
LABEL maintainer="bansug"
RUN apt-get update\
    && apt-get upgrade -y\
    && apt-get install vim git apache2 -y

COPY ./everytime.html /var/www/html/everytime.html
ADD ./everytime.css /var/www/html/everytime.css
ADD ./everytime-logo.png /var/www/html/everytime-logo.png

WORKDIR /var/www/html
EXPOSE 80

CMD [ "-D","FOREGROUND" ]
ENTRYPOINT [ "apachectl" ]
```

- FROM명령어로 이미지의 기반을 ubuntu로 설정해주었다.
- LABEL로 작성자를 적어주었다.
- RUN 명령어로 FROM에서 지정한 이미지 쉘에서 다음 명령어들이 실행되도록 설정했다.
- COPY, ADD를 통해 파일을 이미지에 추가해주었다.
- WORKDIR /var/www/html경로로 기본 디렉토리를 설정했다.
- CMD 명령어로 컨테이너가 시작되었을 때 명령을 시작하도록 했다.
- ENTRYPOINT 명령어로 docker run에 실행 명령어가 있어도 먼저 apachectl가 실행된다.

![1](https://user-images.githubusercontent.com/97159967/218309492-1fe80e99-92fd-46ec-a30b-394de25e0036.png)

Dockerfile을 이미지로 만들고 실행해보았다.

![2](https://user-images.githubusercontent.com/97159967/218309497-d7fea11d-5911-4bc4-bc9c-97860615ebc2.png)

[localhost:8000/everytime.html](http://localhost:8000/everytime.html)로 접속시 실행되는 것을 볼 수 있었다.
