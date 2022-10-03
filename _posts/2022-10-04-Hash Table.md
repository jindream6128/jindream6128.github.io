---
layout: single
title: "해쉬 테이블 "
categories: DataStructure stack
tag: DataStructure stack
toc: true
author_profile: false
sidebar: 
    nav: "docs"
---
`언어는 python을 사용하였습니다.`

# 6. 해쉬 테이블(Hash Table)
- 키(Key)에 데이터(Value)를 저장하는 데이터 구조

## 해쉬구조
- Key를 통해 바로 데이터를 받아올 수 있으므로, 속도가 매우 빠름
- 파이썬의 딕셔너리(Dictionary) 타입이 해쉬 테이블의 예시 이다.
- 보통 배열로 미리 Haash Table의 사이즈만큼 생성 한 뒤에 사용한다.
- 해쉬 테이블의 크기를 크게 만듦으로써 충돌로 인한 추가적인 알고리즘을 실행시키지 않도록 한다 즉 공간과 탐색 시간을 맞바꾸는 기법 이다.
- 배열보다 빠르게 데이터를 찾을수 있다.

## 알아둘 용어
- 해쉬(Hash): 임의 값을 고정된 길이로 변환하는 것
- 해쉬 테이블(Hash Table): 키 값의 연산에 의해 직접 접근이 가능한 데이터 구조
- 해싱 함수(Hashing Function): Key에 대해 산술 연산을 이용하여 데이터의 위치를 찾을 수 있는 함수
- 해쉬 값(Hash Value) 또는 해쉬 주소(Hash Address): Key를 해싱 함수로 연산해서, 해쉬 값을 알아내고, 이를 기반으로 해쉬 테이블에서 해당 Key에 대한 데이터 위치를 일관성있게 찾을 수 있음.
- 슬롯(Slot): 한 개의 데이터를 저장할 수 있는 공간

**흐름: 데이터 -> 키 -> 해쉬함수를거쳐 -> 해쉬 테이블의 각 Slot에 데이터가 저장된다.**

## 자료 구조 해쉬 테이블의 장단점과 주요 용도
- (장점) 데이터 저장/읽기 속도 즉 검색 속도가 빠르다.
- (장점) 해쉬 키에 대한 데이터 또는 중복된 데이터가 있는지 확인이 쉽다.
- (단점) 일반적으로 저장공간이 내가 원하는 데이터보다 더 많이 필요하다.
- (단점) 여러 키에 해당하는 주소가 동일할 경우 충돌을 해결하기 위한 자료구조가 필요하다. ->Chaining기법,  Linear Probing 기법
- (쓰임) 1. 검색이 많이 필요한 경우 2. 저장,삭제, 읽기 등이 빈번한 경우 3. 데이터가 있는지 없는지, 중복확인이 쉬우므로 캐쉬 구현시 사용된다.

## 해쉬 테이블 구현하기
 참고 파이썬의 문법 Comprehension
`[출력표현식 for 요소 in 입력Sequence [if 조건식]]`
이를 이용해서 리스트에 0~9까지 값 저장하기
list([0 for i in ragne(10)])

### 리스트 변수를 활용한 해쉬테이블 구현
```python
# 해쉬 함수 key % 8 / 해쉬 키 생성: hash(data)

hash_table = list([0 for i in ragne(8)]) #8칸짜리의 해쉬테이블 생성
def get_key(data): # data -> key
    return hash(data)

def hash_function(key): #key -> hashfunction
    return key % 8

def save_data(data, value): #save 함수
    hash_address = hash_function(get_key(data)) #해쉬 함수를 통해 해쉬 주소를 찾는다
    hash_table[hash_address] = value #찾은 해쉬 주소로 해쉬테이블에 value를 저장한다

def read_data(data): #read 함수
    hash_address = hash_hashfunction(get_key(data))#동일 하게 해쉬주소를 찾고
    return hash_table[hash_address] #해쉬 주소를 통해 해당 해쉬테이블의 value를 반환한다
```

## 충돌(Collision)
- 해쉬 테이블의 가장 큰 문제점은 충돌(Collision)의 경우 이다. 이 문제점을 충돌(Collision) 혹은 해쉬 충돌(Haash collision)이라고 부른다. 
- 이전 해쉬 테이블의 단점처럼 여러 키에 해당하는 주소가 동일할 경우 충돌이 일어나고, 이를 해결하기위해서 **Chaining기법**과 **Linear Probing기법** 이 사용된다.

### 충돌 해결 알고리즘 - Chaining 기법
- 개방 해슁 또는 Open Hashing 기법 중 하나로서 해쉬 테이블 저장공간 외의 공간을 추가로 활용하는 기법이다.
- 충돌이 일어나면 링크드 리스트를 통해 뒤에 데이터를 추가로 연결시켜 저장한다. 

