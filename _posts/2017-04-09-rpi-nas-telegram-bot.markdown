---
layout: post
title:  "라즈베리파이를 nas로 사용하기(Raspberry pi nas) - 3"
category: rpi
---

저번시간에 라즈베리파이를 토렌트 서버 기능을 추가하였습니다.

하지만 하나의 단점이 있습니다.

토렌트 서버로 활용하기 위해서는 토렌트 파일을 업로드 해주어야 합니다.

파일을 업로드하는 여러 방법이 있겠지만 저는 텔레그램 봇(telegram-bot)을 이용해 보도록 하겠습니다.

### 0. 준비물

텔레그램 봇이 필요합니다.

이부분은 이전 게시물을 참조해 주시기 바랍니다.

[텔레그램 봇 만들기-1]({{site.url}}/python/2016/12/08/python-telegram-bot-1.html)

[텔레그램 봇 만들기-2]({{site.url}}/python/2016/12/11/python-telegram-bot-2.html)

### 1. python 준비

라즈베리파이에는 기본적으로 python이 설치되어 있습니다.

물론 pip도 설치되어 있습니다.

만약 설치되어있지 않다면 아래 명령어들을 이용하여 설치할 수 있습니다.

3.5.2버전 기준 설치방법입니다.

~~~
$sudo apt-get install libbz2-dev liblzma-dev libsqlite3-dev libncurses5-dev libgdbm-dev zlib1g-dev libreadline-dev libssl-dev tk-dev
$wget https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tar.xz
$tar xvf Python-3.5.2.tar.xz
$cd Python-3.5.2
$./configure
$make
$sudo make install
~~~

### 2. git에서 소스코드 가져오기

제가 지금 사용하는 코드를 github에 올려두었습니다.

이를 가져오도록 하겠습니다.

~~~
$git clone https://github.com/Bill-Park/torrent_bot.git
~~~

만약 git이 설치되어있지 않다면 아래 명령어로 설치할 수 있습니다.

~~~
$sudo apt-get install git
~~~

### 3. virtualenv 설치하기

clone이 완료되었다면 torrent_bot이라는 폴더가 생성되었을 것입니다.

![clone_folder](https://drive.google.com/uc?id=0B_CtpwiAk5hIUS12MVAycTQta2M)

소스코드는 python 코드로 되어있으며 이를 사용하기 위해서 모듈이 몇개 필요합니다.

모듈을 바로 설치할 수 있지만 관리의 편의를 위해 virtualenv를 사용하도록 하겠습니다.

이 부분은 아래 블로그를 참조해 주시기 바랍니다.

[virtualenv 상세설명](https://beomi.github.io/2016/12/28/HowToSetup-Virtualenv-VirtualenvWrapper/)

설치가 완료되었다면 초기 설정을 해주어야 합니다.

git clone으로 생성된 torrent_bot 폴더를 virtualenv로 만들 것입니다.

~~~
$virtualenv torrent_bot
~~~

그러면 torrent_bot 폴더 안에 bin폴더가 생성되었을 것입니다.

![bin_folder](https://drive.google.com/uc?id=0B_CtpwiAk5hISFRWZ1poWDdVQW8)

bin 폴더 안에있는 activate 파일을 실행시켜 줍니다.

~~~
$source bin/activate
~~~

그러면 아래와 같이 pi@~~~ 앞에 (torrent_bot) 이라는 하얀 글자가 붙게됩니다.

![run_virtualenv](https://drive.google.com/uc?id=0B_CtpwiAk5hIRWVtZXJ4dG9XOFE)

### 4. 관련 모듈 설치하기

python은 pip를 이용하여 모듈을 관리합니다.

필요한 모듈은 requirements.txt에 전부 저장되어 있기에 명령어 하나로 간단하게 설치가 가능합니다.

requirements.txt안에는 아래와 같이 모듈명과 버전이 적혀있습니다.

![requirements](https://drive.google.com/uc?id=0B_CtpwiAk5hIWm1jWU5zU2k0RkE)

pip를 이용하여 모듈들을 설치해 보도록 하겠습니다.

### ※주의

**반드시 virtualenv가 실행된 상태여야 합니다.**

~~~
$pip install -r requirements.txt
~~~

아직 하나의 준비가 더 남았습니다.

**login_data.py**라는 파일을 만들어 주어야 합니다.

programs 폴더 안에 get_file.py라는 코드와 같이 있어야 합니다.

여기에는 user, password, 봇의 token등 중요한 정보가 담겨있습니다.

.gitignore에 추가되어있어 github에 올라가지 않습니다.

또한 사용자별로 상이하여 직접 입력해 주어야 합니다.

![login_data](https://drive.google.com/uc?id=0B_CtpwiAk5hISTYyN2NlaDhfUGs)
~~~
user에는 이름(기본값은 pi)

passwd는 transmission에서 사용하는 비밀번호(password)

token은 telegram-bot의 token값
~~~

전부 **''**(문자열을 나타냄) 사이에 있어야 합니다.

이제 파이썬(Python) 코드를 실행시켜 보도록 하겠습니다.

![python](https://drive.google.com/uc?id=0B_CtpwiAk5hIZ0dMdTJvRTlZSUk)

코드가 실행된 상태에서 파일을 업로드하면 파일명과 상태가 나옵니다.

웹페이지에서 텔레그램 봇으로 보내는 아래와 같습니다.

## 1-2-3

![1](https://drive.google.com/uc?id=0B_CtpwiAk5hIUVhMbWRsQnRBNVE){: width="30%" height="30%"}
![2](https://drive.google.com/uc?id=0B_CtpwiAk5hIcGE2eTY2b0lOcDQ){: width="30%" height="30%"}
![3](https://drive.google.com/uc?id=0B_CtpwiAk5hILVhRa1R0TUhwWFE){: width="30%" height="30%"}

## 4-5-6

![4](https://drive.google.com/uc?id=0B_CtpwiAk5hIX19tX2tMbEFMRGs){: width="30%" height="30%"}
![5](https://drive.google.com/uc?id=0B_CtpwiAk5hIUEZJYnRiNk1qMEk){: width="30%" height="30%"}
![6](https://drive.google.com/uc?id=0B_CtpwiAk5hIQzNwZ3NZSGd2cW8){: width="30%" height="30%"}

텔레그램 봇은 업데이트가 될수도 안될수도 있습니다.

기능추가는 언제나 환영입니다.




