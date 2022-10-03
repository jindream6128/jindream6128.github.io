---
layout: single
title: "자료구조 "
categories: DataStructure stack
tag: DataStructure stack
toc: true
author_profile: false
sidebar: 
    nav: "docs"
---
`언어는 python을 사용하였습니다.`

# 5. 알고리즘의 복잡도 표현

- 알고리즘을 해결하는 방법에는 여러가지 방법이 있고, 여러가지 방법중 더 좋은 알고리즘을 분석하기 위해 계산한다.
  ex) 1부터 10까지의 합을 구하는 방법. (1)1부터 10까지 모두 더한다. (2)공식을 사용한다.

## 알고리즘 복잡도 계산 항목

- 시간 복잡도 : 알고리즘 실행 속도
- 공간 복잡도 : 알고리즘이 사용하는 메모리 사이즈
- 가장 중요한 것은 **시간 복잡도** 로서, 시간 복잡도는
  **반복문**이 가장 큰 영향을 미친다.

## 알고리즘 성능 표기법

- Big O(빅-오) 표기법: **O(N)**
  -> 알고리즘의 최악의 실행 시간을 나타낸다.
  -> 가장 많이 사용한다.
  -> **아무리 최악의 상황이더라도, 최소한 이정도의 성능은 보장한다 라는 의미**
- Ω (오메가) 표기법: Ω(N)
  -> 알고리즘의 최상의 실행 시간을 나타낸다.
- Θ (세타) 표기법: Θ(N)
  -> 알고리즘의 평균 실행시간을 나타낸다.

## Big O(빅-오) 표기법 O(N)

- O(입력)
  -> 입력 n 에 따라서 시간 복잡도가 결정된다.
  -> O(1), O( 𝑙𝑜𝑔𝑛 ), O(n), O(n 𝑙𝑜𝑔𝑛 ), O( 𝑛2 ), O( 2𝑛 ), O(n!)등으로 표기함
  -> 입력에 따라 시간복잡도는 기하급수적으로 늘어나며, 반복문이 가장 큰 영향을 미친다.

## Big O 표기법의 시간 복잡도의 크기

> O(1) < O($log n$) < O(n) < O(n$log n$) < O($n^2$) < O($2^n$) < O(n!)

<p align ="cnenter"><img src ="https://t1.daumcdn.net/cfile/tistory/99EF1E395C7EB4B601"></p>

- 입력을 n이라고 하였을때, 몇번 실행되는지 계산하면 된다.
- 표현식에서 가장 큰 영향을 미치는 n의 단위로 표기

1) n이 1,10,100,1000 이든 무족건 상수회 실행할때.

- **O(1)**

```python
if n>10:
    print(n)
```

2) n에 따라서, n+10, 3n+10번 등 실행할때

- **O(n)**

```python
variable=1
for num in ragne(3):
    for index in range(n):
        print(index)
# n번 도는 반복문이 크게 3번 돌게 되므로 3n
```

3) n에 따라, $n^2$번, $n^2$ + 1000 번, 100$n^2$ - 100, 또는 300$n^2$ + 1번등 실행할때

- **O($n^2$)**

```python
variable = 1
for i in ragne(300):
    for num in range(n):
        for index in range(n):
            print(index)
# n번 도는 반복문이 n번 돌고 또 300 번 돌게 된다 300n^2
```

- 만약 시간복잡도의 함수가 2$n^2$ + 3n 라면, 가장 높은 차수는 **2$n^2$** 이고, 그외 일차항과, 상수항은 n의 값이 커지게되면 크게 영향을 미치지 않으므로 빅 오 표기법은 **O($n^2$)** 가 된다.

**References**

Do it! 점프 투 파이썬
Do it! 자료구조와 함께 배우는 알고리즘 입문 파이썬편
[잔재미코딩](https://www.fun-coding.org/Chapter08-timecomplexity.html)
[위키피디아](https://en.wikipedia.org/wiki/Linked_list)
