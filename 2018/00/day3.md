# [DAY 3] 챗봇 만들기

## 조건문

의사결정해야하는 상황에서 컴퓨터가 판단하게 만들려면 어떻게 해야할까?

그와 관련해 다음과 같은 코드를 콘솔에서 실행해본다.

```python
1 + 2 = 3
```

위 코드는 문제가 없어지만 막상 실행하면 에러가 난다. 왜냐면 프로그램에서 `=`는 오른쪽의 값을 왼쪽에 넣으라는 뜻이기 때문이다. 

```python
1 + 2 == 3
```

위 코드가 바로 좌변과 우변이 동일한지 확인하라는 뜻이다. 실행하면 콘솔에 `True`가 뜨는 것을 볼 수 있다.

```python
1 + 2 == 4
```

위와 같이 실행하면 콘솔에 `False`라고 뜬다.

```python
'abc' == 'apple'
[1, 2, 3] == [3, 4]
```

위와 같이 글자와 배열끼리 비교를 할 수도 있다.

이렇게 얻는 예(True), 아니오(False) 정보를 이용해 컴퓨터가 원하는데로 동작하게 할 수 있다.

```python
if 1 + 2 == 3:
  print('Hello World')
```

위 코드를 실행하면 `Hello World`가 뜬다. 당연히 `1 + 2 == 3`이 `True`이기 때문이다.

```python
if 1 + 2 == 4:
  print('Hello World')
```

이렇게 하면 `Hello World`가 뜨지 않는다. `if`문은 조건이 맞는 경우에만 실행된다.

```python
if 1 + 2 == 4:
  print('Hello World')
else:
  print('Bye')
```

위와 같이 하고 조건을 맞게 했다 틀리게 했다 해본다. 조건이 틀린 경우 `else`에 있는 코드가 실행된다.

## 입력

사용자에게서 키보드 입력을 받고 싶다면 어떻게 해야할까?

```python
name = input('이름을 입력해주세요!')
print(name)
```

위 코드를 실행하면 `이름을 입력해주세요!`라는 글이 뜨고 사용자가 키보드 입력하는 것을 기다린다. 원하는 글자를 적고 엔터를 치면 `name`변수에 입력한 값이 들어간 것을 볼 수 있다.

위 `input`과 `if`문을 이용해 간단한 퀴즈 프로그램을 만들어본다.

## 챗봇 만들기

먼저 `안녕`이라고 말하면 인사하게 만든다.

```python
print('채팅을 시작합니다.')

answer = input('나> ')

if answer == '안녕':
  print('PC> 안녕하세요!')
```

만약 인사를 랜덤하게 하도록 만들려면 어떻게 해야할까?

```python
import random

print('채팅을 시작합니다.')

hi_words = ['안녕!', '안녕하세요!', '어! 왔니?']

answer = input('나> ')

if answer == '안녕':
  r = random.randrange(0, len(hi_words))
  print('PC> ' + hi_words[r])
```

문제는 위와 같이 짜면 한번만 실행되고 끝난다는 것이다. 계속 반복하도록 만들고 싶다. 이때 사용하는 것이 `while`문이다.

```python
while True:
  print('Hello World')
```

위 코드를 실행하면 계속 `Hello World`가 찍힌다. `while`은 조건이 `True`인 경우에 계속 실행된다.

```python
a = 0

while a < 3:
  print('Hello World')
  a = a + 1
```

위 코드를 실행하면 `Hello World`가 3번만 실행된다.

```python
a = 0

while True:
  if a > 3:
    break
  print('Hello World')
  a = a + 1
```

`break`는 `for`문이나 `while`문에서 빠져 나갈때 사용한다.

```python
import random
import time

print('채팅을 시작합니다.')

hi_words = ['안녕!', '안녕하세요!', '어! 왔니?']

while True:
  answer = input('나> ')

  if answer == '안녕':
    r = random.randrange(0, len(hi_words))
    print('PC> ' + hi_words[r])
  
  time.sleep(1)
```

위와 같이 코드를 실행하면 1초마다 계속 입력하도록 만든다.

```python
import random
import time

print('채팅을 시작합니다.')

hi_words = ['안녕!', '안녕하세요!', '어! 왔니?']

while True:
  answer = input('나> ')

  if answer == '안녕':
    r = random.randrange(0, len(hi_words))
    print('PC> ' + hi_words[r])
  elif answer == '그만하자':
    print('PC> 그래 안녕!')
    break

  time.sleep(1)
```

위와 같이 코드를 실행하면 `그만하자`라고 입력했을때 프로그램이 종료된다.

여기서 `elif`는 `if`에서 조건이 맞지 않은 것 중에 다시 조건을 검사할때 사용한다.

```python
import random
import time

print('채팅을 시작합니다.')

hi_words = ['안녕!', '안녕하세요!', '어! 왔니?']

while True:
  answer = input('나> ')

  if '안녕' in answer:
    r = random.randrange(0, len(hi_words))
    print('PC> ' + hi_words[r])
  elif answer == '그만하자':
    print('PC> 그래 안녕!')
    break

  time.sleep(1)
```

위와 같이 `'안녕' in answer`처럼 왼쪽에 있는 글자가 오른쪽에 있는 글자에 포함되어있는지 확인할 수 있다.

## Mission

나만의 인공지능 챗봇 만들어보기!
