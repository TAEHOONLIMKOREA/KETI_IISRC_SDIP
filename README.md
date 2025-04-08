# KETI_IISRC_SDIP

(KETI)  Korea Electronics Technology Institute  <br/>
(IISRC) Intelligent Integrated Software Research Center  <br/>
(SDIP)  Sensor Data Ingest Process

#### 개발 환경
Window 10 <br/>
Python 3.9 <br/>

#### 동작 환경
ubuntu 22.04 <br/>
python 3.9 <br/>
Docker version 25.0.4, <br/>
TimescaleDB version 2.16.1 <br/>
MongoDB version v7.0.11 <br/>
Redis server v=7.2.4 <br/>
celery==5.4.0 <br/>

<hr>

### [1] 서버 구성도
![image](https://github.com/user-attachments/assets/115c5a87-4694-4683-af74-ae1642565eb6)


### [2] 모니터링 웹 서비스 사용 (pgAdmin)
주소 : http://bigsoft.iptime.org:55413 <br/>

### [3] API Docs 접속
주소 : http://bigsoft.iptime.org:55414 <br/>
클릭시 API Docs 페이지 이동 <br/>
위 주소에 API 경로를 병합해서 사용 ( e.g. bigsoft.iptime.org:55414/sensor/InputSensorData )


### [4] 서버 실행 방법

#### &ensp; 1) 원하는 디렉토리에 git 명령어를 이용하여 코드 다운로드
``` {bash}
$ git clone git@github.com:TAEHOONLIMKOREA/KETI_IISRC_SDIP.git
```
iisrc-bridge

##### &ensp; ※ 아래 단계들을 진행하기 전에 $\it{\large{\color{#DD6565}.env 파일}}$을 만들어 서버 주소와 계정 정보들을 변수에 담아주어야함 <br> &ensp;&ensp; (현재 사용된 .env 파일은 따로 공유함)


#### &ensp; 2) DB서버(docker container) 실행 
 - docker-compose를 활용하여 서버(container)들을 실행시킵니다.
 - 서버를 실행하기 전 container들이 하나의 docker bridge로 묶여있기 때문에 bridge를 하나 만들어줍니다.
``` {bash}
$ docker network create iisrc-bridge
```
- "iisrc-bridge" 라는 이름의 bridge를 만들었습니다.
- (이름은 다르게 해도 상관없으나 각 compose 스크립트 파일내에 bridge 이름을 모두 바꿔주어야합니다.)
- 이제 docker-compose 명령어를 활용하여 서버를 실행합니다

``` {bash}
$ docker-compose -f timescale-compose.yml up -d
```
``` {bash}
$ docker-compose -f mongo-compose.yml up -d
```

#### &ensp; 3) 코드를 docker-image로 빌드 후 container 실행
``` {bash}
$ docker build -t keti_iisrc_sdip_api_server .
$ docker-compose up -d
```
