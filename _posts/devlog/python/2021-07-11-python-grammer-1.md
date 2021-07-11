---
layout: post
title: Python 문법 정리 (1)
description: >
    Python 내용 정리
category: devlog
tags: python
sitemap: true
hide_last_modified: true
---

# Python 문법 정리 (1)

1. 기본 문법 및 연산
2. 문자열
3. 자료형
    1. List
    2. Dictionary
    3. Tuple
    4. Set
4. 자료 구조 변경
{:toc}

## 기본 문법 및 연산
```python
# print에 end=" "를 추가하면 줄바꿈을 하지 않는다는 의미
print("Python", end=" ")
print("C++") # 한줄에 python C++이 출력된다.

# 삼항 연산자
a = 5
b = 10
print("같다" if a is b else "다르다")
print("같지 않다" if a is not b else "같다")

print(4 / 2) # 2.0 나누기
print(4 // 2) # 2 나눈 몫
print(4 % 3) # 1 나머지
print(2 ** 2) # 4 거듭제곱(2의 2제곱)

# & 와 and 같이 쓸 수 있음
print((3 > 0) and (3 < 5))
print((3 > 0) & (3 < 5)) 

# | 와 or 같이 쓸 수 있음
print((3 > 0) | (3 > 5))
print((3 > 0) or (3 > 5))

# Math
print(abs(-5))
print(pow(4, 2)) # 4의 2승
print(max(5, 12))
print(min(5, 12))
print(round(3.14))

# Math Library 사용
from math import *
print(floor(4.99)) # 내림 4
print(ceil(3.14)) # 올림 4
print(sqrt(16)) # 제곱근 4

# Random Library 사용
from random import *

print(random()) # 0.0 ~ 1.0 미만의 임의이 값 생성
print(random() * 10) # 0.0 ~ 10.0 미만의 임의이 값 생성

print(int(random() * 10)) # 0 ~ 10 미만의 임의의 값 생성
print(int(random() * 10) + 1) # 1 ~ 10 이하의 임의의 값 생성

print(int(random() * 45) + 1) # 1~ 45 이하의 임의의 값 생성
print(randrange(1, 46)) # 1 부터 46 미만의 임의의 값 생성
print(randint(1, 45)) # 1 부터 45 이하의 임의의 값 생성

```

## 문자열
- 문자열은 ''' ''', """ """ 3개까지 묶을 수 있음

```python
# 문자열 관련 함수
text = "hobby"
text.count('b') # 들어간 문자열의 개수를 세어준다.
text.find('b') # 가장 먼저 나오는 b의 인덱스를 가져오는데 없으면 -1 Return
text.index('b') # 가장 먼저 나오는 b의 인덱스를 가져오는데 없으면 Exception 발생

text = ",".join("abcd") # a,b,c,d (abcd 사이에 ,를 넣어준다.)
text = "  a bcd  ".strip() # a bcd (양 끝 공백을 없애준다.)
text = text.replace("ho", "aa") # aabby (문자열 대체)

text = "a b c d"
text.split() # 문자열을 띄어쓰기 기준으로 자른다. (Default)

text = "a:b:c:d"
text.split(":") # 지정한 문자열을 기준으로 자른다.

# 문자열 인덱싱
sentence = "python"
print(sentence[0]) # p (순방향)
print(sentence[-1]) # n (역방향)

# 문자열 포맷
# 방법 1
print("나는 %d살입니다." % 20)
print("나는 %s를 좋아해요." % "파이썬")
print("나는 %c입니다." % 'A')
print("나는 %s살입니다." % 20) # %s 는 모두 가능

# 방법 2
print("나는 {}살입니다.".format(20))
print("나는 {}색과 {}색을 좋아합니다.".format("빨간", "파란"))
print("나는 {1}색과 {0}색을 좋아합니다.".format("빨간", "파란")) # 파란색과 빨간색을 좋아합니다.

# 방법 3
print("나는 {age}살이며, {color}색을 좋아해요.".format(age = 20, color = "빨간"))

# 방법 4 (v3.6 이상~)
age = 20
color = "빨간"
print(f"나는 {age}살이며, {color}색을 좋아해요.") # 앞에 f를 붙이면 앞에 선언된 실제 변수의 값을 사용한다.

# 소수점 포맷
value = "%0.4f" % 3.23311 # 소수점 4자리까지 출력

# 문자열 슬라이싱
sentence = "Lifeistooshort" # sentence[이상:미만:간격] 
print(sentence[:8]) # 첫 글자부터 시작해서 8번 인덱스 전까지 출력 -> Lifeisto
print(sentence[8:]) # 8번 인덱스 이상부터 끝까지 출력 -> oshort
print(sentence[::2]) # 2칸 간격으로 처음부터 끝까지 출력 -> Lfitohr
```

