# 📚 Growth Study: 22.01.15.토

##  :scroll: 목차

- 코딩 테스트
  - 프로그래머스 - 오픈채팅방 (Lv.2)
- 개인 발표
  - Hash Map
  - ...





## 🎯 코딩 테스트

### 프로그래머스: 오픈채팅방 (Lv.2) [[링크]](https://programmers.co.kr/learn/courses/30/lessons/42576)

#### 나의 풀이

```java
import java.util.*;

class Solution {

    private HashMap<String, String> nameOfUid = new HashMap<>();
    private ArrayList<MsgLog> msgLogs = new ArrayList<>();

    public String[] solution(String[] record) {


        for (String message : record) {
            String[] arr = message.split(" ");
            switch (arr[0].charAt(0)) {
                case 'E':
                    msgLogs.add(new MsgLog(true, arr[1]));
                    nameOfUid.put(arr[1], arr[2]);
                    break;
                case 'L':
                    msgLogs.add(new MsgLog(false, arr[1]));
                    break;
                default:
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





## 📝 개인 발표

### <u>Hash Map</u>

#### Map Collection

Map 컬렉션은 키(key)와 값(Value)로 구성된 `Entry<K, V>` 객체를 저장하는 구조이다.

키는 중복 저장을 허용하고 값은 중복 저장을 허용하지 않는다. 따라서 기존에 저장된 키와 동일한 키로 새로운 값을 저장하면 기존 값은 없어지고 새로운 값으로 대체된다.

![image-20220114162910776](C:\Code\koowin.github.io\assets\images\image-20220114162910776.png)

#### Map Methods

Map.java에 구현된 Map 인터페이스의 주요 메소드와 설명이다.

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| int <span style="color:orange">size</span>();                | 저장된 모든 키의 수를 리턴                                   |
| boolean <span style="color:orange">isEmpty</span>();         | Map이 비어있는지 여부를 리턴                                 |
| boolean <span style="color:orange">containsKey</span>(Object key); | 주어진 키가 있는지 여부를 리턴                               |
| boolean <span style="color:orange">containsValue</span>(Object value); | 주어진 값이 있는지 여부를 리턴                               |
| V <span style="color:orange">get</span>(Object key);         | 주어진 키의 값을 리턴                                        |
| V <span style="color:orange">put</span>(K key, V value);     | 주어진 키와 값 쌍을 저장. 동일한 키의 이전 값을 리턴(없다면 null) |
| V <span style="color:orange">remove</span>(Object key);      | 주어진 키의 값을 삭제하고 해당 값을 리턴                     |
| Set<K> <span style="color:orange">keySet</span>();           | 모든 키를 Set 객체에 담아 리턴                               |
| Collection<V> <span style="color:orange">values</span>();    | 모든 값을 Collection 객체에 담아 리턴                        |
| Set<Map.Entry<K, V>> <span style="color:orange">entrySet</span>(); | 모든 키와 값 쌍을 Set 객체에 담아 리턴                       |



#### Hash Map



#### Hash Map 관련 코테 문제들

- 프로그래머스: 완주하지 못한 선수 (Lv.1) [[링크]](https://programmers.co.kr/learn/courses/30/lessons/42576)
- 프로그래머스: 오픈채팅방 (Lv.2) [[링크]](https://programmers.co.kr/learn/courses/30/lessons/42888)

✏추가 예정

