---
layout: post
title: gulp (3) Image Optimization
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

- gulp-image 설치
> yarn add gulp-image


## Gulp Code

- `gulpfile.babel.js`에 다음과 같이 작성

```js
import gulp from "gulp";
import gpug from "gulp-pug";
import { async } from "regenerator-runtime";
import del from "del";
import ws from "gulp-webserver";
import image from 'gulp-image';

const routes = {
    pug: {
        watch: "src/**/*.pug", // 모든 pug 파일을 지켜본다.
        src: "src/*.pug",
        dest: "build" 
    },
    img: {
        src: "src/img/*",
        dest: "build/img"
    }
}

// gulp는 pipe랑 쓰인다.
const pug = async () => {
    gulp.src(routes.pug.src)
        .pipe(gpug())
        .pipe(gulp.dest(routes.pug.dest));
}
// build clear
const clean = () => del(["build/"]);

// - gulp webserver 플러그인 설치 
const webserver = () => {
    gulp.src("build")
        .pipe(ws({livereload:true, open:true}));
}

//예제 image Optimization = 시간이 오래걸린다. 
const img = () => {
    gulp.src(routes.img.src)
        .pipe(image())
        .pipe(gulp.dest(routes.img.dest));
}

// Task = File watch
const watch = () => {
    gulp.watch(routes.pug.watch, pug); // 변경되면 어떤 Task를 수행할 것인지 -> pug
}

const prepare = gulp.series([clean]);

const assets = gulp.series([pug, img]);

// 두 가지를 병행하려면 parallel을 쓴다.
const live = gulp.parallel([webserver, watch]);

// task들의 series
export const dev = gulp.series([prepare, assets]);
```