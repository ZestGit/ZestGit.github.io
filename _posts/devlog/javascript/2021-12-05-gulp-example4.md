---
layout: post
title: gulp (4) sass를 css로 변경
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

- `node-sass` 설치
> yarn add node-sass

- `gulp-sass` 설치
> yarn add gulp-sass

- `gulp-csso` 설치
> yarn add gulp-csso

- `gulp-autoprefixer` 설치
> yarn add gulp-autoprefixer


`gulp-csso`: css를 만들어도 공백하나하나가 byte이기 떄문에 minify를 수행한다.

`gulp-autoprefixer`: 작업한 코드를 알아듣지 못하는 구형 브라우저도 호환 가능하도록 해준다.


## Gulp Code

- `gulpfile.babel.js`에 다음과 같이 작성

```js
import gulp from "gulp";
import gpug from "gulp-pug";
import { async } from "regenerator-runtime";
import del from "del";
import ws from "gulp-webserver";
import image from 'gulp-image';
const sass = require("gulp-sass")(require("node-sass")); // 현재 버전 기준 gulp sass 사용법
import autoprefixer from "gulp-autoprefixer";
import minify from "gulp-csso";

const routes = {
    pug: {
        watch: "src/**/*.pug", // 모든 pug 파일을 지켜본다.
        src: "src/*.pug",
        dest: "build" 
    },
    img: {
        src: "src/img/*",
        dest: "build/img"
    },
    scss: {
        watch: "src/scss/**/*.scss",
        src:"src/scss/style.scss",
        dest: "build"
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

//gulp image 플러그인 설치 
const img = () => {
    gulp.src(routes.img.src)
        .pipe(image())
        .pipe(gulp.dest(routes.img.dest));
}

//예제 sass를 css로 변경해준다.
// css 파일을 최소화시킨다. (브라우저에서 더욱 빠르게 만들기위함)
const styles = async () => {
    gulp.src(routes.scss.src)
    .pipe(sass().on("error", sass.logError)) // sass만의 에러 출력
    .pipe(autoprefixer())
    .pipe(minify())
    .pipe(gulp.dest(routes.scss.dest));
}

// Task = File watch
const watch = () => {
    gulp.watch(routes.pug.watch, pug); // 변경되면 어떤 Task를 수행할 것인지 -> pug
    gulp.watch(routes.scss.watch, styles);
}

const prepare = gulp.series([clean]);

//const assets = gulp.series([pug, img]);
const assets = gulp.series([pug, styles]);

// 두 가지를 병행하려면 parallel을 쓴다.
const live = gulp.parallel([webserver, watch]);

// task들의 series
export const dev = gulp.series([prepare, assets]);
```