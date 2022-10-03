---
layout: single
title: "링크드 리스트 "
categories: DataStructure stack
tag: DataStructure stack
toc: true
author_profile: false
sidebar: 
    nav: "docs"
---
`언어는 python을 사용하였습니다.`

# 4. 링크드 리스트(Linked List)

- 링크드 리스트는 연결 리스트라고도 하며, 배열을 순차적으로 연결된 공간에 데이터를 나열하는 데이터 구조 이다.
- C언어에서 주요한 데이터 구조 이지만, 파이썬에서는 리스트 타입이 링크드 리스트의 기능을 지원 한다.
- 링크드 리스트의 형태

<p align ="cnenter"><img src ="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Singly-linked-list.svg/408px-Singly-linked-list.svg.png"></p>

- 노드(Node): 데이터 저장 단위로서, 데이터값과 포인터로 구성된다.
- 포인터(pointer): 각 노드 안에서, 다음이나 이전의 노드와의 연결 정보 즉 주소를 가지고 있는 공간 이다.

```python
#링크드 리스트 만들기
class Node:
    def __init__(self, data, next=None):
        self.data = data
        self.next = next
# 데이터 추가하기
def add(data):
    node = head #시작하는 시작점 
    while node.next: 
        node = node.next
    node.next = Node(data)
        #node.next 즉 포인터에 주소가 있으면 다음 노드로 이동하고, 주소가 없으면 그 노드에 데이터를 삽입한다. 
```

## 링크드 리스트의 장 단점

- (장점) 배열과 달리 미리 데이터의 공간을 할당하지 않아도 된다.
- (단점) 연결을 위한 주소를 저장할 데이터 공간이 필요하므로, 저장공간 효율이 높지 않다.
- (단점) 연결 정보를 찾는 시간이 필요하여 속도가 느리다.
- (단점) 중간 데이터를 삭제하게 된다면 앞뒤 데이터의 연결을 재구성하는 작업이 필요하다.

## 링크드 리스트 사이에 데이터 추가

<p align ="cnenter"><img src ="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/CPT-LinkedLists-addingnode.svg/474px-CPT-LinkedLists-addingnode.svg.png"></p>

- 위의 그림처럼 링크드 리스트 사이에 데이터를 추가하기 위해선  앞뒤 노드의 주소를 재구성 하는 작업이 필요하다.

```python
# 링크드 리스트에 (1~10까지 데이터 집어넣기)
node1 = Node(1)
head = node1 #헤드, 시작점 지정
for index in range(2,10):
    add(index)
#1~10 까지의 데이터가 들어감
```

`1과 2 사이에 1.5값 추가하기`

```python
node2 = Node(1.5) #추가할 데이터
node = head
search = True
while search: #반복하기
    if node.data == 1:  #넣고싶은 데이터 앞 데이터이면 반복이 멈춘다
        search = False
    else:
        node = node.next

node_next = node.next #2의 앞 주소를 임의의 변수로 저장
node.next = node2 #새로 생성될 주소로 변경
node2.next = node_next #새로 생성된 주소에서 그다음으로 연결
```

1, 1.5, 2, 3, 4, 5, 6, 7, 8, 9 가 출력된다.

## 파이썬  객체지향으로 링크드 리스트 기능 구현하기

```python
class Node: # 각각의 노드를 생성 할 수 있는 클래스
    def __init__(self, data, next=None):
        self.data = data
        self.next = next

class NodeMgmt: #링크드 리스트를 관리 할 수 있는 클래스
    def __init__(self, data): #제일 앞에 값(헤드), 기준을 정해줌
        self.head = Node(data)

    def add(self, data): #링크드 리스트 제일 마지막에 노드를 추가하는 함수
        if self.head == '':
            self.head = Node(data)
        else:
            node = self.head
            while node.next: #제일 뒤에 노드를 찾기 위함, 값이 있다면 그다음 노드로, 값이 없다면 해당 노드로
                node = node.next
            node.next = Node(data)

    def desc(self): #링크드 리스트 출력
        node = self.head
        while node:
            print(node.data)
            node = node.next

#링크드 리스트에서 삭제하는 경우는 3가지가 있다. 
# 1. head에 노드를 삭제 2. 마지막 노드를 삭제 3. 중간에 노드를 삭제
    def delete(self, data): #링크드 리스트에서 노드를 삭제하는 함수
        if self.head =='' #삭제데이터를 가진 노드가 존재하지 않을때
            print("노드가 없습니다")
            return

        if self.head.data == data: #1. head를 삭제할때
            temp = self.head #헤드를 임시 변수에 저장하고
            self.head = self.head.next #헤드의 주소에서 두번째 노드를 헤드로 바꿔준다. (링크드 리스트에는 항상 헤드가 존재하므로 헤드를 바꾸어 줘야 한다. )
            del temp #그리고 첫번째 였던 헤드를 삭제한다.
        else: 
            node = self.head # 헤드가 존재므로, 헤드를 정해준다
            while node.next:
                if node.next.data == data:
                    temp = node.next
                    node.next = node.next.next #3번의 경우 두번째 노드의 주소를 세번째로 바꿔 헤드와 세번째를 연결한다.
                    del temp #3번의 경우 두번째 값을 지우고, 2번의 경우 마지막 노드의 앞 주소값을 삭제시켜 준다. 
                    return
                else:
                    node = node.next

    def search_node(self, data):
        node = self.head 
        while node: #헤당 노드의 data값을 찾을때까지 앞에서부터 반복된다. 
            if node.data == data:
                return node
            else:
                node = node.next
```

