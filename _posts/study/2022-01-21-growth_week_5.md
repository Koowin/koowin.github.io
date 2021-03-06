---
title:  "Growth Study: 22.01.22.ํ "

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - study

date: 2022-01-21
last_modified_at: 2022-01-21
---

# ๐งฉ๊ณตํต ๋ฌธ์ 

## ํ๋ก๊ทธ๋๋จธ์ค: [1์ฐจ] ์บ์

๋ฌธ์  ๋งํฌ: [[1์ฐจ] ์บ์](https://programmers.co.kr/learn/courses/30/lessons/17680)

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

# ๐๏ธ๊ฐ์ธ ๋ฐํ

<details>
<summary><span style="color:LightSkyBlue">๋๊ธฐ ์ ๊ธฐ/ํผ์น๊ธฐ</span></summary>

 ์ธ์ ๋ถํฐ ์์ํ ์ง ๊ตฌ์ฒด์ ์ผ๋ก ์ ํด์ง์ง๋ ์์์ง๋ง ์คํฐ๋์ ์ต์ข ๋ชฉ์ ๋๋ก ๊ณง ์คํ๋ง ํ๋ ์์ํฌ๋ก ํ๋ก์ ํธ๋ฅผ ๊ณง ์์ํ์ง ์์๊น ์๊ฐํฉ๋๋ค. ์๋ฌด๊ฒ๋ ๋ชจ๋ฅธ์ฑ ์คํ๋ง๋ถํฐ ์์ํด๋ ๋๋ฆ ์ป์ด๊ฐ๋ ๊ฒ๋ ์๊ณ  ์ฌ๋ฏธ์๊ฒ ์ง๋ง, ๋คํธ์ํฌ์ ๋ํ ๊ธฐ๋ณธ ์ดํด๊ฐ ์๋ ์ํ์์ ํ๋ก์ ํธ๋ฅผ ์งํํ๋ฉด ๋ ๋ง์ ๊ฒ์ ๋ฐฐ์ฐ๊ณ  ํฐ ํฅ๋ฏธ๋ฅผ ๊ฐ์ง ์ ์์ ๊ฒ์ด๋ผ ์๊ฐํฉ๋๋ค. ์ด๋ฌํ ์ด์ ๋ก ์ด๋ฒ์๋ ๋คํธ์ํฌ ์ค ์ฐ๋ฆฌ๊ฐ ์ง์  ๋ค๋ค์ผํ  ์น์ ๋ํด ์ค๋ชํ๊ณ , ๋ค์ ์๊ฐ์๋ Web Server, WAS์ ์ฐจ์ด์ ์ด ๋ฌด์์ธ์ง, Spring ํ๋ ์์ํฌ์ ๊ตฌ์กฐ๋ ์ด๋ป๊ฒ ๋์ด์๋์ง ๊ณต๋ถํ์ฌ ๊ฐ๋ตํ๊ฒ ๋ฐํํ  ์์ ์๋๋ค.

</details>

## ๋ฐํ ์๋ฃ

### <span style="color:#ffd101">๋คํธ์ํฌ ๊ณ์ธต</span>

<img src="../../assets/images/2022-01-21-growth_week_5/image-20220121164653721.png" alt="image-20220121164653721"  />

์ด๋ฏธ์ง ์ถ์ฒ: James F. Kurose, Keith W.Ross, ใ์ปดํจํฐ ๋คํธ์ํน ํํฅ์ ์ ๊ทผใ, 45p

<br/>

### <span style="color:#ffd101">HTTP</span>

#### TCP

- ์์ผ์ ํตํด ํต์ 
- 3-way-handshaking

#### Connectionless, Stateless

- ์ฐ๊ฒฐ ํ๋ฆฝ -> ์์ฒญ, ์๋ต -> ์ฐ๊ฒฐ ์ข๋ฃ
- ์ฐ๊ฒฐ์ด ๋์ด์ง๋ฉด ์ด์  ์ํ๋ฅผ ์ ์ฅํ์ง ์์.
- ์๋ฒ๊ฐ ํด๋ผ์ด์ธํธ์ ์ํ๋ฅผ ์ ์ฅํ  ๋ฐฉ๋ฒ ํ์.

<br/>

### <span style="color:#ffd101">์ฟ ํค vs ์ธ์</span>

#### ์ฟ ํค

- Connectionless, Stateless๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด ์กด์ฌ
- ํด๋ผ์ด์ธํธ ๋ก์ปฌ์ ์ ์ฅ๋๋ `key, value`
- HTTP ์๋ต์์ Set-Cookie ํค๋๋ฅผ ํตํด ์์ฑ
- HTTP ์์ฒญ ์ ํค๋์ ์ฟ ํค ๋ด์ ๋ณด๋

#### ์ธ์ ์ฟ ํค, ์ง์ ์ฟ ํค

- ์ธ์ ์ฟ ํค
  - ๋ฉ๋ชจ๋ฆฌ์ ์๋ ๋์ ์ ํจ (๋ธ๋ผ์ฐ์  ๋ฉ๋ชจ๋ฆฌ)
  - ๋ง๋ฃ ๋ ์ง/์๊ฐ ์์
- ์ง์ ์ฟ ํค
  - ํ์ผ๋ก ์ ์ฅ
  - ๋ง๋ฃ ๋ ์ง/์๊ฐ ์์

#### ์ธ์

- Connectionless, Stateless๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด ์กด์ฌ
- ์๋ฒ์์ ์ ์ฅํ๋ ํด๋ผ์ด์ธํธ ID
- ํ์์ ๋ฐ๋ผ ํด๋ผ์ด์ธํธ์๊ฒ ์ธ์ ID ์ ๊ณต (ํด๋ผ์ด์ธํธ๋ ์ด๋ฅผ ์ฟ ํค๋ก ์ ์ฅ)

#### ์ฐจ์ด์ 

- ์ ์ฅ ์์น
- ๋ณด์

<br/>

### <span style="color:#ffd101">ํ๋ก์, ์น ์บ์ฑ</span>

![image-20220122103117496](../../assets/images/2022-01-21-growth_week_5/image-20220122103117496.png)

![image-20220122115238527](../../assets/images/2022-01-21-growth_week_5/image-20220122115238527.png)

์ด๋ฏธ์ง ์ถ์ฒ: James F. Kurose, Keith W.Ross, ใ์ปดํจํฐ ๋คํธ์ํน ํํฅ์ ์ ๊ทผใ, 101~103p

<br/>

## ์ฐธ๊ณ ํ ๋ฌธ์๋ค

- ๐James F. Kurose, Keith W.Ross, ใ์ปดํจํฐ ๋คํธ์ํน ํํฅ์ ์ ๊ทผใ
- ๐[https://jeong-pro.tistory.com/80](https://jeong-pro.tistory.com/80)

<br/>

## ์ฐธ๊ณ  ํฌ์คํธ

- [Network Layer](https://koowin.github.io/network/network_layer/)
- [๋คํธ์ํฌ ์ ํ๋ฆฌ์ผ์ด์์ ์๋ฆฌ](https://koowin.github.io/network/application_layer_principle/)
- [์น, HTTP](https://koowin.github.io/network/application_layer_http/)

<br/>



# ์คํฐ๋ ๋ด์ฉ ์ ๋ฆฌ

- Rest API
- OS Scheduling
- Java String (String pool, ๋ถ๋ณ)
- HTTP ๋ฒ์ 
- ํฌ์๋ย ํ๋ก์, ๋ฆฌ๋ฒ์ค ํ๋ก์

