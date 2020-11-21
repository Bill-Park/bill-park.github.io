---
layout: post
title:  "python으로 telegram bot 활용하기 - 4 Inline Keyboard편"
categories: [coding]
---

텔레그램 봇 만들기 4편(Telegram bot - 4 Inline Keyboard)

텔레그램 봇은 계속 업데이트됩니다.

이번 시간에는 Inline Keyboard를 만들어 보도록 하겠습니다.

[1편 기본 설정편 바로가기]({{ site.url }}/coding/2016/12/08/python-telegram-bot-1.html)

[2편 채널편 바로가기]({{ site.url }}/coding/2016/12/11/python-telegram-bot-2.html)

[3편 챗봇편 바로가기]({{ site.url }}/coding/2018/01/09/python-telegram-bot-3.html)

Inline Keyboard는 선택지를 보여줌으로써 쉽게 선택할 수 있습니다.

### 1. Inline Keyboard 만들기

**/get** 커맨드를 보내면 on,off로 응답하는 형태입니다.

~~~
from telegram.ext import Updater, CommandHandler, CallbackQueryHandler
from telegram import InlineKeyboardButton, InlineKeyboardMarkup

my_token = 'token'

updater = Updater(my_token, use_context=True)

def build_menu(buttons, n_cols, header_buttons=None, footer_buttons=None):
    menu = [buttons[i:i + n_cols] for i in range(0, len(buttons), n_cols)]
    if header_buttons:
        menu.insert(0, header_buttons)
    if footer_buttons:
        menu.append(footer_buttons)
    return menu

def get_command(update, context):
    print("get")
    show_list = []
    show_list.append(InlineKeyboardButton("on", callback_data="on")) # add on button
    show_list.append(InlineKeyboardButton("off", callback_data="off")) # add off button
    show_list.append(InlineKeyboardButton("cancel", callback_data="cancel")) # add cancel button
    show_markup = InlineKeyboardMarkup(build_menu(show_list, len(show_list) - 1)) # make markup

    update.message.reply_text("원하는 값을 선택하세요", reply_markup=show_markup)

get_handler = CommandHandler('get', get_command)
updater.dispatcher.add_handler(get_handler)

updater.start_polling(timeout=1, clean=True)
updater.idle()
~~~

**/get** 커맨드를 보내면 아래와 같이 응답합니다.

![]({{ site.img_url }}/telegram/23.png)

### 2. callback 추가하기

Inline Keyboard만 있을 경우 버튼을 눌러도 아무런 응답이 없습니다.

응답을 위해 callback 추가해 주어야 합니다.

~~~
def get_command(update, context) :
    print("get")
    show_list = []
    show_list.append(InlineKeyboardButton("on", callback_data="on")) # add on button
    show_list.append(InlineKeyboardButton("off", callback_data="off")) # add off button
    show_list.append(InlineKeyboardButton("cancel", callback_data="cancel")) # add cancel button
    show_markup = InlineKeyboardMarkup(build_menu(show_list, len(show_list) - 1)) # make markup

    update.message.reply_text("원하는 값을 선택하세요", reply_markup=show_markup)

def callback_get(update, context):
    print("callback")
    context.bot.edit_message_text(text="{}이(가) 선택되었습니다".format(update.callback_query.data),
                                  chat_id=update.callback_query.message.chat_id,
                                  message_id=update.callback_query.message.message_id)
    
get_handler = CommandHandler('get', get_command)
updater.dispatcher.add_handler(get_handler)
updater.dispatcher.add_handler(CallbackQueryHandler(callback_get))
~~~

**/get** 커맨드를 보낸 후 on을 선택하면 다음과 같이 나옵니다.

![]({{ site.img_url }}/telegram/24.png)

### 3. 여러개의 callback 사용하기

callback이 한번만에 끝나면 좋지만 아닌 경우도 많습니다.

이를 해결하기 위해 InlineKeyboardButton 함수를 보면 callback_data 라는 변수가 있습니다.

callback시 돌아오는 데이터로 보여지는 버튼의 이름과 다를 수 있습니다.

update.callback_query.data로 접근할 수 있습니다.

**,(콤마)**로 callback data를 구분하여 지속적으로 저장하고, 새로운 callback이 있을 때 마다 추가합니다.

**build_button** 이라는 함수를 만들어 주었습니다.

~~~
def build_button(text_list, callback_header = "") : # make button list
    button_list = []
    text_header = callback_header
    if callback_header != "" :
        text_header += ","

    for text in text_list :
        button_list.append(InlineKeyboardButton(text, callback_data=text_header + text))

    return button_list


def get_command(update, context) :
    print("get")
    button_list = build_button(["on", "off", "cancel"]) # make button list
    show_markup = InlineKeyboardMarkup(build_menu(button_list, len(button_list) - 1)) # make markup
    update.message.reply_text("원하는 값을 선택하세요", reply_markup=show_markup) # reply text with markup


def callback_get(update, context) :
    data_selected = update.callback_query.data
    print("callback : ", data_selected)
    if len(data_selected.split(",")) == 1 :
        button_list = build_button(["1", "2", "3", "cancel"], data_selected)
        show_markup = InlineKeyboardMarkup(build_menu(button_list, len(button_list) - 1))
        context.bot.edit_message_text(text="상태를 선택해 주세요.",
                                      chat_id=update.callback_query.message.chat_id,
                                      message_id=update.callback_query.message.message_id,
                                      reply_markup=show_markup)

    elif len(data_selected.split(",")) == 2 :
        context.bot.edit_message_text(text="{}이(가) 선택되었습니다".format(update.callback_query.data),
                                      chat_id=update.callback_query.message.chat_id,
                                      message_id=update.callback_query.message.message_id)
~~~

선택한 값이 누적되어 나오는 것을 볼 수 있습니다.

![]({{ site.img_url }}/telegram/25.png)

### 4. cancel 추가하기

cancel 버튼은 계속 있었지만 cancel처럼 동작하지 않았습니다.

cancel을 cancel답게 해보겠습니다.

~~~
def callback_get(update, context) :
    data_selected = update.callback_query.data
    print("callback : ", data_selected)
    if data_selected.find("cancel") != -1 :
        context.bot.edit_message_text(text="취소하였습니다.",
                                      chat_id=update.callback_query.message.chat_id,
                                      message_id=update.callback_query.message.message_id)
        return

    if len(data_selected.split(",")) == 1 :
        button_list = build_button(["1", "2", "3", "cancel"], data_selected)
        show_markup = InlineKeyboardMarkup(build_menu(button_list, len(button_list) - 1))
        context.bot.edit_message_text(text="상태를 선택해 주세요.",
                                      chat_id=update.callback_query.message.chat_id,
                                      message_id=update.callback_query.message.message_id,
                                      reply_markup=show_markup)

    elif len(data_selected.split(",")) == 2 :
        context.bot.edit_message_text(text="{}이(가) 선택되었습니다".format(update.callback_query.data),
                                      chat_id=update.callback_query.message.chat_id,
                                      message_id=update.callback_query.message.message_id)
~~~

callback_query.data를 참조하여 **cancel**이 있으면 함수를 종료합니다.

![]({{ site.img_url }}/telegram/26.png)


이상으로 **Inline Keyboard**편을 마치도록 하겠습니다.

감사합니다.

