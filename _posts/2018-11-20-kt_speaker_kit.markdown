---
layout: post
title:  "RPI로 KT gigagenie AI 스피커 키트 만들기 - 1편"
categories: [rpi, making, coding]
---

RPI로 KT Gigagenie AI 스피커 키트 만들기 - 1편

이번 시간에는 AI 스피커를 만들어 보도록 하겠습니다.

AI 스피커는 구글에서 나온 Google Home, 아마존의 Echo, 네이버의 Clova, 카카오의 mini등이 있습니다.

그 중 KT의 기가지니를 사용한 AI 스피커 키트가 있어 이를 사용해 보도록 하겠습니다.

### 기가지니 가입하기

![]({{ site.img_url }}/kt_voice_kit/1.png)

사이트에 들어가면 우측 상단에 **로그인**과 **회원가입**버튼이 있습니다.

![]({{ site.img_url }}/kt_voice_kit/2.png)

약관에 동의를 누른 후

![]({{ site.img_url }}/kt_voice_kit/3.png)

휴대폰이나 이메일로 인증한 후 다음을 눌러줍니다.

![]({{ site.img_url }}/kt_voice_kit/4.png)

이름, 닉네임등등 기본 정보를 넣어줍니다.

![]({{ site.img_url }}/kt_voice_kit/5.png)

회원가입이 완료되면 **서비스 - GiGA Genie**를 눌러줍니다.

![]({{ site.img_url }}/kt_voice_kit/6.png)

**Service SDK - 이용 신청 하기**를 눌러줍니다.

![]({{ site.img_url }}/kt_voice_kit/7.png)

API LINK 사이트로 넘어왔습니다.

**서비스 등록하기 - 3rd Party Device List**를 클릭해 줍니다.

![]({{ site.img_url }}/kt_voice_kit/8.png)

**AI MAKERS Kit (DEV)**를 선택하고 3개의 리소스를 전부 선택한 뒤 서비스명을 확인합니다.

![]({{ site.img_url }}/kt_voice_kit/9.png)

신청을 누르고 3~5초 뒤 새로고침을 눌러줍니다.

![]({{ site.img_url }}/kt_voice_kit/10.png)

**My Service - OS Image**의 다운로드를 눌러 Raspberry Pi의 이미지파일을 받습니다.

![]({{ site.img_url }}/kt_voice_kit/11.png)

받은 파일의 압축을 풀어 img파일을 확인합니다.

![]({{ site.img_url }}/kt_voice_kit/12.png)

Win32 Disk Imager 혹은 Etcher를 이용하여 이미지를 USB에 넣어줍니다.

![]({{ site.img_url }}/kt_voice_kit/13.png)

위와 같은 화면이 나오면 이미지가 잘 들어간 것입니다.

다음 시간에는 기본 예제를 구동해 보도록 하겠습니다.

감사합니다.

