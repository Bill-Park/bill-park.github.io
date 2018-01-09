---
layout: post
title:  "python으로 telegram bot 활용하기 - 1 기본 설정편"
category: coding
---

텔레그램 봇 만들기 1편(Telegram bot - 3 start)

프로젝트 도중에 휴대폰으로 알림을 주는 기능이 필요해서 찾다가 telegram bot(텔레그램 봇)을 사용하기로 하였습니다.  

telegram bot은 telegram이라는 메신저 앱에서 사용 가능한 bot(로봇과 비슷합니다.)입니다.  

bot은 메세지를 보내거나, 채팅방의 데이터를 수집하는 등 여러 용도로 사용이 가능합니다.  

또한 API가 공개되어 있어 편리하게 사용이 가능하며 얼마 전 지진 경보를 재난안전처보다 빨리 알려주는 '지진희알림'도 Telegram bot을 이용하여 만들어 졌습니다.

시작에 앞서 몇가지 용어를 보고 들어가겠습니다.

~~~
계정 : 하나의 주체입니다.  
사용자 혹은 bot등이 여기 해당됩니다.

채널 : 열린 채팅방입니다.
그룹이 단순히 여러명이 모여 대화를 나누는 곳이라면 여기에는 그 이상의 기능이 가능합니다.  
채널을 공개하여 여러 사람이 들어올 수도 있으며(지진희알림등) 관리자등을 지정하고 이들만 채팅이 가능하도록 하는 등 알림용도로도 사용이 가능합니다.  

BotFather : bot을 생성, 관리할 수 있는 계정(bot 형태)입니다.  
BotFather과 대화로 bot을 생성하고 여러 기능을 설정할 수 있습니다.
~~~

준비물 : 휴대폰에 telegram 어플이 필요합니다. 메세지를 받아야 하니 당연하겠죠?  

대화상대에서 BotFather를 검색하여 추가해 줍니다.

