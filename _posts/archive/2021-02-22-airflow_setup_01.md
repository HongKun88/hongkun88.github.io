---
layout: single
title: "Airflow 설치"
categories: [archive]
tags: [Airflow]
---
# 시작에 앞서  
개인적으로 찾아보기 위한 기록이기 때문에. 포스팅 후 내용 추가 및 수정이 될 수 있음.  
운영체제는 Ubuntu 20.04 LST  
Python Version - 3.8  
Airflow Database - PostgreSQL
---
<br>

# 선행 작업  
아래 작업은 Python 설치가 선행되어야 한다.  
만약, 설치가 되지 않았다면 설치는 하고 진행하자. -> Python 설치 링크  
Python 설치가 되어있다는 가정하에 아래 스크립트를 순차적으로 실행한다.
---
<br>

## Python 라이브러리 설치
```shell
sudo apt-get install python3-pip -y
sudo apt-get install python3-setuptools -y
sudo apt-get install python3-dev -y
sudo apt-get install python3-mysqldb -y
```

---
## PostgreSQL
### PostgreSQL 설치
```shell
sudo apt-get install postgresql postgresql-contrib -y
```

---
### PostgreSQL 접근
```shell
postgres psql
```

---
### PostgreSQL 계정 및 Database 생성
Database에 접근을 하게되면 'postgres=# ' 가 보이게 되면,  
아래 계정 생성 및 Database SQL을 순차적으로 실행해준다.    
```sql
create role how2overcome;
create database airflow;
grant all privileges on database airflow to how2overcome;
alter role how2overcome superuser;
alter role how2overcome createdb;
alter role how2overcome with login;
grant all privileges on all tables in schema public to how2overcome;

\c airflow
# You are now connected to database "airflow" as user "postgres".

\conninfo
# You are connected to database "airflow" as user "postgres" via socket in "/var/run/postgresql" at port "5432”.

\q
```
## 기타 라이브러리 설치
```shell
sudo apt-get install libmysqlclient-dev -y
sudo apt-get install libssl-dev -y
sudo apt-get install libkrb5-dev -y
sudo apt-get install libsasl2-dev -y
```
---
<br>

# Airflow 설치

### Airflow 환경변수 등록
```shell
echo 'export AIRFLOW_HOME=~/airflow' > ~/.bash_profile
```
---
### Airflow 패키지 설치
패키지 설치 시 2.x 버전의 경우, 에러가 발생하는 현상이 있다.  
그래서, 패키지 버전을 명시하여 주었고, 1.10.14 버전을 설지하였다.  
만약 pip명령을 사용 할 수 없다면, 하단 링크를 확인  
-> python / pip alias 등록
```shell
sudo pip install apache-airflow==1.10.14
## sudo SLUGIFY_USES_TEXT_UNIDECODE=yes pip install apache-airflow==1.10.14
```
---
### Airflow Config 수정
Config 파일의 위치는 '~/airflow/airflow.cfg' 이다.  
vim이 아니더라도 본인이 익숙한 에디터를 활용하여 수정을 하자.
```shell
sudo vi ~/airflow/airflow.cfg
```
shell 명령이 아니라, config 파일에 아래 정보로 수정을 하자.(실행명령 아님.)
```shell
executor = CeleryExecutor
sql_alchemy_conn = postgresql+psycopg2:///airflow
broker_url = amqp://guest:guest@localhost:5672//
result_backend = amqp://guest:guest@localhost:5672//
```
수정이 완료되면, 아래 Database 초기화 명령을 실행하자.
```shell
airflow initdb
```

---
### 기타 패키지 설치
celery 패키지의 경우 병렬처리를 위한 패키지이며,  
아래 목록은 추가적인 패키지를 설치하자.  
```
sudo pip install celery
sudo pip install psycopg2 >> error
sudo pip install mysqlclient
sudo pip install psycopg2-binary
sudo pip install apache-airflow['kubernetes']
sudo pip install apache-airflow[celery]
sudo pip install apache-airflow[rabbitmq]
sudo pip install apache-airflow[mysql]
sudo pip install apache-airflow[postgres]
```
필요한 패키지가 모두 설치되었다면, Database 초기화를 한번 더 실행해보자.  
```shell
airflow initdb
```
---
<br>

# Airflow 완료 테스트
Dag 디렉토리 생성  
```shell
mkdir -p ~/airflow/dags
```
스케줄러 실행  
```shell
airflow scheduler -D
```
워커 실행  
```shell
airflow worker -D
```
웹 서비스 실행  
```shell
airflow webserver -p 8080 -D
```