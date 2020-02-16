---
layout: post
title: "[성능테스트 툴] Apache Jmeter 설치부터 간단한 사용까지..!!"
img: default.png # Add image post (optional)
date: 2020-02-12 21:09:00 +0900
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
tag: [Jmeter,성능테스트,서버]
---
오늘은 성능테스트 도구로 많이 쓰이고 있는 Apache Jmeter의 간단한 사용법을 알려드리도록 하겠습니다.

###  Apache Jmeter란…
![](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTYJkbicw3sb1sfnbxYUXb3EJKZiWNtVvnncWrruaZySt4awi07)
<br/>
서버가 제공하는 서비스에 대한 성능을 측정하고 사용자에게 보여주는 테스트 도구라고 할 수 있습니다.

간단하게 말하자면… 
**서버에 요청을 많이 때려서 서버가 얼마나 버틸 수 있는지 볼 수 있는 도구다라고 보시면 될 것 같습니다 ㅎㅎ**

### 설치법
제가 맥을 사용하기 때문에 Mac First로 적겠습니다.
Mac은 HomeBrew라는 편리한 패키지 매니저가 있기 때문에 HomeBrew를 이용하겠습니다.

```bash
brew install jmeter
Or
brew install jmeter —-with-plugins
```
사실 저같은 경우는,, 아래가 설치가 안되서 위를 설치했는데, 
저 같은 중생(?)을 위해서 TPS를 보기위한 플러그인 설치하는 과정까지 보여드리도록 하겠습니다.

++ 윈도우 사용자 분들은
다운로드 URL : http://jmeter.apache.org/download_jmeter.cgi
여기서 설치하면 된다고 합니다^^

### 실행법
brew의 설치가 끝이 난다면 다음과 같은 명령어를 입력하시면 jmeter를 실행할 수 있습니다.
```bash
open /usr/local/bin/jmeter
```
그러면 Jmeter가 실행 될 겁니다

++윈도우 사용자 분들은 그냥 오픈하시면 될 듯..!

### 플러그인 설치

![](https://github.com/ehdrms2034/ehdrms2034.github.io/blob/master/assets/img/202002/2020-02-12-jmeter1.png?raw=true)
<br/>
실행을 하면 다음과 같은 화면을 볼 수 있을 것이다.


만약 저처럼 jmeter만 설치한 사람들을 위해서 플러그인을 설치하고 가겠다.
![](https://github.com/ehdrms2034/ehdrms2034.github.io/blob/master/assets/img/202002/2020-02-12-jmeter2.png?raw=true)
<br/>
Option -> Plugin Manager를 들어가면 위 스크린샷과 같은 화면을 볼 수 있는데
Available Plugins에 들어가서 우리가 설치할 플러그인은 다음과 같다.
1. 3Basic Graphs
2. Custom Thread Gropus

### 간단한 사용법
간단하게 알아볼 실험은 서버에 http요청에 부하를 줘 보겠다.
![](https://github.com/ehdrms2034/ehdrms2034.github.io/blob/master/assets/img/202002/2020-02-12-jmeter3.png?raw=true)
<br/>
Test Plan(우클릭) -> Add -> ThreadsGroup 을 눌러 추가시켜준다.

![](https://github.com/ehdrms2034/ehdrms2034.github.io/blob/master/assets/img/202002/2020-02-12-jmeter4.png?raw=true)
<br/>
다음은 ThreadGroup을 우클릭하여 다음 항목을 추가 시켜준다.
1. ThreadGroup(우클릭) -> Add -> Sampler -> Http Request을 눌러준다.
2. ThreadGroup(우클릭) -> Add -> Listener -> View Results Tree
3. ThreadGroup(우클릭) -> Add -> Listener -> Summary Report
4. ThreadGroup(우클릭) -> Add -> Listener -> Transaction Per Second
를 추가 시켜준다.

#### 전부 추가시켜줬다면 ThreadGroup을 눌러주자..!
![](https://github.com/ehdrms2034/ehdrms2034.github.io/blob/master/assets/img/202002/2020-02-12-jmeter5.png?raw=true)
다음과 같은 화면을 볼 수 있을 것이다
각 항목에 대해 설명을 하자면 
<br/>

**Number of Threads(users)**<br/>
가상의 생성자를 몇 명으로 설정할건지에 대한 값이다. (= 몇 개의 쓰레드를 생성할 것인지의 값이다)<br/>
이 값이 커질수록 당연히 서버는 많은 부하를 받을 것이다.<br/>

**Ramp-up Period(in seconds)**<br/>
한번의 실행을 몇초 동안 완료 시킬것인지에 대한 설정값<br/>
<br/>

**Loop Count**<br/>
반복하고자 하는 횟수, Infinite를 누르면 무제한 실행.<br/>
 
#### 다음은 Http Request를 눌러주자..!
![](https://github.com/ehdrms2034/ehdrms2034.github.io/blob/master/assets/img/202002/2020-02-12-jmeter6.png?raw=true)
<br/>
어떤 Url에 부하를 줄건지 설정한다.
자신의 서버값에 맞춰 설정하도록 하자..!!

#### start button을 누르면 다음과 같은 결과값들이 기록된다.

![](https://github.com/ehdrms2034/ehdrms2034.github.io/blob/master/assets/img/202002/2020-02-12-jmeter7.png?raw=true)
<br/>
Summary Report

![](https://github.com/ehdrms2034/ehdrms2034.github.io/blob/master/assets/img/202002/2020-02-12-jmeter8.png?raw=true)
<br/>
Transaction per second

50명의 동시 사용자에 대해 localhost:3000 url은 15000-20000의 tps를 처리할 수 있다는 결과값을 얻게 됐다.

### 총평 : 서버에 대한 성능을 가시적으로 볼 수 있는 도구!
위결과가 정확한 것은 아니다. 실제로는 한 url로만의 요청을 받아들이는것도 아니고 DB나 서버에 부하를 주는 복잡한 알고리즘을 사용하게 된다면 더 낮은 tps값을 기록시킬것이다.

실제값에 가까워지기 위해서는 위보다 더 자세한 시나리오를 설정해서 기록을 한다면, 실제 상용화 했을때 처리할 수 있는 tps에 정확하지 않을까 싶댜.
또한 이를 바탕으로 많은 부하를 견딜 수 있는 서버를 만들지 않을 까 싶다.

End.