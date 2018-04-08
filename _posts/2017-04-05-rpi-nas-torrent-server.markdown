---
layout: post
title:  "라즈베리파이를 nas로 사용하기(Raspberry pi nas) - 2"
category: rpi
---

저번 시간에 ftp 서버를 설치하였습니다.

이 ftp 서버에 파일이 없다면 무용지물이 됩니다.

이번 시간에는 서버에 파일을 올려 보겠습니다.

그 전에 앞서 라즈베리파이는 micro sd를 기본 저장공간으로 사용합니다.

용량이 크다해도 32G정도이기에 서버로써는 턱없이 부족합니다.

하지만 라즈베리파이 3는 4개의 USB 포트가 있습니다.

외장하드나 고용량의 USB를 사용하여 부족한 용량을 먼저 보충해 주도록 하겠습니다.

### 1. USB 연결하기

USB가 어디에 연결되어 있는지 확인합니다.

~~~
$sudo fdisk -l
~~~

![]({{ site.img_url }}/rpi_nas/3.png)

/dev/sdx1의 형태입니다.

저는 2개가 연결되어 있으므로 sda1, sdb1이 나왔습니다.

usb를 NTFS로 포맷하였으므로 ntfs-3g를 설치합니다.

ntfs-3g는 ntfs 방식에 **쓰기**를 가능하게 해줍니다.

~~~
$sudo apt-get install ntfs-3g
~~~

이제 마운트를 해주어야 합니다.

sda1을 먼저 해주겠습니다.

~~~
$sudo mkdir /mnt/usb1 #마운트할 폴더를 생성합니다.
$sudo mount -t ntfs -o uid=pi,gid=pi /dev/sda1 /mnt/usb1 #마운트합니다.
~~~

uid와 gid는 마운트 한 폴더의 소유자, 소유그룹을 의미합니다.

![]({{ site.img_url }}/rpi_nas/4.png)

그러면 위와같이 에러가 발생합니다.

이는 부팅시 자동마운트로 해결할 수 있습니다.

~~~
$sudo nano /etc/fstab

/dev/sda1 /mnt/usb1 ntfs defaults,uid=1000,gid=1000 0 0
를 적어줍니다. (띄워쓰기 칸 수는 상관없습니다.)
~~~

![]({{ site.img_url }}/rpi_nas/5.png)

저장한 뒤 재부팅을 해줍니다.
nano에서 저장은 ctrl+x, y를 입력하면 됩니다.

~~~
$sudo reboot
~~~

mnt로 이동하여 마운트가 잘 되었는지 확인해 줍니다.

![]({{ site.img_url }}/rpi_nas/6.png)

초록색으로 하이라이트, 그리고 소유자와 그룹이 pi면 잘 된것입니다.

usb를 제거할 일이 있다면 **언마운트(Unmount)**를 해주어야 합니다.

이는 윈도우의 안전제거와 비슷하다고 보면 됩니다.

~~~
$sudo umount /mnt/usb1 #마운트한 폴더 위치를 적어줍니다.
~~~


### 2. transmission-daemon 설치하기

라즈비안(Raspbian)에서는 transmission이라는 토렌트 클라이언트(torrent client)가 있습니다.

apt-get을 이용하여 간단하게 설치할 수 있습니다.

~~~
$sudo apt-get install transmission-daemon
~~~

[이전편]({{site.url}}/rpi/2017/03/28/rpi-nas-ftp-server.html)에서 ftp를 설정해주듯 transmission도 설정해 줄 것이 있습니다.

~~~
sudo nano /etc/transmission-daemon/settings.json
~~~

여러가지 세팅이 있지만 아래 부분을 먼저 바꾸어 줍니다.

~~~
"download-dir": "/mnt/usb1/completed",
"incomplete-dir": "/mnt/usb1/progress",
"incomplete-dir-enabled": true,
"rpc-password": "패스워드",
"rpc-port": 9091,
"rpc-username": "pi",
"rpc-whitelist-enabled": false,
"umask": 2,
~~~

