---
layout: post
title:  "윈도우에서 python 시작하기(작업환경 구축)"
category: coding
---

이떄까지는 mac 혹은 linux(Raspbian) 환경에서 여러 코딩을 해왔습니다.  
하지만 우리나라는 윈도우의 보급률이 압도적으로 높은 관계로 윈도우에서 작업환경을 구축해 보도록 하겠습니다.

window는 gui가 잘 구성되어 있어 꽤나 설치가 간편합니다.

### 1. python 다운로드

[여기](https://www.python.org/downloads/)에서 파이썬을 다운로드해 줍니다.  
2.7.x와 3.5.x가 있습니다.  
저는 3버전을 주로 사용하므로 3.5.2(2016.11.02기준 최신)를 다운받도록 하겠습니다.  
다운받은 파일(python-3.5.2.exe)을 실행시켜 줍니다.

**※주의** 중간에 pip를 설치를 묻는 부분이 있는데 이는 반드시 체크해 주시기 바랍니다.  
만약 하지 않았을 경우 easy_install 을 거쳐 pip 를 설치해야 하는 번거로움이 있습니다.

**※주의2** 전체 사용자를 위해 설치해 주시기 바랍니다.  
특정 사용자를 위한 설치를 하면 경로를 찾기가 복잡해 질 수 있습니다.  
전체 사용자의 경우 C 드라이브 안에, 특정 사용자의 경우 유저의 AppData 내에 설치됩니다.

### 2. path 설정

코딩시에 주로 pycharm 등의 에디터를 사용하는 경우가 많습니다.  
하지만 cmd창에서 python을 사용해야 할 경우가 종종 있기에 미리 설정해 주었습니다.  
제어판-시스템 및 보안-시스템 으로 이동합니다.  
혹은 윈도우키 + Pause/Break(방향키 상단에 위치)를 눌러도 됩니다.  
왼쪽 탭의 고급시스템 설정 - 아래쪽의 환경 변수를 클릭합니다.  
Path를 찾아 시스템 변수의 편집(단축키 Alt + I)을 눌러 변수 값의 맨 마지막에 파이썬 설치 경로를 입력해 줍니다.  
전체 사용자로 설치하였을 경우 C:\Program Files (x86)\Python35-32 에 있습니다.  
변수 값이 빈칸이 아니라면 맨 뒤에 ;(세미콜론)을 넣어준 뒤 경로를 적어줍니다.  
cmd 창을 열어(실행(윈도우 + R) - cmd) python을 입력하여 테스트가 가능합니다.

![1](https://drive.google.com/uc?id=0B_CtpwiAk5hIXzBDdFFOVGg1WUE)


※참고자료 : [Alpha Beta Gamma님의 블로그](http://radiation.tistory.com/entry/%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98%EC%97%90-Python-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0)

### 3. easy_install 및 pip 설치

처음 설치할 때 pip를 설치하셨다면 이 부분은 스킵하셔도 됩니다. pip는 파이썬의 패키지 관리를 도와주는 툴로 이후에 import할 모듈등을 설치할 때 사용됩니다. python이 설치된 폴더 - Scripts 폴더를 보면 설치 여부를 알 수 있습니다. 만약 설치되어 있지 않다면 easy_install을 먼저 설치해 주어야 합니다. <a href="https://pypi.python.org/pypi/setuptools">다운로드 링크</a>에서 ez_setup.py 를 클릭하면 다운로드가 시작됩니다. 다운로드가 완료되었다면 적당한 위치로 옮긴 뒤(cmd창에서 이동하기 편한 곳) python을 이용하여 실행해 줍니다. 예를들어 바탕화면에 ez_setup.py가 있다면 cmd창에서 C:\Users\admin\Desktop 로 이동해 줍니다.
~~~
python ez_setup.py
~~~
위 명령어를 입력하면 설치가 시작됩니다. 설치가 완료되었다면 python 폴더 - Scripts 안에 easy_install이 있을 것입니다. 이제 거의 다왔습니다. pip를 설치하기 전에 Scripts 폴더도 환경변수에 넣어줍니다. 경로는 파이썬 설치 경로/Scripts입니다. 저는 C:\Program Files (x86)\Python35-32\Scripts 로 되어 있습니다.
~~~
easy_install pip
~~~
그 후 위 명령어를 입력해 주면 pip 설치가 완료됩니다.

![2](https://drive.google.com/uc?id=0B_CtpwiAk5hIVWxEQndWZkNVQ2M)

설치가 잘 되었는지 확인하려면
~~~
pip --version
~~~
을 입력해 보면 됩니다.

![3](https://drive.google.com/uc?id=0B_CtpwiAk5hIVnhCdXY5VEk2QTA)

저는 8.1.1 버전으로 나오네요.

**※참고자료** : [코랩's 코드 조각 블로그](http://blog.colab.kr/11)

이상으로 윈도우에서 개발환경 구축을 마치도록 하겠습니다.