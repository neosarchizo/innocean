# [DAY 7] 웹 자료 받기

## 파일 읽기

```python
with open('helloworld.txt') as f:
    read_data = f.read()
    print(read_data)
```

스케치를 저장하고 아래와 같이 스케치 폴더를 연다.

![day7_00](img/day7_00.jpg)

`스케치` 메뉴에서 `스케치 폴더 열기`를 선택한다.

`helloworld.txt`라고 파일을 만들고 다음과 같이 내용을 입력한다.

```textile
Hello World!
Hello World!!
Hello World!!!
Hello World!!!!
Hello World!!!!!
```

`with`는 특정 변수가 동작하는 영역을 설정하는 것이다. 이 영역을 벗어나면 알아서 변수가 초기화된다.

`open`은 파일을 여는 명령어다.

파일을 열면 `f`라는 이름의 변수가 연 파일을 제어할 수 있게 된다.

이 변수에서 `read` 명령어를 사용하면 파일의 내용을 읽어 반환한다.



```python
with open('helloworld.txt') as f:
    for line in f:
        print(line)
```

위와 같이 실행시 파일의 내용을 한 줄씩 읽는다.



## 파일 쓰기

```python
with open('test.txt', 'w') as f:
    f.write('abc\nabc\nabc\nabc\n')
```

파일에 내용을 쓰기 위해서는 `open('test.txt', 'w')` 와 같이 입력해야한다. 만약 `test.txt` 파일이 없다면 파일을 만든다.

`write` 명령어를 사용하면 입력한 값을 파일에 적는다.

```python
with open('test.txt', 'a') as f:
    f.write('abc\nabc\nabc\nabc\n')
```

`open('test.txt', 'a')`와 같이 입력하면 내용을 기존 파일 맨 뒤에 덧 붙인다.



## 파일 다운로드

`atom`을 열고 다음과 같이 입력한다.

```python
import urllib.request
import shutil

with urllib.request.urlopen('http://www.innocean.com/imgs/img_logo.svg') as response:
    with open('a.svg', 'wb') as out_file:
        shutil.copyfileobj(response, out_file)
```

`urllib.request`이 웹에서 데이터를 받을때 사용하는 모듈이고, `shutil`이 파일을 저장할때 사용하는 모듈이다.

```python
import urllib.request
import shutil

def download_file(url):
    with urllib.request.urlopen(url) as response:
        name_parts = url.split('/')
        with open(name_parts[-1], 'wb') as out_file:
            shutil.copyfileobj(response, out_file)

download_file('http://digitalspyuk.cdnds.net/18/14/1600x1066/gallery-1522945902-mlu-17652-r.jpg')

```

## Dialog로 입력 값 받기

```python
from tkinter import *

class InputDialog(object):

    def __init__(self,requestMessage):
        self.root = Tk()
        self.string = ''
        self.frame = Frame(self.root)
        self.frame.pack()
        self.acceptInput(requestMessage)

    def acceptInput(self,requestMessage):
        r = self.frame
        self.e = Entry(r,text='Name')
        self.e.pack(side='left')
        self.e.focus_set()
        k = Label(r,text=requestMessage)
        k.pack(side='left')
        b = Button(r,text='okay',command=self.gettext)
        b.pack(side='right')

    def gettext(self):
        self.string = self.e.get()
        self.root.destroy()

    def getString(self):
        return self.string

    def waitForInput(self):
        self.root.mainloop()

def getText(requestMessage):
    msgBox = InputDialog(requestMessage)
    #loop until the user makes a decision and the window is destroyed
    msgBox.waitForInput()
    return msgBox.getString()

var = getText('enter your name')
print("Var:" + var)
```
