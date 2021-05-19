---
layout: post
title: Git 명령어 모음
description: >
    Git Command
category: devlog
tags: development
sitemap: true
hide_last_modified: true
---

## Git 명령어 모음
주로 사용하는 Git 명령어를 간단히 정리하였으며, 필요할 때마다 추가하도록 할 예정입니다.

```
git init
```
>- 현재 디렉토리에 저장소를 생성한다.

```
git status
```
>- 현재까지 변경사항을 조회한다.

```
git add [파일명]  
git add .
```
>- Staging Area(스테이지)에 추가한다. 
>- 파일의 수정, 삭제 등의 정보를 Git에 기록한다.
>- `.` 지정 시 현재까지 변경된 모든 파일을 추가한다.


```
git commit -m 'Commit Message'
```
> - Staging에 있는 파일들을 로컬 저장소에 추가한다.  
> - 'Commit Message'에 변경 사항에 대한 메시지를 입력할 수 있다.

```
git push
```
>- 로컬 저장소에 추가된 파일들을 원격 저장소에 업로드한다.

```
git pull
```
>- 원격 저장소의 수정된 내용을 로컬 저장소로 업데이트한다.
>- pull 명령어는 원격 저장소의 내용을 가져온 후 자동으로 병합(Merge) 처리한다.

```
git fetch
```
>- 원격 저장소의 수정된 내용을 로컬 저장소로 업데이트한다.
>- pull과 달리 병합(Merge)을 처리해주지 않으므로 수동으로 처리한다.

```
git clone [주소]
```
>- 원격 저장소에서 프로젝트를 내려받는다.

```
git diff
``` 
>- 수정된 내용을 확인한다.

```
git branch  
git branch -v
```
>- 현재 등록되어있는 브랜치 목록을 확인한다.
>- `-v` 옵션을 주면 상세한 정보를 볼 수 있다.

```
git branch [branch명]
```
>- 브랜치를 생성한다.

```
git checkout [branch명]
```
>- 현재 master 브랜치에서 사용할 브랜치로 이동한다.

```
git checkout -b
```
>- 브랜치를 생성하고 해당 브랜치로 이동된다.

```
git branch -d [branch명]
```
>- 브랜치를 제거한다.

***
## pull과 fetch의 차이
    pull : 자동으로 병합(Merge)되기 때문에 어떤 내용이 병합되었는지 알기 힘들다.
    fetch : 수동으로 병합(Merge)하므로 원격 저장소와 로컬 저장소의 차이를 비교하여 체크를 할 수 있다.




