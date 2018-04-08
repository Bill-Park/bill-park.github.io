---
layout: post
title:  "python으로 telegram bot 활용하기 - 3 챗봇편"
categories: [coding]
---

텔레그램 봇 만들기 3편(Telegram bot - 3 chat bot)

저번 시간이 마지막이라 생각했지만 하나 더 남아있었습니다.

이번 시간에는 **챗봇**을 만들어 보도록 하겠습니다.

[1편 기본 설정편 바로가기]({{ site.url }}/coding/2016/12/08/python-telegram-bot-1.html)

[2편 채널편 바로가기]({{ site.url }}/coding/2016/12/11/python-telegram-bot-2.html)

텔레그램을 이용한 챗봇은 **무료**라는 장점으로 널리 쓰이고 있습니다.

챗봇을 만들기 위해서는 **토큰**이 필요합니다.

토큰을 이용하여 updater를 만들어 주고 handler를 추가해 주는 형식입니다.

간단한 메세지 응답 챗봇을 만들어 보도록 하겠습니다.

### 1. 메세지 응답하기

~~~
from telegram.ext import Updater, MessageHandler, Filters  # import modules

my_token = ''

print('start telegram chat bot')

# message reply function
def get_message(bot, update) :
    update.message.reply_text("got text")
    update.message.reply_text(update.message.text)
    

updater = Updater(my_token)

message_handler = MessageHandler(Filters.text, get_message)
updater.dispatcher.add_handler(message_handler)

updater.start_polling(timeout=3, clean=True)
updater.idle()

~~~

get_message 함수는 MessageHandler에 의해 호출됩니다.

호출되었을 경우 ***got text*** 와 받은 메세지를 답장합니다.

updater는 봇의 업데이트 사항이 있으면 이를 가져오는 클래스입니다.

Handler는 각종 메세지들을 다루기 위한 클래스입니다.

Filters.text는 텍스트에 대해 응답하며 이때 get_message 함수를 호출합니다.

updater의 dispatcher.add_handler를 이용하여 handler를 추가해 줍니다.

start_polling을 이용하여 polling을 시작합니다. 

timeout은 polling에 걸리는 시간의 최대치를 정해줍니다. 
너무 낮을 경우 polling이 제대로 되지 않을 수 있습니다.

clean을 True로 할 경우 기존에 텔레그램 서버에 저장되어 있던 업데이트 내역을 지웁니다.
내역이 남아있으면 헷갈리는 경우가 있어 True로 해주었습니다.

idle은 updater가 종료되지 않고 계속 실행되어 있도록 하는 함수입니다.

이를 실행시키고 텔레그램에서 봇에 메세지를 보내면 아래와 같이 응답합니다.

![]({{ site.img_url }}/telegram/17.png)

### 2. Command 응답하기

여기에 CommandHandler를 붙여보도록 하겠습니다.

텔레그램에서 Command는 맨 앞에 / 혹은 @(설정했을 경우)가 붙은 메세지를 말합니다.

이 때 메세지는 파란색으로 클릭할 수 있는 형태로 보이게 됩니다.

~~~
from telegram.ext import Updater, MessageHandler, Filters, CommandHandler  # import modules

my_token = ''

print('start telegram chat bot')


# message reply function
def get_message(bot, update) :
    update.message.reply_text("got text")
    update.message.reply_text(update.message.text)


# help reply function
def help_command(bot, update) :
    update.message.reply_text("무엇을 도와드릴까요?")


updater = Updater(my_token)

message_handler = MessageHandler(Filters.text, get_message)
updater.dispatcher.add_handler(message_handler)

help_handler = CommandHandler('help', help_command)
updater.dispatcher.add_handler(help_handler)

updater.start_polling(timeout=3, clean=True)
updater.idle()

~~~

help_command라는 CommandHandler에 의해 호출될 함수를 만들어 줍니다.

CommandHandler에서 ***help***는 ***/help***에 응답합니다.

실행시킨 뒤 /help를 보내봅니다.

![]({{ site.img_url }}/telegram/18.png)

### 3. 사진 응답 및 저장하기

챗봇은 텔레그램을 통해 받은 사진에 대해 응답하고, 챗봇 서버에 저장할 수 있습니다.

~~~
from telegram.ext import Updater, MessageHandler, Filters, CommandHandler  # import modules
import os

