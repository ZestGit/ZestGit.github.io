---
layout: post
title: Python 문법 정리 (2)
description: >
    Python 내용 정리
category: devlog
tags: python
sitemap: true
hide_last_modified: true
---


# Python 문법 정리 (2)

1. if
2. for
3. while
4. 함수 선언
5. 함수 기본값, 키워드, 가변 인자 등
{:toc}

## if
```python
weather = input("오늘 날씨는 어때요? ")
if weather == "비" or weather == "눈":
    print("우산을 챙기세요")
elif weather == "미세먼지":
    print("마스크를 쓰세요")
else:
    print("준비물 필요 없어요")

temp = int(input("기온은 어때요? "))
if 30 <= temp:
    print("너무 더워요")
elif 10 <= temp and temp < 30:
    print("괜찮네요")
elif 0 <= temp < 10:
    print("외투 챙기세요")
else:
    print("너무 추워요")
```

## for
```python
wait = []
for waiting_num in range(1, 6):
    wait.append(waiting_num)

print(wait) # 1,2,3,4,5

absent = [2, 5]
no_book = [7]
for student in range(1, 11):
    if student in absent:
        continue
    elif student in no_book:
        print("책 없는 사람 : {0}".format(student))
        break
    print("{0}, 책을 읽어봐".format(student))

# 숫자에 100씩 더함
students = [1,2,3,4,5]
students = [i+100 for i in students] # students에 있는 i를 하나씩 불러온 값들에 100을 더한다.
print(students)

# 학생 이름을 길이로 변환
students = ["Iron man", "Thor", "I am groot"]
students = [len(i) for i in students]
print(students)

# 학생 이름을 대문자로 변환
students = ["Iron man", "Thor", "I am groot"]
students = [i.upper() for i in students]
print(students)
```

## while
```python
customer = "토르"
index = 5
while index >= 1:
    print("{0}, 커피가 준비되었습니다. {1} 번 남았어요.".format(customer, index))
    index -= 1
    if index == 0:
        print("커피는 폐기처분되었습니다.")

customer = "토르"
person = "UnKnown"

while person != customer :
    print("{0}, 커피가 준비되었습니다.".format(customer))
    person = input("이름이 어떻게 되세요? ")
```

## 함수 선언
```python
# def로 함수 선언
def open_account():
    print("새로운 계좌가 생성되었습니다.")

def deposit(balance, money):
    print("입금이 완료되었습니다. 잔액은 {0}원입니다.".format(balance+money))
    return balance+money

def withdraw(balance, money):
    if balance >= money:
        print("출금이 완료되었습니다. 잔액은 {0}원입니다.".format(balance - money))
        return balance - money
    else:
        print("출금이 실패하였습니다. 잔액은 {0}원입니다.".format(balance))

def withdraw_night(balance, money):
    commision = 100 # 수수료 100원
    return commision, balance - commision - money # 튜플 형식으로 반환

comm, money = withdraw_night(2000, 100) # 튜플로 받기
print("수수료 : {0}, 잔액 : {1}".format(comm, money))
```

## 함수 기본값, 키워드, 가변 인자 등
```python
# 기본값
# 줄바꿈할 때는 \를 치고 한칸 내린다.
def profile(name, age = "17", main_lang = "파이썬"):
    print("이름 : {0}, 나이 : {1}, 주 사용 언어 : {2}"\
        .format(name, age, main_lang))

# 키워드값
def profile(name, age, main_lang):
    print(name, age, main_lang)

profile(name="유재석", main_lang="파이썬", age=20)

# 가변인자 (*변수이름)
def profile(name, age, *language):
    print("이름 : {0}\t나이 : {1}\t".format(name, age), end=" ")
    for lang in language:
        print(lang, end=" ")
    print()

profile("유재석", 20 , "파이썬", "자바", "C", "C++", "C#")
profile("김태호", 25 , "코틀린", "자바스크립트")

# 지역 변수와 전역 변수
gun = 10
def checkpoint(soldiers):
    global gun # 전역 공간에 있는 gun 사용 (global 키워드 사용)
    gun = gun - soldiers
    print("[함수 내] 남은 총 : {0}".format(gun)) # 8

gun = checkpoint(2) # 8
print("남은 총 : {0}".format(gun))

def checkpoint_ret(gun, soldiers):
    gun = gun - soldiers # 지역 변수를 사용하여 계산하고 Return한다.
    print("[함수 내] 남은 총 : {0}".format(gun))
    return gun

gun = checkpoint_ret(gun, 2) # 8 
print("남은 총 : {0}".format(gun))
```