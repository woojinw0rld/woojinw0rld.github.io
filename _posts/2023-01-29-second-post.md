---
title: Javascript
layout: post
post-image: C:\Users\User\Documents\GitHub\woojinw0rld.github.io\_posts\_images\javascript.jpeg
description: 공부한 자바스크립트의 내용을 챕터별로 나누어서 올릴 예정이다. 이 post에서는 ch2에 대한 복습을 할 것이다. 
tags:
- javascript
---

JavaScript_CH2
=======
*자바스크립트는 html, css와 함께 프론트엔드에서 주로 사용되는 프로그래밍언어이다.  풀스택개발자를 목표로 공부해 볼것이다.*
*배운 내용들을 복습하는 의미로 글을 쓰는 것이기 때문에 코드들을 분석해보는 쪽으로 써내려 가 볼 것이다.*

_*목차는 이렇다*_

1. [글자색 바꾸기](#글자색-바꾸기)
2. [이름입력하기](#글자색-바꾸기)
3. [예제](#예제)
---

본론으로 들어가기 전 기본적인 것들을 먼저 보겠다. 

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title></title>
        <style></style>


    </head>
    <body>    
        
    </body>
</html>
<script></script>
```
`<!DOCUTYPE html>`은 5버전의 html을 사용한다는 뜻이다. `<html lang="ko">`은 한국어를 쓸 것이란 이야기고 `<meta charset="utf-8">`를 써주지 않으면 한국어가 깨진다. 
다른 `<mata>`부분은 딱히 신경쓰지 않아도 될듯 하다.`<title>`부분은 말 그대로 제목이다. `<style>`에는 css가 들어간다. `<body>`에는 html가 들어간다. 
`<script>`에는 javascript가 들어간다. 

### 글자색 바꾸기

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>글자색 바꾸기</title>      
        <link rel="stylesheet" href="1.css">     
    </head>
    <body>
        <h1 id="heading">자바스크립트</h1> 
        <p id="text">위 텍스트를 클릭해 보세요</p>
        <script src="1.js"></script>
    </body>
</html>
```
`<link rel= "stylesheet" href= "1.css">`를 사용하여 css코드를 불러온것을 볼수있다. 그리고 body에선 `<h1 id="heading">자바스크립트</h1> `h1은 제목이다. id는 heading으로 지정, 자바스크립트라는 제목을 출력한 모습이다. 
`<p id="text">위 텍스트를 클릭해 보세요</p>`에선 `<p>`로 문단을 나타낸다. id는 text로 설정한 모습니다. 출력내용은 `<p>'여기사이다.'</p>` 그리고 `<script src="1.js"></script>`로 자바스크립트를 불러온다.

**css code**
```css
#heading{
    color:pink;
}
```
css code를 이용하여 id인 heading에 접근해 핑크색으로 디자인해준 모습이다. id는 #로 접근한다.

**javascript**
```javascript
var heading=document.querySelector("#heading");
heading.onclick=function(){
    heading.style.color="red";
}
```

`var heading` heading변수를 선언한다. `document.querySelector("#heading");` html코드에 선언된 heading의 값을 반환하여 heading에 저장하였다. 

### 이름입력하기

### 예제
