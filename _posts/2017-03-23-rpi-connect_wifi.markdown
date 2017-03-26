---
layout: post
title:  "공유기 없이 라즈베리파이와 주변장치 연결하기(ap mode)"
category: rpi
---

얼마 전(사실 몇달 전) 라즈베리파이를 얻게(지원받게)되었습니다.

그 후 이것저것 깨작거리기 시작했습니다.

그러다 알게 된 것이 라즈베리파이3에 내장된 BCM43438 칩이 ap mode를 지원한다는 것이였습니다.

이 말인 즉슨 공유기 없이도 라즈베리파이 - 휴대폰, 라즈베리파이 - 노트북 등 직업 연결이 가능하다는 것이였습니다.

그래서 시도해 보았습니다.

시작하기 전에 필수품인 전원부 준비하려고 보니 권장이 2.5A

5V 2.5A 어댑터가 집에 있을리가 없죠

그래서 그냥 2A짜리 휴대폰 충전기 사용했습니다.

다음으로 micro sd카드... 대충 굴러다니는 8GB 잡아다가 백업-포멧해버렸습니다.

제일 처음 셋업할 때 hdmi케이블 같은게 없으니 이더넷을 이용해서 연결하였습니다.

이제 준비가 끝났으니 시작해 보겠습니다.

