# [DAY 8] 페이스북 챗봇 만들기

## 파이썬 실행파일 만들기

다음과 같이 실행파일을 만들고 싶은 프로그램을 짠다. 파일명을 `helloworld.py`라고 저장한다.

```python
print('Hello World')
```

### 윈도우

터미널에서 아래와 같이 입력해 `py2exe`를 설치한다.

```bash
pip install py2exe
```

다음과 같이 입력해 `setup.py`를 작성한다.

```python
from distutils.core import setup
import py2exe

setup(console=['helloworld.py'])
```

터미널에서 다음과 같이 입력한다.

```
python setup.py py2exe
```

실행하면 `dist`폴더에 실행할 수 있는 `hello.exe`파일이 생긴다.

### 맥

터미널에서 아래와 같이 입력해 `py2app`을 설치한다.

```bash
pip install py2app
```

다음과 같이 입력해 `setup.py`를 작성한다.

```python
from setuptools import setup
setup(
    app=["helloworld.py"],
    setup_requires=["py2app"],
)
```

터미널에서 다음과 같이 입력한다.

```undefined
python setup.py py2app -A
```

실행하면 `dist`폴더에 실행할 수 있는 파일이 생긴다.

만약 터미널에서 실행하려면 다음과 같이 입력한다.

```
./dist/helloworld.app/Contents/MacOS/helloworld
```

## 소리 추가하기

## Yahoo Weather API

[https://developer.yahoo.com/weather/](https://developer.yahoo.com/weather/) 에 접속한다.

설정을 통해 서울의 날씨 정보를 얻을 수 있다.

```python
import urllib.request

with urllib.request.urlopen('https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22seoul%2C%20ko%22)&format=json&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys') as response:
    text = response.read()
    print(text)
```

위와 같이 실행하면 날씨 정보에 대한 JSON을 받아서 출력한다.

```python
import urllib.request
import json

with urllib.request.urlopen('https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22seoul%2C%20ko%22)&format=json&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys') as response:
    text = response.read()
    print(text)
    j = json.loads(text)
```

`json` 모듈을 추가해 파이썬에서 json을 제어할 수 있다.
