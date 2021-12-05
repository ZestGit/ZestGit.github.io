---
layout: post
title: gulp (5) Babelify + Browserify
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

- `gulp-bro` 설치
> yarn add gulp-bro

- `babelify` 설치
> yarn add babelify

- `uglifyify` 설치
> yarn add uglifyify


`Browserify`: 브라우저는 import, export 같은 구문을 이해하지 못하는데 Browserify가 이걸 도와준다.

`Babelify`: Browserify안에 Babel을 함께 실행시킨다.

`uglifyify`: 코드를 압축해준다.

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
import bro from "gulp-bro";
import babelify from "babelify";

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
    },
    js: {
        watch: "src/js/**/*.js",
        src: "src/js/main.js",
        dest: "build/js"
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

// css 파일을 최소화시킨다. (브라우저에서 더욱 빠르게 만들기위함)
const styles = async () => {
    gulp.src(routes.scss.src)
    .pipe(sass().on("error", sass.logError)) // sass만의 에러 출력
    .pipe(autoprefixer())
    .pipe(minify())
    .pipe(gulp.dest(routes.scss.dest));
}

// 예제 Babelify + Browserify
// 만약에 react를 작업한다면 presets에 react preset을 넣어주면 된다.
const js = async () => {
    gulp.src(routes.js.src)
    .pipe(bro({
        transform: [
            babelify.configure({ presets: ["@babel/preset-env"] }),
            [ 'uglifyify', { global: true } ]
        ]
    }))
    .pipe(gulp.dest(routes.js.dest));
}

// Task = File watch
const watch = () => {
    gulp.watch(routes.pug.watch, pug); // 변경되면 어떤 Task를 수행할 것인지 -> pug
    gulp.watch(routes.scss.watch, styles);
    gulp.watch(routes.js.watch, js);
}

const prepare = gulp.series([clean]);

//const assets = gulp.series([pug, img]);
const assets = gulp.series([pug, styles, js]);

// 두 가지를 병행하려면 parallel을 쓴다.
const live = gulp.parallel([webserver, watch]);

// task들의 series
export const dev = gulp.series([prepare, assets]);
```