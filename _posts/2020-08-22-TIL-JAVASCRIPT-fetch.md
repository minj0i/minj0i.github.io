---
layout: post
title: "TIL-JAVASCRIPT - bind"
subtitle: "JAVASCRIPT - bind"
background: '/img/posts/02.jpg'
---

# Fetch API
(출처: https://developer.mozilla.org/ko/docs/Web/API/Fetch_API)
(출처: https://www.zerocho.com/category/HTML&DOM/post/595b4bc97cafe885540c0c1c)

Fetch에는 일반적인 오브젝트로로 Request 와 Response가 포함되어 있습니다. 이것들은 service worker이나 Cache API같이 Response와 Request객체를 다루는 API나 독자적으로 리스폰스를 발생시키는 경우에도 사용 가능합니다.
최신 API이기 때문에 아쉽게도 IE에서는 사용할 수 없습니다.(IE에서 사용하려면 polyfill을 사용)

`fetch()`를 불러들이는 경우, 취득할 리소스를 반드시 인수로 지정하지 않으면 안됩니다. 읽어들인 뒤,  fetch()는 `Promise`객체를 반환합니다. 리퀘스트가 성공하든 실패하든 해당 리퀘스트 통신에 대한 `Response`객체가 취득됩니다. fetch()의 두번째 인수는 초기화에 사용되는 객체를 정의하고 있습니다. 이 인수는 기입하지 않아도 함수의 동작에 문제가 없습니다. 

> fetch 기본 구조

```
fetch('주소', 설정객체).then(콜백).catch(콜백);
```
```JAVASCRIPT
fetch('https://www.zerocho.com/api/get').then((res) => {
  if (res.status === 200 || res.status === 201) { // 성공을 알리는 HTTP 상태 코드면
    res.text().then(text => console.log(text)); // 텍스트 출력
  } else { // 실패를 알리는 HTTP 상태 코드면
    console.error(res.statusText);
  }
}).catch(err => console.error(err));
```

응답으로 받는 res는 Response 객체입니다. Response 객체는 응답에 대한 정보를 담고 있습니다. 객체 안의 status와 statusText 등은 성공 여부를 판가름할 때 쓰시면 되고요. headers는 응답에 대한 헤더 정보를 담고 있는 Headers 객체입니다.

## Response 객체에서 값을 볼 수 있게 해주는 메소드 5가지
**text, arrayBuffer, blob, json, formData**

모두 Promise를 return합니다. 그래서 위에서 `res.text().then(text => console.log(text))`으로 또 한 번 결과를 Promise로 받았습니다. 만약 json 데이터가 응답으로 오면 `res.json().then(json => console.log(json));` 이렇게 받으면 되겠죠? blob이나 arrayBuffer는 이미지나 파일같은 데이터일 때 사용하면 됩니다.

## Headers 객체
**append, delete, entries, get, has, keys, set, values 메소드를 지원합니다.**

```JAVASCRIPT
res.headers.entries().next().value; // ['content-type', 'text/html; charset=utf-8']
```

## fetch 사용 예시
```JAVASCRIPT
const req = new Request('https://www.zerocho.com/api/get');
fetch(req).then((res) => { // Request 객체에 주소를 넣느니 그냥 fetch에 넣으면 됨
  if (res.status === 200 || res.status === 201) { // 성공을 알리는 HTTP 상태 코드면
    res.text().then(text => console.log(text)); // 텍스트 출력
  } else { // 실패를 알리는 HTTP 상태 코드면
    console.error(res.statusText);
  }
});
```

JSON을 전송하는 POST 요청
```JAVASCRIPT
const body = { name: 'zerocho' };
fetch('https://www.zerocho.com/api/post/json', {
  method: 'POST',
  body,
  headers: new Headers(), // 이 부분은 따로 설정하고싶은 header가 있다면 넣으세요
}).then((res) => {
  if (res.status === 200 || res.status === 201) {
    res.json().then(json => console.log(json));
  } else {
    console.error(res.statusText);
  }
}).catch(err => console.error(err));
```

formData를 사용한 POST요청
```JAVASCRIPT
const formData = new FormData();
formData.append('name', 'zero')
fetch('https://www.zerocho.com/api/post/formdata', {
  method: 'POST', // POST 메소드 지정
  body: formData, // formData를 데이터로 설정
}).then((res) => {
  if (res.status === 200 || res.status === 201) {
    res.json().then(json => console.log(json));
  } else {
    console.error(res.statusText);
  }
}).catch(err => console.error(err));
```

(출처: https://velog.io/@prayme/Fetch-API)
## JQuery와 가장 다른점 세가지

- fetch()가 반환하는 Promise는 response가 HTTP 404, 500 같은 HTTP error status여도 거부하지 않고 다 받아온다.
- cross-site cookies를 받지 않는다. fetch()는 cross-site session을 설정할 수 없다. 다른 사이트의 Set-Cookie 헤더는 자동으로 무시한다.
- credential init 옵션을 설정하지 않으면 cookie를 전송하지 않는다.

Fetch에는 fetch(), Headers, Request, Response 인터페이스가 존재한다.