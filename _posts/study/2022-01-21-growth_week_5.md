---
title:  "Growth Study: 22.01.22.토"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - study

date: 2022-01-21
last_modified_at: 2022-01-21
---

# 공통 문제

## 프로그래머스: [1차] 캐시

문제 링크: [[1차] 캐시](https://programmers.co.kr/learn/courses/30/lessons/17680)

```java
import java.util.LinkedList;

public class Solution {
    public int solution(int cacheSize, String[] cities) {
        int answer = 0;
        Cache cache = new Cache(cacheSize);

        for(String page: cities){
            answer += cache.getExecuteTime(page);
        }

        return answer;
    }

    class Cache{
        private final int cacheSize;
        LinkedList<String> pages = new LinkedList<>();

        Cache(int cacheSize){
            this.cacheSize = cacheSize;
        }

        private int getExecuteTime(String input){
            final int CACHE_HIT_TIME = 1;
            final int CACHE_MISS_TIME = 5;

            if(findPage(input.toLowerCase())) {
                return CACHE_HIT_TIME;
            }
            return CACHE_MISS_TIME;
        }

        private boolean findPage(String input){
            if(cacheSize == 0){
                return false;
            }
            int index = pages.indexOf(input);
            if(index == -1) {
                if(pages.size() == cacheSize){
                    pages.remove(0);
                }
                pages.add(input);
                return false;
            }
            pages.remove(index);
            pages.add(input);
            return true;
        }
    }
}
```

<br/><br/>

# 개인 발표

## 발표 자료

<br/>

## 출처

<br/>

## 참고 포스트

<br/>



# 스터디 내용 정리



