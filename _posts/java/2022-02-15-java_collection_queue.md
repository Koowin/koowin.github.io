---
title:  "Collection - Queue"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - java

date: 2022-02-15
last_modified_at: 2022-02-15
sitemap:
  changefreq: daily
  priority: 1.0
---

# 개요

## Hierarchy of Collection

![Collection](../../assets/images/2022-02-15-java_collection_queue/Collection-16449055108191-16449090337232.jpg)

<br><br>

# Methods of Queue interface

| Method             | Description                                                  |
| ------------------ | ------------------------------------------------------------ |
| boolean offer(E e) | 원소 e 삽입                                                  |
| E remove()         | 가장 앞에 있는 원소 제거 후 반환, queue 가 비어있다면 exception 발생 |
| E poll()           | 가장 앞에 있는 원소 제거 후 반환, queue 가 비어있다면 null 반환 |
| E element()        | 가장 앞에 있는 원소 제거하지 않고 반환, queue 가 비어있다면 exception 발생 |
| E peek()           | 가장 앞에 있는 원소 제거하지 않고 반환, queue 가 비어있다면 null 반환 |

<br><br>

# Methods of Deque interface

Queue 의 메소드와 마찬가지로 remove 는 deque 가 비어있을 경우 exception 을 발생시키고, poll 은 null 을 반환합니다. 해당 설명은 생략하겠습니다.

| Method                                  | Description                                      |
| --------------------------------------- | ------------------------------------------------ |
| void addFirst(E e)                      | 가장 앞에 원소 e 추가                            |
| void addLast(E e)                       | 가장 뒤에 원소 e 추가                            |
| boolean offerFirst(E e)                 | 가장 앞에 원소 e 추가                            |
| boolean offerLast(E e)                  | 가장 뒤에 원소 e 추가                            |
| E removeFirst()                         | 가장 앞에 있는 원소 제거 후 반환                 |
| E removeLast()                          | 가장 뒤에 있는 원소 제거 후 반환                 |
| E pollFirst()                           | 가장 앞에 있는 원소 제거 후 반환                 |
| E pollLast()                            | 가장 뒤에 있는 원소 제거 후 반환                 |
| E getFirst()                            | 가장 앞에 있는 원소 제거하지 않고 반환           |
| E getLast()                             | 가장 뒤에 있는 원소 제거하지 않고 반환           |
| E peekFirst()                           | 가장 앞에 있는 원소 제거하지 않고 반환           |
| E peekLast()                            | 가장 뒤에 있는 원소 제거하지 않고 반환           |
| boolean removeFirstOccurrence(Object o) | 앞에서 가장 가까운 원소 o 제거 (만약 존재한다면) |
| boolean removeLastOccurrence(Object o)  | 뒤에서 가장 가까운 원소 o 제거 (만약 존재한다면) |
| Iterator\<E> descendingIterator()       | 반대 방향(뒤에서 앞)으로 순회하는 iterator 반환  |

<br><br>

## Methods for Stack

deque 에서는 특이하게 stack 에 대한 메소드도 제공하고 있습니다.

java.util 패키지 내의 Stack.java 파일의 설명을 살펴보니,

> A more complete and consistent set of LIFO stack operations is provided by the Deque interface and its implementations, which should be used in preference to this class. For example: `Deque<Integer> stack = new ArrayDeque<Integer>();`

위와 같이 나와 있습니다. Stack 을 사용하는 것보다 Deque 를 Stack 처럼 사용하는 것을 추천하고 있습니다.

| Method         | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| void push(E e) | 가장 앞에 원소 e 삽입                                        |
| E pop()        | 가장 앞에 있는 원소 반환, deque 가 비어있다면 exception 발생 |

<br><br>

# 같이 보면 좋은 포스트

* [Collection](../java_collection)
* [Collection - List](../java_collection_list)
* [Collection - Set](../java_collection_set)
* [Collection - PriorityQueue](../java_collection_priorityqueue)

<br><br>

# 참고한 문서

* java.util 패키지 내 Queue.java, Deque.java, Stack.java