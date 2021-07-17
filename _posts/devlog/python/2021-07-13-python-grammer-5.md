---
layout: post
title: Python 문법 정리 (예외 처리)
description: >
    Python 내용 정리
category: devlog
tags: python
sitemap: true
hide_last_modified: true
---

# Python 문법 정리 (예외 처리)

1. try except
2. 사용자 정의 예외 처리
{:toc}

# 예외 처리

## 1. try except

```python
try:
    print("나누기 전용 계산기입니다.")
    nums = []
    nums.append(int(input("첫 번째 숫자를 입력하세요 : ")))
    nums.append(int(input("두 번째 숫자를 입력하세요 : ")))
    # nums.append(int(nums[0] / nums[1]))
    print("{0} / {1} = {2}".format(nums[0], nums[1], nums[2]))
except ValueError:
    print("에러 발생")
except ZeroDivisionError as err: # err는 메시지
    print(err)
except Exception as err: # 모든 에러
    print(err)
```

## 2. 사용자 정의 예외 처리

- `raise`로 예외를 발생시킨다.

```python
class BigNumberError(Exception): # 사용자 정의 Exception 클래스
    def __init__(self, msg):
        self.msg = msg

    def __str__(self): # 에러 메시지 지정
        return self.msg

try:
    print("한 자리 숫자 나누기 전용 계산기입니다.")
    num1 = int(input("첫 번째 숫자를 입력하세요 : "))
    num2 = int(input("두 번째 숫자를 입력하세요 : "))
    if num1 >= 10 or num2 >= 10:
        raise BigNumberError("입력값 : {0}, {1}".format(num1, num2)) # 예외를 발생시킨다.
    print("{0} / {1} = {2}".format(num1, num2, int(num1/num2)))
except ValueError:
    print("잘못된 값을 입력하였습니다. 한 자리 숫자만 입력하세요")
except BigNumberError as err:
    print("에러가 발생하였습니다. 한 자리 숫자만 입력하세요")
    print(err)
finally:
    print("계산기를 이용해주셔서 감사합니다.")       
```