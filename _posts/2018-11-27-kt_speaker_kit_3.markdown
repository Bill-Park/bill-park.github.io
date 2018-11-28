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

### 예제 1번 기가지니 부르기

예제 1번은 **기가지니**를 호출하는 예제입니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/5.png)

~~~
$cd ~/ai-makers-kit/python
$python3 ex1_kwstest.py
~~~

python 예제가 있는 폴더로 이동하여 예제1번 **ex1_kwstest.py**를 실행시켜 줍니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/6.png)

**기가지니**라고 부르면 효과음을 내며 **detect rc = 200**과 함께 종료됩니다.

### 예제 2번 STT 기능 사용하기

Sound To Text(STT)를 사용하는 예제입니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/7.png)

텍스트에디터를 이용하여 **CLIENT_ID, KEY, SECRET** 값을 넣어줍니다.

이 값은 2번째 시간에 받은 **clientKey.json**파일 안에 있습니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/8.png)

~~~
$python3 ex2_getVoice2Text.py
~~~

예제 2번을 실행시켜 줍니다.

실행하면 ALSA 라이브러리가 실행되며 장치를 찾습니다.

에러가 아니므로 안심하셔도 됩니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/9.png)

말한 단어가 나오며 종료됩니다.

처음에 왜 말하기가 나가기로 인식되었는지 모르겠네요.

아무튼 잘 인식되는걸 볼 수 있습니다.

### 예제 3번 Text - Voice 변환 Url 가져오기

입력한 텍스트를 소리로 들을 수 있는 Url을 반환하는 예제입니다.

바로 4번으로 넘어가도 되지만 다른곳에 사용할 수 있으니 해보도록 하겠습니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/10.png)

2번 예제와 마찬가지로 **CLIENT_ID, KEY, SECRET**를 넣어줍니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/11.png)

~~~
$python3 ex3_getText2VoiceUrl.py
~~~

예제를 실행하면 Url이 하나 나옵니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/12.png)

이를 인터넷 브라우저를 열어 붙여넣어줍니다.

소리 파일이 실행되며 기본으로 설정되어있던 **안녕하세요. 반갑습니다.**가 재생됩니다.

### 예제 4번 Text - Voice 파일로 저장하기

예제 3번의 업그레이드 버전입니다.

입력된 텍스트를 소리 파일로 변환하는 예제입니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/13.png)

어김없이 **CLIENT_ID, KEY, SECRET**를 넣어줍니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/14.png)

밑으로 내려 **안녕하세요. 반갑습니다.**라고 되어있던 부분을 다른 텍스트로 바꿔주었습니다.

한글 입력의 경우 우측 상단의 키보드 모양을 누르면 태극문양으로 바뀌며 한글 입력이 가능합니다.

저는 **텍스트를 소리로.**를 넣고 저장해 주었습니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/15.png)

~~~
$python3 ex4_getText2VoiceStream.py
~~~

예제 4번을 실행시켜 줍니다.

200 코드와 함께 Audio Stream이 나왔다면 성공한 것입니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/16.png)

파일 목록중 **testtts.wav**라는 파일이 생성된 것을 확인할 수 있습니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/17.png)

~~~
$aplay testtts.wav
~~~

**aplay** 명령어를 이용하여 소리 파일을 실행시켜 줍니다.

입력했던 텍스트가 소리로 바뀌어 재생되는 것을 들을 수 있습니다.

### 예제 5번 텍스트로 query문 보내기

AI 스피커라면 전부 가지고 있는 query문(질문하기)이 나왔습니다.

텍스트로 질문을 보내면 텍스트로 답하는 예제입니다.

**CLIENT_ID, KEY, SECRET**를 넣는 과정은 생략하도록 하겠습니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/18.png)

~~~
$python3 ex5_queryText.py
~~~

예제 5번을 실행시키면 기본 query문인 **안녕**이 실행됩니다.

응답으로는 **안녕하세요~~~**가 온 것을 볼 수 있습니다.

### 예제 6번 소리로 query문 보내기

6번은 소리를 통해 query문을 보내는 예제입니다.

먼저 **CLIENT_ID, KEY, SECRET**를 넣어줍니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/19.png)

~~~
$python3 ex6_queryVoice.py
~~~

예제 6번을 실행시켜줍니다.

![]({{ site.img_url }}/kt_voice_kit/3_example/20.png)

입력한 소리에 따라 **\***가 나오게 됩니다.

**몇시야**라는 질문을 해봤습니다. 대답이 잘 나오는걸 볼 수 있습니다.

이상으로 python으로 예제 실행하기 편을 마치도록 하겠습니다.

감사합니다.
