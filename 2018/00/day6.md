# [DAY 6] 게임 만들기

## 창 크기 설정

```python
def setup():
    size(600, 400)
```

## 배경색 흰색 설정

```python
def setup():
    size(600, 400)
    
def draw():
    background(255)
```

## 플레이어 그리기

```python
def setup():
    size(600, 400)
    
def draw():
    background(255)
    ellipse(300, 350, 50, 50)
```

## 마우스에 맞춰 플레이어 움직이기

```pytho
def setup():
    size(600, 400)
    
def draw():
    background(255)
    ellipse(mouseX, 350, 50, 50)
```

## 플레이어 클래스 만들기

### 메인

```python
from player import *

def setup():
    global player
    player = Player()
    size(600, 400)
    
def draw():
    background(255)
    global player
    player.display()
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)
        
    def display(self):
        self.pos.x = mouseX
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

## 아이템 클래스 만들기

### 메인

```python
from player import *
from item import *

def setup():
    global player
    player = Player()
    global item
    item = Item()
    size(600, 400)
    
def draw():
    background(255)
    global player
    player.display()
    global item
    item.display()
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)
        
    def display(self):
        self.pos.x = mouseX
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        x = random.randrange(0, width)
        self.pos = PVector(x, -50)
        
    def display(self):
        self.pos.y = self.pos.y + 5
        ellipse(self.pos.x, self.pos.y, 25, 25)
```

## update / display 분리

### 메인

```python
from player import *
from item import *

def setup():
    global player
    player = Player()
    global item
    item = Item()
    size(600, 400)
    
def draw():
    background(255)
    global player
    player.update()
    player.display()
    global item
    item.update()
    item.display()
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)
        
		def update(self):
        self.pos.x = mouseX
         
    def display(self):
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        x = random.randrange(0, width)
        self.pos = PVector(x, -50)
        
    def update(self):
        self.pos.y = self.pos.y + 5

    def display(self):
        ellipse(self.pos.x, self.pos.y, 25, 25)
```

## reset 함수 만들기

### 메인

```python
from player import *
from item import *

def setup():
    global player
    player = Player()
    global item
    item = Item()
    size(600, 400)
    
def draw():
    background(255)
    global player
    player.update()
    player.display()
    global item
    item.update()
    item.display()
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)
    
    def update(self):
        self.pos.x = mouseX
         
    def display(self):
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        self.reset()
        
    def reset(self):
        x = random.randrange(0, width)
        self.pos = PVector(x, -50)
        
    def update(self):
        self.pos.y = self.pos.y + 5

    def display(self):
        ellipse(self.pos.x, self.pos.y, 25, 25)
```

## 아이템이 아래로 다 떨어지면 다시 초기화하기

### 메인

```python
from player import *
from item import *

def setup():
    global player
    player = Player()
    global item
    item = Item()
    size(600, 400)

def draw():
    background(255)
    global player
    player.update()
    player.display()
    global item
    item.update()
    item.display()
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)

    def update(self):
        self.pos.x = mouseX

    def display(self):
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        self.reset()
        
    def reset(self):
        x = random.randrange(0, width)
        self.pos = PVector(x, -50)
        
    def update(self):
        self.pos.y = self.pos.y + 5
        if self.pos.y > height:
            self.reset()

    def display(self):
        ellipse(self.pos.x, self.pos.y, 25, 25)
```

## 아이템 갯수 늘리기

### 메인

```python
from player import *
from item import *

items = []

def setup():
    global player
    player = Player()
    global items
    for n in range(0, 10):
        items.append(Item())
    size(600, 400)
    
def draw():
    background(255)
    global player
    player.update()
    player.display()
    global items
    for item in items:
        item.update()
        item.display()
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)
    
    def update(self):
        self.pos.x = mouseX
         
    def display(self):
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        self.reset()
        
    def reset(self):
        x = random.randrange(0, width)
        self.pos = PVector(x, -50)
        
    def update(self):
        self.pos.y = self.pos.y + 5
        if self.pos.y > height:
            self.reset()

    def display(self):
        ellipse(self.pos.x, self.pos.y, 25, 25)
```

## 아이템 속도, 시작 위치 다르게 하기

### 메인

```python
from player import *
from item import *

items = []

def setup():
    global player
    player = Player()
    global items
    for n in range(0, 10):
        items.append(Item())
    size(600, 400)

def draw():
    background(255)
    global player
    player.update()
    player.display()
    global items
    for item in items:
        item.update()
        item.display()
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)

    def update(self):
        self.pos.x = mouseX

    def display(self):
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        self.reset()
        
    def reset(self):
        x = random.randrange(0, width)
        y = random.randrange(50, height)
        v = random.randrange(5, 11)
        self.pos = PVector(x, -y)
        self.velocity = v
        
    def update(self):
        self.pos.y = self.pos.y + self.velocity
        if self.pos.y > height:
            self.reset()

    def display(self):
        ellipse(self.pos.x, self.pos.y, 25, 25)
```

## 아이템 충돌 확인하기

### 메인

```python
from player import *
from item import *

items = []

def setup():
    global player
    player = Player()
    global items
    for n in range(0, 10):
        items.append(Item())
    size(600, 400)
    
def draw():
    background(255)
    global player
    player.update()
    player.display()
    global items
    for item in items:
        item.update(player)
        item.display()
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)

    def update(self):
        self.pos.x = mouseX

    def display(self):
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        self.reset()
        
    def reset(self):
        x = random.randrange(0, width)
        y = random.randrange(50, height)
        v = random.randrange(5, 11)
        self.pos = PVector(x, -y)
        self.velocity = v
        
    def update(self, player):
        self.pos.y = self.pos.y + self.velocity
        
        if dist(player.pos.x, player.pos.y, self.pos.x, self.pos.y) < 37.5:
            self.reset()
        elif self.pos.y > height:
            self.reset()

    def display(self):
        ellipse(self.pos.x, self.pos.y, 25, 25)
