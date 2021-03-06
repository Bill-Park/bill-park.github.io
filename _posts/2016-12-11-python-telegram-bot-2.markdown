---
layout: post
title:  "python으로 telegram bot 활용하기 - 2 채널편"
category: coding
---

텔레그램 봇 만들기 2편(Telegram bot - 3 channel)

저번 시간에 이어 telegram bot을 이용하여 채널에 메세지를 보내보도록 하겠습니다.

혹시 telegram bot을 만드는 방법을 모르신다면 저번 시간을 참조해 주시기 바랍니다.

**[1편 기본 설정편 바로가기]({{ site.url }}/coding/2016/12/08/python-telegram-bot-1.html)**

채널이란 공개된 채팅방이라 생각하면 편합니다.  

제가 계속해서 언급하는 '지진희알림'도 채널형태로 정보를 제공하고 있습니다.  

telegram의 채널에는 관리자 라는 개념이 있으며 이들의 권한은 아직 테스트 해보지 못했습니다.

중요한건 봇으로 채널에 메세지를 보내는 것이기에 바로 시작해 보도록 하겟습니다.  
(채널에서 메세지를 읽을 수는 없습니다.)

채널을 만들고 설정해 줍니다. 

이는 사진을 보면서 따라해 보도록 하겠습니다.  

아이폰으로 진행하였으며 안드로이드는 차이가 있을 수 있습니다.  

### 새로운 대화를 시작합니다.  

![]({{ site.img_url }}/telegram/6.png)

### 새로운 채널을 만들어 줍니다.

![]({{ site.img_url }}/telegram/7.png)

### 채널의 이름을 설정하고 다음을 클릭합니다.

![]({{ site.img_url }}/telegram/8.png)

### 저는 비공개를 선택하였습니다.

![]({{ site.img_url }}/telegram/9.png)

### 테스트용이기에 구성원은 패스하겠습니다.

![]({{ site.img_url }}/telegram/10.png)

### 마크를 클릭하여 설정으로 들어갑니다.

![]({{ site.img_url }}/telegram/11.png)

### 중간에 사진이 빠졌지만 채널 정보에서 '관리자'를 클릭한 뒤 관리자 추가를 클릭합니다.

![]({{ site.img_url }}/telegram/12.png)

### 나오는 검색창에서 봇의 아이디를 입력하여 추가해 줍니다.

![]({{ site.img_url }}/telegram/13.png)

### 봇이 메세지를 보낼 수 있게 우측 상단에 '수정' - 링크를 클릭해 줍니다.

![]({{ site.img_url }}/telegram/14.png)

### 링크는 telegram.me/xxx 형태를 가집니다. 여기서 @xxx 가 채널의 아이디가 됩니다. 여기서 만든 링크는 지워주면 동작하지 않습니다.

![]({{ site.img_url }}/telegram/15.png)

## 코딩을 해 주도록 하겠습니다.  

~~~
import telegram

my_token = '토큰값 입력' #토큰을 설정해 줍니다.

bot = telegram.Bot(token = my_token) #봇을 생성합니다.

bot.sendMessage(chat_id='@bill_chat', text="I'm bot") #@bill_chat 으로 메세지를 보냅니다.
~~~
아래와 같이 메세지가 도착했습니다.

![]({{ site.img_url }}/telegram/16.png)

이때 링크가 살아있으면 왠지모를 불안함이 들어 이전 시간에 했던 것 처럼 chat_id를 이용하여 보내보도록 하겠습니다.

사용했던 함수중 bot.sendMessage는 return 값을 가지고 있습니다.  

이 return값에는 updates만큼 많은 데이터가 있고 이중에는 보낼 곳의 주소인 chat_id(우리가 보냈던 @xxx 형태가 아닌 숫자형태의 고유값)도 포함되어 있습니다.  
이를 얻기 위해서는
~~~
id_channel = bot.sendMessage(chat_id='@bill_chat', text="I'm bot").chat_id
~~~
를 이용하면 됩니다. 채널의 chat_id는 -로 시작하는 형태를 띄고 있습니다.(몇번의 테스트에서 모두 이런 특징이 나타났습니다.)

이제 링크를 지워도 id_channel 을 이용하여 메세지를 보낼 수 있습니다.

[3편 챗봇편 바로가기]({{ site.url }}/coding/2018/01/09/python-telegram-bot-3.html)


