---
layout: post
title: Python 문법 정리 (모듈과 패키지)
description: >
    Python 내용 정리
category: devlog
tags: python
sitemap: true
hide_last_modified: true
---

# Python 문법 정리 (모듈과 패키지)

1. 모듈
2. 패키지
3. 내장함수와 외장함수
    1. 내장함수
    2. 외장함수
{:toc}

## 모듈

- 모듈 파일 `theater_module.py` 생성

```python
# 일반 가격
def price(people):
    print("{0}명 가격은 {1}원 입니다.".format(people, people*10000))

# 조조할인 가격
def price_morning(people):
    print("{0}명 조조 할인 가격은 {1}원 입니다.".format(people, people*6000))

# 군인할인 가격
def price_soldier(people):
    print("{0}명 군인 할인 가격은 {1}원 입니다.".format(people, people*4000))
```

- 모듈 사용

```python
import theater_module # import로 파일을 지정한다.
theater_module.price(3)
theater_module.price_morning(4)
theater_module.price_soldier(5)

import theater_module as mv # as로 별명을 붙일 수 있음
mv.price(3)
mv.price_morning(4)
mv.price_soldier(5)

from theater_module import * # 바로 모두 사용 가능
price(3)
price_morning(4)
price_soldier(5)

from theater_module import price, price_morning # 특정 함수들만 사용
from theater_module import price_soldier as price_s # 특정 함수에 별명을 붙여 사용
```

## 패키지

폴더를 만들고 하위에 다음과 같이 파일을 만든다.

- `__init__.py` 파일 생성

```python
# 3.3 버전 이후에는 __init__이 없어도 패키지로 인식되지만 하위호환을 위해 __init__.py를 작성하는 것이 원칙
# import *에서 모듈 이름(vietnam, thailand)을 export할 것을 명시
__all__ = ["vietnam", "thailand"] 
```

- `thailand.py` 파일 생성

```python
class ThailandPackage:
    def detail(self):
        print("[태국 패키지 3박 5일] 방콕, 파타야 여행 (야시장 투어) 50만원")

# 이 파일로 바로 실행했는지 외부에서 실행되었는지 확인
# if __name__ == "__main__":
#     print("Thailand 모듈을 직접 실행")
#     trip_to = ThailandPackage()
#     trip_to.detail()
# else:
#     print("Thailand 외부에서 모듈 호출")
```

- `vietnam.py` 파일 생성

```python
class VietnamPackage:
    def detail(self):
        print("[베트남 패키지 3박 5일] 다낭 효도 여행 60만원")
```

- 패키지 사용

```python
import travel.thailand
# import travel.thailand.ThailandPackage # 이런 방식으로는 사용 불가능
trip_to = travel.thailand.ThailandPackage()
trip_to.detail()

from travel.thailand import ThailandPackage # travel.thailand 안에 클래스를 import
trip_to = ThailandPackage()
trip_to.detail()

from travel import vietnam
trip_to = vietnam.VietnamPackage()
trip_to.detail()

from travel import thailand
trip_to2 = thailand.ThailandPackage()
trip_to2.detail()
```

**NOTE**
- `pip`는 파이썬 패키지 관리 시스템이다.
- 구글에 `pipy` 사이트에서 파이썬 패키지를 검색하여 사용할 수 있다.

>- `pip list` : pip 리스트 보기
>- `pip show 패키지명` : 패키지명에 대한 정보 보기
>- `pip install --upgrade 패키지명` : 패키지 업데이트


## 내장 함수와 외장 함수

### 내장 함수

- `list of python builtins`를 검색하면 내장 함수들에 대한 정보를 얻을 수 있다.

몇 가지 예는 다음과 같다.

>- `input` : 사용자 입력을 받는 함수
>- `dir` : 어떤 객체를 넘겼을 때 객체가 어떤 변수와 함수를 가지고 있는지 표시

### 외장 함수

- `list of python modules`를 검색하면 외장 함수들에 대한 정보를 얻을 수 있다.

몇 가지 예는 다음과 같다.

>- `glob` : 경로 내의 폴더 / 파일 목록 조회
>- `os` : 운영체제에서 제공하는 기본 기능
>- `time` : 시간 관련 함수

```python
# time : 시간 관련 함수
import time
print(time.localtime())
print(time.strftime("%Y-%m-%d %H:%M:%S"))

import datetime
print("오늘 날짜는 ", datetime.date.today())

# timedelta : 두 날짜 사이의 간격
today = datetime.date.today() # 오늘 날짜 저장
td = datetime.timedelta(days=100) # 100일 저장
print("우리가 만난지 100일은", today + td) # 오늘부터 100일 후
```