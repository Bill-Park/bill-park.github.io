---
layout: post
title:  "윈도우에서 깃북 제작 및 깃헙 페이지로 호스팅하기"
categories: [coding]
---

## Create Gitbook with GitHub Pages on windows

NUCLEO F103RB 시리즈를 깃북으로 만들면서 여러 어려움이 있었습니다.

자료가 많이 없기도 했지만 그나마 있는 자료도 mac에 맞춰져 있는 등 자료가 너무 빈약했습니다.

그래서 윈도우에서 깃북을 만들고, 깃헙에 호스팅까지 진행해 보겠습니다.

### 1. node js(npm)와 gitbook 설치하기

아래 사이트에서 node js를 설치합니다.

[https://nodejs.org/en/](https://nodejs.org/en/)

작성일(2018-01-31) 기준으로 최신 LTS 버전인 8.9.4를 설치하였습니다.

다운받은 msi파일(윈도우 인스톨러 파일)을 실행하여 설치해 줍니다.

설치가 완료되면 커맨드창을 열어 확인해 줍니다.

~~~
$ node -v
~~~

![]({{ site.img_url }}/gitbook_on_window/1.png)

깃북을 만들 폴더로 이동한 뒤 아래 명령어를 입력하여 깃북을 설치합니다.

~~~
$ npm install gitbook-cli -g
~~~

![]({{ site.img_url }}/gitbook_on_window/2.png)

### 2. Gitbook 만들기

Gitbook init을 실행하여 새로운 Gitbook을 만듭니다.

~~~
$ gitbook init my_gitbook
~~~

![]({{ site.img_url }}/gitbook_on_window/3.png)

my_gitbook 폴더가 생성됩니다.

들어가보면 README.md와 SUMMARY.md라는 파일이 있습니다.

README.md는 표지이며 SUMMARY는 목차를 설정하는 파일입니다.

설정 전에 gitbook에서 파일을 가져오도록 하겠습니다.

마크다운 파일은 posts폴더에, 이미지 파일은 img 폴더에 넣어줍니다.

![]({{ site.img_url }}/gitbook_on_window/4.png)

이제 SUMMARY.md를 열고 목차를 수정해 줍니다.

NUCLEO F103RB 시리즈의 목차는 아래와 같습니다.

#### SUMMARY.md
~~~
# Summary

- [NUCLEO F103RB 시작하기](README.md)
- [LED 켜고 끄기 - LED Blink](posts/2017-09-28-nucleo_f103rb_start.markdown)
- [버튼 입력받기 - Button Input](posts/2017-10-25-nucleo_f103rb_digital_input.markdown)
- [시리얼 통신 - 송수신](posts/2017-11-01-nucleo_f103rb_serial-1.markdown)
- [시리얼 통신 - 수신값으로 GPIO 제어](posts/2017-11-02-nucleo_f103rb_serial-2.markdown)
- [시리얼 통신 - printf 함수 사용](posts/2017-11-03-nucleo_f103rb_serial-3.markdown)
- [ADC 사용하기 - 아날로그 값 읽기](posts/2017-11-14-nucleo_f103rb_adc-1.markdown)
- [ADC 사용하기 - DMA 사용하기](posts/2017-11-25-nucleo_f103rb_adc-2.markdown)
- [타이머 인터럽트 - Timer Interrupt](posts/2017-12-04-nucleo_f103rb_timer_interrupt.markdown)
- [외부 인터럽트 - External Interrupt](posts/2017-12-08-nucleo_f103rb_external_interrupt.markdown)
~~~

gitbook으로 만들기 전 book.json 파일을 만들어 각종 설정을 해줍니다.

#### book.json
~~~
{
    "plugins": ["ga"],
    "pluginsConfig": {
        "ga": {
            "token": "GA 토큰값, 예시 : UA-123456-1"
        }
    },
    "variables": {
        "BASE_URL": "발행할 URL, 예시 : https://blog.psangwoo.com/gb-gitbook_windows"
    }
}
~~~

### 3. Gitbook 발행하기

이제 github에 올려보도록 하겠습니다.

git을 이용하므로 git 저장소로 만들어 줍니다.

~~~
$ git init
~~~

![]({{ site.img_url }}/gitbook_on_window/5.png)

github에서 gitbook을 발행할 레포를 만들고 원격 저장소를 추가해 줍니다.

~~~
$ git remote add origin '저장소의 URL'
~~~

![]({{ site.img_url }}/gitbook_on_window/6.png)

github에서는 GitHub Pages를 2가지 방식을 설정할 수 있습니다.

**1. master branch 전체를 GitHub Pages로 만들기**

**2. /docs 폴더를 GitHub Pages로 만들기**

여기서는 2번째 방법을 사용하도록 하겠습니다.

docs 폴더를 만들고 GitHub Pages를 만들기 위해 아래와 같은 bat 파일을 만들어 줍니다.

#### gitbook_publish.bat
~~~
rd /s /q _book
rd /s /q docs

call gitbook install
call gitbook build

call xcopy _book\*.* docs\ /e /h /k

git clean -fx node_modules
git clean -fx _book

git add .
git commit -a -m "Update docs"
git push -u origin master
~~~

다음과 같이 실행해 줍니다.

~~~
$ gitbook_publish.bat
~~~

![]({{ site.img_url }}/gitbook_on_window/7.png)

명령어들이 순차적으로 입력되면서 git push까지 완료됩니다.

저장소로 가보면 아래와 같이 발행되어 있을 것입니다.

![]({{ site.img_url }}/gitbook_on_window/9.png)

GitHub Pages 설정을 위해 우측 상단에 표시된 Settings를 클릭합니다.

![]({{ site.img_url }}/gitbook_on_window/10.png)

표시된 부분을 **master branch / docs folder** 로 바꾸고 Save를 눌러줍니다.

![]({{ site.img_url }}/gitbook_on_window/11.png)

어느 주소로 publish 되었는지 나오며 링크를 클릭해서 들어가보면 GitBook이 나옵니다.

![]({{ site.img_url }}/gitbook_on_window/12.png)

이상으로 윈도우에서 GitHub Pages를 이용하여 GitBook 만들기를 마치겠습니다.

### 참고 블로그

[https://beomi.github.io/2017/11/20/Deploy-Gitbook-to-Github-Pages/](https://beomi.github.io/2017/11/20/Deploy-Gitbook-to-Github-Pages/)
