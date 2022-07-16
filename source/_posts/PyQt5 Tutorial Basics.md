---
title: "PyQt5 Tutorial Basic"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: PyQt5
clearReading: true
thumbnailImage: PyQt-Logo.wine.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-07-16 22:45:55'
---

PyQt5 Basic
<!-- excerpt -->

# PyQt5 Tutorial Basics

# PyQt5를 이용해서 간단한 창 만들기

## 기초 창 띄우기

---

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget

class MyApp(QWidget):

    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('My First Application')
        self.move(300, 300)
        self.resize(400, 200)
        self.show()

if __name__ == '__main__':
   app = QApplication(sys.argv)
   ex = MyApp()
   sys.exit(app.exec_())

```

### 설명

---

```python
        self.setWindowTitle('My First Application')
        self.move(300, 300)
        self.resize(400, 200)
        self.show()

```

- setWindowTitle() 은 타이틀창의 제목 설정
- move() 는 스크린의 x = 300px, y = 300px 의 위치로 이동
- resize() 는 크기를 너비 400px, 높이 200px 로 조절
- show() 는 스크린 출력함수

```python
if __name__ == '__main__':

```

- '**name**' 은 현재 모듈의 이름이 저장되는 내장 변수
- 만약에 '[moduleA.py](http://modulea.py/)' 라는 코드를 import 해서 예제 코드를 수행하면 __name__은 'moduleA' 가 된다.
- 코드를 직접 짜서 실행할 경우 **name** 은 **main** 이 된다.
- 즉, 코드를 보고 직접 실행하는지 모듈을 통해 불러오는지를 확인할 수 있다.

```python
    app = QApplication(sys.argv)

```

- 모든 PyQt5 애플리케이션은 애플리케이션 객체를 생성해야 한다.
- 출처 : [https://wikidocs.net/21920](https://wikidocs.net/21920)

### 결과

---

![2_1_opening.png](/images/PyCharm Tutorial Basics/2_1_opening.png)

## 어플리케이션 아이콘 넣기

---

- 타이틀바의 왼쪽 끝에 보여질 작은 이미지 넣기
- 아이콘으로 사용할 이미지 파일을 저장한다.
    
    ![web.png](/images/PyCharm Tutorial Basics/web.png)
    

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget
from PyQt5.QtGui import QIcon

class MyApp(QWidget):

  def __init__(self):
      super().__init__()
      self.initUI()

  def initUI(self):
      self.setWindowTitle('Icon')
      self.setWindowIcon(QIcon('web.png'))
      self.setGeometry(300, 300, 300, 200)
      self.show()

if __name__ == '__main__':
  app = QApplication(sys.argv)
  ex = MyApp()
  sys.exit(app.exec_())

```

### 설명

---

```python
self.setWindowIcon(QIcon('web.png'))

```

- setWindowIcon() 는 어플리케이션 아이콘을 설정함
- QIcon 객체를 따로 생성하여 QIcon()에 보여질 이미지('web.png')를 입력
- 이미지 파일을 다른 폴더에 따로 저장할 경우 경로까지 같이 입력하면 된다.

```python
self.setGeometry(300, 300, 300, 200)

```

