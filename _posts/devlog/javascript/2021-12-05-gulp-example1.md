---
layout: post
title: gulp (1) 모든 pug파일을 HTML로 바꾸기
description: >
    gulp 내용 정리
category: devlog
tags: javascript
sitemap: true
hide_last_modified: true
---

1. 설치 플러그인
2. Gulp Code
{:toc}

## 설치 플러그인

- gulp-pug 설치(pug template을 컴파일 해준다.)
> yarn add gulp-pug


## Gulp Code


- `index.pug`에 다음과 같이 작성

```pug
extends templates/layout

block content
    img(src="img/logo.svg")
    h1 Awesome Minimalism
```


- `gulpfile.babel.js`에 다음과 같이 작성

```js
import gulp from "gulp";
import gpug from "gulp-pug";
import { async } from "regenerator-runtime";
import del from "del";

// 첫번째 예제 Task = 모든 pug파일을 HTML로 바꾸는 task
const routes = {
    pug: {
        watch: "src/**/*.pug", // 모든 pug 파일을 지켜본다.
        src: "src/*.pug",
        dest: "build" 
    }
}

// gulp는 pipe랑 쓰인다.
const pug = async () => {
    gulp.src(routes.pug.src)
        .pipe(gpug())
        .pipe(gulp.dest(routes.pug.dest));
}

// 이걸 다시 build했을 때 생길 수 있는 문제점은 기존에 있는 build랑 충돌될 수 있다.
// 먼저 build 폴더를 clear한 후 build한다. (del 모듈 사용)
// build clear
const clean = () => del(["build/"]);

// Task = File watch (파일 변경 감지)
const watch = () => {
    gulp.watch(routes.pug.watch, pug); // 변경되면 어떤 Task를 수행할 것인지 -> pug
}

const prepare = gulp.series([clean]);

// task들의 series
export const dev = gulp.series([prepare, pug]);
```