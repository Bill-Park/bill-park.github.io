---
layout: post
title:  "RPI로 KT gigagenie AI 스피커 키트 만들기 - 2편"
categories: [rpi, making, coding]
---

RPI로 KT Gigagenie AI 스피커 키트 만들기 - 2편

저번 시간에는 AI 스피커를 사용하기 위한 기본 설정을 마쳤습니다.

이번 시간에는 기본적으로 제공되는 예제들을 구동해 보도록 하겠습니다.

### 스피커 및 마이크 테스트

![]({{ site.img_url }}/kt_voice_kit/2_login/1.png)

바탕화면에 보면 **Check Audio**라는 파일이 있습니다.

이를 더블클릭하여 실행시켜 줍니다.

![]({{ site.img_url }}/kt_voice_kit/2_login/2.png)

처음 실행 후 엔터를 누르면 띠리리리링 하는 소리가 납니다.

만약 들리지 않을 경우 스피커와 관련 부분을 확인해 주세요.

소리가 잘 난다면 y를 입력하고 엔터를 눌러 넘어갑니다.

![]({{ site.img_url }}/kt_voice_kit/2_login/3.png)

다음으로 엔터를 누르면 녹음을 시작합니다.

약 5초간 녹음을 하며 녹음된 소리가 다시 재생됩니다.

스피커는 정상이나 녹음한 소리가 안나온다면 마이크를 확인해 주세요.

![]({{ site.img_url }}/kt_voice_kit/2_login/4.png)

정상이라면 y를 입력하고 엔터를 눌러 다음으로 넘어갑니다.

한번 더 엔터를 누르면 창이 종료됩니다.

![]({{ site.img_url }}/kt_voice_kit/2_login/5.png)

왼쪽 상단의 지구본모양을 눌러 인터넷 브라우저를 켠 후 아래 링크를 입력합니다.

https://apilink.kt.co.kr/sdpapply/console/index.do

![]({{ site.img_url }}/kt_voice_kit/2_login/6.png)

아이디, 비밀번호, SMS 인증을 완료하고 로그인을 해줍니다.

![]({{ site.img_url }}/kt_voice_kit/2_login/65.png)

우측 상단 창에서 **Console**버튼을 눌러 콘솔창으로 넘어갑니다.

![]({{ site.img_url }}/kt_voice_kit/2_login/7.png)

왼쪽 메뉴에서 **GiGA Genie - My Service**를 클릭합니다.

![]({{ site.img_url }}/kt_voice_kit/2_login/8.png)

**Key 보기**를 눌러 키 값을 확인합니다.

![]({{ site.img_url }}/kt_voice_kit/2_login/9.png)

JSON 다운로드를 눌러 키 값, ID등이 저장된 파일을 다운로드합니다.

이 파일이 있으면 권한 대부분을 사용할 수 있으므로 주의해 주시기 바랍니다.

![]({{ site.img_url }}/kt_voice_kit/2_login/10.png)

Downloads 폴더 안에 **clientKey.json**파일이 있는 것을 확인할 수 있습니다.

이 파일을 직접 사용하기도 하고 파일 안의 clientID, Key값등을 직접 넣어서 사용하기도 합니다.

이상으로 2편을 마치도록 하겠습니다.

감사합니다.
