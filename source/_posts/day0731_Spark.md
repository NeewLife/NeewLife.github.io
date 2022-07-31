---
title: "Spark 툴 설치 및 설정"
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
date: '2022-07-31 13:34:21'
---

### Apache Spark 설치 및 설정
### PySpark 설치 및 설정
<!-- excerpt -->


# Apache Spark 설치 및 설정

- hadoop 폴더를 하나 만들고
    
    ![Untitled](/images/0731_Spark/Untitled.png)
    
- cd hadoop 으로 이동 후 다음 코드 입력

```python
sudo apt-get install openjdk-8-jdk

sudo wget https://archive.apache.org/dist/spark/spark-3.2.0/spark-3.2.0-bin-hadoop3.2.tgz
```

- ls로 압축파일만 있는지 확인하고, 다른게 있으면 삭제하기.

### TAB 키 활용하기!!

- sudo tar -xvzf s 까지 치고 tab키 누르고 압축파일 풀기
    
    ![Untitled](/images/0731_Spark/Untitled%201.png)
    

- mv s (tab키) ~/spark3 입력
    
    ![Untitled](/images/0731_Spark/Untitled%202.png)
    

- cd .. 입력 후, spark3 폴더로 이동
- cp -r spark3/ spark-node입력
    
    ![Untitled](/images/0731_Spark/Untitled%203.png)
    
- spark3 폴더 안에 sbin 폴더로 이동
    
    ![Untitled](/images/0731_Spark/Untitled%204.png)
    
- 다음 명령어 입력
    
    ![Untitled](/images/0731_Spark/Untitled%205.png)
    
    ```python
    cp start-master.sh start-head.sh
    cd ~/spark-node/sbin
    cp start-slave.sh start-node.sh
    ```
    
- 이렇게 하면 spark3 폴더에는 master → head 로 이름이 변경되었고
    
    spark-node 폴더에는 slave → node 로 이름이 변경되었다.
    
- 이제 spark3/sbin 폴더에서 head 를 실행시키고 spark-node/sbin 폴더에서 node를
    
    실행 시키자.
    
    ![Untitled](/images/0731_Spark/Untitled%206.png)
    
    ![Untitled](/images/0731_Spark/Untitled%207.png)
    

- 그 뒤에 인터넷 주소창에 [localhost:8080](http://localhost:8080) 을 치면 사이트가 나온다.
    
    ![Untitled](/images/0731_Spark/Untitled%208.png)
    

---

# PySpark 설치 및 설정

- 환경 변수 설정으로 (vi ~/.bashrc)  들어가서 다음과 같이 입력한다
    
    ![Untitled](/images/0731_Spark/Untitled%209.png)
    

```python
export AIRFLOW_HOME=/home/dhtpdud2009/airflow
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export SPARK_HOME=/home/dhtpdud2009/spark3
export PATH=$JAVA_HOME/bin:$PATH
export PATH=$SPARK_HOME/bin:$PATH
export PYSPARK_PYTHON=/usr/bin/python3
# export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
```

- dhtpdud2009 부분은 알아서 바꾸기
- chapter14 폴더 만들고 가상환경 세팅하기
    
    ![Untitled](/images/0731_Spark/Untitled%2010.png)
    
- pip3 install findspark 입력 / pip install pyspark 입력
    
    ![Untitled](/images/0731_Spark/Untitled%2011.png)
    
    ![Untitled](/images/0731_Spark/Untitled%2012.png)
    
- pip3 install jupyter 입력
    
    ![Untitled](/images/0731_Spark/Untitled%2013.png)
    
- 그리고 다시 환경 변수 세팅 들어가서 주석처리 제거
    
    ![Untitled](/images/0731_Spark/Untitled%2014.png)
    
    source ~/.bashrc 까지 하기!
    

- Ubuntu 껐다가 다시 켜서 CHAPTER14 에서 code . 로 열기
- 새 파일 만들고 가상환경 접속 후 다음과 같이 입력
    
    ![Untitled](/images/0731_Spark/Untitled%2015.png)
    
    ![Untitled](/images/0731_Spark/Untitled%2016.png)
    

- jupyter notebook 입력
    
    ![Untitled](/images/0731_Spark/Untitled%2017.png)
    
- [localhost:8888](http://localhost:8888) 여기 ctrl+클릭하면 Jupyter Notebook 를 열 수 있음
    
    ![Untitled](/images/0731_Spark/Untitled%2018.png)