download-dir : 다운로드한 파일이 저장되는 위치입니다.
incomplete-dir : 다운로드중인 파일이 저장되는 위치입니다.
incomplete-dir-enabled : 다운로드중인 파일의 저장유무를 결정합니다.
rpc-password : rpc기능을 사용할 때 패스워드를 설정합니다. 재부팅시 암호화처리됩니다.
rpc-port : rpc기능을 사용할 포트를 지정합니다. 기본은 9091입니다.
rpc-username : rpc기능을 사용할 때 유저이름입니다.
rpc-whitelist-enabled : 화이트리스트(지정 사용자 이외 금지) 사용 유무를 결정합니다.
umask : 접속권한을 설정합니다.

umask의 기본값은 18인데 이는 022와 같은 의미입니다.

022는 8진수, 이를 10진수로 변환한 것이 18입니다.

umask에 대해서는 [이전편]({{site.url}}/rpi/2017/03/28/rpi-nas-ftp-server.html)에 설명이 되어있으니 참조해 주시기 바랍니다.

설정이 끝나면 파일을 저장하고 설정값을 다시 호출합니다.

~~~
$sudo service transmission-daemon reload
~~~

웹 브라우저를 켜서 transmission에 접속해 보겠습니다.

주소는 라즈베리파이의 ip:포트번호(기본 9091) 형태입니다.

예를들어 ip가 123.456.789.111 이고 포트가 기본값이라면(9091) 주소는 아래와 같습니다.

~~~
123.456.789.111:9091
~~~

![]({{ site.img_url }}/rpi_nas/7.png)

사용자 이름에는 rpc-username을, 비밀번호에는 rpc-password의 값을 입력합니다.

![]({{ site.img_url }}/rpi_nas/8.png)

왼쪽 상단의 서류파일 모양(빨간색 네모)을 클릭하면 토렌트파일을 업로드 할 수 있습니다.

시험용으로 만든 토렌트파일을 업로드 해 보겠습니다.

![]({{ site.img_url }}/rpi_nas/9.png)

다운로드가 완료되었습니다.

![]({{ site.img_url }}/rpi_nas/10.png)

다운로드가 잘 되었는지 확인해 줍니다.

![]({{ site.img_url }}/rpi_nas/11.png)

테스트에 사용한 토렌트파일은 아래 링크에서 다운받을 수 있습니다.

[test_torrent](https://drive.google.com/uc?id=0B_CtpwiAk5hIajd6elJPQlRGLUU)

### 당부의 한마디

**토렌트를 함부로 사용하다가 저작권법 위반으로 처벌받을 수 있습니다.**


## 추가내용

FTP 서버와 연동 사용시에 경로가 /mnt 안일경우 에러가 발생하는 것을 확인했습니다.

따라서 usb 마운트 위치와 transmission의 위치를 변경해 주어야 합니다.

usb 마운트 위치는 fstab의 설정을 바꿔주면 됩니다.

**/etc/fstab**

이부분을
~~~
/dev/sda1 /mnt/usb1 ntfs defaults,uid=1000,gid=1000 0 0
~~~
아래와 같이 바꿔줍니다.
~~~
/dev/sda1 /home/pi/usb1 ntfs defaults,uid=1000,gid=1000 0 0
~~~

transmission의 경우 settings.json을 바꿔주면 됩니다.

**/etc/transmission-daemon/settings.json**

이부분을
~~~
"download-dir": "/mnt/usb1/completed",
"incomplete-dir": "/mnt/usb1/progress",
~~~
아래와 같이 바꿔줍니다.
~~~
"download-dir": "/home/pi/usb1/completed",
"incomplete-dir": "/home/pi/usb1/progress",
~~~


참조 블로그 목록

[https://www.modmypi.com/blog/how-to-mount-an-external-hard-drive-on-the-raspberry-pi-raspian](https://www.modmypi.com/blog/how-to-mount-an-external-hard-drive-on-the-raspberry-pi-raspian)

[http://www.notforme.kr/archives/793](http://www.notforme.kr/archives/793)