## 더블 링크드 리스트

- 앞과 뒤가 연결된 링크드 리스트로서 노드 탐색이 앞뒤 모두 가능하다.

<p align ="cnenter"><img src ="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Doubly-linked-list.svg/610px-Doubly-linked-list.svg.png"></p>

- 링크드 리스트와의 아치는 이전 데이터의 주소까지 가지고 있다.

```python
class Node:
    def __init__(self, data, prev=None, next=None): #노드 생성, 이전 주소값도 지정
        self.prev = prev
        self.data = data
        self.next = next

class NodeMgmt:
    def __init__(self, data): #뒤에서도 검색이 가능하므로, head,와 tail  이 있다. 처음 1개일때는 head, tail 동일
        self.head = Node(data)
        self.tail = self.head

    def insert(self, data):
        if self. head == None:
            self.head = Node(data)
            self.tail = self.head
        else:
            node = self.head
            while node.next:
                node = node.next
            new = Node(data)
            node.next = new #앞에 데이터의 주소도 알려줘야함
            new.prev = node
            self.tail = new

        def desc(self):
            node = self.head
            while node
                print(node.data)
                node = node.next
```

` 특정한 값 앞,뒤에 데이터 추가`

```python
class Node:
    def __init__(self, data, prev=None, next=None): 
        self.prev = prev
        self.data = data
        self.next = next

class NodeMgmt:
    def __init__(self, data): 
        self.head = Node(data)
        self.tail = self.head

    def insert(self, data): #특정한값에 데이터삽입
        if self. head == None:
            self.head = Node(data)
            self.tail = self.head
        else:
            node = self.head
            while node.next:
                node = node.next
            new = Node(data)
            node.next = new
            new.prev = node
            self.tail = new

    def desc(self): #출력
        node = self.head
        while node:
            print (node.data)
            node = node.next

    def search_from_head(self, data) #head검색, 앞에서부터
        if self.head == None:
            return False

        node = self.head
        while node:
            if node.data == data:
                return node
            else:
                node = node.next
        return False

    def search_from_tail(self,data:)#tail 검색, 뒤에서부터
        if self.head == None:
            return False:
      
        node = self.tail
        while node:
            if node.data == data:
                return node
            else:
                node = node.prev
        return False
  
    #특정 data 전에 데이터추가
    def insert_before(self, data, before_data):
        if self.head == None: #첫번째 데이터 일때
            self.head = Node(data)
            return True
        else:
            node = self.tail
            while node.data != before_data:
                node = node.prev
                if node == None:
                    return False
                #1번 에서 3번 으로 연결된 링크드 리스트에 2번의 새로운 노드를 넣는다고 가정
                new = Node(data) #새로운 데이터의 이전값도 지정해주어야함 
                before_new = node.prev  # 3번 노드의 이전은 1번이다라고 찾고 
                before_new.next = new #1번의 이전 노드의 다음 주소값을 2번 새로운 노드로
                new.prev = before_new #2번 새로운 노드의 이전 주소값을 1번의 노드값으로
                new.next = node # 2번의 새로운 노드 다음 주소를 3번의 노드 주소로
                node.prev = new  #3번의 이전 주소값을 2번 새로운 노드값으로
                return True
  
    #노드 뒤에 놓기
    def insert_before(self, data, after_data):
        if self.head == Node:
            self.head = Node(data)
            return True
        else:
            node = self.head
            while node.data != after_data
            node = node.next
            if node  == None:
                return False
            new = Node(data)
            after_new = node.next  # 1번 노드 위에 새로운 노드를 넣을때, 뒤에 노드를 찾는다
            new.next = after_new #2번 노드의 다음 주소값을 3번 노드 주소값으로
            new.prev = node #2번 새로운 노드의 이전 주소값은 찾은 1번 노드주소로
            node.next = new #1번 노드의 다음 주소값은 2번으로 연결
            if new.next == None: #새로 연결하는 2번 노드 뒤에 노드가 없을 수도 있다.
                self.tail = new #이때는 새로 연결하는 2번 노드가 꼬리가 된다.
            return True
```
**References**
Do it! 점프 투 파이썬
Do it! 자료구조와 함께 배우는 알고리즘 입문 파이썬편
[잔재미코딩](https://www.fun-coding.org/Chapter07-linkedlist-live.html)
[위키피디아](https://en.wikipedia.org/wiki/Linked_list)