---
layout: post
title: "TIL-Javascript"
subtitle: "Javascript"
background: '/img/posts/02.jpg'
---

## IE에서 화면에 false 출력될 때
```
<script>
  function test() {
    if (true) {
      return false;
    }
  }
</script>
```

<!-- 페이지에 return false;가 출력됨 -->
<a href="javascript:test();">테스트</a>

<!-- 대체 -->
<a href="javascript://" onClick="test();">테스트</a>
