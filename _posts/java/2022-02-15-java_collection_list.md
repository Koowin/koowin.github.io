---
title:  "Collection - List"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - java

date: 2022-02-15
last_modified_at: 2022-02-15
---

# 개요

##  Hierarchy of Collection

![Collection](../../assets/images/2022-02-15-java_collection_list/Collection-16449055108191-16449090337232.jpg)

<br><br>

# Methods of List interface

| Method                                               | Description                                                  |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| boolean addAll(int index, Collection<? extends E> c) | 특정 index 에 Collection c 들의 원소를 삽입 (기존 원소들은 뒤로 밀림) |
| void sort(Comparator <? super E> c)                  | Comparator 에 정의된 정렬 기준으로 정렬                      |
| E get(int index)                                     | index 에 있는 원소를 반환                                    |
| E set(int index, E element)                          | index 에 있는 기존 원소를 새로운 원소로 대체, 기존 원소를 반환 |
| void add(int index, E element)                       | index 에 새로운 원소 추가                                    |
| E remove(int index)                                  | index 에 있는 원소 제거, 해당 원소 반환                      |
| int indexOf(Object o)                                | 특정 원소의 index 반환 (앞에서 가장 가까운)                  |
| int lastIndex(Object o)                              | 특정 원소의 index 반환 (뒤에서 가장가까운)                   |
| List\<E> subList(int fromIndex, int toIndex)         | fromIndex 부터 toIndex 까지의 sub List 를 반환               |

<br><br>

# 같이 보면 좋은 포스트

* [Collection](../java_collection)
* [Collection - Queue](../java_collection_queue)
* [Collection - Set](../java_collection_set)

<br><br>

# 참고한 문서

* java.util 패키지 내 List.java
