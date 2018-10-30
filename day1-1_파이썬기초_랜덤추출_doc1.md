# day1 파이썬 기초(랜덤추출)

#### 1. 파이썬 리스트 랜덤추출방법

- 복원(중복가능)

```python
import random
menu = ["스파게티","존맛탱","또먹고싶음","3개가능"]
# random.choice(리스트)
# 1개 뽑기
random.choice(menu)
# n번 뽑기
picked = [random.choice(menu) for i in range(n)]


```

- 비복원(중복불가)

```python
import random
menu = ["스파게티","존맛탱","또먹고싶음","3개가능"]
# random.sample(리스트)
# 직접 n개 아이템 아이템 뽑기
random.sample(리스트, n)
# 인덱스 랜덤으로 n 개 뽑아서 뽑기
lotto = list(range(46))
index = [random.randrange(시작,끝(포함x)) for i in range(n)]
lotto_number = []
for i in index:
    lotto_number.append(lotto[i])
print(sorted(lotto_number))


```

##### 파이썬 format으로 변수 출력하는 방법

```python

```

