---
title: "Linux 환경 만들기"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: Linux
clearReading: true
thumbnailImage: Linux.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-07-27 16:54:02'
---

## Linux 설치
<!-- excerpt -->
## vi 편집기 사용 꼭 공부 하기


- 윈도우 버전이 20H1, 20H2, 21H1, 21H2 보다 높아야 됨

![Untitled](/images/Linux/Untitled.png)

- powershell 관리자로 실행
- 다음 코드 입력

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

```

- 인터넷 주소창에 다음 코드 입력

```powershell
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
```

- 다운 받은 후 설치
- Microsoft Store 에서 ubuntu 설치

![Untitled](/images/Linux/Untitled%201.png)

- Ubuntu 20.04.4 버전으로 다운로드
    - 나중에 설정이 꼬였을 때 윈도우 포맷하는 것 처럼 Ubuntu를 삭제하고 다시 설치하면 된다.

![Untitled](/images/Linux/Untitled%202.png)

- Ubuntu 실행

![Untitled](/images/Linux/Untitled%203.png)

- 만약 다음과 같은 메세지가 뜬다면 가상환경을 확인해야 한다

![Untitled](/images/Linux/Untitled%204.png)

- Windows 기능 켜기/끄기 열기

![Untitled](/images/Linux/Untitled%205.png)

- Windows 하이퍼바이저 플랫폼 체크 후 재부팅

![Untitled](/images/Linux/Untitled%206.png)

- 재부팅 후 Ubuntu 실행
- Ubuntu 아이디 비밀번호 만들기 (***비밀번호는 입력해도 안 보인다!!***)

![Untitled](/images/Linux/Untitled%207.png)

- 다시 powershell 실행 후 다음 코드 입력

```powershell
wsl --set-default-version 2
```

- 다음과 같이 뜨면 성공!

![Untitled](/images/Linux/Untitled%208.png)

- 코드 wsl -l -v 입력 후 버전이 1이 나오면 Ubuntu 제거 후 다시 설치하고 Ubuntu 로그인 후
- 맨 위에 PowerShell 코드 다시 입력

![Untitled](/images/Linux/Untitled%209.png)

- 그 다음 wsl -l -v 치면 버전 2가 나옴(나오면 꺼도 됨)

- 시스템 환경 변수 들어가서 환경 변수 탭 —> Path 편집

![Untitled](/images/Linux/Untitled%2010.png)

![Untitled](/images/Linux/Untitled%2011.png)

![Untitled](/images/Linux/Untitled%2012.png)

- VS Code 저 경로가 있는지 확인한다.

---

### 환경변수를 사용하는 이유

빅데이터 플랫폼 / 웹사이트 구축할 때

- 레고블록 쌓을때 맞물려 쌓듯이 연결해주는 것이 Configuration(환경 변수) 인데
    
    이 환경 변수가 유기적으로 연결 되지 않으면 에러가 뜨거나 실행이 안된다.
    

---

- 다음 사이트 참고하여서 VS Code 에 연결
- [https://dschloe.github.io/settings/vscode_wsl2/](https://dschloe.github.io/settings/vscode_wsl2/)

- C드라이브에 폴더를 만든다(여기에선 dataEngineering)
- Ubuntu를 열고 다음 코드를 입력해 C\dataEngineering 폴더에 접속한다.
- mkdir abc = 새로운 abc 폴더 생성
- rm -rm abc : abc폴더 만 지운다
- rm -rm * : 전체 삭제

```
cd mnt
cd c
cd dataEngineering

code .
```

- code . 까지 입력하면 VS Code 가 열릴텐데 터미널 열고서 파이썬 버전 확인

![Untitled](/images/Linux/Untitled%2013.png)

- sudo apt-get update 입력

![Untitled](/images/Linux/Untitled%2014.png)

- sudo apt install python3-pip 입력

![Untitled](/images/Linux/Untitled%2015.png)

- sudo pip3 install virtualenv 입력

![Untitled](/images/Linux/Untitled%2016.png)

- 가상환경 생성 코드 virtualenv venv 입력
- 가상환경 접속 코드 source venv/bin/activate 입력
- 윈도우와 리눅스의 가상환경 차이점 =  source venv 다음 /bin 으로 시작한다

![Untitled](/images/Linux/Untitled%2017.png)

### 환경 변수 설정하기

- pwd 입력 후 경로 확인후 복사

![Untitled](/images/Linux/Untitled%2018.png)

- vi ~/.bashrc 입력 하면 환경 변수에 접속한다

![Untitled](/images/Linux/Untitled%2019.png)

- 다음과 같은 화면이 뜨면 vi 편집기로 활성화 됨
- 여기서 “i” 를 누르면 INSERT 모드로 진입된다. 맨 밑으로 스크롤해서 내림
- export AIRFLOW_HOME=(아까 그 pwd 경로입력)

![Untitled](/images/Linux/Untitled%2020.png)

- 중간에 ‘=’ 을 띄어쓰기 하면 안됨!!
- 입력모드 종료는 ESC 키 누르면 됨
- :wq! 를 입력(저장한다는 뜻)   :q!  는 저장하지 않고 나간다는 뜻, 잘못 만졌을 때 유용하다.

![Untitled](/images/Linux/Untitled%2021.png)

- source ~/.bashrc 까지 입력해야 배포가 완료됨

![Untitled](/images/Linux/Untitled%2022.png)

- 배포하면 venv 가 사라지기 때문에 항상 다시 가상환경 설정해야함
- echo $AIRFLOW_HOME 입력 해서 배포됐는지 확인

![Untitled](/images/Linux/Untitled%2023.png)

- pip3 install ‘apache-airflow[postgres,slack,celery]’  입력

![Untitled](/images/Linux/Untitled%2024.png)

- 설치 완료되면 airflow db init 입력

![Untitled](/images/Linux/Untitled%2025.png)

- 다음 코드를 입력해서 airflow 입력

```
airflow users create --username airflow --password airflow --firstname evan --lastname airflow --role Admin --email your_email@some.com
```

- airflow webserver -p 8081 입력
- 주소창에 [localhost:1234](http://localhost:1234) 로 접속하면 airflow 로컬 홈페이지가 나온다