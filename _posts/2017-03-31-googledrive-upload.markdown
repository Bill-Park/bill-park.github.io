---
layout: post
title:  "구글 드라이브를 이용하여 지킬에 이미지 올리기"
category: coding
---

## Upload image to Jekyll blog using Google Drive

깃헙페이지(github page)를 이용하여 포스팅을 하다 보면 이미지를 넣어줄 때가 있습니다.

img/ 같은 폴더를 이용하여 이미지 주소로 활용하는 방법도 있습니다.

하지만 양이 많아지면 관리가 힘들 것 같아 이미지 서버를 별도로 두기로 하였습니다.

처음에는 Dropbox를 이용하였으나 트래픽 제한(20GB)과 적은 용량(5GB)으로 아쉬운 점이 있습니다.

차선으로 Google Drive를 찾아보았는데 명시된 트래픽 제한이 없으며 기본 15G를 제공한다는 장점이었습니다.

### 1. 구글 드라이브에 이미지 저장하기

[drive.google.com](drive.google.com)에 접속한 뒤 로그인합니다.

원하는 파일을 끌어다 놓습니다. (드래그 앤 드롭)

그러면 파일이 업로드됩니다.

![drag-and-drop](https://drive.google.com/uc?id=0B_CtpwiAk5hIRDZFYlcySDQ4OE0)

혹은 구글드라이브 PC용을 설치하여 업로드 할 수도 있습니다.

### 2. 사진 업로드하기

지킬(Jekyll)은 마크다운(Markdown)을 이용하여 글을 쓰게(posting) 되어있습니다.

저는 크램다운(kramdown)을 사용하고 있기에 아래와 같은 문법을 사용합니다.

~~~
![설명](주소)
~~~
!는 []안의 내용을 표시하지 않음  
[]는 표시할 내용  
()는 연결될 주소(링크)를 의미합니다.

설명은 표시되지 않으므로 편한 대로 넣어주시면 됩니다.

사진의 주소를 얻기 위해서는 

![get-image](https://drive.google.com/uc?id=0B_CtpwiAk5hIa09XcjFzRzk4R1U)

**파일-우클릭-공유 가능한 링크 가져오기** 를 클릭하면 됩니다.

자동으로 클립보드에 저장되며
~~~
https://drive.google.com/open?id='이미지의 id'
~~~
형태를 가집니다.

이를 아래와 같이 수정해 줍니다.

~~~
https://drive.google.com/uc?id='이미지의 id'
~~~
com/ 뒤에 있는 open?를 uc?로 바꿔주면 됩니다.

이 주소를 이용하여 마크다운 문법에서 이미지를 넣으면 아래와 같습니다.

~~~
![이미지이름](이미지주소)
~~~

그 뒤
~~~
$Jekyll Serve
~~~
를 이용하여 테스트해 줍니다.

만약 주소가 제대로 되어있지 않는다면 아래와 같이 나옵니다.

![crack-image](https://drive.google.com/uc?id=0B_CtpwiAk5hIcXlJdFRmY1FWbGs)

이 경우 주소가 올바른지 확인해 주시기 바랍니다.

주소를 테스트하기 위해서는 웹브라우저의 주소창에 넣어보면 테스트가 가능합니다.
