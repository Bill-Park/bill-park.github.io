---
layout: post
title:  "스피커-헤드셋 원클릭 바꾸기"
category: coding
---

스피커-헤드셋을 쉽게 전환할 수 없을까?

PC방에 가보면 출력장치를 전환하는 파일이 눈에 띕니다.

저도 스피커와 헤드셋을 각각 사용하기에 전환할 일이 자주 있습니다.

최근에 사운드카드를 추가하면서 더 필요해졌습니다.

매번 바꾸는 것도 귀찮아서 바로가기 형태로 만들어 보았습니다.

## 1. 재생 장치 확인하기

**제어판 - 소리** 에 들어가보면 상단에 **재생** 이라는 탭이 있습니다.

![sound](https://drive.google.com/uc?id=0B_CtpwiAk5hIeEwybk90ZW54LWM)

저는 스피커, Realtek Digital Output, 헤드폰 이라는 장치가 있습니다.

만약 장치이름이 중복이라면 **해당 장치 우클릭 - 속성**을 눌러

![name](https://drive.google.com/uc?id=0B_CtpwiAk5hIWmxNTTV6RzlZOXM)

이름을 바꿔주면 됩니다.

## 2. bat 파일 만들기

재생 장치를 변경하기 위해서는 nircmd라는 프로그램을 받아야 합니다.

[nircmd 홈페이지](http://www.nirsoft.net/utils/nircmd.html)

[다운로드-32bit](http://www.nirsoft.net/utils/nircmd.zip)

[다운로드-64bit](http://www.nirsoft.net/utils/nircmd-x64.zip)

압축파일이 받아지는데 안에는 3개의 파일이 있습니다.

그중 nircmd.exe를 실행시켜 봅니다.

![nircmd](https://drive.google.com/uc?id=0B_CtpwiAk5hIS3lkeEZScHdfa28)

Windows Directory로 이동시켜서 사용해도 되고 그냥 사용하셔도 됩니다.

편의를 위해 Copy To Windows Directory를 눌러 이동시키도록 하겠습니다.

만약 이동이 되지 않는다면 **관리자 권한으로 실행**해 주시면 됩니다.

bat 파일은 Linux등의 sh 파일에 비하면 정말 간단하게 만들 수 있습니다.

메모장을 열고

![blank_notepad](https://drive.google.com/uc?id=0B_CtpwiAk5hIdkZOcGtOamNDSWc)

원하는 명령어를 적어준 뒤 저장하면 됩니다.

![command_notepad](https://drive.google.com/uc?id=0B_CtpwiAk5hIaDFLWXEtUWdLNU0)

저장할 때 주의할 점은 **텍스트 문서(\*.txt)**가 아니라 **모든 파일(\*.\*)**로 해주어야 합니다.

텍스트문서로 저장할 경우 bat 파일이 아닌 txt 파일이 생성됩니다.

![save_notepad](https://drive.google.com/uc?id=0B_CtpwiAk5hIWm9MUlpKMlQtLVE)

테스트를 해줍니다.

명령 프롬프트(CMD)를 켜고 bat 파일의 이름을 입력해 줍니다.

처음 2~3문자를 입력하고 Tab키를 누르면 뒤쪽은 자동완성이 됩니다.

저는 speaker와 headphone으로 저장하였습니다.

![cmd_write](https://drive.google.com/uc?id=0B_CtpwiAk5hIUWU2X0dWU3VHMFk)

물론 bat파일을 더블클릭하여 직접 실행해 주어도 똑같이 작동합니다.

이상으로 간편하게 스피커-헤드셋을 바꾸는 방법이였습니다.