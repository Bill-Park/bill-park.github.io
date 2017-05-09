---
layout: post
title:  "windows 10 iot core Hello World!"
categories: [rpi, coding]
---

라즈베리파이에 windows 10 iot core를 올릴 수 있게 된건 15년도 8월입니다.

2년정도가 지났지만 아무런 자료를 찾을 수가 없었습니다.

그래서 직접 해보기로 했습니다.

코딩의 시작 **Hello World!**부터 해보도록 하겠습니다.

### 1. 사전준비

windows 10 iot core를 사용하기 위해서는 windows 10 버전의 컴퓨터가 1대 필요합니다.

windows 10은 creator 업데이트가 필요하며 이는 아래 링크에서 받을 수 있습니다.

[https://www.microsoft.com/ko-kr/software-download/windows10](https://www.microsoft.com/ko-kr/software-download/windows10)

위 링크에서 **지금 업데이트**를 클릭하여 파일을 받고 업데이트 해 줍니다.

라즈베리파이에 windows 10 iot core(이하 win 10 iot)를 올려주어야 합니다.

이는 저번시간에 설명한 NOOBS를 사용하거나 Windows 10 IoT Core Dashboard가 필요합니다.

**NOOBS로 올리기**

[이전편]({{site.url}}/rpi/2017/03/28/rpi/2016/10/22/rpi-windows10-iotcore.html)

**Windows 10 Iot Core Dashboard로 올리기**

먼저 Windows 10 IoT Core Dashboard를 다운받습니다.

[https://developer.microsoft.com/en-us/windows/iot/docs/iotdashboard](https://developer.microsoft.com/en-us/windows/iot/docs/iotdashboard)

micro sd를 연결한 뒤(포멧은 자동으로 됩니다.) Dashboard를 아래와 같이 설정해 줍니다.

![iso_install](https://goo.gl/RJsxTf)

계속을 눌러 micro sd카드를 포멧해 줍니다.

![sd_format](https://goo.gl/y3ph2O)

포멧후 자동으로 sd카드에 win 10 iot가 올라가니 잠깐 기다려 줍니다.

완료되면 아래와 같이 나옵니다.

![sd_ready](https://goo.gl/DVMVCw)

### 2. Visual Studio 2017 설정하기

win 10 iot를 사용하기 위해서는 Visual Studio가 필요합니다.

현재 2017버전이 나왔으므로 이를 사용하도록 하겠습니다.

Visual Studio 2017은 아래 링크에서 받을 수 있습니다.

[https://www.visualstudio.com/ko/downloads/?rr=https%3A%2F%2Fwww.google.com%2F](https://www.visualstudio.com/ko/downloads/?rr=https%3A%2F%2Fwww.google.com%2F)

저는 Community 버전을 다운받았습니다.

exe파일을 실행하여 설치를 진행해 줍니다.

설치가 완료되면 Visual Studio Installer라는 파일이 보입니다.

이를 실행시키면 아래와 같은 화면이 뜹니다.

여기서 수정을 눌러 설치할 파일을 정해주어야 합니다.

워크로드에서 체크된 부분을 설치해 줍니다.(총 3개)

![workload_1](https://goo.gl/jlkb3j)

![workload_2](https://goo.gl/7Aak7Q)

개별 구성 요소에서 추가적으로 2가지를 체크해 줍니다.

체크 후 수정을 누르면 설치가 진행됩니다.

![each](https://goo.gl/CHWOXv)

설치가 완료되면 Visual Studio를 실행해 줍니다.

![new](https://goo.gl/BVi31R)

**파일 - 새로 만들기 - 프로젝트**를 눌러 새 프로젝트를 생성합니다.

![universial](https://goo.gl/74bJQm)

버전은 크게 신경쓰지 않으셔도 됩니다.

![version](https://goo.gl/JcdSYk)

### 3. Visual Studio를 사용하여 앱 올리기

**MainPage.xaml**를 더블클릭하여 실행합니다.

UI를 꾸밀 수 있는 곳입니다.

버튼을 하나 끌어다 놓은 뒤 Content 의 값을 Hello World!로 변경해 줍니다.

![button](https://goo.gl/0jAPGz)

솔루션~~ 바로 밑에있는 App6(프로젝트 명)을 우클릭한 뒤 속성을 클릭합니다.

![properties](https://goo.gl/n1lxCx)

**컴퓨터 이름**이라 되어있는 부분에 라즈베리파이의 ip주소를 적어줍니다.

![computer_name](https://goo.gl/bgRaJs)

위쪽 탭에서 초록색 화살표 옆의 로컬 컴퓨터(혹은 Device)의 Dropdown 메뉴에서 원격컴퓨터를 클릭합니다.

![remote_computer](https://goo.gl/m0jwJX)

그리고 초록색 버튼을 눌러 실행하면 잠시 뒤(시간이 조금 걸립니다.) 화면이 아래와 같이 바뀌게 됩니다.

![debug](https://goo.gl/mGyDwW)

라즈베리파이와 연결된 화면을 보면 아래와 같이 나오게 됩니다.

![Hello_World!](https://goo.gl/uoK8Be)

중단하기 위해서는 초록색 화살표 옆에 있는 빨간 네모(정지버튼)를 누르면 됩니다.

### 4. 외부에서 Raspberry Pi Windows 10 iot core 접속하기

작업을 하다보면 외부에서 win 10 iot에 접속해야 할 일이 있습니다.

저는 데스크탑과 공유기가 분리되어있어 외부에서 공유기로 접속하여 라즈베리파이에 코딩을 해야합니다.

이를 위해서는 공유기에서 포트포워딩이라는 것을 해주어야 합니다.

포트란, TCP/IP 프로토콜을 통해 들어온 요청이 마지막으로 분류되는 종단점입니다.

ip를 가지고 들어온 요청을 마지막으로 분류하는 곳입니다.

예를들어 집 주소(ip)를 가지고 집을 찾아간 뒤 그 집의 어느 방 혹은 거실에 들어가야 만날 사람이 있습니다.

여기서 방 혹은 거실이 포트가 되는 것입니다.

하지만 공유기는 1개의 ip를 받아서 연결된 장비에 내부 ip를 할당하여 사용하게 됩니다.

주소를 가지고 찾아간 집이 아파트인 상태입니다.

모든 포트의 입력을 한곳으로 보낼 수도 있지만 각각 지정이 가능합니다.

컴퓨터가 있는 방을 찾아온 사람, TV가 있는 방을 찾아온 사람을 각각 102호 작은방, 105호 큰방으로 보내는 것이라 보면 됩니다.

외부에서 ip를 이용하여 공유기를 찾은 뒤 포트를 보고 공유기가 어디로 갈지 정해주는 것을 포트포워딩이라 합니다.

win 10 iot는 29820번과 8116,8117번 포트를 사용하고 있었습니다.

위 3개의 포트를 포트포워딩을 통해 설정해주면 외부에서도 사용이 가능합니다.

포트포워딩 방법은 각 공유기별 방법이 다르므로 제조사의 설명 혹은 구글링을 참조해 주시기 바랍니다.

이상으로 라즈베리파이(Raspberry Pi) windows 10 iot core 에서 Hello World! 출력하기를 완료하였습니다.

감사합니다.

