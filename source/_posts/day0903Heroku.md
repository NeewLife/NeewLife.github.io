---
title: "Heroku PostgreSQL 연동"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: python
clearReading: true
thumbnailImage: heroku.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-09-03 22:05:23'
---

- Heroku PostgreSQL 연동
- Heroku에 DB를 올려서 PostgreSQL 연동하여 배포하는 형식
<!-- excerpt -->
### 사전준비

- Github에 각 개인에게 맞는 Github Repo를 생성한다.
- 가상환경 설정을 진행한다.
- PostgreSQL DB를 설정한다.
    - [https://www.notion.so/Heroku-f34fbae1867049ad8e297e53ad435282](https://www.notion.so/Heroku-f34fbae1867049ad8e297e53ad435282)
        
        

### Postgres 설정

- 먼저 Local 에서 PostgreSQL을 다운로드 하여 설치한 후, 시스템 환경 변수 설정을 한다.
    
    ![Untitled](/images/0903Heroku/Untitled.png)
    
    ![Untitled](/images/0903Heroku/Untitled%201.png)
    
    ![Untitled](/images/0903Heroku/Untitled%202.png)
    
- 그 후에 Heroku 에서 Postgres 를 설정하기 위해 Heroku Addon 사이트에 접속한다.
    - [https://elements.heroku.com/addons/heroku-postgresql](https://elements.heroku.com/addons/heroku-postgresql)
    
    ![Untitled](/images/0903Heroku/Untitled%203.png)
    

- 설정 방법은 크게 2가지가 있다.
    - CLI(가상환경 터미널)에서 설치하는 방법
    
    ```bash
    heroku addons:create 내 프로젝트 이름:hobby-dev
    ```
    
    - Web UI 를 통해서 설치하는 방법
        - Install Heroku Postgres 버튼을 클릭 후 본인에 맞는 프로젝트를 연결한다.
            
            ![Untitled](/images/0903Heroku/Untitled%204.png)
            
    
    - Settings 탭을 누른 후, View Credentials를 클릭한다.
        
        ![Untitled](/images/0903Heroku/Untitled%205.png)
        
    
    - Password,  URI  등 기억하자.
    
    ![Untitled](/images/0903Heroku/Untitled%206.png)
    

## 테이블 생성 및 데이터 추가 / 조회

- Local 버전에서 iris 테이블을 불러온 후 PostgreSQL에 추가하는 코드를 app.py에 아래와 같이 추가한다.

```bash
# -*- coding: utf-8 -*-
from flask import Flask
import pandas as pd 
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String

## DB 연결 Local
def db_create():
    # 로컬
		engine = create_engine("postgresql://postgres:1234@localhost:5432/chatbot", echo = False)
		
		# Heroku
		engine = create_engine("postgresql://mzgnoxixyinhjd:d7ac5c7c91e4b4b82bfbdc56dc09a762cf9025423f26c0d0d5d0a6a1a6442765@ec2-34-235-31-124.compute-1.amazonaws.com:5432/dfqa3qaa76tclf", echo = False)

    engine.connect()
    engine.execute("""
        CREATE TABLE IF NOT EXISTS iris(
            sepal_length FLOAT NOT NULL,
            sepal_width FLOAT NOT NULL,
            pepal_length FLOAT NOT NULL,
            pepal_width FLOAT NOT NULL,
            species VARCHAR(100) NOT NULL
        );"""
    )
    data = pd.read_csv('data/iris.csv')
    print(data)
    data.to_sql(name='iris', con=engine, schema = 'public', if_exists='replace', index=False)

app = Flask(__name__)

@app.route("/")
def index():
    db_create()
    return "Hello World!"

if __name__ == "__main__":
    db_create()
    app.run()
```

- 이제 Flask 파일을 실행한 후, 정상적으로 DB가 들어가졌는지 확인한다.

```bash
python app.py
```

![Untitled](/images/0903Heroku/Untitled%207.png)

## Heroku에 배포하기

- 이제 Heroku에 동일하게 파일을 배포한다.
- 이 때 변경할 것은 URI만 변경해주고 다시 Push 한다
    
    ```bash
    git add .
    git commit -m "initial updated"
    git push # github repo에 추가
    git push heroku main
    ```
    

- 코드를 수정했기 때문에, 우선 웹사이트가 열리는지를 확인해야 한다.

![Untitled](/images/0903Heroku/Untitled%208.png)

- 이번에는 pgAdmin 에 새로운 서버를 생성한 후, 확인해본다. 먼저 아래와 같이 새로운 서버를 작성한다.
    - 여기서 아까 기억했던 Password, Username 등을 작성한다.
    - General 은 아무 이름이나 작성가능
    
    ![Untitled](/images/0903Heroku/Untitled%209.png)
    

- 그 후에 본인에게 맞는 DB를 찾고 조회가 되는지 확인한다.

![Untitled](/images/0903Heroku/Untitled%2010.png)