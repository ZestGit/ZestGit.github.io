---
layout: post
title: Python 문법 정리 (3)
description: >
    Python 내용 정리
category: devlog
tags: python
sitemap: true
hide_last_modified: true
---


# Python 문법 정리 (3)

1. 표준 입출력
2. 다양한 출력 포맷
3. 파일 입출력
{:toc}

## 1. 표준 입출력

- print문에서 사용되는 옵션
    - `sep` : 단어를 분리할 구분자 지정
    - `end` : 줄 바꿈을 하지않고 문장의 끝에 추가한다.

```python
# sep 
print("python", "java", sep=",") # python, java 

# end
print("python", "java", end="?") # python java? (문장의 끝에 ? 추가)

import sys
print("python", "java", file=sys.stdout) # 표준 출력
print("python", "java", file=sys.stderr) # 표준 에러

#ljust(8) : 왼쪽으로 정렬하는데 8칸의 공간을 확보한다.
#rjust(4) : 오른쪽으로 정렬하는데 4칸의 공간을 확보한다.
scores = { "수학" : 0, "영어" : 50, "코딩" : 100}
for subject, score in scores.items():
    print(subject.ljust(8), str(score).rjust(4), sep=":")
# 수학      :   0
# 영어      :  50
# 코딩      : 100

# zfill(3) : 3 만큼의 공간을 확보하고 빈 공간은 0으로 채운다.
for num in range(1, 21):
    print("대기번호 : " + str(num).zfill(3)) # 대기번호 : 001, 002, ...
```

## 2. 다양한 출력 포맷
```python
# 빈 자리는 빈공간으로 두고, 오른쪽 정렬, 총 10자리 공간 확보
print("{0: >10}".format(500)) #       500

# 양수일 땐 +로 표시, 음수일 땐 -로 표시
print("{0: >+10}".format(500)) #      +500
print("{0: >+10}".format(-500)) #      -500

# 왼쪽 정렬하고, 빈칸을 _로채움
print("{0:_<+10}".format(500)) #+500______

# 3자리마다 콤마 찍기
print("{0:,}".format(10000000)) # 10,000,000

# 3자리마다 콤마 찍기, +- 부호 붙이기
print("{0:+,}".format(10000000)) # +10,000,000
print("{0:+,}".format(-10000000)) # -10,000,000

# 3자리마다 콤마 찍기, +- 부호 붙이기, 자릿수 확보하기, 빈자리는 ^ 표시
print("{0:^<+30,}".format(10000000)) # +10,000,000^^^^^^^^^^^^^^^^^^^

# 소수점 출력
print("{0:f}".format(5/3)) # 1.666667

# 소수점 특정 자리수까지만 표시 (소수점 3번째 자리에서 반올림)
print("{0:.2f}".format(5/3)) # 1.67
```

## 3. 파일 입출력
```python
score_file = open("score.txt", "w", encoding="utf8") # 덮어쓰기
# print문 사용하여 쓰기
print("수학 : 0", file=score_file)
print("영어 : 50", file=score_file)
print("코딩 : 100", file=score_file)
score_file.close()

score_file = open("score.txt", "a", encoding="utf8") # 이어쓰기
# write 사용하여 쓰기
score_file.write("과학 : 80")
score_file.write("\n사회 : 70") # write는 줄 바꿈이 되지 않으므로 \n을 써준다.
score_file.close()

score_file = open("score.txt", "r", encoding="utf8") # 읽기
print(score_file.read()) # 모든 내용을 읽어오기

# 한 줄씩 읽기, 커서는 다음줄로 이동 (end=""를 추가하여 줄바꿈 없앰)
print(score_file.readline(), end="")
print(score_file.readline(), end="")
print(score_file.readline(), end="")
print(score_file.readline(), end="")

# 한줄 씩 읽기
while True:
    line = score_file.readline()
    if not line: # line이 없을 경우
        break
    print(line, end="")

# 자료구조에 저장
lines = score_file.readlines() 
for line in lines:
    print(line, end="")

score_file.close()

# pickle 모듈 (데이터를 파일 형태로 저장) 객체 직렬화
# pickle을 쓰기 위해서는 반드시 binary(b)를 지정하고 Encoding은 적을 필요 없음
import pickle
profile_file = open("profile.pickle", "wb") # wb
profile = {"이름":"박명수", "나이":30, "취미":["축구", "골프","코딩"]}
pickle.dump(profile, profile_file) # profile 데이터를 profile_file에 저장
profile_file.close()

profile_file = open("profile.pickle", "rb") #rb
profile = pickle.load(profile_file) # profile.pickle 파일에 있는 정보를 profile에 불러오기
print(profile)
profile_file.close()

# with 문 사용하기 (매번 Close를 할 필요가 없다.)
with open("profile.pickle", "rb") as profile_file:
    print(pickle.load(profile_file))

# 파일에 쓰기
with open("study.txt", "w", encoding="utf8") as study_file:
    study_file.write("파이썬")

# 파일 읽기
with open("study.txt", "r", encoding="utf8") as study_file:
    print(study_file.read())
```