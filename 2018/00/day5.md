# [DAY 5] 클래스 & 게임 만들기

## 창 크기 설정

```python
def setup():
    size(400, 600)
```

## 배경색 흰색 설정

```python
def setup():
    size(400, 600)
    background(255)
```

## 점으로 빗방울 그리기

```python
def setup():
    size(400, 600)
    background(255)
    point(200, 300)
```

### 점의 두께 바꾸기

```python
def setup():
    size(400, 600)
    background(255)
    strokeWeight(8)
    point(200, 300)
```

## 위에서 아래로 빗방울이 떨어지게 만들기

### 빗방울의 좌표를 저장할 변수 만들기

```python
x = 200
y = 0

def setup():
    size(400, 600)
    background(255)
    strokeWeight(8)
    
def draw():
    point(x, y)
```

위 코드를 실행하면 에러가 난다. 전역 변수와 지역 변수 때문이다.

```python
x = 200
y = 0
```

이 부분은 코드의 모든 부분에서 사용 가능한 전역 변수 부분이다.

```python
point(x, y)
```

여기에 `x`, `y`는 지역 변수로서 설정이 되어있다.

```python
x = 200
y = 0

def setup():
    size(400, 600)
    background(255)
    strokeWeight(8)
    
def draw():
  	global x, y
    point(x, y)
```

위와 같이 `global x, y`처럼 입력해야 전역 변수를 사용할 수 있다.

### 빗방울의 좌표가 계속 아래로 내려가게 만들기

```python
x = 200
y = 0

def setup():
    size(400, 600)
    background(255)
    strokeWeight(8)
    
def draw():
    global x, y
    y = y + 1
    point(x, y)
```

그런데 위 코드를 실행하면 점이 내려가는 것이 아니라 선이 그려진다.

```python
x = 200
y = 0

def setup():
    size(400, 600)
    strokeWeight(8)
    
def draw():
    background(255)
    global x, y
    y = y + 1
    point(x, y)
```

위와 같이 매번 배경이 다시 그려지게 만들어야 한다.

```python
rain = PVector(200, 0)

def setup():
    size(400, 600)
    strokeWeight(8)
    
def draw():
    background(255)
    global rain
    rain.y = rain.y + 1
    point(rain.x, rain.y)
```

프로세싱의 `PVector`를 이용해 쉽게 좌표 정보를 관리할 수 있다.

```python
rain = PVector(200, 0)

def setup():
    size(400, 600)
    strokeWeight(8)
    
def draw():
    background(255)
    global rain
    rain.y = rain.y + 5
    point(rain.x, rain.y)
```

`rain.y = rain.y + 5`와 같이 빗방울의 속도를 바꿔본다.

## 빗방울이 아래로 내려가면 다시 위에서 내려가게 만들기

```python
rain = PVector(200, 0)

def setup():
    size(400, 600)
    strokeWeight(8)
    
def draw():
    background(255)
    global rain
    rain.y = rain.y + 5
    if rain.y > height:
        rain.y = 0
    point(rain.x, rain.y)
```

## 빗방울이 다시 떨어질때 x 좌표가 랜덤하게 바뀌도록 하기

```python
import random

rain = PVector(200, 0)

def setup():
    size(400, 600)
    strokeWeight(8)
    
def draw():
    background(255)
    global rain
    rain.y = rain.y + 5
    if rain.y > height:
        rain.y = 0
        x = random.randrange(0, width)
        rain.x = x
    point(rain.x, rain.y)
```


