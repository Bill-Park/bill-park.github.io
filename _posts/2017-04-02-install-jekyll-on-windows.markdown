---
layout: post
title:  "윈도우에서 지킬 설치하기"
category: coding
---

## Install Jekyll on Windows 10

지킬은 유닉스(Unix), 리눅스(Linux), 맥(OS X)을 지원한다고 나와 있습니다.

윈도우는 빠져있죠. 그래서 윈도우에 지킬을 설치해 보도록 하겠습니다.

설치는 Ruby 그리고 Ruby DevKit으로 충분합니다.

### 1. Ruby 설치

[Ruby Downloads 바로가기](https://rubyinstaller.org/downloads/)

![]({{ site.img_url }}/window_jekyll_install/1.png)

exe 파일로 간단하게 설치할 수 있습니다.

중간에 'PATH에 추가하시겠습니까?' 부분은 반드시 체크해 주시기 바랍니다.

![]({{ site.img_url }}/window_jekyll_install/2.png)

### 2. Ruby DevKit 설치

다운로드 사이트에서 아래쪽으로 내려보면 **DEVELOPMENT KIT** 이라고 적힌 부분이 있습니다.

거기서 버전에 맞는 DevKit을 다운로드 받습니다.

저는 2.3.3 64bit는 표시된 파일을 받으면 됩니다.

![]({{ site.img_url }}/window_jekyll_install/3.png)

실행하면 어디에 압축을 풀지 물어봅니다.

~~~
C:\devkit
~~~

에 풀도록 하겠습니다.

![]({{ site.img_url }}/window_jekyll_install/4.png)

### 3. Jekyll 및 부가기능 설치하기

Ruby는 GEM이라는 패키지 매니저를 가지고 있습니다.

Python의 pip, node js의 npm과 비슷한 도구입니다.

이를 사용하기 위해서 명령 프롬프트(cmd)를 실행해 줍니다.

CMD는 **윈도우키 + R**을 눌러 **실행**을 연 다음 cmd를 입력하고 확인을 누릅니다.

처음 실행할 경우 경로가 
~~~
C:\Users\Admin
~~~
일 것입니다.

위에서 설치한 devkit이 있는 폴더로 이동해 줍니다.

~~~
cd C:\devkit
여기서 ＼(역슬래시)와 ￦ 기호는 같은 의미입니다.
~~~

Ruby DevKit 설치를 먼저 마무리해줍니다.

~~~
ruby dk.rb init
ruby dk.rb install
~~~

![]({{ site.img_url }}/window_jekyll_install/5.png)

위처럼 뜨면 완료된 것입니다.

이제 지킬(Jekyll)을 설치해 보도록 하겠습니다.

지킬을 설치할 폴더로 이동합니다.

~~~
cd c:\             # C 드라이브로 이동합니다.
mkdir jekyll_test  # jekyll_test라는 폴더를 만듭니다.
cd jekyll_test     # jekyll_test 폴더로 이동합니다.
gem install jekyll # gem을 이용하여 jekyll을 설치합니다.
~~~

gem install jekyll을 입력하면 무언가 쭉 뜨면서 설치가 진행됩니다.

설치가 완료되었다면 새로운 사이트를 생성해 보도록 하겠습니다.

~~~
jekyll new .
~~~

마지막의 **.**을 꼭 붙여주시기 바랍니다.

.은 현재 폴더의 경로를 의미합니다.

만약 다른곳에 사이트를 만들고 싶다면 원하는 곳의 경로를 넣어주면 됩니다.

명령어를 실행했을 때 아래와 같은 에러가 나올 수 있습니다.

![]({{ site.img_url }}/window_jekyll_install/6.png)

minima 라는 gem(이때의 gem은 소스코드와 관련 문서를 의미합니다.)이 없다는 의미입니다.

(minima 외의 다른 gem이 없다고 나올수도 있습니다.)

minima와 필요한 gem들을 설치해 줍니다.

~~~
gem install minima
gem install bundler
gem install jekyll-feed
gem install tzinfo-data
~~~

그리고 다시 사이트를 생성합니다.

~~~
jekyll new .
~~~

생성이 완료되었다면 관련 내용을 확인해 줍니다.

~~~
jekyll serve
~~~

명령어는 개발용 서버를 실행하여 git page에 발행(publish)하기 전에 테스트를 할 수 있습니다.

웹브라우저를 하나 실행하여 주소창에

~~~
127.0.0.1:4000
~~~

을 입력하면 생성된 사이트를 볼 수 있습니다.

![]({{ site.img_url }}/window_jekyll_install/7.png)

다들 행복한 블로깅 되시기 바랍니다.