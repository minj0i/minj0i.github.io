---
layout: post
title: "TIL-JAVASCRIPT - axios"
subtitle: "JAVASCRIPT - axios"
background: '/img/posts/02.jpg'
---

# AXIOS

`axios`는 JavaScript를 통해 직접 요청을 보내기 위해 널리 사용되는 라이브러리입니다. GET 메소드로 요청을 보내기 위해 `axios.get()` 함수를 사용할 수 있는데, 이 때 `Promise` 객체가 반환됩니다.

axios는 Promise를 기반으로 하며 async/await문법을 사용하여 XHR요청을 매우 쉽게 할 수 있다.

(출처: https://velog.io/@sss5793/axios-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0-uuk5elxk88)

axios는 node.js와 브라우저를 위한 http통신 javascript 라이브러리입니다. Fetch와 달리 크로스 브라우징에 최적화

catch 에 걸렸을 때, .then(~~~)을 실행하지 않고, console 창에 해당 에러로그를 보여준다.


## AXIOS, FETCH 비교
(출처: https://donghunee.github.io/study/2019/10/21/react/)

### Axios
- 사용하기 더 편하다 (fetch도 물론 편하다)
- fetch에서 지원하지 않는 기능들을 지원해준다.
- Promise base

### Fetch
- import 하지않고 쓸 수 있다.
- React Native의 경우 업데이트가 잦아서, 라이브러리가 업데이트를 쫒아오지 못하는 경우가 생기는데, Fetch의 경우 이런 걱정 필요 없음.
- Promise base
- 네트워크 에러가 발생했을 때, 기다려야 함.. > response timeout API 제공 x
- 지원하지 않는 브라우저가 있음.

[코드 비교]
## FETCH - POST
```JAVASCRIPT
let url = 'https://someurl.com';
let options = {
            method: 'POST',
            mode: 'cors',
            headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json;charset=UTF-8'
            },
            body: JSON.stringify({
                property_one: value_one,
                property_two: value_two
            })
        };
let response = await fetch(url, options);
let responseOK = response && response.ok;
if (responseOK) {
    let data = await response.json();
    // do something with data
}
```

[코드 비교]
## AXIOS - POST
```JAVASCRIPT
let url = 'https://someurl.com';
let options = {
            method: 'POST',
            url: url,
            headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json;charset=UTF-8'
            },
            data: {
                property_one: value_one,
                property_two: value_two
            }
        };
let response = await axios(options);
let responseOK = response && response.status === 200 && response.statusText === 'OK';
if (responseOK) {
    let data = await response.data;
    // do something with data
}
```

## XHR (XMLHttpRequest)
XMLHttpRequest(XHR) 객체는 서버와 상호작용하기 위하여 사용됩니다. 전체 페이지의 새로고침없이도 URL 로부터 데이터를 받아올 수 있습니다. 이는 웹 페이지가 사용자가 하고 있는 것을 방해하지 않으면서 페이지의 일부를 업데이트할 수 있도록 해줍니다. XMLHttpRequest 는 AJAX 프로그래밍에 주로 사용됩니다.