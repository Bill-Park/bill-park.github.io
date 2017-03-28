---
layout: post
title:  "라즈베리파이를 nas로 사용하기(Raspberry pi nas) - 1"
category: rpi
---

NAS는 Network Attached Storage의 약자로 '네트워크에 연결된 저장소'입니다.

노트북, 휴대폰은 외부에서 사용되는 경우가 더 많아지면서 용량의 압박을 느끼게 되었습니다.

특히 16G밖에 안되는 제 휴대폰은 항상 용량이 부족하다고 외치고 있습니다.

그래서 라즈베리파이를 이용하여 nas를 만들어 보도록 하겠습니다.

이번에 만들 Rpi-NAS는 파일 저장소, 음악과 영상 스트리밍, 토렌트서버의 기능을 가지게 될 것입니다.

먼저 파일 저장소로 이용하기 위해 ftp 서버를 설치하도록 하겠습니다.

~~~
$sudo apt-get install vsftpd # vsftpd 설치
$sudo nano /etc/vsftpd.conf # vsftpd 설정하기

local_enable=YES # 로컬 사용자들의 접속을 허용합니다.
write_enable=YES # 쓰기를 사용합니다.
local_umask=022 # 파일의 권한에 관한 부분입니다. 
chroot_local_user=YES # 홈 디렉토리보다 상위로 가지 못하도록 합니다.
chroot_list_enable=YES # 특정 사용자에 상위 디렉토리 접근권한을 줍니다.
chroot_list_file=/etc/vsftpd.chroot_list # chroot_list_enable 사용자 리스트 위치입니다.
~~~

local_umask 부분은 linux 계열의 특징이라 할 수 있습니다.  
linux 계열에서 파일에는 아래와 같은 권한이 있습니다.

|  소유자  |-소유그룹-|   전체  |
|:---------|:--------:|-------:|
|   R(4)   |   R(4)   |  R(4)  |
|   W(2)   |   W(2)   |  W(2)  |
|   X(1)   |   X(1)   |  X(1)  |
{: rules="groups"}

R은 읽기, W는 쓰기, X는 실행에 관한 권한입니다.  
각 권한은 숫자로도 나타내며 이 숫자를 모두 더한 값으로 표시합니다.  
또한 소유자-소유그룹-전체 순서로 표시합니다.  
예를들어 abc.txt 파일의 소유자의 권한이 RWX, 소유그룹의 권한이 RX, 전체는 아무것도 없다면  
소유자   : 4(R) + 2(W) + 1(X) = 7  
소유그룹 : 4(R) + 1(x) = 5  
전체     : 없음  
으로 abc.txt의 권한은 750이 됩니다.  
umask는 파일의 권한에서 -(빼기)되는 부분으로 022이므로 ftp로 접속했을 때 권한은 530(750-022)이 됩니다.

추가적인 설정에 대해서는 아래 블로그를 참조해 주시기 바랍니다.  
[vsftpd 설정 참조](http://2factor.tistory.com/96)

다음으로 chroot_list_enable 사용자 리스트를 편집해 주어야 합니다.
~~~
$sudo nano /etc/vsftpd.chroot_list
~~~

안에 유저만 적어주면 됩니다.

![chroot_list](https://drive.google.com/uc?id=0B_CtpwiAk5hIeXhSaXZaQTBfbG8)

vsftpd를 다시 실행합니다.
~~~
$sudo service vsftpd restart
~~~

ftp 클라이언트를 이용해도 되지만 실험용으로 웹 브라우저(여기서는 크롬)를 사용하였습니다.

브라우저의 주소창에 아래와 같이 입력해 줍니다.
~~~
ftp://pi@라즈베리파이의 ip:포트번호(기본 21)
~~~

만약 ip가 123.456.789.101이고 기본포트일 때(21)
~~~
ftp://pi@123.456.789.101:21 (포트입력 전 콜론 주의)
~~~

를 입력해 주면 됩니다.

![ftp_login](https://drive.google.com/uc?id=0B_CtpwiAk5hITXVLb09mME5WM1E)

사용자 이름에는 유저이름(pi)
비밀번호는 로그인 할 때의 비밀번호와 같습니다.(기본 raspberry)

![ftp_login](https://drive.google.com/uc?id=0B_CtpwiAk5hIRDdQZ2NURTI3X3M)

위와같은 화면이 나왔다면(pi의 HOME 디렉토리입니다.) 성공입니다.

