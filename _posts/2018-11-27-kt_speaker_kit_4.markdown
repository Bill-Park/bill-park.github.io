---
layout: post
title:  "RPI로 KT gigagenie AI 스피커 키트 만들기 - 4편"
categories: [rpi, making, coding]
---

RPI로 KT Gigagenie AI 스피커 키트 만들기 - 4편

저번 시간에는 기본적으로 제공되는 예제들을 구동해 봤습니다.

이번 시간에는 기본 예제를 이용한 GPIO 출력 응용을 해보도록 하겠습니다.

### GPIO 출력하기 

![]({{ site.img_url }}/kt_voice_kit/4_gpio/1.png)

~~~
sudo pip3 install RPi.GPIO
~~~

python으로 GPIO를 제어하기 위해 RPi.GPIO를 설치합니다.

#### gpio_output_test.py

~~~
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BOARD)
GPIO.setup(31, GPIO.OUT)

while True :
    GPIO.output(31, GPIO.HIGH)
    time.sleep(0.5)
    GPIO.output(31, GPIO.LOW)
    time.sleep(0.5)
~~~

위 코드를 이용하여 GPIO의 OUTPUT이 작동하는지 확인합니다.

0.5초 간격으로 버튼의 LED가 깜빡입니다.

종료는 Ctrl+C를 눌러주면 됩니다.

예제 2번을 응용하여 LED 제어를 해 보도록 하겠습니다.

### 예제2번 응용하기

![]({{ site.img_url }}/kt_voice_kit/4_gpio/2.png)

~~~
$cd ~/ai-makers-kit/python
$cp ex2_getVoice2Text.py led_with_voice.py
~~~

python 예제폴더에서 ex2~ 파일을 led_with_voice.py로 복사합니다.

이제 led_with_voice.py 파일을 수정해 보겠습니다.

![]({{ site.img_url }}/kt_voice_kit/4_gpio/3.png)

~~~
CLIENT_ID = CLIENT ID값
CLIENT_KEY = CLIENT KEY값
CLIENT_SECRET = CLIENT SECRET값
~~~

19~21번 줄에 있는 ID, KEY, SECRET 값을 넣어줍니다.

이 값은 2번째 시간에 받은 **clientKey.json**파일 안에 있습니다.

![]({{ site.img_url }}/kt_voice_kit/4_gpio/4.png)

~~~
import RPi.GPIO as GPIO
import time
~~~

gpio와 time 관련 라이브러리를 import 해줍니다.

아직 time을 사용하진 않지만 나중을 위해서 해주었습니다.

![]({{ site.img_url }}/kt_voice_kit/4_gpio/5.png)

~~~
if resultText.find('켜줘') >= 0 :
    GPIO.output(31, GPIO.HIGH)
elif resultText.find('불꺼') >= 0 :
    GPIO.output(31, GPIO.LOW)
~~~

결과 텍스트에서 **켜줘** 혹은 **불꺼**가 있으면 LED를 조작합니다.

한글을 입력하기 위해 상단의 키보드모양을 누르면 태극문양으로 바뀌며 한글 입력이 가능합니다.

한번 더 누르면 다시 키보드모양으로 돌아옵니다.

![]({{ site.img_url }}/kt_voice_kit/4_gpio/6.png)

~~~
GPIO.setmode(GPIO.BOARD)
GPIO.setup(31, GPIO.OUT)
~~~

GPIO의 모드와 31번 핀을 출력으로 설정해 줍니다.

main 함수 안에서 해주었습니다.

![]({{ site.img_url }}/kt_voice_kit/4_gpio/7.png)

~~~
$python3 led_with_voice.py
~~~

수정한 파일을 python3를 이용해 실행합니다.

![]({{ site.img_url }}/kt_voice_kit/4_gpio/8.png)

입력받은 텍스트가 나오며 **켜줘**라고 말하면 LED가 켜지게 됩니다.

![]({{ site.img_url }}/kt_voice_kit/4_gpio/9.png)

위와 같이 텍스트가 나오며 **불꺼**가 입력되면 LED를 끕니다.

이상으로 4편 GPIO조작편을 마치도록 하겠습니다.

감사합니다.