my_token = ''

print('start telegram chat bot')

dir_now = os.path.dirname(os.path.abspath(__file__))  # real path to dirname


# message reply function
def get_message(bot, update) :
    update.message.reply_text("got text")
    update.message.reply_text(update.message.text)


# help reply function
def help_command(bot, update) :
    update.message.reply_text("무엇을 도와드릴까요?")


# photo reply function
def get_photo(bot, update) :
    file_path = os.path.join(dir_now, 'from_telegram.png')
    photo_id = update.message.photo[-1].file_id  # photo 번호가 높을수록 화질이 좋음
    photo_file = bot.getFile(photo_id)
    photo_file.download(file_path)
    update.message.reply_text('photo saved')


updater = Updater(my_token)

message_handler = MessageHandler(Filters.text, get_message)
updater.dispatcher.add_handler(message_handler)

help_handler = CommandHandler('help', help_command)
updater.dispatcher.add_handler(help_handler)

photo_handler = MessageHandler(Filters.photo, get_photo)
updater.dispatcher.add_handler(photo_handler)

updater.start_polling(timeout=3, clean=True)
updater.idle()


~~~

os 모듈을 불러온 뒤 dir_now라는 경로를 만들어 줍니다.

이는 받은 사진이 저장될 경로입니다.

get_photo 함수를 보면 **경로 생성 - 받은 사진의 id값 받아오기 - id값을 이용하여 파일 받기**의 순서로 동작합니다.

사진 파일의 경우 받은 업데이트 내역을 보면 여러 종류의 사진을 받습니다.

![]({{ site.img_url }}/telegram/19.png)

제일 마지막 사진이 화질이 제일 좋으므로 -1을 넣어서 마지막 사진을 저장합니다.

MessageHandler와 Filters.photo를 이용하여 사진에 대해 응답하는 Handler를 추가해 줍니다.

![]({{ site.img_url }}/telegram/20.png)

### 4. 파일 응답 및 저장하기

텔레그램에는 여타 메신저들과 같이 파일 전송기능도 가지고 있습니다.

위에서 사진을 저장할 수 있듯 파일도 저장이 가능합니다.

~~~
from telegram.ext import Updater, MessageHandler, Filters, CommandHandler  # import modules
import os

my_token = ''

print('start telegram chat bot')

dir_now = os.path.dirname(os.path.abspath(__file__))  # real path to dirname


# message reply function
def get_message(bot, update) :
    update.message.reply_text("got text")
    update.message.reply_text(update.message.text)


# help reply function
def help_command(bot, update) :
    update.message.reply_text("무엇을 도와드릴까요?")


# photo reply function
def get_photo(bot, update) :
    print("get photo")
    print(update.message)
    file_path = os.path.join(dir_now, 'from_telegram.png')
    photo_id = update.message.photo[-1].file_id  # photo 번호가 높을수록 화질이 좋음
    photo_file = bot.getFile(photo_id)
    photo_file.download(file_path)
    update.message.reply_text('photo saved')


# file reply function
def get_file(bot, update) :
    file_id_short = update.message.document.file_id
    file_url = os.path.join(dir_now, update.message.document.file_name)
    bot.getFile(file_id_short).download(file_url)
    update.message.reply_text('file saved')


updater = Updater(my_token)

message_handler = MessageHandler(Filters.text, get_message)
updater.dispatcher.add_handler(message_handler)

help_handler = CommandHandler('help', help_command)
updater.dispatcher.add_handler(help_handler)

photo_handler = MessageHandler(Filters.photo, get_photo)
updater.dispatcher.add_handler(photo_handler)

file_handler = MessageHandler(Filters.document, get_file)
updater.dispatcher.add_handler(file_handler)

updater.start_polling(timeout=3, clean=True)
updater.idle()


~~~

사진과 마찬가지로 **경로 생성 - 파일의 id값 받아오기 - id값을 이용하여 파일 받기**의 순서로 동작합니다.

Handler를 보면 파일의 경우 Filters.document 형식으로 주의해 주시기 바랍니다.

![]({{ site.img_url }}/telegram/21.png)

이상으로 챗봇편을 마치도록 하겠습니다.

문의사항이 있는 경우 아래 메일로 보내주시면 답변드리도록 하겠습니다.

감사합니다.

