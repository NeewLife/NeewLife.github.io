---
title: "Heroku 세팅"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: Python
clearReading: true
thumbnailImage: python.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-08-01 16:32:01'
---

- Heroku 세팅하기
<!-- excerpt -->

---

![Untitled](/images/Heroku/Untitled.png)

![Untitled](/images/Heroku/Untitled%201.png)

- [Heroku 홈페이지](https://id.heroku.com/login)에 들어가서 회원가입
    - 비밀번호양식 → 영문+숫자+특수문자

- [Heroku 다운로드](https://devcenter.heroku.com/articles/heroku-cli)

- GitHub 에서 새로운 Repository 생성하기
    
    ![Untitled](/images/Heroku/Untitled%202.png)
    

- Add a README File 체크 후 생성한다.
- 바탕화면에 git clone 으로 불러온 후 VSCode로 연다.
    
    ![Untitled](/images/Heroku/Untitled%203.png)
    

- 가상환경 생성 및 접속, Flask 설치
    
    ![Untitled](/images/Heroku/Untitled%204.png)
    

```python
virtualenv venv

source venv/Scripts/activate

pip install Flask gunicorn
```

- 파일 만들기
    
    ![Untitled](/images/Heroku/Untitled%205.png)
    
    ![Untitled](/images/Heroku/Untitled%206.png)
    

```python
pip freeze > requirements.txt
```

- 코드 입력

```python
python.exe -m pip install --upgrade pip
```

![Untitled](/images/Heroku/Untitled%207.png)

- [app.py](http://app.py) 파일 만들기
    
    ![Untitled](/images/Heroku/Untitled%208.png)
    

- [app.py](http://app.py) 파일 안에 코드 입력 후 저장

```python
# -*- coding: utf-8 -*-
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello World!"
```

- 코드 입력
    
    ![Untitled](/images/Heroku/Untitled%209.png)
    

```python
export FLASK_ENV=development

export FLASK_APP=app

flask run
```

- flask run 까지 입력했다면 다음과 같이 나오는데 주소창을 클릭하면 로컬에서 테스트 하는 형태로 된다.(Git 블로그 hexo server 와 같은 로직)
    
    ![Untitled](/images/Heroku/Untitled%2010.png)
    

- [app.py](http://app.py) 에 코드 추가
    
    ![Untitled](/images/Heroku/Untitled%2011.png)
    

```python
if __name__ == "__main__":
	app.run(port=5000)
```

- ‘Procfile’ 파일을 하나 만들고 코드 입력
    
    ![Untitled](/images/Heroku/Untitled%2012.png)
    
    ![Untitled](/images/Heroku/Untitled%2013.png)
    

```python
web: gunicorn wsgi:app
```

- ‘[wsgi.py](http://wsgi.py)’ 파일을 하나 만들고 코드 입력
    
    ![Untitled](/images/Heroku/Untitled%2014.png)
    

```python
from app import app

if __name__ == "__main__":
    app.run()
```

- 파이썬 버전체크, 파이썬 실행(나가는 명령어는 exit())
    
    ![Untitled](/images/Heroku/Untitled%2015.png)
    
    ![Untitled](/images/Heroku/Untitled%2016.png)
    

```python
python -V

python
```

- ‘runtime.txt’ 를 만들어서 파이썬 버전을 입력해준다
    
    ![Untitled](/images/Heroku/Untitled%2017.png)
    

- flask run 으로 로컬 테스트 해본 뒤 git 에 업로드 한다

```python
flask fun

git add .

git commit -m "your msg"

git push
```

---

## Heroku 로그인

- heroku login 입력
    
    ![Untitled](/images/Heroku/Untitled%2018.png)
    

```python
heroku login
```

- 사이트 업그레이드(app.py 만 업그레이드)
    - 만약 “app” 를 “main “ 으로 이름을 바꾼다면 Procfile, [wsgi.py](http://wsgi.py) 등등 수정을 해야한다.
    
    ![Untitled](/images/Heroku/Untitled%2019.png)
    
- templates 폴더 하나 만들기(그 안에 index.html 파일 만들기)
    
    ![Untitled](/images/Heroku/Untitled%2020.png)
    
    ![Untitled](/images/Heroku/Untitled%2021.png)
    
- index.html 파일 만들고 세팅한 후 flask run 으로 홈페이지 들어가기
    
    ![Untitled](/images/Heroku/Untitled%2022.png)
    

- 샘플 html

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>FlaskBlog</title>
</head>
<body>
   <h1>aaaaa</h1>
</body>
</html>
```

- [app.py](http://app.py) 에 다음 코드 입력 수정
    
    ![Untitled](/images/Heroku/Untitled%2023.png)
    

```python
render_template

return render_template('index.html')
```

- git 블로그와 로직은 똑같다. 로컬 환경에서 테스트 —> 서버로 배포
- flask run 으로 로컬 환경에서 테스트
    
    ![Untitled](/images/Heroku/Untitled%2024.png)
    

- 잘 나왔다면 Heroku로 배포
- Heroku 로 배포 할 때
    1. git add.
    2. git commit -m “”
    3. git push origin main
    4. git push heroku main
    
     4 까지 진행했으면 Heroku에서 Open App 누르면 수정된 홈페이지가 나온다
    
    ![Untitled](/images/Heroku/Untitled%2025.png)
    
    ![Untitled](/images/Heroku/Untitled%2026.png)
    
    주소 창 비교 확인!
    

## 폰트 바꿔보기

- static폴더를 만들고 안에 또 css 폴더를 만들고 그 안에 style.css 파일을 하나 만든다.
    
    ![Untitled](/images/Heroku/Untitled%2027.png)
    
- style.css 파일에 다음 샘플코드 복붙

```python
h1 {
    border: 2px #eee solid;
    color: brown;
    text-align: center;
    padding: 10px;
}
```

- index.html 파일에 head 부분에 다음 문장 복붙

```python
<link rel="stylesheet" href="{{ url_for('static', filename= 'css/style.css') }}">
```

![Untitled](/images/Heroku/Untitled%2028.png)

- 저장 후 flask run 으로 테스트 하고 heroku 에 배포