---
layout: post
title: JavaScript
description: >
    JavaScript 내용 정리
category: devlog
tags: javascript
sitemap: true
hide_last_modified: true
---

# JavaScript (1)

## 기본 내용

JavaScript란 HTML과 CSS 만들어진 웹 페이지를 동적으로 변경할 수 있는 언어

`Vanilla JS`란 Frameworks나 Library를 사용하지 않는 순수한 자바스크립트 

- 특징
    1. 객체 기반의 언어이다.
    2. 인터프리터 언어로서 클라이언트 웹 브라우저에 의해 해석되고 실행된다.
    3. Node.js로 백엔드에도 사용할 수 있다.
    4. 객체형/함수형에 모두 표현 가능하다.

`ES(ECMAScript)`는 Javascript의 `Specification`이며 `Specification`는 체계적인 설명서(표준)라고 보면 된다. Chrome, Firefox, IE 등의 브라우저는 `Specification`을 받아서 각자의 방식으로 실행한다.

Javascript에 대한 모든 Event는 [MDN](https://developer.mozilla.org/ko/docs/Web/Events)을 참고한다.
{:.note}

## 기본 문법

원래는 `var`밖에 없었는데 `let`과 `const`가  만들어졌다.
`var`는 같은 이름으로 계속 선언할 수 있어서 실수를 유발할 수 있다. 현재는 `let`과 `const`만 쓰이는 듯 하다.

- `let` : 변수
- `const` : 상수

### Code

- 기본 변수 사용

~~~js
 const a = 100;
 let b = a - 5;
 console.Log(b); // 콘솔에 출력
~~~

- List 사용

~~~js
// [] 안에 값을 넣는다. 
//(string, boolean, number, array, object 등을 모두 넣을 수 있다.)
const daysOfWeek = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sun"];

const myInfo = 
{
    name : "Name",
    age : 30,
    gender : "male",
    favoriteMovies : ["Harry Potter", "Iron man"],
    favoriteFoods : [
        {
            name : "chicken",
            fatty : true
        },
        {
            name : "Kimchi",
            fatty : false
        }
    ]
};
~~~

- 함수 사용

~~~js
 function sayHello(name, age)
 {
     // 예전에 쓰던 방식
     //console.log("Hello!", name, "you have", age, "years of age.");
     //  `` (백틱 문법 -> 강력한 String 기능)
     console.log(`Hello ${name} you are ${age} years old`);
 }

// return 함수
 function sayHello2(name, age)
 {
     return `Hello ${name} you are ${age} years old`;
 }

 // Math Test
 const calulator = 
 {
     plus : function(a, b) { return a + b;},
     minus : function(a, b) { return a - b;},
     multiply : function(a, b) { return a * b;},
     divide : function(a, b) { return a / b;}
 }

 const plusValue = calulator.plus(5, 5);
 console.log(plusValue);
~~~

- javascript에서는 `" "`, `' '` 둘 다 string
{:.note}
