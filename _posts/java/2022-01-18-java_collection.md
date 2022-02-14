---
title:  "Collections"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - java

date: 2022-01-18
last_modified_at: 2022-01-18
---

# 개요

## 동기

 평소 Collection의 상속 관계에 대해 완전히 알지 못한 채 ArrayList, LinkedList, HashMap 등을 사용하였습니다. 그러다가 프레임워크에 대해 코딩테스트 문제 해결 중 Queue를 사용할 일이 있었는데 Queue가 LinkedList로 구현되었다는 것을 알게되어 이번 기회에 Collection에 대해 정리해보았습니다.



## Collection

 Collection은 자바에서 제공하는 프레임워크로, 객체들을 저장하는 다양한 클래스와 이들의 사용 방법을 정의한 인터페이스들을 제공합니다.

<br><br>


# Hierarchy of Collection framework

 Collection의 계층 구조는 다음과 같습니다.


![java-collection](../../assets/images/2022-01-18-java_collection/image-20220118175233977.png)

이미지 출처: [https://www.javatpoint.com/collections-in-java](https://www.javatpoint.com/collections-in-java)

<br><br>

# Methods of Collection interface

많은 메서드들이 있지만, 몇 개는 생략하고 코딩테스트에서 주로 활용하는 메서드만 정리하였습니다.

| 메서드                                           | 설명                                      |
| ------------------------------------------------ | ----------------------------------------- |
| public boolean add(E e)                          | 원소 추가                                 |
| public boolean addAll(Collection<? extends E> c) | c에 있는 모든 원소 추가                   |
| public boolean remove(Object element)            | 특정 원소 제거                            |
| public boolean removeAll(Collection <?> c)       | c에 있는 원소들과 일치하는 모든 원소 제거 |
| public int size()                                | 원소의 수 반환                            |
| public void clear()                              | 모든 원소 삭제                            |
| public Iterator iterator()                       | iterator 반환                             |
| public Object[] toArray()                        | 배열로 반환                               |
| public \<T> T[] toArray(T[] a)                   | T의 배열로 반환                           |
| public boolean isEmpty()                         | 배열이 비어있는지를 반환                  |

<br><br>

# 참고한 문서들

- 📄 [https://www.javatpoint.com/collections-in-java](https://www.javatpoint.com/collections-in-java)