## 자료형

### List
```python
lstString = ["유재석", "박명수", "정준하", "노홍철"] # string List
lstAll = [1, 2, "int", ["1", "2"]] # int, string, list를 모두 list에 넣을 수도 있다.

# 값 추가
lstString.append("하하") # 목록의 가장 뒤에 추가하기
lstString.insert(1, "하하") # 중간에 추가하기

# 값 변경
lstString[0] = "정형돈"
lstString[0:2] = ["정형돈", "하하"] # 0부터 2미만까지 변경 가능 (0, 1 값 변경)

# 값 삭제
lstString[0:2] = [] # 0, 1번 값 삭제 (빈 리스트 할당)
del lstString[0] # 0번 삭제

# list도 string처럼 더하기 연산 가능
lst1 = [1, 2, 3]
lst2 = [4, 5, 6] 
print(lst1+lst2) # [1,2,3,4,5,6]

lst1.extend(lst2)
print(lst1) # [1,2,3,4,5,6]

lst1.extend([7,8])
print(lst1) # [1,2,3,7,8]

# 관련 함수
lst1.sort() # 정렬
lst1.reverse() # 뒤집기
lst1.clear()  # 모두 지우기
lst1.remove(3) # 해당 값을 지우기 (여러개 있을 경우 처음 나온 1개만 지움)
lst1.pop() # 마지막 원소가 튀어 나오고 목록에서 제거된다.
len(lst1) # 리스트 전체 개수 구하기
```

**NOTE**: `+=`은 두 list를 합쳐 새로운 List를 만들면서 생성과 복사 연산이 일어나 느리다.
* List에 항목을 하나씩 추가할 경우 `append` 사용
* list들을 이을 경우 `+=` 또는 `extend` 사용 (list를 이을 때는 `+=`이 `extend`보다 빠르다.)

### Dictionary
```python
# Key, Value { Key : Value } 중괄호
cabinet = {3 : "유재석", 100 : "김태호"} 
print(cabinet[5]) # 값이 없으면 exception 발생
print(cabinet.get(5)) # 값이 없으면 None 출력
print(cabinet.get(5, "사용 가능")) # 값이 없으면 사용 가능 출력

# in 키워드로 값이 있는 지 확인
print(3 in cabinet) # True
print(5 in cabinet) # False

cabinet2 = { "A-3" : "유재석", "B-100" : "김태호"}
cabinet2["C-20"] = "조세호" # 데이터 삽입
cabinet2["A-3"] = "김종국" # 데이터 변경
del cabinet2["A-3"] # 데이터 제거

print(cabinet2.keys()) # Key 목록 출력
print(cabinet2.values()) # Value 목록 출력
print(cabinet2.items()) # Key, Value 쌍으로 목록 출력
```

### Tuple
- List보다 속도가 빠르지만 데이터 변경 및 추가 불가능

```python
# 괄호, 콤마
menu = ("돈까스", "치즈까스") 
print(menu[0]) # 돈까스
print(menu[1]) # 치즈까스

name = "김종국"
age = 20
hobby = "코딩"
print(name, age, hobby)

# 위의 내용을 tuple로 받기
(name, age, hobby) = ("김종국", 20, "코딩") 
print(name, age, hobby)
```

### Set
```python
my_set = {1,2,3,3,3} # 중괄호
print(my_set)

java = {"유재석", "김태호", "양세형"}
python = set(["유재석", "박명수"])

# 추가
python.add("김태호")
print(python)

# 삭제
java.remove("김태호")
print(java)

# 교집합 (java와 python을 모두 할 수 있는 개발자)
print(java & python)
print(java.intersection(python))

# 합집합 (java를 할 수 있거나 Python을 할 수 있는 개발자)
print(java | python)
print(java.union(python))

# 차집합 (java는 할 수 있지만 python을 할 줄 모르는 개발자)
print(java - python)
print(java.difference(python))
```

## 자료 구조 변경
```python
menu = {"커피", "우유", "주스"} # set으로 선언
print(menu, type(menu)) # set

menu = list(menu) # list로 변경
print(menu, type(menu))

menu = tuple(menu) # tuple로 변경
print(menu, type(menu))

menu = set(menu) # set으로 변경
print(menu, type(menu))

users = range(1, 21) # 1부터 20까지 숫자 생성
users = list(users) # range로 생성한 것은 range 타입이므로 list 타입으로 변경
```