---
title: "Python 가상환경 설정"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: Python
clearReading: true
thumbnailImage: image.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-07-18 15:42:20'
---

Python 가상환경을 Jupyter Notebook 으로 설정하는 방법
<!-- excerpt -->

# Python_venv

- 폴더 들어가서

```python
pip install virtualenv
```

입력 후

![Untitled](/images/Python_venv/Untitled.png)

```python
virtualenv venv
```

입력 후

![Untitled](/images/Python_venv/Untitled%201.png)

```python
code .
```

를 치면 Visual Studio 가 나온다

![Untitled](/images/Python_venv/Untitled%202.png)

- Visual Studio 에서 터미널을 Git Bash 로 열고

![Untitled](/images/Python_venv/Untitled%203.png)

```python
source venv/Scripts/activate

pip install numpy pandas scikit-learn matplotlib seaborn jupyterlab mlflow
Collecting numpy
```

순서대로 입력

![Untitled](/images/Python_venv/Untitled%204.png)

```python
jupyter lab
```

입력하면 JupyterLab 열림