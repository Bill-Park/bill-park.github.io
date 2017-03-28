---
layout: post
title:  "거울손 프로젝트(Mirror Hand Project)"
categories: [making, avr_arm]
---

안녕하세요. 오늘은 Mirror Hand (거울손) 프로젝트에 대해 써 보겠습니다.

먼저 모습은

![1](https://drive.google.com/uc?id=0B_CtpwiAk5hISzV3Sk14N0VTZXc)

이렇게 생겼습니다.

아두이노 우노, 브레드보드(배선), HC-06 블루투스 모듈, 서보모터 5개, 스테인리스와이어와 볼트, 3D프린트된 손으로 이루어 져 있습니다.  
손모양은 http://www.inmoov.fr 에 가시면 다운받으실 수 있습니다.

위의 손만 있으면 재미 없겠죠? 그래서 장갑을 만들었습니다.

![2](https://drive.google.com/uc?id=0B_CtpwiAk5hIQmdPNG9oczBESFU)

네 엄청 조잡합니다. 
달리 구할 수 있는게 없어서 일단 저렇게 만들었습니다.  
밑부분이 짤렸는데 저 부분은

![3](https://drive.google.com/uc?id=0B_CtpwiAk5hIaDBCQ1NPaTVfdWs)

위와같은 회로입니다.

저항이 연결된 소형 브레드보드, HC-06 블루투스 보드와 로보티즈사의 OpenCM9.04보드입니다.

여기 첨부된 소스코드를 업로드합니다. (참고용으로만 사용해 주시기 바랍니다.)

프로토콜은 [ 를 먼저 보내고, 문자열 길이인 len 2문자를 보냅니다.  
a로 시작하여 b로 끝나는 사이에 엄지손가락 데이터, c로 시작하여 d로 끝나는 부분에 검지손가락 데이터 순으로 하여 j로 끝나는 새끼손가락까지 보냅니다.  
그리고 마지막 문자인 ] 를 보냅니다.

그러면 아래와 같은 작동이 나옵니다.


<iframe width="560" height="315" src="https://www.youtube.com/embed/MkwLLEvCAiU" frameborder="0"></iframe>


다시보니 아쉬움이 많이 남는 프로젝트입니다.

꼭 업그레이드 버전을 만들 수 있도록 하겠습니다.