- setGeometry() 는 창의 위치와 크기를 설정함.
- 1, 2번째 변수는 창의 x, y 위치를 결정하고 / 3, 4번째 변수는 창의 너비와 높이를 결정함
- 출처 : [https://wikidocs.net/21853](https://wikidocs.net/21853)

### 결과

---

![2_2_icon.png](/images/PyCharm Tutorial Basics/2_2_icon.png)

## 창 닫기 버튼

---

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton
from PyQt5.QtCore import QCoreApplication

class MyApp(QWidget):

  def __init__(self):
      super().__init__()
      self.initUI()

  def initUI(self):
      btn = QPushButton('Quit', self)
      btn.move(50, 50)
      btn.resize(btn.sizeHint())
      btn.clicked.connect(QCoreApplication.instance().quit)

      self.setWindowTitle('Quit Button')
      self.setGeometry(300, 300, 300, 200)
      self.show()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = MyApp()
    sys.exit(app.exec_())

```

### 설명

---

```python
from PyQt5.QtCore import QCoreApplication

```

- QtCore 모듈의 QCoreApplication 클래스를 불러온다

```python
btn = QPushButton('Quit', self)

```

- 버튼을 하나 만든다.
- 이 버튼(btn) 은 QPushButton 클래스의 인스턴스이다.
- 생성자 (QPushButton())의 첫 번째 파라미터에는 버튼에 표시될 텍스트를 입력하고, 두 번째 파라미터에는 버튼이 위치할 부모위젯을 입력한다.

```python
btn.clicked.connect(QCoreApplication.instance().quit)

```

- PyQt5 에서의 이벤트 처리는 [시그널과 슬롯](https://wikidocs.net/22020) 메커니즘으로 이루어진다.
- 버튼(btn)을 클릭하면 'clicked' 시그널이 만들어진다.
- instance() 는 현재 인스턴스를 반환한다.
- clicked 시그널은 어플리케이션을 종료하는 quit() 에 연결된다.
- 이렇게 발신자와 수신자, 두 객체간에 커뮤니케이션이 이루어져야 한다.
- 여기에서는 발신자는 푸시버튼 (btn)이고, 수신자는 어플리케이션 객체(app)이다.
- 마찬가지로 버튼 위치도 조정 가능하다.

### 결과

---

![2_3_closing.png](/images/PyCharm Tutorial Basics/2_3_closing.png)

## 툴팁 나타내기

---

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QToolTip
from PyQt5.QtGui import QFont

class MyApp(QWidget):

    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        QToolTip.setFont(QFont('SansSerif', 10))
        self.setToolTip('This is a <b>QWidget</b> widget')

        btn = QPushButton('Button', self)
        btn.setToolTip('This is a <b>QPushButton</b> widget')
        btn.move(50, 50)
        btn.resize(btn.sizeHint())

        self.setWindowTitle('Tooltips')
        self.setGeometry(300, 300, 300, 200)
        self.show()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = MyApp()
    sys.exit(app.exec_())

```

### 설명

---

```python
QToolTip.setFont(QFont('SansSerif', 10))
self.setToolTip('This is a <b>QWidget</b> widget')

```

- 먼저 툴팁에 사용될 폰트를 설정한다. 여기에서는 10px 크기의 'SansSerif' 폰트를 사용한다.
- 툴팁을 만들기 위해서는 setToolTip() 을 사용해서, 표시될 텍스트를 입력한다.

```python
btn = QPushButton('Button', self)
btn.setToolTip('This is a <b>QPushButton</b> widget')

```

- 푸시버튼을 하나 만들고, 이 버튼에도 툴팁을 달아준다.

```python
btn.move(50, 50)
btn.resize(btn.sizeHint())

```

- 버튼의 위치와 크기를 설정
- sizeHint() 는 버튼을 적절한 크기로 설정하도록 해준다
- 출처 : [https://wikidocs.net/21860](https://wikidocs.net/21860)

### 결과

---

![2_4_tooltip.png](/images/PyCharm Tutorial Basics/2_4_tooltip.png)

## 상태바 만들기

### 개념

---

- 메인창은 메뉴바, 툴바, 상태바를 갖는 전형적인 어플리케이션 창이다.
- QMenuBar, QToolBar, QDockWidget, QStatusBar 등의 고유의 레이아웃을 가지고 있다.
- 가운데 영역에 중심위젯을 위한 영역을 갖고 있으며, 여기에는 어떤 위젯도 들어올 수 있다.

![mainwindowlayout.png](/images/PyCharm Tutorial Basics/mainwindowlayout.png)

- QMainWindow 클래스를 이용해서 메인 어플리케이션 창을 만들 수 있다.
- QStatuseBar를 이용해서 메인 창에 상태바(status bar)를 하나 만들어보자.
- 상태바는 어플리케이션의 현재 상태를 알려주기 위해 어플리케이션의 하단에 위치하는 위젯이다
- 상태바에 텍스트를 표시하기 위해서는 showMessage() 를 사용한다
- 텍스트를 사라지게 하고 싶다면 clearMessage() 를 사용하거나, showMessage() 에 텍스트가 표시되는 시간도 설정할 수 있다.
- 현재 상태바에 표시되는 메세지 텍스트를 갖고 오고 싶을 때는 currentMessage()를 사용한다.
- QStatusBar 클래스는 상태바에 표시되는 메세지가 바뀔 때 마다 messageChanged() 시그널을 발생시킨다

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow

class MyApp(QMainWindow):

    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.statusBar().showMessage('Ready')

        self.setWindowTitle('Statusbar')
        self.setGeometry(300, 300, 300, 200)
        self.show()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = MyApp()
    sys.exit(app.exec_())
```

### 설명

---

```python
self.statusBar().showMessage('Ready')
```

- 상태바는 QMainWindow 클래스의 statusBar() 를 이용해서 만드는데, statusBar() 를 최초로 호출함으로써 만들어진다.
- 그 다음 호출부터는 상태바 객체를 반환한다.
- showMessage()를 통해 상태바에 보여질 메세지를 설정할 수 있다.
- 출처 : [https://wikidocs.net/21928](https://wikidocs.net/21928)

### 결과

---

![2_5_statusbar.png](/images/PyCharm Tutorial Basics/2_5_statusbar.png)

## 메뉴바 만들기

### 개념

---

- GUI 어플리케이션에서 메뉴바(menu bar)는 흔하게 사용된다.
- 다양한 명령들의 모음이 메뉴바에 위치한다. ([QMenuBar 공식 문서](https://doc.qt.io/qt-5/qmenubar.html))
- 우선 폴더안에 메뉴에 해당하는 아이콘(exit.png)을 저장한다
    
    ![exit.png](/images/PyCharm Tutorial Basics/exit.png)
    

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QAction, qApp
from PyQt5.QtGui import QIcon

class MyApp(QMainWindow):

    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        exitAction = QAction(QIcon('exit.png'), 'Exit', self)
        exitAction.setShortcut('Ctrl+Q')
        exitAction.setStatusTip('Exit application')
        exitAction.triggered.connect(qApp.quit)

        self.statusBar()

        menubar = self.menuBar()
        menubar.setNativeMenuBar(False)
        filemenu = menubar.addMenu('&File')
        filemenu.addAction(exitAction)

        self.setWindowTitle('Menubar')
        self.setGeometry(300, 300, 300, 200)
        self.show()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = MyApp()
    sys.exit(app.exec_())
```

- 어플리케이션을 종료하는 메뉴바를 만들었다. 이 기능은 단축키 (Ctrl+Q)로도 실행이 가능하다.

### 설명

---

```python
exitAction = QAction(QIcon('exit.png'), 'Exit', self)
exitAction.setShortcut('Ctrl+Q')
exitAction.setStatusTip('Exit application')
```

- 아이콘 (exit.png)과 ‘Exit’ 라벨을 갖는 하나의 동작 (action)을 만들고, 이 동작에 대해 단축키(shortcut)를 정의한다.
- 또한 메뉴에 마우스를 올렸을 때, 상태바에 나타날 상태팁을 setStatusTip()을 사용하여 설정한다.

```python
exitAction.triggered.connect(qApp.quit)
```

- 이 동작을 선택했을 때, 생성된 (triggered) 시그널이 QApplication 위젯의 quit() 에 연결되고, 어플리케이션을 종료하게 된다.

```python
menubar = self.menuBar()
menubar.setNativeMenuBar(False)
fileMenu = menubar.addMenu('&File')
fileMenu.addAction(exitAction)
```

- menuBar() 는 메뉴바를 생성한다. 이어서 ‘File’ 메뉴를 하나 만들고, 거기에 ‘exitAction’ 동작을 추가한다.
- ‘&File’ 의 앰퍼샌드(ampersand,&)는 간편하게 단축키를 설정하도록 해준다.
- ‘F’ 앞에 앰퍼샌드(&)가 있으므로’Alt+F’ 가 File 메뉴의 단축키가 된다. 만약 ‘File’의 ‘i’ 앞에 ‘&’을 넣으면 ‘Alt+I’가 단축키가 된다.
- 출처 : [https://wikidocs.net/21866](https://wikidocs.net/21866)

### 결과

---

![2_6_menubar.png](/images/PyCharm Tutorial Basics/2_6_menubar.png)

## 툴바 만들기

---

- 메뉴(menu)가 어플리케이션에서 사용되는 모든 명령의 모음이라면, 툴바(toolbar)는 자주 사용하는 명령들을 더 편리하게 사용하도록 해준다.
- 폴더 안에 툴바의 각 기능에 해당하는 아이콘들을 저장한다

![save.png](/images/PyCharm Tutorial Basics/save.png)

save.png

![edit.png](/images/PyCharm Tutorial Basics/edit.png)

edit.png

![print.png](/images/PyCharm Tutorial Basics/print.png)

print.png

![exit.png](/images/PyCharm Tutorial Basics/exit%201.png)

exit.png

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QAction, qApp
from PyQt5.QtGui import QIcon

class MyApp(QMainWindow):

    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        exitAction = QAction(QIcon('exit.png'), 'Exit', self)
        exitAction.setShortcut('Ctrl+Q')
        exitAction.setStatusTip('Exit application')
        exitAction.triggered.connect(qApp.quit)

        self.statusBar()

        self.toolbar = self.addToolBar('Exit')
        self.toolbar.addAction(exitAction)

        self.setWindowTitle('Toolbar')
        self.setGeometry(300, 300, 300, 200)
        self.show()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = MyApp()
    sys.exit(app.exec_())
```

### 설명

---

```python
exitAction = QAction(QIcon('exit.png'), 'Exit', self)
exitAction.setShortcut('Ctrl+Q')
exitAction.setStatusTip('Exit application')
exitAction.triggered.connect(qApp.quit)
```

- 메뉴바의 경우와 마찬가지로 QAction 객체를 하나 생성한다.
- 이 객체는 아이콘 (exit.png), 라벨 (’Exit’)을 포함하고, 단축키 (Ctrl+Q)를 통해 실행가능하다.
- 상태바에 메세지(’Exit application’) 를 보여주고, 클릭 시 생성되는 시그널은 quit() 에 연결되어있다.

```python
self.toolbar = self.addToolBar('Exit')
self.toolbar.addAction(exitAction)
```

- addToolbar()를 이용해서 툴바를 만들고, addAction() 을 이용해서 툴바에 exitAction 동작을 추가한다
- 출처 : [https://wikidocs.net/21932](https://wikidocs.net/21932)

### 결과

---

![2_7_toolbar.png](/images/PyCharm Tutorial Basics/2_7_toolbar.png)

## 창을 화면의 가운데로 띄우기

---

![2_8_centering.png](/images/PyCharm Tutorial Basics/2_8_centering.png)

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QDesktopWidget

class MyApp(QWidget):

    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle('Centering')
        self.resize(500, 350)
        self.center()
        self.show()

    def center(self):
        qr = self.frameGeometry()
        cp = QDesktopWidget().availableGeometry().center()
        qr.moveCenter(cp)
        self.move(qr.topLeft())

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = MyApp()
    sys.exit(app.exec_())
```

### 설명

---

```python
self.center()
```

- center() 를 통해서 창이 화면의 가운데로 위치하게 된다.

```python
qr = self.frameGeometry()
```

- frameGeometry() 를 이용해서 창의 위치와 크기 정보를 가져온다.

```python
cp = QDesktopWidget().availableGeometry().center()
```

- 사용하는 모니터 화면의 가운데 위치를 파악한다.

```python
qr.moveCenter(cp)
```

- 창의 직사각형 위치를 화면의 중심의 위치로 이동시킨다.

```python
self.move(qr.topLeft())
```

- 현재 창을, 화면의 중심으로 이동했던 직사각형(qr)의 위치로 이동시킨다.
- 결과적으로 현재 창의 중심이 화면의 중심과 일치하게 돼서 창이 가운데에 나타난다.
- 출처 : [https://wikidocs.net/26684](https://wikidocs.net/26684)

## 날짜와 시간 표시하기

### 날짜 표시하기(QDate)

---

- QDate 클래스는 날짜와 관련된 기능들을 제공한다.

### 현재 날짜 출력하기

---

```python
from PyQt5.QtCore import QDate

now = QDate.currentDate()
print(now.toString())
```

- currentDate() 는 현재 날짜를 반환한다.
- toString() 는 현재 날짜를 문자열로 출력할 수 있다.

### 날짜 형식 지정하기

---

- toString() 의 format 파라미터를 설정함으로써 날짜의 형식을 정할 수 있다.

```python
from PyQt5.QtCore import QDate, Qt

now = QDate.currentDate()
print(now.toString('d.M.yy'))
print(now.toString('dd.MM.yyyy'))
print(now.toString('ddd.MMMM.yyyy'))
```

- ‘d’는 일(day), ‘M’은 달(month), ‘y’는 연도(year)를 나타낸다. 각 문자의 개수에 따라 날짜의 형식이 다르게 출력된다.

```python
print(now.toString(Qt.ISODate))
print(now.toString(Qt.DefaultLocaleLongDate))
```

- Qt.ISODate, Qt.DefaultLocaleLongDate를 입력함으로써 ISO 표준 형식 또는 어플리케이션의 기본 설정에 맞게 출력할 수 있다.

### 시간 표시하기(QTime)

---

- QTime 클래스를 이용해서 현재의 시간을 출력할 수 있다.

### 현재 시간 출력하기

---

```python
from PyQt5.QtCore import QTime

time = QTime.currentTime()
print(time.toString())
```

- currentTime() 은 현재 시간을 반환한다.
- toString() 은 현재 시간을 문자열로 반환한다.

### 시간 형식 설정하기

---

```python
from PyQt5.QtCore import QTime, Qt

time = QTime.currentTime()
print(time.toString('h.m.s'))
print(time.toString('hh.mm.ss'))
print(time.toString('hh.mm.ss.zzz'))
print(time.toString(Qt.DefaultLocaleLongDate))
print(time.toString(Qt.DefaultLocaleShortDate))
```

- ‘h’는 시간(hour), ‘m’은 분(minute), ‘s’는 초(second), 그리고 ‘z’는 1000분의 1초를 나타낸다
- 날짜와 마찬가지로 Qt.DefaultLocaleLongDate 또는 Qt.DefaultLocaleShortDate 등으로 시간의 형식을 설정할 수 있다.

### 날짜와 시간 표시하기(QDateTime)

---

- QDateTime 클래스를 이용해서 현재 날짜와 시간을 함께 출력할 수 있다.

### 현재 날짜와 시간 출력하기

---

```python
from PyQt5.QtCore import QDateTime

datetime = QDateTime.currentDateTime()
print(datetime.toString())
```

- currentDateTime() 은 현재의 날짜와 시간을 나타내준다.
- toString() 은 날짜와 시간을 문자열 형태로 변환해준다.

### 날짜와 시간 형식 설정하기

---

```python
from PyQt5.QtCore import QDateTime, Qt

datetime = QDateTime.currentDateTime()
print(datetime.toString('d.M.yy hh:mm:ss'))
print(datetime.toString('dd.MM.yyyy, hh:mm:ss'))
print(datetime.toString(Qt.DefaultLocaleLongDate))
print(datetime.toString(Qt.DefaultLocaleShortDate))
```

- 위의 예제에서와 마찬가지로 날짜에 대해 ‘d’, ‘M’, ‘y’, 시간에 대해 ‘h’, ‘m’, ‘s’ 등을 사용해서 날짜와 시간이 표시되는 형식을 설정할 수 있다.
- 또한 Qt.DefaultLocaleLongDate 또는 Qt.DefaultLocaleShortDate 를 입력할 수 있다.

### 상태표시줄에 날짜 표시하기

---

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow
from PyQt5.QtCore import QDate, Qt

class MyApp(QMainWindow):

    def __init__(self):
        super().__init__()
        self.date = QDate.currentDate()
        self.initUI()

    def initUI(self):
        self.statusBar().showMessage(self.date.toString(Qt.DefaultLocaleLongDate))

        self.setWindowTitle('Date')
        self.setGeometry(300, 300, 400, 200)
        self.show()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = MyApp()
    sys.exit(app.exec_())
```

- currentDate() 를 통해 현재 날짜를 얻고 showMessage() 로 상태표시줄에 현재 날짜를 표시한다
- 출처 : [https://wikidocs.net/22074](https://wikidocs.net/22074)

### 결과

![2_9_showing_date.png](/images/PyCharm Tutorial Basics/2_9_showing_date.png)

## 스타일 꾸며보기

---

### 코드

```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QVBoxLayout

class MyApp(QWidget):

    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):

        lbl_red = QLabel('Red')
        lbl_green = QLabel('Green')
        lbl_blue = QLabel('Blue')

        lbl_red.setStyleSheet("color: red;"
                             "border-style: solid;"
                             "border-width: 2px;"
                             "border-color: #FA8072;"
                             "border-radius: 3px")
        lbl_green.setStyleSheet("color: green;"
                               "background-color: #7FFFD4")
        lbl_blue.setStyleSheet("color: blue;"
                              "background-color: #87CEFA;"
                              "border-style: dashed;"
                              "border-width: 3px;"
                              "border-color: #1E90FF")

        vbox = QVBoxLayout()
        vbox.addWidget(lbl_red)
        vbox.addWidget(lbl_green)
        vbox.addWidget(lbl_blue)

        self.setLayout(vbox)

        self.setWindowTitle('Stylesheet')
        self.setGeometry(300, 300, 300, 200)
        self.show()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ex = MyApp()
    sys.exit(app.exec_())
```

### 설명

---

```python
lbl_red = QLabel('Red')
lbl_green = QLabel('Green')
lbl_blue = QLabel('Blue')
```

- QLabel 클래스를 이용해서 3개의 라벨 위젯을 만든다
- 텍스트는 각각 ‘Red’, ‘Green’, ‘Blue’ 로 설정한다

```python
lbl_red.setStyleSheet("color: red;"
"border-style: solid;"
"border-width: 2px;"
"border-color: #FA8072;"
"border-radius: 3px")
```

- setStyleSheet() 를 이용해서 글자색을 빨간색(red)으로
- 경계선을 실선(solid)으로
- 경계선 두께를 2px로
- 경계선 색을 #FA8072 색으로
- 경계선의 모서리를 3px만큼 둥글게 설정한다

```python
lbl_green.setStyleSheet("color: green;"
                        "background-color: #7FFFD4")
```

- 마찬가지로, lbl_green 라벨의 글자색을 녹색(green)으로
- 배경색을 #7FFFD4 색으로 설정한다

```python
lbl_blue.setStyleSheet("color: blue;"
                       "background-color: #87CEFA;"
                       "border-style: dashed;"
                       "border-width: 3px;"
                       "border-color: #1E90FF")
```

- lbl_blue 라벨의 글자색을 파란색(blue)으로
- 배경색을 #87CEFA 색으로
- 경계선을 대쉬 스타일로
- 경계선 두께를 3px로
- 경계선 색을 #1E90FF으로 설정합니다

```python
vbox = QVBoxLayout()
vbox.addWidget(lbl_red)
vbox.addWidget(lbl_green)
vbox.addWidget(lbl_blue)

self.setLayout(vbox)
```

- 수직 박스 레이아웃(QVBoxLayout())을 이용해서 세 개의 라벨 위젯을 수직으로 배치한다

### 결과

---

![2_10_stylesheets_8r6WeZv.png](/images/PyCharm Tutorial Basics/2_10_stylesheets_8r6WeZv.png)