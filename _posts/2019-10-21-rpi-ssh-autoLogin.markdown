---
layout: post
title:  "라즈베리파이 자동 로그인하기(raspberry pi auto login with ssh key)"
categories: [rpi]
---

얼마전 라즈베리파이4가 새로 나오고, 다시 ssh를 켜서 작업할 일이 생겼습니다.

보통 windows 유저라면 putty라는 프로그램을 이용하게 됩니다.

기존 설정은 다 어디갔는지 모르겠고 매번 해야하는 로그인은 귀찮습니다.

그래서 자동 로그인을 해보도록 하겠습니다.

**반드시 개인 컴퓨터에서 사용하세요**

### 준비물
1. putty [다운로드](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. puttygen [다운로드](https://www.puttygen.com/#Download_PuTTYgen_on_Windows)
3. ssh 접속 가능한 raspberry pi [구매하기](https://mecha.kr/XqcFgf)

## puttygen으로 키 만들기

puttygen을 실행하여 Generate를 해줍니다.

생성할 키 종류는 RSA로 해주면 됩니다.

만들 때 마우스를 빈 칸 위에서 흔들면 더 빨리 생성됩니다.

![]({{ site.img_url }}/rpi_ssh_auto_login/1.png)

Save private key를 눌러 저장합니다.

**이 파일이 유출되지 않도록 주의하세요**

아직 창을 닫지말고 라즈베리파이 설정으로 넘어갑니다.

## 라즈베리파이 설정하기

평소와 같이 로그인 후 폴더-파일을 생성해 줍니다.

**.ssh**라는 폴더를 만들고 안에 **authorized_keys**라는 파일을 만들어 줍니다.

![]({{ site.img_url }}/rpi_ssh_auto_login/2.png)

puttygen에서 생성한 Public Key를 복사하여 authorized_keys에 넣어줍니다.

![]({{ site.img_url }}/rpi_ssh_auto_login/3.png)

**이 때 한줄로 들어가야 합니다. 줄바꿈이 되면 제대로 인식되지 않습니다.**

![]({{ site.img_url }}/rpi_ssh_auto_login/4.png)

붙여넣기가 완료되면 저장 후 나와줍니다.

## putty 설정하기

자동 로그인을 위해 putty에 private key를 등록해 주어야 합니다.

putty에서 왼쪽 탭의 Connection - SSH - Auth로 이동합니다.

Browse를 클릭하여 puttygen에서 저장한 private key 파일을 불러옵니다.

![]({{ site.img_url }}/rpi_ssh_auto_login/5.png)

제일 처음 Session으로 돌아와 ip를 넣어주고 저장을 해줍니다.

![]({{ site.img_url }}/rpi_ssh_auto_login/6.png)

저장을 하지 않을경우 매번 private key를 불러와야 합니다.

Open을 누르면 username 입력창이 뜨고 pi를 넣어주면 로그인이 됩니다.

![]({{ site.img_url }}/rpi_ssh_auto_login/7.png)

여기서 pi를 입력하는 과정까지 생략해 보겠습니다.

아까 putty에서 저장한 Session을 불러옵니다.

Connection - Data로 이동하여 Auto-login username에 pi를 넣어줍니다.

![]({{ site.img_url }}/rpi_ssh_auto_login/8.png)

다시 Session으로 돌아와 저장을 해준 뒤 Open을 눌러봅니다.

![]({{ site.img_url }}/rpi_ssh_auto_login/9.png)

자동으로 로그인 되는것을 확인할 수 있습니다.