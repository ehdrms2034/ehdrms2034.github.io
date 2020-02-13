---
layout: post
title: "[서버 개발 캠프 4기] 첫번째 과제 ShortUrl Service, 단축 URL 제공 서비스"
img: 202001/20200112shorturl.png # Add image post (optional)
date: 2020-01-12 23:12:00 +0900
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
tag: [Smilegate,서버개발캠프]
---
## [서버개발캠프4기] 첫번째 과제 ShortUrl Service ,단축 URL 제공 서비스
서버 개발 캠프를 진행한지 일주일이 지났다.
서버 개발 캠프는 총 두 달동안 진행이 되는데, 그 동안 **팀 프로젝트 1개**와 **개인 프로젝트 2개** 를 진행하게 될 것이다.

첫 번째 개인 프로젝트 과제는 Short URL Service 이다.
완성 코드는 깃허브 링크에 올려 놨으니 참고 바란다.
[GitHub - ehdrms2034/ShortUrlService-with-Node](https://github.com/ehdrms2034/ShortUrlService-with-Node)

<img src="https://raw.githubusercontent.com/ehdrms2034/ehdrms2034.github.io/master/assets/img/202001/20200112shorturl.png" width="600px"/><br/>
샘플코드 레이아웃

### 프로젝트 소개
첫번째 개인과제는 ShortUrl Service이다. 긴 URL 주소를 짧은 URL 주소로 변경해주는 서비스이다. 생소한 사람들을 위해서 bit.ly 사이트나 goo.gl 이라는 단축 URL 서비스를 예를 들면 생각하기 편할 것 같다.

다만 서버는 local에서 제작되고 테스트 되기 때문에, 아마 ‘localhost/단축URL주소’ 가 되지 않을 까 싶다.

즉 요약하자면
https://길다란주소주소주소/길다란주소주소주소를 <br/>
http://localhost/짧은주소 로 변경해주는 서비스를 제공하는 서버를 제작한다는 것!



### 개인 과제를 처음 들었을 때 들었던 생각
처음 개인과제를 들었을 때, 노드 서버에서 hash map 구조를 이용해서 단축 URL 서비스를 제공하면 되지 않을 까 했다.

일단 hash map를 생각했던 까닭은 *2가지 이유*가 있다.

1. **구조가 적합하다**<br/>
Hash map 구조는 일단 (key, value) 의 자료형태를 가지고 있다.
그렇다면 (key, value) -> (짧은URL, 긴 URL) 과 같은 형태로 제공한다면 적합한 구조가 될 수 있을 것이라 생각했다.

2. **속도가 빠르다**<br/>
이론상, 해쉬 구조의 속도는 d(d는 해쉬 테이블의 개수)에 수렴해서, 모든 Search 알고리즘 중에서 가장 빠른 속도를 자랑하고 있다.

자료양이 많아지면, 짧은 URL을 통해서 긴 URL을 찾아야하는 속도가 줄어들기 마련일텐데, 해쉬구조를 이용하면 최적화된 속도를 유저에게 제공할 수 있을 것이라 생각했다.

### 그러나 조건이 있었다.
```
1. DB를 이용할 것
2. 8자리 이내의 짧은 URL을 제공할 것
3. 같은 긴 URL은 하나의 짧은 URL로 대응 될 것.
```

그럼 검색같은 경우는 DB가 다 알아서 해줄꺼잖아?
그럼 다음 문제는 짧은 URL을 어떻게 만들 것인가?

P.S) 사실 DB에 저장한다는 조건이 없었다면 hash map 구조로 그대로 만들었을 것이다.

### 답은 Random String
사실 유일성문제를 판단하는 경우 Hash 알고리즘이 적합하지 않을까 생각해봤는데, 대다수가 8자리보다 길게 나오는 경우가 발생했다.
그럼 그런 경우라면 그냥 Random String으로 돌려버리고 거기에 대한 중복체크만 제대로한다면 서비스를 제공하는데 있어 최적의 구조가 아닐까라고 생각을 했다.

만들고 나서 찾아본건데 Base64등 다른 알고리즘이 많았다 (뭐가 맞는지는 잘 모르겠다)

### DB는 MongoDB로!
데이터의 작은 입력과 읽음이 많을 것이라 생각했고 RDBMS보다는 MongoDB가 사용목적에 더 부합하다고 생각했다. 실제로도 우수한 성능을 보여주지 않을까 싶다.

Node와 연동하는데에는 Mongoose를 이용해서 연동했다.
항상 구조는 MVC 패턴으로다가 제작했다!. (궁금하면 샘플 코드 참조)

<img src="https://raw.githubusercontent.com/ehdrms2034/ehdrms2034.github.io/master/assets/img/202001/20200112mongo.png" width="600px"/><br/>
몽고 DB에 저장된 데이터 구조 예시

## 총평 : 워밍업 정도의 과제, 간단하지만 재밌었다.
첫주차 개인 프로젝트의 난이도는 어렵지 않게 풀 수 있었다. 
찾아보니 서버개발캠프3기를 뽑을 때 냈던 문제라고 본 것 같다.
2주차때는 Redis 서버를 이용한 Auth 서버 제작이라고 하는데, 더 재밌을 것 같은 느낌적 느낌이다.

End..