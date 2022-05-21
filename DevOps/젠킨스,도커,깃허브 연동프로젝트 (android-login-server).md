# 젠킨스,도커,깃허브 연동프로젝트 (android-login-server)

## 로그인 정보 등

- awsip : 3.39.137.227
- RDS master password : Password!23
- 젠킨스 : admin / Password!23
- 슬랙
  설치되면 왼쪽 탐색 모음에서 Jenkins 관리를 다시 클릭한 후 시스템 구성으로 이동합니다. 글로벌 Slack Notifier 설정 섹션을 찾아 다음 값을 추가합니다.
  팀 하위 도메인: theslackconnect
  통합 토큰 자격 증명 ID: 12jKipUlOoIchcUzq4AQ1BZA 토큰을 값으로 사용하여 암호 텍스트 자격 증명을 생성합니다.
  기타 필드는 선택 사항입니다. 자세한 내용을 알아보려면 옆에 있는 물음표 아이콘을 클릭하세요. 작업을 완료하면 저장을 누릅니다.

---

## 기초

### https://more-learn.tistory.com/19 시리즈를 바탕으로 따라 함




- key 생성시 : ssh-keygen -t rsa -b 4096 -m PEM

- Publish over SSH

	jenkins서버에서 id_rsa 키값 발급받아서 키 넣어두고 ( 발급 방법 구글에 찾아보자 )
	remote서버 root에서 ~/.ssh/authorized_keys 에 id_rsa.pub 키 등록 후 테스트 진행
	(이렇게 되면 비번없이 서버 접속이 된다.)


	Test Configuration 눌렀을 때 이런 오류가 나올경우!
	
	jenkins.plugins.publish_over.BapPublisherException: Failed to connect and initialize SSH connection. Message: [Failed to connect session for config [server__name]. Message [Auth fail]]
	이유는 각자 jenkins ssh Server 설정에 적어놓은 userName에 해당하는 것으로 접속해야함!
	
	1. reomote서버에서 내가 젠킨스 설정에 적은 UserName로 접속
	
	su - userName
	~/.ssh/authorized_keys 여기에 jenkins서버에서 발급받은 id_rsa.pub key를 추가해줘야함


​	
- jenkins sudo 비밀번호 없이 사용

  1. 관리자 권한 설정 파일을 연다.
  $ sudo gedit /etc/sudoers
  2. jenkins에 관리자 권한을 제공하기 위해 아래의 내용을 추가 한 후 저장한다.
  jenkins ALL=(ALL) NOPASSWD: ALL

  

- EC2 프리티어에서 Jenkins가 돌아가지 않는 문제 해결하기
	https://tape22.tistory.com/22



- 날짜로 파일생성

	touch backup_$(date +"%Y%m%d-%H%M%S").txt

	// 출력 결과
	2020-07-01 09:47:06 +0900

	touch backup_$(date +"%Y%m%d").txt

	// 생성된 파일 이름
	backup_20200701.txt

---

## 서버에서 docker hub 접속

```
 cat ~/my_password.txt | docker login --username foo --password-stdin
```

---



+ docker로 pm2를 돌리려면 따로 작업을 해주어야한다 

  + nodejs express 서버 docker에서 pm2로 기동하기

---

## aws 볼륨 재할당 및 수정

- https://m.blog.naver.com/jogilsang/221370362752

---

## zabbix 적용

- https://boying-blog.tistory.com/40?category=886300

- docker inspect zabbix-agent | grep "IPAddress\": "

- ```
  docker run --name mysql-server -t -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="zabbix" -e MYSQL_PASSWORD="Password!23" -e MYSQL_ROOT_PASSWORD="Password!23" -d mysql --character-set-server=utf8 --collation-server=utf8_bin --default-authentication-plugin=mysql_native_password
  ```

- ```
  docker run --name zabbix-server-mysql -t -e DB_SERVER_HOST="mysql-server" -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="zabbix" -e MYSQL_PASSWORD="Password!23" -e MYSQL_ROOT_PASSWORD="Password!23" -e ZBX_JAVAGATEWAY="zabbix-java-gateway" --link mysql-server:mysql --link zabbix-java-gateway:zabbix-java-gateway -p 10051:10051 --restart unless-stopped -d zabbix/zabbix-server-mysql
  ```