```

여기서 `dist`는 두 점의 거리를 재는 명령어다. 

## 플레이어 목숨 표시하기

### 메인

```python
from player import *
from item import *

items = []

def setup():
    global player
    player = Player()
    global items
    for n in range(0, 10):
        items.append(Item())
    size(600, 400)
    
def draw():
    background(255)
    global player
    player.update()
    player.display()
    global items
    for item in items:
        item.update(player)
        item.display()
    drawLife()

def drawLife():
    fill(0)
    textSize(30)
    text("Life : " + str(player.life), 20, 40)
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)
        self.life = 5
    
    def update(self):
        self.pos.x = mouseX
         
    def display(self):
        fill(255)
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        self.reset()
        
    def reset(self):
        x = random.randrange(0, width)
        y = random.randrange(50, height)
        v = random.randrange(5, 11)
        self.pos = PVector(x, -y)
        self.velocity = v
        
    def update(self, player):
        self.pos.y = self.pos.y + self.velocity
        
        if dist(player.pos.x, player.pos.y, self.pos.x, self.pos.y) < 37.5:
            self.reset()
        elif self.pos.y > height:
            self.reset()

    def display(self):
        fill(255)
        ellipse(self.pos.x, self.pos.y, 25, 25)
```

`textSize`는 텍스트 크기를 설정하는 명령어다. `text`는 화면에 글자를 쓰는 명령어다. `text("Life : " + str(player.life), 20, 40)`에서 `"Life : " + str(player.life)`가 글자로 찍힌다. 글자의 왼쪽 아래가 좌표 (20, 40)에 온다.

## 아이템을 먹었을때 생명을 더하거나 빼기

### 메인

```python
from player import *
from item import *

items = []

def setup():
    global player
    player = Player()
    global items
    for n in range(0, 10):
        items.append(Item())
    size(600, 400)
    
def draw():
    background(255)
    global player
    player.update()
    player.display()
    global items
    for item in items:
        item.update(player)
        item.display()
    drawLife()

def drawLife():
    fill(0)
    textSize(30)
    text("Life : " + str(player.life), 20, 40)
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)
        self.life = 5
    
    def update(self):
        self.pos.x = mouseX
         
    def display(self):
        fill(255)
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        self.reset()
        
    def reset(self):
        x = random.randrange(0, width)
        y = random.randrange(50, height)
        v = random.randrange(5, 11)
        m = random.randrange(0, 2)
        self.pos = PVector(x, -y)
        self.velocity = v
        self.mode = m
        
    def update(self, player):
        self.pos.y = self.pos.y + self.velocity
        
        if dist(player.pos.x, player.pos.y, self.pos.x, self.pos.y) < 37.5:
            if self.mode == 0:
                player.life = player.life + 1
                if player.life > 10:
                    player.life = 10
            elif self.mode == 1:
                player.life = player.life - 1
                if player.life < 0:
                    player.life = 0
            self.reset()
        elif self.pos.y > height:
            self.reset()

    def display(self):
        if self.mode == 0:
            fill(0, 0, 255)
        elif self.mode == 1:
            fill(255, 0, 0)

        ellipse(self.pos.x, self.pos.y, 25, 25)
```

## 성공 / 실패 표시하기

### 메인

```python
from player import *
from item import *

items = []

def setup():
    global player
    player = Player()
    global items
    for n in range(0, 10):
        items.append(Item())
    size(600, 400)
    
def draw():
    background(255)
    global player
    if player.life == 10:
        textSize(50)
        textAlign(CENTER)
        text("Clear", width/2, height/2)
        return
    elif player.life == 0:
        textSize(50)
        textAlign(CENTER)
        text("Failed", width/2, height/2)
        return
    
    player.update()
    player.display()
    global items
    for item in items:
        item.update(player)
        item.display()
    drawLife()
    
def drawLife():
    fill(0)
    textSize(30)
    textAlign(LEFT)
    text("Life : " + str(player.life), 20, 40)
```

### player.py

```python
class Player:
    def __init__(self):
        self.pos = PVector(width/2, 350)
        self.life = 5
    
    def update(self):
        self.pos.x = mouseX
         
    def display(self):
        fill(255)
        ellipse(self.pos.x, self.pos.y, 50, 50)
```

### item.py

```python
import random

class Item:
    def __init__(self):
        self.reset()
        
    def reset(self):
        x = random.randrange(0, width)
        y = random.randrange(50, height)
        v = random.randrange(5, 11)
        m = random.randrange(0, 2)
        self.pos = PVector(x, -y)
        self.velocity = v
        self.mode = m
        
    def update(self, player):
        self.pos.y = self.pos.y + self.velocity
        
        if dist(player.pos.x, player.pos.y, self.pos.x, self.pos.y) < 37.5:
            if self.mode == 0:
                player.life = player.life + 1
                if player.life > 10:
                    player.life = 10
            elif self.mode == 1:
                player.life = player.life - 1
                if player.life < 0:
                    player.life = 0
            self.reset()
        elif self.pos.y > height:
            self.reset()

    def display(self):
        if self.mode == 0:
            fill(0, 0, 255)
        elif self.mode == 1:
            fill(255, 0, 0)

        ellipse(self.pos.x, self.pos.y, 25, 25)
```

`textAlign`은 텍스트의 정렬을 정하는 명령어다. `textAlign(CENTER)`는 가운데 정렬한다는 뜻이다.

## Mission

게임에 소리를 넣는다던지 이미지를 넣어 더 꾸며본다.