![rpi_kit](https://www.dropbox.com/s/30rbxhing24d0sa/rpi_kit.jpg?dl=1){: width="40%" height="40%"}

SSH로 접속하고 로그인 하는 과정은 생략하도록 하겠습니다.  
## **1. 업데이트 & 업그레이드**
~~~
$sudo apt-get update
$sudo apt-get upgrade -y
~~~
## **2. 패키지 설치**
~~~
$sudo apt-get install hostapd -y
$sudo apt-get install dnsmasq -y
~~~
여기서 hostapd는 wifi ap mode로 설정할 때 사용하며

dnsmasq 는 DHCP나 DNS를 설정할 때 사용합니다.

 
## **3. 자동실행 설정**
~~~
$sudo systemctl disable hostapd
$sudo systemctl disable dnsmasq
~~~
여기서 바로 넘어가면 설정이 되지 않은채로 실행되므로 이를 정지시켜 줍니다.
## **4. hostapd 설정**

**# /etc/hostapd/hostapd.conf**
맨 밑에 추가해 주면 됩니다.
~~~
interface=wlan0
driver=nl80211
ssid=RPI3wifi
hw_mode=g
channel=6
wmm_enabled=0
macaddr_acl=0
auth_algs=1
wpa=2
wpa_passphrase=1234567890
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
~~~
대충 보자면 wlan0을 설정하고 ssid를 설정하고 뭐라뭐라 되있는데 솔직히 2개만 신경썼습니다.

ssid랑 wpa_passphrase

ssid는 우리가 와이파이를 켰을 때 보이는 이름이며

wpa_passphrase는 비밀번호입니다.

다른건 드라이버나 채널 암호화 방식등등 입니다.

완료되었다면 저장 후 종료를 해줍니다.

nano 에디터 기준으로 Ctrl + x, y, enter 를 하면 저장 후 종료하게 됩니다.

**# /etc/default/hostapd**
~~~
#demon_conf=""
~~~
부분을
~~~
demon_conf="/etc/hostapd/hostapd.conf"
~~~
로 바꾸어 줍니다.
## **5. dnsmasq 설정**
~~~
**# /etc/dnsmasq.conf
#Pi3Hotspot Config
#stop DNSmasq from using resolv.conf
no-resolv
#Interface to use
interface=wlan0
bind-interfaces
dhcp-range=10.0.0.3,10.0.0.20,12h
~~~
저장-종료를 해줍니다.
## **6. network 설정**
**# /etc/network/interfaces**
~~~
allow-hotplug wlan0
iface wlan0 inet manual
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
~~~
3번째 줄에 #을 추가하여 아래와 같이 바꿔줍니다.
~~~
allow-hotplug wlan0
iface wlan0 inet manual
#wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
~~~

이제 스크립트를 수정해 주어야 합니다.

왜 수정하느냐?

라즈베리파이를 켰을 때 일일이 연결해서(이더넷같은 방법으로) ap mode 켜주고 할 순 없으니까요
## **7. rc.local 설정**
rc.local은 라즈베리파이가 부팅될 대 실행되는 프로그램이나 커맨드에 관한 부분입니다. 자세한 내용은 아래 링크를 참조해 주시기 바랍니다.

[https://www.raspberrypi.org/documentation/linux/usage/rc-local.md](https://www.raspberrypi.org/documentation/linux/usage/rc-local.md)

**# /etc/rc.local**
~~~
#!/bin/sh -e
~~~
위와같이 되어있는 맨 윗줄을
~~~
#!/bin/bash -e
~~~
로 바꾸어 줍니다.

그리고 fi (printf ~~ 바로 아래) 와 exit 0 사이에 아래 스크립트를 추가해 줍니다.
~~~
#Wifi config - if no prefered Wifi generate a hotspot
#RPi Network Conf Bootstrapper
 
createAdHocNetwork()
{
    echo "Creating RPI Hotspot network"
    ifconfig wlan0 down
    ifconfig wlan0 10.0.0.5 netmask 255.255.255.0 up
    service dnsmasq start
    service hostapd start
    echo " "
    echo "Hotspot network created"
    echo " "
}
 
echo "================================="
echo "RPi Network Conf Bootstrapper"
echo "================================="
echo "Scanning for known WiFi networks"
ssids=( 'mySSID1','mySSID2' )
connected=false
for ssid in "${ssids[@]}"
do
    echo " "
    echo "checking if ssid available:" $ssid
    echo " "
    if iwlist wlan0 scan | grep $ssid > /dev/null
    then
        echo "First WiFi in range has SSID:" $ssid
        echo "Starting supplicant for WPA/WPA2"
        wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf > /dev/null 2>&1
        echo "Obtaining IP from DHCP"
        if dhclient -1 wlan0
        then
            echo "Connected to WiFi"
            connected=true
            break
        else
            echo "DHCP server did not respond with an IP lease (DHCPOFFER)"
            wpa_cli terminate
            break
        fi
    else
        echo "Not in range, WiFi with SSID:" $ssid
    fi
done
 
if ! $connected; then
    createAdHocNetwork
fi
~~~
 

제일 처음 고쳤던 sh를 bash로 바꾸는 부분을 잘 몰라서 검색을 해보았습니다.

키워드 : sh vs bash

얻은 링크 : [http://stackoverflow.com/questions/5725296/difference-between-sh-and-bash](http://stackoverflow.com/questions/5725296/difference-between-sh-and-bash)

다음으로 스크립트에 관한 내용입니다.

여기서 신경쓸 부분은

ssids=( 'ssid1', 'ssid2' )

부분입니다.

이 부분은 주변에 와이파이를 스캔해본 뒤 일치하는 ssid가 있으면 wpa_supplicant.conf 에 설정되어 있는데로 연결을 시도하며 그게 아니라면 ap mode로 진입합니다.

위처럼 ',' 를 이용하여 여러개를 넣을 수 있으며 1개만 넣어주어도 됩니다.

일치하는 ssid가 있으면 ap mode로 바뀌지 않으므로 일부러 틀린 ssid를 넣어 와이파이가 공유기에 접속하지 못하게 하였습니다.


저장-종료 후 재부팅을 해줍니다.
~~~
$sudo reboot
~~~
이까지 되었다면 라즈베리파이를 ap mode로 사용할 수 있습니다.

![wifi](https://www.dropbox.com/s/nvqa3lwdsvcfxwc/wifi.png?dl=1){: width="40%" height="40%"}

### **8. 추가사항(필수)**
이대로 진행해보니 에러가 하나 발생하였습니다.

pip를 설치하려는데 에러가 나길레
~~~
$ping google.com
~~~
을 해보니 알 수 없는 주소라는 에러가 출력되었습니다.

그런데
~~~
$ping 8.8.8.8
~~~
은 잘됩니다.

dns 문제인가 싶어 dnsmasq를 먼저 수정해 보았습니다.

하지만 뭘 수정해야 할지 모르므로 구글링

키워드 : dnsmasq raspberry pi

얻은 링크 : [https://www.raspberrypi.org/forums/viewtopic.php?t=46154](https://www.raspberrypi.org/forums/viewtopic.php?t=46154)

중간에  server=8.8.8.8 이라는 부분이 보였습니다.

이를 dnsmasq.conf에 추가해 줍니다.

**#/etc/dnsmasq.conf**
~~~
server=8.8.8.8
~~~
를 맨 마지막에 추가해 주었습니다.

저장-종료 후 재부팅을 해줍니다.
~~~
$sudo reboot
~~~
설정이 잘 되었는지 확인
~~~
$ping google.com
~~~
잘 되는군요.

여기까지 이번 글을 마치도록 하겠습니다.

다음 시간에는 Django 설치법으로 뵙겠습니다.

참고자료 목록

[http://www.raspberryconnect.com/network/item/315-rpi3-auto-wifi-hotspot-if-no-internet](http://www.raspberryconnect.com/network/item/315-rpi3-auto-wifi-hotspot-if-no-internet)
[http://elinux.org/RPi_Setting_up_a_static_IP_in_Debian](http://elinux.org/RPi_Setting_up_a_static_IP_in_Debian)
[https://frillip.com/using-your-raspberry-pi-3-as-a-wifi-access-point-with-hostapd/](https://frillip.com/using-your-raspberry-pi-3-as-a-wifi-access-point-with-hostapd/)
