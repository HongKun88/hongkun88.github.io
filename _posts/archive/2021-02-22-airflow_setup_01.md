---
layout: single
title: "Airflow 설치"
categories: [archive]
tags: [Airflow]
---
# 시작에 앞서  
개인적으로 찾아보기 위한 기록이기 때문에. 포스팅 후 내용 추가 및 수정이 될 수 있음.



---
# 선행 작업  
Python 설치가 선행되어야 한다. Python 설치 링크



Python 설치가 되어있다는 가정하에 아래 스크립트를 순차적으로 실행한다.

sudo apt-get install python3-pip -y
sudo apt-get install python3-setuptools -y
sudo apt-get install python3-dev -y
sudo apt-get install python3-mysqldb -y


sudo apt-get install postgresql postgresql-contrib -y

postgres psql

## SQL
postgres=# 

create role how2overcome;
create database airflow;
grant all privileges on database airflow to how2overcome;
alter role how2overcome superuser;
alter role how2overcome createdb;
alter role how2overcome with login;
grant all privileges on all tables in schema public to how2overcome;

\c airflow
You are now connected to database "airflow" as user "postgres".

\conninfo
You are connected to database "airflow" as user "postgres" via socket in "/var/run/postgresql" at port "5432”.

\q



echo 'export AIRFLOW_HOME=~/airflow' > ~/.bash_profile

sudo apt-get install libmysqlclient-dev -y
sudo apt-get install libssl-dev -y
sudo apt-get install libkrb5-dev -y
sudo apt-get install libsasl2-dev -y



sudo SLUGIFY_USES_TEXT_UNIDECODE=yes pip install apache-airflow==1.10.14


sudo pip install celery
sudo pip install psycopg2 >> error
sudo pip install mysqlclient
sudo pip install psycopg2-binary
sudo pip install apache-airflow['kubernetes']
sudo pip install apache-airflow[celery]
sudo pip install apache-airflow[rabbitmq]
sudo pip install apache-airflow[mysql]
sudo pip install apache-airflow[postgres]






executor = CeleryExecutor
sql_alchemy_conn = postgresql+psycopg2:///airflow
broker_url = amqp://guest:guest@localhost:5672//
result_backend = amqp://guest:guest@localhost:5672//



mkdir -p ~/airflow/dags

airflow scheduler -D
airflow worker -D
airflow webserver -p 8080 -D