---
layout: post
title:  "라즈베리파이3에 windows 10 iot 올리기"
category: rpi
---

이번 시간에는 라즈베리파이3에 windows 10 iot core를 올려보도록 하겠습니다.

라즈베리파이는 여러가지의 os를 구동할 수 있으며 대표적으로 raspbian, ubuntu등이 있습니다.

windows 10 iot core 는 15년도 8월경 배포가 시작되어 linux 계열의 os가 아닌 windows 계열의 os를 처음 라즈베리파이에 올릴 수 있게 되었습니다.

설치를 시작해 보겠습니다.

### 1. NOOBS 다운로드

[noobs 다운로드 링크](https://www.raspberrypi.org/downloads/noobs/)

위 링크에서 NOOBS(NOOBS LITE 아닙니다.)를 다운받습니다. 토렌트를 사용하니 빨랐습니다.

다운로드 하는 사이에 8GB 가량의 micro sd를 포멧해 줍니다.

다운로드가 완료되었다면 압축파일이 하나 나올 것입니다. 이 압축을 풀어 안에 있는 파일들을 포멧이 완료된 micro sd에 복사해 주면 끝입니다.

### 2. 실행

micro sd를 라즈베리파이에 꽂고 모니터 혹은 TV등에 hdmi to hdmi, hdmi to DVI등으로 연결해 줍니다. 다음으로 마우스 혹은 키보드를 연결합니다. 그 후 Ethernet 케이블을 연결해 줍니다.

그 후 전원을 연결하면 아래와 같은 화면이 나옵니다. windows 10 iot core를 선택하고 왼쪽 상단의 Install(키보드의 경우 'i') 을 클릭해 줍니다.


![1](https://drive.google.com/uc?id=0B_CtpwiAk5hIblJXRHJHVDhLUkk)

### 3. 기다림

이제 설치가 완료될 때 까지 기다리면 됩니다. 중간에 버전을 선택하는 듯한 부분이 나오는데(pre-release 의 경우 자료가 느릴 것을 우려하여) RTM 버전으로 선택해 주었습니다. 중간에 관련 개발자 분으로 추정되는 사진이 있어 찍어보았습니다.

![2](https://drive.google.com/uc?id=0B_CtpwiAk5hIMVlXOGZxWEg1YTQ)
![3](https://drive.google.com/uc?id=0B_CtpwiAk5hIVV9tSmRDSnlTQ0k)
![4](https://drive.google.com/uc?id=0B_CtpwiAk5hIaEMxci1oVHExLXM)

설치가 완료되면 아래와 같이 현재 상태가 나옵니다. (반사된 상황이 조금 부끄럽네요..)

![5](https://drive.google.com/uc?id=0B_CtpwiAk5hIRkw0NGtpTFd0cWM)

다음 시간에는 windows 10 iot 에서의 개발환경 구축, hello world 까지 시도해 보도록 하겠습니다.

감사합니다.