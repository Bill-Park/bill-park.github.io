---
layout: post
title:  "RPI로 KT gigagenie AI 스피커 키트 만들기 - 3편"
categories: [rpi, making, coding]
---

RPI로 KT Gigagenie AI 스피커 키트 만들기 - 3편

저번 시간에는 예제 구동을 위해 회원가입과 키 값 가져오기를 해봤습니다.

이번 시간에는 기본 예제들을 구동해 보도록 하겠습니다.

KT Ai Gigaginie 키트는 Node js와 python 2가지로 예제가 제공됩니다.

먼저 Python을 사용해 보도록 하겠습니다.

### python 예제 사용 준비하기

![]({{ site.img_url }}/kt_voice_kit/3_example/1.png)

~~~
$sudo apt-get install libasound-dev
$sudo apt-get install libportaudio0 libportaudio2 libportaudiocpp0 portaudiol9-dev
~~~

사운드 관련 라이브러리를 설치해 줍니다.

마지막의 portaudiol9-dev의 l은 **알파벳 L** 입니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/2.png)

~~~
$sudo apt-get install python3-pyaudio
~~~

Python으로 audio를 사용하기 위한 라이브러리입니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/3.png)

~~~
$sudo pip3 install grpcio grpcio-tools
~~~

gprc를 사용하기 위해 pip3를 이용하여 설치해 줍니다.

pip만 사용하면 python2버전으로 설치되니 주의해 주시기 바랍니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/4.png)

~~~
$sudo python3 -m easy_install ktkws-1.0.1-py3.5-linux-armv7l.egg
~~~

easy_install을 이용하여 ktkws를 설치해 줍니다.

이상으로 python3로 예제 구동을 하기 위한 준비가 끝났습니다.

### python으로 예제 구동하기

현재 버그가 있어 수정 후 추가하도록 하겠습니다.

감사합니다.
