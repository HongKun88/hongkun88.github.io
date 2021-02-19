---
layout: single
title: "시간을 기준으로 최초값/최종값 구하기"
categories: [SQL]
tags: [SQL, HiveQL]
---



### 응용 버전
아래 코드의 이 점은 Sorting 정렬을 사용하지 않기 때문에.  
대용량 데이터 처리에 용이함.
```sql
SELECT    `기준값` AS RS_COL_01
     ,    SUBSTRING(MIN(CONCAT(FROM_UNIXTIME(UNIX_TIMESTAMP(`데이터 생성 일시`), 
            'yyyy-MM-dd HH:mm:ss'), [COLUMS_NAME_03]) 
                           AS RS_COL_02
     ,    SUBSTRING(MAX(CONCAT(FROM_UNIXTIME(UNIX_TIMESTAMP(`데이터 생성 일시`), 
            'yyyy-MM-dd HH:mm:ss'), `얻고자 하는 값`) 
                           AS RS_COL_02
  FROM    TB_NAME
 GROUP BY `기준값`
```
   
---
---
### 응용 버전
아래 코드의 이 점은 Sorting 정렬을 사용하지 않기 때문에.  
대용량 데이터 처리에 용이함.
```sql
SELECT    `기준값` AS RS_COL_01
     ,    SUBSTRING(MIN(CONCAT(FROM_UNIXTIME(UNIX_TIMESTAMP(`데이터 생성 일시`), 
            'yyyy-MM-dd HH:mm:ss'), [COLUMS_NAME_03]) 
                           AS RS_COL_02
     ,    SUBSTRING(MAX(CONCAT(FROM_UNIXTIME(UNIX_TIMESTAMP(`데이터 생성 일시`), 
            'yyyy-MM-dd HH:mm:ss'), `얻고자 하는 값`) 
                           AS RS_COL_02
  FROM    TB_NAME
 GROUP BY `기준값`
```