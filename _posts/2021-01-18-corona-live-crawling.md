---
title: 코로나 라이브 사이트 크롤링 후기
tags:
- Python
- Crawling
- Axios
- Cheerio
- Github
- 코로나라이브
- 코로나
category:
- Crawling
---

## 코로나라이브 크롤링
![코로나라이브](/assets/images/2.png)

React Native 개발 중 [코로나라이브](http://corona-live.com) 확진자 정보를 가져오려고 알아보다가

개발 후기 같은 것도 있을 법하다 생각했으나 [인터뷰](http://https://blog.naver.com/mofakr/222180244510?proxyReferer=&proxyReferer=https%3A%2F%2Fwww.google.com%2F)만 있고 그런 건 아무리 찾아봐도 없었다.

Axios, Cheerio 등을 사용하여 크롤링을 시도해보았으나

동적 웹이라 모든 항목을 바로 불러올 수 없는 경우라 동적 크롤링이 필요했다.

Selenium으로 하면 되긴 하는데 개발 언어가 React Native라 사용이 불가했다.

### corona-live-client

혹시 Github에 뭔가 있지 않을까 싶어 검색해 봤더니

[corona-live-client 레포지터리](https://github.com/DevChinchilla/corona-live-client)가 있길래 샅샅이 뒤져봤다.

TypeScript 기반으로 제작된 걸 일단 알아냈는데

중요한 핵심 데이터들은 [관리자 사이트(API)](https://apiv2.corona-live.com/) 에서 따로 가져오는 구조라 사용하기는 커녕 직접 볼 수도 없었다.

### CovidApp

관련 레퍼지터리를 찾고자 github을 더 뒤져보다가 흥미로운 걸 발견했다.

[corona-live API 접근을 성공한 어플(CovidApp)](https://github.com/ZzangWoo/CovidApp)이 막바지 개발 단계였다. 

Open API도 아니던데 어떻게 가져온 것일까...


## 결론
코로나라이브 개발진에게 문의를 넣음.

![문의](/assets/images/1.png)

API를 가져올 수 없으면 코로나라이브 개발진처럼 직접 실시간으로 확진자 정보를 수집해야 하는데,

인터뷰를 참고하여 방법 정도만 우선 생각해 보았다. 개발은 조만간..

## 실시간 코로나 확진자 수 집계 방법

먼저 [국민재난안전포털](https://www.safekorea.go.kr/idsiSFK/neo/sfk/cs/sfc/dis/disasterMsgList.jsp?menuSeq=679) 혹은
[네이버 실시간 확진자 추가 안내 서비스](https://m.news.naver.com/covid19/live.nhn)
에서 재난문자를 크롤링한다. (동적 크롤링 필요x)

크롤링한 각각의 재난문자를 실시간 확진자 수에 반영을 할 것인지를 판단해야 한다.
###### 제외할 경우
* 코로나 정보가 아닌 경우 (재난 경보 등) 
* 코로나 정보이지만 확진자의 정보가 아닌 경우 (특정 장소 방문자 검사 요청 등) 
* 코로나 정보이고 확진자의 정보이지만 집계하지 않는 경우(다른날에 집계가 이미 된 경우, 전날 확진자의 번호가 나올 경우,기존에 있던 확진자의 접촉자 정보일 경우 등)

###### 반영할 경우
* 확진자 번호만 언급하는 경우 (n번 확진자 발생)
* 몇명인지 언급하는 경우(n명 발생)

다소 복잡하겠지만 문자열 처리를 통해 대부분 걸러낼 수 있을 듯하다.

## References
* https://github.com/ZzangWoo/CovidApp
* https://apiv2.corona-live.com/
* https://github.com/DevChinchilla/corona-live-client
* https://blog.naver.com/mofakr/222180244510?proxyReferer=&proxyReferer=https%3A%2F%2Fwww.google.com%2F
* http://corona-live.com