```python
# 해쉬 함수 key % 8 / 해쉬 키 생성: hash(data)
hash_table = list([0 for i in ragne(8)]) #8칸짜리의 해쉬테이블 생성
def get_key(data): # data -> key
    return hash(data)

def hash_function(key): #key -> hashfunction
    return key % 8

def save_data(data, value):
    index_key = get_key(data) #hash 키를 별도의 변수에 저장한다 / 각각의 데이터를 구분학기 위해서 각각의 데이터의 키값을 별도의 index_key 변수에 저장한다.
    hash_address = hash_function(index_key)

    if hash_table[hash_address] != 0: #8개의 해쉬 테이블 중에서 default 값은 0 이다 즉 0이 아니여야 해쉬 테이블의 slot에 데이터가 존재한다는 뜻이다.
        for index in range(len(hash_table[hash_address])): #해쉬 테이블에 데이터가 들어가 있을때, 그 크기만큼 반복을 한다.
            if hash_table[hash_address][index][0] == index_key: #키값과, 데이터를 저장하는걸 2차원 배열형태로 쪼개고 (index_key, value)가 해쉬 테이블에 저장이 된다.
                hash_table[hash_address][index][1] = value
                return
        hash_table[hash_address].append([index_key, value])  # 한개도 없을때는 append를 통해 list형태로 집어 넣는다.

    else:
        hash_table[hash_address] = list([index_key, value]) # 해쉬 테이블에 0이 있으면 데이터가 존재하지 않는다는 뜻이므로, 바로 list 형태로 집어 넣는다.

def read_data(data):
    index_key = get_key(data)
    hash_address = hash_function(index_key)

    if hash_table[hash_address] != 0: # 데이터가 저장되어 있는 링크드 리스트 찾기
        for index in range(len(hash_table[haash_address])): #해쉬 테이블에 데이터 가 들어있으니, 그 크기만큼 조회
            if hash_table[hash_address][index][0] == index_key: # 0번이 키값이라면 실제 데이터는 1번에 존재
                return hash_table[hash_address][index][1] # 실제 데이터를 반환
        return None #링크드 리스트를 돌았을때도 해당 값이 없으면 None값을 반환
    else:
        return None
```
### 충돌 해결 알고리즘 - Linear Probing 기법
- 폐쇄 해슁 또는 Close Hasing 기법 중 하나로서, 해쉬 테이블 저장공간 안에서 충돌 문제를 해결하는 기법이다.
- 충돌이 일어나면 해당 hash address의 다음  address 부터 맨 처음 나오는 빈 공간에 저장하는 기법이다.
- 간단히 해쉬 테이블 공간 내에서 빈공간을 활용하는 기법으로서 저장공간의 활용도를 높이기 위한 기법이다.

```python
# 해쉬 함수 key % 8 / 해쉬 키 생성: hash(data)
hash_table = list([0 for i in ragne(8)]) #8칸짜리의 해쉬테이블 생성
def get_key(data): # data -> key
    return hash(data)

def hash_function(key): #key -> hashfunction
    return key % 8

def save_data(data, value):
    index_key = get_key(data)
    hash_address = hash_function(index_key)
    # 여기서도 (index_key, value)인 이유는 해쉬 테이블에서 데이터의 키가 충돌이 일어나서 다른곳에 저장되어있는지, 아니면 원래 저장이 된것인지 알수가 없기 때문이다.
    if hash_table[hash_address] != 0: #데이터가 존재할때
        for index in ragne(hash_address, len(hash_table)): #해쉬테이블에 존재하는 주소부터, 해쉬테이블의 크기만큼 반복을 돌며 해쉬 테이블 내의 slot에서 빈곳을 찾는다.
            if hash_table[index] == 0: #빈곳을 찾으면 데이터를 넣는다
                hash_table[index] = [index_key, value]
                return
            elif hash_table[index][0] == index_key: #키가 동일하면 무조건 다음 slot으로 넘어가는것이 아니라,  값을 업데이트 해야한다
                hash_table[index][1] = value
                return
    else:
        hash_table[hash_address] = [index_key, value] #비어있으면 해당 데이터를 바로 넣는다.

def read_data(data):
    index_key = get_key(data)
    hash_address = hash_function(index_key)

    if hash_table[hash_address] != 0: 
        for index in range(hash_adderss, len(hash_table)): # 데이터가 존재하므로 있는 쪽 부터 순서대로 찾아간다.
            if hash_table[index] == 0: # 0 이라면 해당되는 데이터가 저장된 적이 없다.
                return None
            elif hash_table[index][0] == index_key: # 내가 원하는 key라면 데이터를 반환한다.
                return hash_table[index][1]

    else:
        return None #0이면 비어있기 때문에 바로 None를 return
```

## 빈번한 충돌을 개선하기 위한 방법
- 해쉬 테이블의  slot 저장공간을 50프로 이상 사용하고 있다면,  크기를 2배이상 늘리는것이 일반 적 이다.

## 시간 복잡도
- 일반적인 경우 (Collision이 없는 경우) -> **O(1)**
- 최악의 경우 (Collision이 모두 발생하는 경우) -> **O(n)**

`해쉬 테이블의 경우, 일반적인 경우를 생각하고 사용하기 때문에 보통 시간 복잡도는, O(1)이라고 말한다.`

- 32개의배열에서 데이터를 저장하고 검색할때 O(n)
- 32개의 데이터 저장공간을 가진 해쉬 테이블에 데이터를 저장하고, 검색할때 O(1)


**References**
Do it! 점프 투 파이썬
Do it! 자료구조와 함께 배우는 알고리즘 입문 파이썬편
[잔재미코딩](https://www.fun-coding.org/Chapter09-hashtable-live.html)

