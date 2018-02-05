---
layout: post
title:  "X9Cxxx 시리즈 사용하기(Digital Potentiometer)"
categories: [coding]
---

## X9C Series - Digital Potentiometer Tutorial

대부분의 아날로그 신호는 PWM이라는 기능을 이용하여 만들어 지고 있습니다.

하지만 PWM으로는 할 수 없는, **가짜 아날로그 신호**가 아닌 진짜 아날로그 신호가 필요할 때가 있습니다.

대표적인 예로 **교류**를 사용할 때나 기존의 장비를 수정할 떄 필요합니다.

예로 스피커의 볼륨조절장치는 대표적인 Potentiometer(가변저항) 중 하나입니다.

이를 자동으로 조절하는 데 필요한 것이 Digital Potentiometer 입니다.

크게 I2C나 SPI 통신을 이용한 방식, High Low 신호를 이용하는 방식이 있습니다.

이번 시간에 사용할 X9Cxxx 시리즈(여기서는 X9C104)는 High, Low 신호를 사용하는 방식입니다.

### 1. 데이터시트 살펴보기

[X9C 시리즈 데이터시트](https://www.intersil.com/content/dam/Intersil/documents/x9c1/x9c102-103-104-503.pdf)

데이터시트에서 중요하게 살펴보아야 할 몇 가지가 있습니다.

#### 1. 핀아웃(Pinout)

![]({{ site.url }}/img/x9c/1.png)

각 핀의 이름과 위치가 나와 있습니다.

결선할 때 참조하게 됩니다.

#### 2. 핀 설명(Pin Descriptions)

![]({{ site.url }}/img/x9c/2.png)

각 핀에 대한 설명입니다.

핀 번호 - 이름 - 기능에 관해 서술되어 있습니다.

#### 3. 한계치(Absolute Maximum Ratings)

![]({{ site.url }}/img/x9c/3.png)

한계치에 대한 설명입니다.

각 핀에 인가할 수 있는 최대 전압, 전류, 전력이 표기되어 있습니다.

이를 간과할 경우 IC가 폭발할 수 있습니다.

#### 4. 모드 선택(Mode Selection)

![]({{ site.url }}/img/x9c/4.png)

모드 선택에 관해 표로 설명되어 있습니다.

이를 참조하여 코드를 짜게 됩니다.

참고로 화살표가 우측 상향인 것은 Rising Edge, 하향인 것은 Falling Edge라고 부릅니다.

### 2. 결선하기(Wiring)

Vcc(전원+)와 Vss(전원-)를 먼저 연결해 줍니다.

데이터시트에서는 5V±10%를 추천하고 있습니다.

INC와 U/D, CS를 디지털 출력이 가능한 핀에 각각 연결해줍니다.

VH에 전원+, VL에 전원-를 연결해 줍니다.

VW에는 아날로그 입력이 가능한 핀(A0)에 연결해 줍니다.

### 3. 사용하기(Use)

UD와 CS핀에 신호를 넣어 모드를 만들어 주고 INC에 Falling Edge가 발생하면 Wiper가 이동하는 방식입니다.

Wiper는 가변저항에서 값을 결정하는 핀입니다.

Wiper를 초기화하기 위해 UD와 CS에 LOW 신호(전원-)를 넣어줍니다.

Wiper Down 상태로 이때 INC에 Falling Edge가 발생하면 Wiper가 내려가게 됩니다.

for 문(혹은 비슷한 반복문)을 이용하여 INC 핀을 100번 Down, Up 반복합니다.

이후 아날로그 핀의 값을 읽어보면 0이 나올 것입니다.

UD핀을 HIGH로 만들고 INC 핀을 Down, UP (Up->Down일 때 변합니다.)을 반복합니다.

총 100 포인트가 있으며 초기화 후 100번의 하강 엣지가 발생하면 아날로그 신호가 최대치가 됩니다.

![]({{ site.url }}/img/x9c/5.png)

아날로그 값의 흔들림이 있긴 하지만 순차적으로 오르는 것을 볼 수 있습니다.

100을 넘었을 경우에 값이 바뀌지 않는 것도 확인이 가능합니다.