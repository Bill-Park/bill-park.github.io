---
layout: post
title:  "깃헙 페이지 이미지를 aws s3에서 호스팅하기"
categories: [coding]
---

### github page image host on AWS s3

깃헙 페이지를 통해 블로그를 운영하면서 이미지 호스트를 많이 바꿔왔습니다.

처음엔 구글 드라이브를 사용했으나 구글이 막힌 곳이 많아 이미지가 안보이는 경우가 생겼습니다.

그래서 github에 페이지와 동시에 img 폴더를 만들어 호스팅하기 시작했습니다.

막힌 곳도 없었고 집에서 잘 보였기에 신경 쓰지 않고 있었습니다.

어느날 외부에서 usb 테더링으로 블로그를 볼 일이 생겼는데 속도가 너무 느려 이미지가 로딩되는데 1분이 넘게 걸렸습니다.

그래서 aws s3를 이용하여 이미지 호스팅을 해보기로 하였습니다.

[aws s3 바로가기](https://aws.amazon.com/ko/s3/)

![]({{ site.img_url }}/s3_hosting/0.png)

aws s3로 이동하여 **Get started with Amazon S3**를 클릭합니다.

aws 아이디가 있다면 로그인을, 없다면 계정을 생성해 줍니다.

로그인이 완료되면 bucket 목록이 보일 것입니다.

bucket은 파일, 폴더들을 저장하는 최상위 폴더라고 생각하면 됩니다.

![]({{ site.img_url }}/s3_hosting/1.png)

Create bucket을 눌러 bucket을 생성합니다.

![]({{ site.img_url }}/s3_hosting/2.png)

Bucket name은 이미지 주소에 사용되므로 알기 쉽도록 작성합니다.

Region은 서버가 존재하는 지역으로 Asia Pacific (Seoul)을 선택합니다.

입력이 완료되면 Create를 눌러 생성해 줍니다.

새 Bucket이 생성되었습니다.

![]({{ site.img_url }}/s3_hosting/3.png)

생성된 Bucket을 클릭하고 Permissions 탭으로 들어갑니다.

![]({{ site.img_url }}/s3_hosting/4.png)

하단에 Public access의 Everyone을 클릭합니다.

![]({{ site.img_url }}/s3_hosting/5.png)

List objects에 체크해준 뒤 Save를 눌러 저장합니다.

![]({{ site.img_url }}/s3_hosting/6.png)

**This bucket has public access**라는 문구가 나옵니다.

bucket에 아무나 접속(objects를 읽는 권한만 주었습니다)할 수 있다는 주의 문구입니다.

![]({{ site.img_url }}/s3_hosting/7.png)

Overview로 돌아와 Upload를 눌러 이미지를 업로드합니다.

폴더나 이미지를 끌어다 놓아도 되고 Add files를 클릭하여 추가해도 됩니다.

![]({{ site.img_url }}/s3_hosting/8.png)

업로드 된 폴더(혹은 이미지)를 클릭하고 우클릭(혹은 상단의 More클릭) - Make public을 눌러줍니다.

![]({{ site.img_url }}/s3_hosting/9.png)

오브젝트에 대해 **아무나 읽기 가능**권한을 부여한다는 의미입니다.

Make public을 눌러 아무나 읽을 수 있도록 해줍니다.

이로써 아무나 파일을 읽을 수 있습니다.

![]({{ site.img_url }}/s3_hosting/10.png)

업로드 한 파일중 하나를 클릭하여 들어갑니다.

하단에 Link 라는 주소가 보이는데 이것이 이미지의 주소입니다.

![]({{ site.img_url }}/s3_hosting/11.png)

이를 주소창에 넣으면 이미지가 나오게 됩니다.

주소의 일부를 깃헙 페이지의 변수로 만들어 markdown에서 이미지 링크를 추가해 보겠습니다.

먼저 변수로 만들 bucket의 주소를 찾습니다.

이미지의 주소중 bucket name까지 복사해 줍니다.

저는 **https://s3.ap-northeast-2.amazonaws.com/img.psangwoo.com**입니다.

깃헙 페이지 폴더로 이동하여 **_config.yml**파일을 열어줍니다.

메모장이나 vim등 텍스트 에디터를 사용하면 됩니다.

맨 아래에 아래와 같이 추가해 줍니다.

~~~
img_url: "https://s3.ap-northeast-2.amazonaws.com/img.psangwoo.com"
~~~

img_url 변수에 주소값을 저장합니다.

{% raw %}
	{{ site.img_url }}
{% endraw %}

**중괄호 + site.변수명**을 이용하여 변수를 사용할 수 있습니다.

예를 들어 아래 이미지의 주소는 s3_hosting 폴더 안의 sample.png 사진입니다.

![]({{ site.img_url }}/s3_hosting/sample.png)

{% raw %}
	![]({{ site.img_url }}/s3_hosting/sample.png)
{% endraw %}

이상으로 **이미지를 aws s3에서 호스팅하기**를 마칩니다.