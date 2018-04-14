# [DAY 2] 로또 기계 만들기

## 분석

로또 기계 프로그램을 짜기 전에 로또 기계에 대해 분석한다.

- 1 ~ 45개 숫자

- 보너스 번호 포함 숫자 7개 뽑기

- 중복된 숫자 나오면 안됨

## 반복

```python
print('옛날에 한 농부가 살고 있었어요.')
print('어느 겨울날, 밭에 나갔다가 들어온 농부가 “어휴 추워, 날씨가 무척 춥군.” 하면서 방에서 혼잣말을 했어요.')
print('그러자 “어휴 추워, 날씨가 무척 춥군” 하면서 방 안에서 누군가 농부의 말을 따라 하는 것이 아니겠어요?')
print('아주 똑같이 말하니 메아리가 아닐까 생각했지만, 목소리는 달랐어요.')
print('누군가가 농부의 흉내를 내는 것이었어요.')
```

위에서 `농부`가 다른 이름으로 바뀌면서 똑같은 내용이 3번 반복되어 출력되도록 해본다.

```python
users = ['철수', '영희', '소라']
for user in users:
  print('옛날에 한 ' + user + '가 살고 있었어요.')
  print('어느 겨울날, 밭에 나갔다가 들어온 ' + user + '가 “어휴 추워, 날씨가 무척 춥군.” 하면서 방에서 혼잣말을 했어요.')
  print('그러자 “어휴 추워, 날씨가 무척 춥군” 하면서 방 안에서 누군가 ' + user + '의 말을 따라 하는 것이 아니겠어요?')
  print('아주 똑같이 말하니 메아리가 아닐까 생각했지만, 목소리는 달랐어요.')
  print('누군가가 ' + user + '의 흉내를 내는 것이었어요.')
```

위와 같이 하면 각 이름으로 바뀌면서 실행된다. 이때 `for user in users:` 이 부분이 반복이 되도록 하는 부분이다.

이걸 for 문이라고 한다. for문은 in 다음에는 오는 배열에 있는 값을 하나씩 꺼내 for 다음에 있는 변수에 넣고 반복한다.

```python
for n in range(0, 3):
  print('Hello World')
```

위와 같이 입력하면 `Hello World`가 3번 반복된다. 여기서 `range`는 배열처럼 작동한다.

`range(0, 3)`은 `[0, 1, 2]`와 같다.

```python
nums = []
nums.append(1)
nums.append(2)
nums.append(3)
for n in nums:
  print(n)
```

배열은 `array.append`를 이용해 값을 추가할 수 있다. 값을 추가할때 배열 가장 끝에 값이 추가된다.

## 모듈

프로그래밍을 하다보면 모듈 또는 라이브러리란 단어를 듣게된다. 모듈과 라이브러리는 일종의 공구함과 같다. 자주 사용하는 기능을 위해 공구함처럼 미리 정리해놓은 것이다.

```python
import random
```

위 코드는 `random`이라는 모듈을 추가한다는 뜻이다. `random`은 난수를 생성할때 사용하는 모듈이다.

```python
import random

print(random.random())
```

위 코드를 실행하면 0부터 1 전까지 중에서 난수를 만들어준다.

```python
import random

print(random.randrange(0, 10))
```

위 코드는 0부터 10 전까지 중에서 난수를 만들어준다.

## 로또 기계 만들기

```python
import random

print(random.randrange(1, 46))
print(random.randrange(1, 46))
print(random.randrange(1, 46))
print(random.randrange(1, 46))
print(random.randrange(1, 46))
print(random.randrange(1, 46))
print(random.randrange(1, 46))
```

위와 같이 하면 1에서 45까지의 수 중 난수를 뽑는데 그걸 7번 한다. 그런데 이 코드는 문제가 있다. 바로 중복이 일어난다는 것이다.

중복을 제거하는 방법은 두 가지가 있다.

1. 난수를 뽑되 이전에 뽑은 난수와 동일한 난수가 나왔을때 다시 뽑아서 중복되지 않은 난수를 뽑는다.

2. 뽑을 번호들을 미리 한 곳에 다 넣어놓고 하나씩 빼가면서 난수를 뽑는다.

1번의 방법은 조건문이란 것을 배우지 않아서 할 수 없다.

```python
import random

nums = []

for n in range(1, 46):
  nums.append(n)
  
for n in range(0, 7):
  r = random.randrange(0, len(nums))
  print(nums(r))
  nums.pop(r)
```

2번 방법을 위해 위 코드와 같이 작성한다. 여기서 `len`은 배열의 크기를 알려주는 명령어다. 그리고 `pop`은 `array.pop` 명령어로 배열에서 해당 번호 서랍을 삭제한다. `array.pop`명령어를 실행하면 배열의 크기가 줄어든다.

```python
import random
import time

nums = []

for n in range(1, 46):
  nums.append(n)

for n in range(0, 7):
  r = random.randrange(0, len(nums))
  print(nums(r))
  nums.pop(r)
  time.sleep(1)
```

`time`모듈 시간 관련 명령어를 쓸 수 있도록 해주는 모듈이다. `time.sleep`은 프로그램이 잠시 멈추도록 하는 명령어다. `time.sleep(1)`은 1초 멈추라는 뜻이다. 
