---
layout: post
title: Python 문법 정리 (class)
description: >
    Python 내용 정리
category: devlog
tags: python
sitemap: true
hide_last_modified: true
---

# Python 문법 정리 (Class)

1. 기본적인 사용법
2. 상속
3. 추상 클래스
4. 정적 메소드와 클래스 메소드
{:toc}


## Class

- 객체를 구별하기 위해 메소드의 첫 번째 인자로 `self`를 전달한다.
- C++과 같이 다중 상속이 가능하다.
- 메소드 오버로딩이 없다. (같은 이름의 메소드를 선언하면 나중에 선언된 것만 유지된다.)

### 기본적인 사용법

- 생성자로 객채 생성이 호출되면 먼저 `__new__`를 호출하여 객체를 생성 할당하고, `__new__` 메소드가 `__init__` 메소드를 호출하여 초기값들을 초기화한다.
- 일반적으로 `__init__` 메소드만 오버라이딩하여 초기화를 수행한다.
- 파이썬에서 변수는 기본적으로 모두 public이다.

```python
# 일반 유닛
class Unit:
    def __init__(self, name, hp, speed): # __init__ 파이썬에서 쓰이는 객체 초기화 함수
        self.name = name
        self.hp = hp
        self.speed = speed
    
    def move(self, location):
        print("[지상 유닛 이동]")
        print("{0} : {1} 방향으로 이동합니다. [속도 {2}]".format(\
            self.name, location, self.speed))
```

- `_` 네이밍 컨벤션은 내부적으로 사용되는 변수라는 의미
- `_`는 내부 변수라는 의미로만 알고 있는 것이고 외부에서 접근이 가능하다. 따라서 원천적인 접근을 막기 위해서는 `__` 더블 언더바를 사용한다. (비공개 속성)

``` python
class Flight:
    def __init__(self, number):
        self.__number = number # __number는 비공개 속성
```

- self.속성은 모두 인스턴스 속성이며, 클래스 속성은 class에서 바로 할당한다.
- `__` 더블 언더바로 비공개 클래스 속성으로 만들 수 있다.
- 인스턴스와 클래스에 같은 이름의 속성이 있으면 인스턴스부터 찾는다.

```python
class MyClass:
    # 클래스 속성
    attr = [] # 속성명 = 값 -> 여러 객체가 공유한다.
    __name = "MyClass" # 비공개 ㄹ래스 속성

    def __init__(self):
        # 인스턴스 속성을 같은 이름으로 선언
        self.attr = [] # 같은 속성이 있을 경우 인스턴스부터 찾음
```

### 상속

```python
# 상속
class AttackUnit(Unit): # 공격 유닛
    def __init__(self, name, hp, speed, damage):
        Unit.__init__(self, name, hp, speed) # 부모 생성자 호출
        self.damage = damage
    
    def attack(self, location):
        print("{0} : {1} 방향으로 적군을 공격합니다. [공격력 {2}]"\
            .format(self.name, location, self.damage))

    def damaged(self, damage):
        print("{0} : {1} 데미지를 입었습니다.".format(self.name, damage))
        self.hp -= damage
        print("{0} : 현재 체력은 {1} 입니다.".format(self.name, self.hp))
        if self.hp <= 0:
            print("{0} : 파괴되었습니다.".format(self.name))

# 다중 상속
class Flyable: # 날 수 있는 기능을 가진 클래스
    def __init__(self, flying_speed):
        self.flying_speed = flying_speed

    def fly(self, name, location):
        print("{0} : {1} 방향으로 날아갑니다. [속도 : {2}]".format(\
            name, location, self.flying_speed))

# 공중 공격 유닛 클래스
class FlayableAttackUnit(AttackUnit, Flyable): # 다중 상속
    def __init__(self, name, hp, damage, flying_speed):
        AttackUnit.__init__(self, name, hp, 0, damage) # 지상 speed 0
        Flyable.__init__(self, flying_speed)
    
    def move(self, location): # 메소드 오버라이딩
        print("[공중 유닛 이동]")
        self.fly(self.name, location)

 # 건물
class BuildingUnit(Unit):
    def __init__(self, name, hp, location):
        # super로 init (self는 안쓴다.)
        # 다중 상속을 받을 경우에는 첫번째로 쓴 클래스 생성자를 초기화한다. 
        # (Unit, Flyable)라고 쓴 경우 Unit 생성자 호출
        super().__init__(name, hp, 0) 
        self.location = location
        # pass # 아무런 동작을 하지 않고 다음 코드 계속해서 진행
```

`mro()` 메소드를 통해 클래스의 상속 관계를 확인할 수 있다.
{:.note}

### 추상 클래스

- `abc` 모듈을 import 해야한다.
- 추상 메소드에 `@abstractmethod` 데코레이터를 붙인다.

```python
from abc import *

class AbstractStudent(metaclass=ABCMeta):
    @abstractmethod # 추상 메소드 데코레이터
    def study(self):
        pass

    @abstractmethod
    def go_to_school(self):
        pass

class Student(AbstractStudent): # 추상 클래스 상속
    # 추상 메소드 구현
    def study(self):
        print("공부를 한다.")
    
    def go_to_school(self):
        print("학교에 간다.")
```

### 정적 메소드와 클래스 메소드

- 정적 메소드에는 `@staticmethod` 데코레이터를 붙인다.
- `self` 매개 변수를 지정하지 않는다.

```python
class Calculator:
    @staticmethod 
    def add(a, b):
        print(a + b)

 Calculator.add(1, 1)
```

- 클래스 메소드에는 `@classmethod` 데코레이터를 붙인다.
- 첫 번째 매개 변수에 cls를 지정해야한다.
- 정적 메소드처럼 인스턴스 없이 호출이 가능하다.
- 메소드 안에서 클래스 속성, 클래스 메소드에 접근해야할 때 사용한다.

```python
class Calculator:
    name = "계산기"
    @classmethod 
    def show_name(cls): # cls에는 클래스가 들어온다.
        print(cls.name) # cls로 클래스 속성에 접근 가능

Calculator.show_name()
```

