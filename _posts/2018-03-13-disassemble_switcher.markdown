---
layout: post
title:  "스위처 분해하기"
categories: [making]
---

미리 말씀드리자면 전 순수한 스위처 사용자입니다.

1년전부터 스위처라는 제품을 구매하여 사용하고 있었습니다.

전등스위치에 부착하여 휴대폰으로 켜고, 끌 수 있는 장치인데 침대에 누워있다가 잘 때 주로 사용합니다.

대표 사이트는 아래와 같습니다.

[https://www.switcher.kr](https://www.switcher.kr)

분해를 마음먹은 이유는 얼마전부터 스위치 1개가 소리가 이상해서 시도해보기로 했습니다.

먼저 날카롭고 얇은 도구를 이용하여 덮개를 열어줍니다.

저는 윗판을 먼저 열어주었습니다.

![]({{ site.url }}/img/switcher/IMG_6641.JPG)

여는 과정에서 고정핀이 부러질 수 있으므로 주의해서 열어줍니다.

볼트가 4개 보이는데(1개는 이미 풀었습니다.) 전부 풀어줍니다.

볼트를 풀어주니 아랫판이 더 쉽게 열렸습니다.

![]({{ site.url }}/img/switcher/IMG_6643.JPG)

ㄱ자 모양으로 덮개가 안빠지도록 고정핀이 있습니다.

![]({{ site.url }}/img/switcher/IMG_6644.JPG)

밑판까지 다 열어주면 내부가 보입니다.

![]({{ site.url }}/img/switcher/IMG_6646.JPG)

볼트를 다 풀고 고정프레임을 들어내자 pcb가 2개 보입니다.

![]({{ site.url }}/img/switcher/IMG_6647.JPG)

하단 pcb 밑에는 배터리가 숨겨져 있습니다.

![]({{ site.url }}/img/switcher/IMG_6648.JPG)

왼쪽 하단에 보이는게 nRF51822라는 BLE 칩입니다.

오른쪽 상단에는 tp4056이라는 충전 회로가 보입니다.

3핀 커넥터가 총 5개가 있는데 따라가보니 상단 스위치 1개,

상부 서보모터에 2개, 하부 서보모터에 2개를 사용합니다.

![]({{ site.url }}/img/switcher/IMG_6651.JPG)

3.7V 750mAh 배터리를 사용하고 있습니다.

![]({{ site.url }}/img/switcher/IMG_6652.JPG)

대충 사이즈는 이정도 입니다.

![]({{ site.url }}/img/switcher/IMG_6653.JPG)

본격적으로 모터를 뜯어보겠습니다.

![]({{ site.url }}/img/switcher/IMG_6655.JPG)

아래쪽 볼트 6개가 있는 커버를 뜯어보니 랙-피니언 세트가 나오네요.

저기 랙(막대모양)이 스위치를 눌러 온/오프를 해줍니다.

![]({{ site.url }}/img/switcher/IMG_6656.JPG)

기다란 볼트 4개를 뜯어보니 모터가 나왔습니다.

서보모터를 분해해서 넣은듯 합니다.

![]({{ site.url }}/img/switcher/IMG_6657.JPG)

한번 더 열어보면 기어박스가 나옵니다.

그리스칠이 되어있네요.

![]({{ site.url }}/img/switcher/IMG_6658.JPG)

다시 조립해 줍니다.

![]({{ site.url }}/img/switcher/IMG_6660.JPG)

배터리에 붙어있던 양면테이프의 접착력이 낮아져서 3M 테이프를 발라주었습니다.

![]({{ site.url }}/img/switcher/IMG_6661.JPG)

pcb 뒤쪽에 있는 커넥터에 배터리를 끼워주고 잘 덮어줍니다.

![]({{ site.url }}/img/switcher/IMG_6662.JPG)

pcb를 잘 덮어준 뒤

![]({{ site.url }}/img/switcher/IMG_6663.JPG)

프레임을 끼우고 볼트로 고정해 줍니다.

![]({{ site.url }}/img/switcher/IMG_6664.JPG)

하단 커버에 FRONT.COVER.3 이라고 적혀있습니다.

![]({{ site.url }}/img/switcher/IMG_6665.JPG)

상단 커버에는 FRONT.COVER.2라고 적혀 있습니다.

다 덮어주고 전원을 켜서 잘 동작하는지 확인합니다.