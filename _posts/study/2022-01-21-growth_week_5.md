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

# 🧩공통 문제

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

# 🎙️개인 발표

<details>
<summary><span style="color:LightSkyBlue">동기 접기/펼치기</span></summary>

 언제부터 시작할지 구체적으로 정해지지는 않았지만 스터디의 최종 목적대로 곧 스프링 프레임워크로 프로젝트를 곧 시작하지 않을까 생각합니다. 아무것도 모른채 스프링부터 시작해도 나름 얻어가는 것도 있고 재미있겠지만, 네트워크에 대한 기본 이해가 있는 상태에서 프로젝트를 진행하면 더 많은 것을 배우고 큰 흥미를 가질 수 있을 것이라 생각합니다. 이러한 이유로 이번에는 네트워크 중 우리가 직접 다뤄야할 웹에 대해 설명하고, 다음 시간에는 Web Server, WAS의 차이점이 무엇인지, Spring 프레임워크의 구조는 어떻게 되어있는지 간략하게 공부하여 발표할 예정입니다.

</details>

## 발표 자료

<br/>

## 출처

📘James F. Kurose, Keith W.Ross, 『컴퓨터 네트워킹 하향식 접근』

<br/>

## 참고 포스트

- [Network Layer](https://koowin.github.io/network/network_layer/)
- [네트워크 애플리케이션의 원리](https://koowin.github.io/network/application_layer_principle/)
- 

<br/>



# 스터디 내용 정리



