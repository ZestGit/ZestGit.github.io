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

javaScript란 HTML과 CSS로 만들어진 웹 페이지를 동적으로 변경할 수 있는 언어
javaScript는 모든 브라우저들에 내장되어있다.
현재까지 프론트엔드가 사용할 수 있는 언어는 자바스크립트 뿐이다.


`Vanilla JS`란 Frameworks나 Library를 사용하지 않는 순수한 자바스크립트 

- 특징
    1. 객체 기반의 언어이다.
    2. 인터프리터 언어로서 클라이언트 웹 브라우저에 의해 해석되고 실행된다.
    3. Node.js로 백엔드에도 사용할 수 있다.
    4. 객체형/함수형에 모두 표현 가능하다.

`ES(ECMAScript)`는 javascript의 `Specification`이며 `Specification`는 체계적인 설명서(표준)라고 보면 된다. Chrome, Firefox, IE 등의 브라우저는 `Specification`을 받아서 각자의 방식으로 실행한다.

javascript에 대한 모든 Event는 [MDN](https://developer.mozilla.org/ko/docs/Web/Events)을 참고한다.
{:.note}

## 변수 선언 (var, let, const)

원래는 `var`밖에 없었는데 ES6 이후 `let`과 `const`가  만들어졌다.
`var`는 `Hositing` 현상이 발생할 수 있으므로 가급적이면 `let`과 `const`를 사용하는 것이 좋다.

- var 특징

~~~js
// var는 변수 재선언이 가능하다.
// 코드량이 많아지면 파악이 힘들고 값이 바뀔 수 있으므로 위험하다.
 var name = "Kim";
 console.log(name); // Kim

 var name = "Lee";
 console.log(name); // Lee
~~~


#### Hosting
`Hosting`이란 함수 안에 있는 선언들을 유효 범위의 최상단에 끌어올리는 것을 말한다.
변수의 선언과 할당이 동시에 일어나지 않고 분리되는 것이다.


~~~js
// 에러가 나지 않고 Undefined가 나온다.
console.log(name); // Undefined
var name = "Kim";

// 왜냐하면 실행 시 호이스팅이 일어나기 때문
var name; // name 변수가 호이스팅되면서 최상단에 선언된다.
console.log(name);
name = "Kim"; // 값 할당
~~~

- `let`과 `const`는 블록 레벨 스코프
    - {} 블록 내부에서만 라이프타임 유지
- `var`는 함수 레벨 스코프
    - 블록 내부에 선언되도 접근 가능

~~~js
// let과 var 차이
{
    let name = "Kim";
} // 블록내에서만 살아있는 변수이기 때문에 에러
console.log(name); // ReferenceError

{
    var gender = "male";
} // var는 외부에서 접근 가능
console.log(gender); // male
~~~

#### 데이터 타입별 사용 방법

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