![1](https://drive.google.com/uc?id=0B_CtpwiAk5hIZHA0ZFhEZUhzSTA)

~~~
/start
~~~
![2](https://drive.google.com/uc?id=0B_CtpwiAk5hIejZ1NGdTOWRXVWM)

라는 메세지를 보내면 시작할 수 있습니다. 여러가지 설명이 나오며 bot을 먼저 만들어야 하기에
~~~
/newbot
~~~
를 보냅니다.

그러면 이름을 지어달라고 합니다.

봇의 이름을 지어줍니다.(채팅방에서 보이는 이름입니다.)

원하는 이름을 메세지로 보내면 됩니다.

그러면 username을 지어달라고 합니다. 이는 아이디입니다.

![3](https://drive.google.com/uc?id=0B_CtpwiAk5hIQWhrWElqZnBybnc)

아이콘 바로 옆에있는 bill_bot이 봇의 이름, 아이디에 있는 @로 시작하는 부분이 username입니다.  

봇을 검색할 때 사용됩니다.

전체 과정은 아래와 같습니다.  

(user name 짓는 부분에서 중복되면서 약간의 편집이 있었습니다. 그림판 죄송합니다 ㅠㅠ)

![4](https://drive.google.com/uc?id=0B_CtpwiAk5hIN3JaSUJBT0g0M0E)

마지막에 검은색 박스로 쳐진 부분이 있습니다. 

이 부분은 token(토큰)으로 xxxx:yyyyyy 형태로 이루어 져 있습니다.  

토큰이 있으면 해당 계정(여기서는 봇)의 권한을 거의 전부 사용할 수 있다고 보시면 됩니다.  

그렇기에 관리를 해주시는 것이 필수입니다.

python으로 넘어가기 전에 한가지 준비를 해주어야 합니다.  

현재 봇은 생성되었지만 저에게 메세지를 보낼 수 없습니다.  

왜냐하면 제가 누군지 모르니까요.  

그렇기에 봇에게 먼저 말을 걸어보고 파이썬으로 넘어가도록 하겠습니다.

BotFather를 추가했던 것 처럼 봇의 아이디를 검색하여 채팅을 시작합니다.  

메세지는 아무거나 보내도 됩니다.

이제 코딩을 시작해 보겠습니다.

python에서 저는 telegram api를 사용하기 위해 python-telegram-bot 이라는 모듈을 사용하고 있습니다.  

pip 혹은 소스코드를 직접 내려받아 설치가 가능합니다.

pip를 이용할 경우
~~~
$pip install python-telegram-bot --upgrade
~~~
소스코드를 이용하여 직접 설치할 경우
~~~
$git clone https://github.com/python-telegram-bot/python-telegram-bot
$cd python-telegram-bot
$python setup.py install
~~~

설치가 완료되었다면 토큰을 이용하여 봇을 사용해 보도록 하겠습니다.  

(토큰이 담긴 메세지를 메일로 보내 컴퓨터에서 여는 방식으로 토큰을 입력해주었습니다. 솔직히 어떻게 하나하나 다 치고 있습니까...)
~~~
import telegram   #텔레그램 모듈을 가져옵니다.

my_token = '여기에 토큰을 입력해 주세요'   #토큰을 변수에 저장합니다.

bot = telegram.Bot(token = my_token)   #bot을 선언합니다.

updates = bot.getUpdates()  #업데이트 내역을 받아옵니다.

for u in updates :   # 내역중 메세지를 출력합니다.

print(u.message)
~~~
응답(메세지는 이렇게 많은 데이터를 담고 있습니다. 일부분은 사생활 보호를 위해(?) 삭제하였습니다.)

~~~
{
  'caption':'',
  'text':'봇 테스트',
  'new_chat_title':'',
  'entities':[
  ],
  'delete_chat_photo':False,
  'message_id':6,
  'chat':{
    'username':'보호',
    'title':'',
    'first_name':'보호',
    'id':보호,
    'last_name':'보호',
    'all_members_are_admins':False,
    'type':'private'
  },
  'group_chat_created':False,
  'from':{
    'first_name':'보호',
    'id':보호,
    'last_name':'Park',
    'type':'',
    'username':'bill_park'
  },
  'supergroup_chat_created':False,
  'date':1481120854,
  'migrate_from_chat_id':0,
  'migrate_to_chat_id':0,
  'channel_chat_created':False,
  'new_chat_photo':[
  ],
  'photo':[
  ]
}
~~~
u.message에서 텍스트(내용), 누구한테서 왔는지, 발신자의 id(username과 동일하게 사용됩니다.)등을 볼 수 있습니다.  

만약 수신한 텍스트(내용)만 보려면 u.message.text 를 사용하면 됩니다.

이제 메세지를 보내볼 차례입니다.

메세지를 보내기 위해서는 보낼 상대의 username - api에서 말하는 chat_id를 알아야 합니다.  

bot을 테스트 할 때 메세지를 보내 두었다면 또 위의 예제가 잘 실행되었다면 u.message.chat.id 로 메세지를 보낸 사람의 chat_id를 알아낼 수 있습니다.  

chat 그룹 안의 id부분이 chat_id를 나타내고 있습니다.
~~~
chat_id = bot.getUpdates()[-1].message.chat.id #가장 최근에 온 메세지의 chat id를 가져옵니다

bot.sendMessage(chat_id = chat_id, text="저는 봇입니다.")
~~~
그러면 bot이 메세지를 보낸 것을 확인할 수 있습니다.

![5](https://drive.google.com/uc?id=0B_CtpwiAk5hIOTU1Vk5BUURNY0U)

이상으로 python에서 telegram bot 만들기를 마치도록 하겠습니다.

다음 python - telegram bot 편에서는 봇으로 채널을 이용하는 것을 알아보겠습니다.

[2편 채널편 바로가기]({{ site.url }}/coding/2016/12/11/python-telegram-bot-2.html)

[3편 챗봇편 바로가기]({{ site.url }}/coding/2018/01/09/python-telegram-bot-3.html)