- ```
  docker run --name zabbix-web-nginx-mysql -t -e DB_SERVER_HOST="mysql-server" -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="zabbix" -e MYSQL_PASSWORD="Password!23" -e MYSQL_ROOT_PASSWORD="Password!23" --link mysql-server:mysql --link zabbix-server-mysql:zabbix-server -p 81:8080 --restart unless-stopped -d zabbix/zabbix-web-nginx-mysql
  ```

- 

---

## docker prune

```
· docker container prune은 중지된 모든 컨테이너를 삭제한다.

· docker image prune은 이름 없는 모든 이미지를 삭제한다.

· docker network prune은 사용되지 않는 도커 네트워크를 모두 삭제한다.

· docker volume prune은 도커 컨테이너에서 사용하지 않는 모든 도커 볼륨을 삭제한다.

· docker system prune -a는 중지된 모든 컨테이너, 사용되지 않은 모든 네트워크, 하나 이상의 컨테이너에서 사용되지 않는 모든 이미지를 삭제한다. 따라서 남아있는 컨테이너 또는 이미지는 현재 실행 중인 컨테이너에서 필요하다.
```

---

## zabbix docker-compose.yml

```
version: '3.3'

services:
  postgres-server:
    container_name: postgres-server
    image: postgres:13.0-alpine
    restart: always
    environment:  
      POSTGRES_USER: zabbix
      POSTGRES_PASSWORD: Password!23
      POSTGRES_DB: zabbix
      PG_DATA: /var/lib/postgresql/data/pgdata

  zabbix-server:
    container_name: zabbix-server
    image: zabbix/zabbix-server-pgsql:ubuntu-5.4.9
    restart: always
    environment:
      POSTGRES_USER: zabbix
      POSTGRES_PASSWORD: Password!23
      POSTGRES_DB: zabbix
      ZBX_HISTORYSTORAGETYPES: log,text
      ZBX_DEBUGLEVEL: 1
      ZBX_HOUSEKEEPINGFREQUENCY: 1
      ZBX_MAXHOUSEKEEPERDELETE: 5000
    depends_on:
      - postgres-server
    volumes:
      - ./volumes/zabbix/alertscripts:/usr/lib/zabbix/alertscripts

  zabbix-frontend:
    container_name: zabbix-frontend
    image: zabbix/zabbix-web-nginx-pgsql:ubuntu-5.4.9
    restart: always
    ports:
      - '80:8080'
    environment:
      POSTGRES_USER: zabbix
      POSTGRES_PASSWORD: Password!23
      POSTGRES_DB: zabbix
      ZBX_SERVER_HOST: zabbix-server
      ZBX_POSTMAXSIZE: 64M
      PHP_TZ: "Asia/Seoul"  
      ZBX_MAXEXECUTIONTIME: 500
    depends_on:
      - postgres-server
      - zabbix-server

  zabbix-agent:
    container_name: zabbix-agent
    image: zabbix/zabbix-agent:latest
    privileged: true
    restart: unless-stopped
    environment:
      - ZBX_SERVER_HOST=zabbix-server

  grafana:
    container_name: grafana
    image: grafana/grafana
    restart: always
    ports:
      - '3001:3001'
    environment: 
      - GF_INSTALL_PLUGINS=alexanderzobnin-zabbix-app
    depends_on:
      - postgres-server
      - zabbix-server
```

---

## xshell로 파일 전송

```
sudo apt install lrzsz
```

---

## docker container로 파일전송

```
		전송할 파일 컨테이너명:저장할 파일 경로 
docker cp alldb.dmp oracle10g:/alldb.dmp
```

---

## root 권한으로 container 접근하기

```
root 권한으로 bash shell을 실행해야 하는데, 다행히 docker exec에서 제공하는 "u" 옵션을 붙여 해결할 수 있습니다.

// Root user in Docker Container 문서 참고

docker exec -itu 0 7bd3e7787b5e /bin/bash
```

