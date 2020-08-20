---
layout: post
title: "TIL-JAVASCRIPT - Ajax"
subtitle: "JAVASCRIPT - Ajax"
background: '/img/posts/02.jpg'
---
(출처: https://poiemaweb.com/js-ajax)

# 비동기식 처리 모델과 Ajax

> ## Ajax(Asynchronous JavaScript and XML)

[전통적인 웹 페이지]
<div style="width:50%; margin: 0 auto">

![TraditionWebPageLifeCycle](https://poiemaweb.com/img/traditional-webpage-lifecycle.png)

</div>

[비동기적 웹 페이지]

Ajax(Asynchronous JavaScript and XML)는 자바스크립트를 이용해서 비동기적(Asynchronous)으로 서버와 브라우저가 데이터를 교환할 수 있는 통신 방식을 의미한다.

서버로부터 웹페이지가 반환되면 화면 전체를 갱신해야 하는데 페이지 일부만을 갱신하고도 동일한 효과를 볼 수 있도록 하는 것이 Ajax이다. 페이지 전체를 로드하여 렌더링할 필요가 없고 갱신이 필요한 일부만 로드하여 갱신하면 되므로 빠른 퍼포먼스와 부드러운 화면 표시 효과를 기대할 수 있다.
<div style="width:50%; margin: 0 auto">

![AjaxLifeCycle](https://poiemaweb.com/img/ajax-webpage-lifecycle.png)

</div>

> ## JSON(JavaScript Object Notation)

JSON(JavaScript Object Notation)은 클라이언트와 서버 간 데이터 교환을 위한 규칙 즉 데이터 포맷을 말한다.

JSON은 일반 텍스트 포맷보다 효과적인 데이터 구조화가 가능하며 XML 포맷보다 가볍고 사용하기 간편하며 가독성도 좋다.

자바스크립트의 객체 리터럴과 매우 흡사하다. 하지만 JSON은 순수한 텍스트로 구성된 규칙이 있는 데이터 구조이다.

키는 반드시 `큰따옴표(작은따옴표 사용불가)`로 둘러싸야 한다.

```JAVASCRIPT
//예시
{
  "name": "Lee",
  "gender": "male",
  "age": 20,
  "alive": true
}
```

> ### JSON.stringify
객체를 JSON 형식의 문자열로 변환한다.
```JAVASCRIPT
const o = { name: 'Lee', gender: 'male', age: 20 };

// 객체 => JSON 형식의 문자열
const strObject = JSON.stringify(o);
console.log(typeof strObject, strObject);
// string {"name":"Lee","gender":"male","age":20}

// replacer
// 값의 타입이 Number이면 필터링되어 반환되지 않는다.
function filter(key, value) {
  // undefined: 반환하지 않음
  return typeof value === 'number' ? undefined : value;
}

// 객체 => JSON 형식의 문자열 + replacer + prettify
const strFilteredObject = JSON.stringify(o, filter, 2);
console.log(typeof strFilteredObject, strFilteredObject);
/*
string {
  "name": "Lee",
  "gender": "male"
}
*/
```

> ### JSON.parse
JSON 데이터 문자열을 객체로 변환한다.
```
서버로부터 브라우저로 전송된 JSON 데이터는 문자열이다. 이 문자열을 객체로서 사용하려면 객체화하여야 하는데 이를 역직렬화(Deserializing)이라 한다. 역직렬화를 위해서 내장 객체 JSON의 static 메소드인 JSON.parse를 사용한다.
```

```JAVASCRIPT
const todos = [
  { id: 1, content: 'HTML', completed: true },
  { id: 2, content: 'CSS', completed: true },
  { id: 3, content: 'JavaScript', completed: false }
];

// 배열 => JSON 형식의 문자열
const str = JSON.stringify(todos);
console.log(typeof str, str);

// JSON 형식의 문자열 => 배열
const parsed = JSON.parse(str);
console.log(typeof parsed, parsed);
```

> ## XMLHttpRequest
브라우저는 XMLHttpRequest 객체를 이용하여 Ajax 요청을 생성하고 전송한다. 서버가 브라우저의 요청에 대해 응답을 반환하면 같은 XMLHttpRequest 객체가 그 결과를 처리한다.

> ### Ajax.request
```JAVASCRIPT
// XMLHttpRequest 객체의 생성
const xhr = new XMLHttpRequest();
// 비동기 방식으로 Request를 오픈한다
xhr.open('GET', '/users');
// Request를 전송한다
xhr.send();
```

1. XMLHttpRequest.open

XMLHttpRequest 객체의 인스턴스를 생성하고 XMLHttpRequest.open 메소드를 사용하여 서버로의 요청을 준비한다. XMLHttpRequest.open의 사용법은 아래와 같다.
```JAVASCRIPT
XMLHttpRequest.open(method, url[, async])
```
- 매개변수 /	설명
- method	/ HTTP method (“GET”, “POST”, “PUT”, “DELETE” 등)
- url	    / 요청을 보낼 URL
- async	  / 비동기 조작 여부. 옵션으로 default는 true이며 비동기 방식으로 동작한다.


2. XMLHttpRequest.send

XMLHttpRequest.send 메소드로 준비된 요청을 서버에 전달한다.

기본적으로 서버로 전송하는 데이터는 GET, POST 메소드에 따라 그 전송 방식에 차이가 있다.

GET 메소드의 경우, URL의 일부분인 쿼리문자열(query string)로 데이터를 서버로 전송한다.

POST 메소드의 경우, 데이터(페이로드)를 Request Body에 담아 전송한다.

만약 요청 메소드가 GET인 경우, send 메소드의 인수는 무시되고 request body은 null로 설정한다.

```JAVASCRIPT
xhr.send(null);
// xhr.send('string');
// xhr.send(new Blob()); // 파일 업로드와 같이 바이너리 컨텐트를 보내는 방법
// xhr.send({ form: 'data' });
// xhr.send(document);
```

3. XMLHttpRequest.setRequestHeader

XMLHttpRequest.setRequestHeader 메소드는 HTTP Request Header의 값을 설정한다. setRequestHeader 메소드는 반드시 XMLHttpRequest.open 메소드 호출 이후에 호출한다.

자주 사용하는 Request Header인 Content-type, Accept에 대해 살펴보자.

Content-type은 request body에 담아 전송할 데이터의 MIME-type의 정보를 표현한다. 자주 사용되는 MIME-type은 아래와 같다.

타입 |	서브타입
- text 타입 |	text/plain, text/html, text/css, text/javascript
- Application 타입 | application/json, application/x-www-form-urlencode
- File을 업로드하기 위한 타입 |	multipart/formed-data

```JAVASCRIPT
//예시)
// json으로 전송하는 경우
xhr.open('POST', '/users');

// 클라이언트가 서버로 전송할 데이터의 MIME-type 지정: json
xhr.setRequestHeader('Content-type', 'application/json');

const data = { id: 3, title: 'JavaScript', author: 'Park', price: 5000};

xhr.send(JSON.stringify(data));
// x-www-form-urlencoded으로 전송하는 경우
xhr.open('POST', '/users');

// 클라이언트가 서버로 전송할 데이터의 MIME-type 지정: x-www-form-urlencoded
// application/x-www-form-urlencoded는 key=value&key=value...의 형태로 전송
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');

const data = { title: 'JavaScript', author: 'Park', price: 5000};

xhr.send(Object.keys(data).map(key => `${key}=${data[key]}`).join('&'));
// escaping untrusted data
// xhr.send(Object.keys(data).map(key => `${key}=${encodeURIComponent(data[key])}`).join('&'));
```

> ### Ajax.response

```JAVASCRIPT
//예시
// XMLHttpRequest 객체의 생성
var xhr = new XMLHttpRequest();
// 비동기 방식으로 Request를 오픈한다
xhr.open('GET', 'data/test.json');
// Request를 전송한다
xhr.send();

// XMLHttpRequest.readyState 프로퍼티가 변경(이벤트 발생)될 때마다 콜백함수(이벤트 핸들러)를 호출한다.
xhr.onreadystatechange = function (e) {
  // 이 함수는 Response가 클라이언트에 도달하면 호출된다.

  // readyStates는 XMLHttpRequest의 상태(state)를 반환
  // readyState: 4 => DONE(서버 응답 완료)
  if (xhr.readyState !== XMLHttpRequest.DONE) return;

  // status는 response 상태 코드를 반환 : 200 => 정상 응답
  if(xhr.status === 200) {
    console.log(xhr.responseText);
  } else {
    console.log('Error!');
  }
};
```

> ## Ajax 예제

1. JSONP

요청에 의해 웹페이지가 전달된 서버와 동일한 도메인의 서버로 부터 전달된 데이터는 문제없이 처리할 수 있다. 하지만 보안상의 이유로 다른 도메인(http와 https, 포트가 다르면 다른 도메인으로 간주한다)으로의 요청(크로스 도메인 요청)은 제한된다. 이것을 동일출처원칙(Same-origin policy)이라고 한다.
![sop](https://poiemaweb.com/img/cdr.jpg)

동일출처원칙을 우회하는 방법은 세가지가 있다.

1. 웹서버의 프록시 파일

서버에 원격 서버로부터 데이터를 수집하는 별도의 기능을 추가하는 것이다. 이를 프록시(Proxy)라 한다.

2. JSONP

script 태그의 원본 주소에 대한 제약은 존재하지 않는데 이것을 이용하여 다른 도메인의 서버에서 데이터를 수집하는 방법이다. 자신의 서버에 함수를 정의하고 다른 도메인의 서버에 얻고자 하는 데이터를 인수로 하는 함수 호출문을 로드하는 것이다.
![jsonp](https://poiemaweb.com/img/comparison_between_ajax_and_jsonp.png)

```HTML
<!--예시-->
<!-- 루트 폴더(webserver-express/public)/loadjsonp.html -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="https://poiemaweb.com/assets/css/ajax.css">
  </head>
  <body>
    <div id="content"></div>
  <script>
    function showTours(data) {
      console.log(data); // data: object

      // JSON → HTML String
      let newContent = `<div id="tours">
          <h1>Guided Tours</h1>
        <ul>`;

      data.tours.forEach(tour => {
        newContent += `<li class="${tour.region} tour">
            <h2>${tour.location}</h2>
            <span class="details">${tour.details}</span>
            <button class="book">Book Now</button>
          </li>`;
      });

      newContent += '</ul></div>';

      document.getElementById('content').innerHTML = newContent;
    }
    </script>
    <script src='https://poiemaweb.com/assets/data/data-jsonp.js'></script>
    <!-- <script>
      showTours({
        "tours": [
          {
            "region": "usa",
            "location": "New York, USA",
            "details": "$1,899 for 7 nights"
          },
          {
            "region": "europe",
            "location": "Paris, France",
            "details": "$2,299 for 7 nights"
          },
          {
            "region": "asia",
            "location": "Tokyo, Japan",
            "details": "$3,799 for 7 nights"
          }
        ]
      });
    </script> -->
  </body>
</html>
```

3. Cross-Origin Resource Sharing

HTTP 헤더에 추가적으로 정보를 추가하여 브라우저와 서버가 서로 통신해야 한다는 사실을 알게하는 방법이다. W3C 명세에 포함되어 있지만 최신 브라우저에서만 동작하며 서버에 HTTP 헤더를 설정해 주어야 한다.

Node.js로 구현한 서버의 경우, CORS package를 사용하면 간단하게 Cross-Origin Resource Sharing을 구현할 수 있다.

```JAVASCRIPT
const express = require('express')
const cors = require('cors')
const app = express()

app.use(cors())

app.get('/products/:id', function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for all origins!'})
})

app.listen(80, function () {
  console.log('CORS-enabled web server listening on port 80')
})
```