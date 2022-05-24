---
title:  "스프링 부트와 AWS로 혼자 구현하는 웹 서비스 1: hello"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - spring

published: false

date: 2022-05-21
last_modified_at: 2022-05-21
sitemap:
  changefreq: daily
  priority: 1.0

---

# 개요

처음 스프링을 접할 당시 [스프링 부트와 AWS로 혼자 구현하는 웹 서비스](http://www.yes24.com/Product/Goods/83849117) 책을 읽으며 공부해보려 했었습니다. 하지만, 2019년 말에 나온 책이어서 JUnit 5 를 사용하고 싶었지만, 책에서는 JUnit 4 를 사용하는 등 약간씩 달라지는 부분이 있어 '스프링 강의를 먼저 듣고 다시 보자!' 라는 생각을 하게 되었습니다. (그 땐 gradle 이 무엇인지도 잘 몰랐었습니다.)

지금은 스프링의 구조가 어떻게 되는지 대략 감을 잡은 상태라 다시 읽어보려고 합니다.

책에서 구현하는 게시판 웹 서비스를 따라 만들어보는 것이 목표이고, 책과 다른 점은 JUnit 5 를 사용했다는 점입니다.



# 