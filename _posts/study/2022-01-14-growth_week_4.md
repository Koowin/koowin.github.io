---
title:  "Growth Study: 22.01.15.토"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - study

date: 2022-01-14
last_modified_at: 2022-01-14
---

# 🎯 공통 문제

## 프로그래머스: 오픈채팅방 (Lv.2) [[링크]](https://programmers.co.kr/learn/courses/30/lessons/42888)

### 나의 풀이

```java
import java.util.*;

class Solution {

    private HashMap<String, String> nameOfUid = new HashMap<>();
    private ArrayList<MsgLog> msgLogs = new ArrayList<>();

    public String[] solution(String[] record) {
        for (String message : record) {
            String[] arr = message.split(" ");
            switch (arr[0].charAt(0)) {
                case 'E':	//"Enter"
                    msgLogs.add(new MsgLog(true, arr[1]));
                    nameOfUid.put(arr[1], arr[2]);
                    break;
                case 'L':	//"Leave"
                    msgLogs.add(new MsgLog(false, arr[1]));
                    break;
                default:	//"Change"
                    nameOfUid.put(arr[1], arr[2]);
                    break;
            }
        }
        int size = msgLogs.size();
        String[] answer = new String[size];

        for (int i = 0; i < size; i++) {
            answer[i] = msgLogs.get(i).toString();
        }

        return answer;
    }

    class MsgLog {
        private final boolean isEnter;
        private final String uid;

        MsgLog(boolean isEnter, String uid) {
            this.isEnter = isEnter;
            this.uid = uid;
        }

        public String toString() {
            String returnVal = nameOfUid.get(this.uid) + "님이 ";
            final String[] actions = {"들어왔습니다.", "나갔습니다."};

            if (this.isEnter) {
                return returnVal + actions[0];
            } else {
                return returnVal + actions[1];
            }
        }
    }
}
```

<br/><br/>

# 📝 개인 발표

[Java - HashMap](https://koowin.github.io/categories/java)

포스트를 옮겼습니다. 위 링크를 참조해주세요.

<br/><br/>

# 스터디 내용 정리

 이번 주는 예정했던 시간보다 1시간 더 긴 3시간 동안 스터디를 진행하였습니다. 예정대로 각자 풀이를 가져와서 피드백하는 시간을 가졌고 이후 개인 발표 시간을 가졌습니다. 개인 발표 내용은 다음과 같았습니다.

1. Java - HashMap
2. Algorithm - Union-Find
3. Architecture - MVC Model
4. OS - Intro, History
5. Design Pattern - Observer

 저는 대부분 처음 접하는 내용들이라 아주 흥미롭게 들었습니다. 다음 주에는 [[1차] 캐시](https://programmers.co.kr/learn/courses/30/lessons/17680)를 공통문제로 풀어오기로 하였습니다. 또한, 발표 내용이 겹치지 않도록 수요일까지 개인발표 주제를 픽스하여 알려주기로 하였습니다. 다음 주에는 체스 게임 구현 혹은 카카오 2차 코딩테스트 문제 중 하나를 선정하여 문제 소개 및 과제 일정에 대해 이야기하기로 하였습니다.
