

# 크롤링 설치

- 바탕화면에 폴더 만들고
- ‘requirements.txt’ 파일을 생성한 후 아래 코드

```python
beautifulsoup4==4.11.1
ipywidgets==7.7.1
jupyterlab==3.4.4
lxml==4.9.1
matplotlib==3.5.2
numpy==1.23.1
openpyxl==3.0.10
pandas==1.4.3
requests==2.28.1
selenium==4.3.0
tqdm==4.64.0
```

- 라이브러리
    
    ![Untitled](/images/Crawling_Practice/Untitled.png)


- git bash 터미널로 열고 virtualenv venv 입력
    
    ![Untitled](/images/Crawling_Practice/Untitled%201.png)
    
- 다음과 같이 가상환경에 접속한다.
- which python 은 접속됐는지 확인하는 코드
    
    ![Untitled](/images/Crawling_Practice/Untitled%202.png)
    
- pip install -r requirements.txt 입력(파일은 tab키로 입력한다.)
    
    ![Untitled](/images/Crawling_Practice/Untitled%203.png)
    
- [https://dschloe.github.io/python/crawling/python_selenium_crawling/](https://dschloe.github.io/python/crawling/python_selenium_crawling/) 참고해서
    
    크롬 버전에 맞는 chromedriver.exe 파일 다운(윈도우는 32버전 다운)
    
- Jupyter lab 실행
    
    ![Untitled](/images/Crawling_Practice/Untitled%204.png)
    
- 코드는 이런식으로 작성
    
    ![Untitled](/images/Crawling_Practice/Untitled%205.png)
    

### 크롤링 연습 및 홈페이지 예제 만들기

- 크롤링 연습 및 html
    
    ![Untitled](/images/Crawling_Practice/Untitled%206.png)
    
- Live Server 확장 설치
    
    ![Untitled](/images/Crawling_Practice/Untitled%207.png)
    
- 오른쪽 아래 Go Live 클릭하면 위에 코드 친 대로 홈페이지 생성
    
    ![Untitled](/images/Crawling_Practice/Untitled%208.png)