# 파이썬과 sql 연동, db와 테이블 만들기


```python
import pymysql
```

## connect 한 것을 'db'에 저장


```python
db = pymysql.connect(host="localhost",user="root",password="0345",charset = "utf8")
```

## cursor() 함수 불러오기


```python
cursor = db.cursor()
```

## cursor.excute를 통해 sql 실행

### example 이라는 이름을 가진 스키마 생성


```python
cursor.execute('CREATE DATABASE example')
```




    1




```python
cursor.execute('USE example;')
```




    0



### example 안에 lang 이라는 테이블 생성


```python
cursor.execute('CREATE TABLE lang(name VARCHAR(255),description VARCHAR(255),study VARCHAR(255))')
```




    0



### 테이블 생성되었는지 확인


```python
cursor.execute("SHOW TABLES")
for x in cursor:
    print(x)
```

    ('lang',)
    

### ALTER TABLE을 이용해 테이블 수정


```python
# primary key 삽입
sql = "ALTER TABLE lang ADD COLUMN id INT AUTO_INCREMENT PRIMARY KEY"
cursor.execute(sql)
```




    0




```python
cursor.execute("SHOW COLUMNS FROM lang FROM example")
for x in cursor:
    print(x)
```

    ('name', 'varchar(255)', 'YES', '', None, '')
    ('description', 'varchar(255)', 'YES', '', None, '')
    ('study', 'varchar(255)', 'YES', '', None, '')
    ('id', 'int', 'NO', 'PRI', None, 'auto_increment')
    

### INSERT INTO 를 이용해 테이블에 데이터 삽입


```python
cursor.execute('INSERT INTO lang (name,description, study, id) VALUES ("JAVA","JAVA IS PROGRAMMING",FALSE,1)')
```




    1




```python
db.commit()
db.close()
```


```python

```
