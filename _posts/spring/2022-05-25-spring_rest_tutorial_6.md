---
title:  "스프링 REST 튜토리얼 따라해보기 6: HATEOAS"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - spring

published: false

date: 2022-05-25
last_modified_at: 2022-05-25
sitemap:
  changefreq: daily
  priority: 1.0
---

# 개요

REST API 의 요구조건 중 Uniform interface - Hypermedia as the Engine of Application State (줄여서 HATEOAS) 가 있었습니다.

이번 장이 REST 튜토리얼의 마지막 장이며, HATEOAS 가 무엇인지에 대해 자세히 다룹니다.

비즈니스 로직은 필연적으로 바뀌기 마련입니다. 자주 하는 실수가 서버의 로직을 클라이언트로 가져오는 것인데, 이렇게 되면 둘 간의 결합을 강하게 합니다. REST 에서는 클라이언트와 서버가 분리되어 각각 독립적으로 진화하는 것을 요구하고 있습니다. 즉, REST 가 깨지게 되는 것이죠.



# Order

Order 라는 새로운 도메인 모델을 추가해보겠습니다.

```
```



# 출처

* [Building REST services with Spring](https://spring.io/guides/tutorials/rest/)