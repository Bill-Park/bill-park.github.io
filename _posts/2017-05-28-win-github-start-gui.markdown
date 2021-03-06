---
layout: post
title:  "Github 시작하기 - GUI 사용하기"
category: coding
---

git, github은 한번쯤 들어보셨을 것입니다.

물론 사용하고 있거나 사용해본 사람도 많이 있습니다.

기초강의, 시작하기 강의도 많고 Github 공식 홈페이지에도 정말 설명이 잘 되어있습니다.

하지만 CLI 환경에 익숙하지 않거나 영어 울렁증등으로 인하여 멀리하는 사람도 있습니다.

그래서 GUI를 이용하여 github을 사용해 보도록 하겠습니다.

### 1. GitHub 가입하기

[GitHub](https://github.com/) 에 접속합니다.

접속하면 아래와 같이 회원가입(Sign Up)을 할 수 있는 화면이 나옵니다.

![]({{ site.img_url }}/github_gui/1.png)

여기에 정보를 입력해 줍니다.

맨 위는 Username(닉네임) 다음은 email 주소(확인에 사용)입니다.

마지막은 비밀번호입니다.

![]({{ site.img_url }}/github_gui/2.png)

Public repository(공개 저장소)만 사용할 것인지

월 7$에 무제한 private repository(개인 저장소)를 사용할 것인지를 묻습니다.

일단 공개 저장소를 선택하고 Continue를 클릭합니다.

![]({{ site.img_url }}/github_gui/3.png)

관심 항목을 선택하는 부분입니다.

체크해도 되고 맨 밑에 skip this step을 클릭하여 넘겨도 됩니다.

![]({{ site.img_url }}/github_gui/4.png)

가이드 읽기와 프로젝트 시작하기가 있습니다.

바로 Start a project를 눌러줍니다.

![]({{ site.img_url }}/github_gui/5.png)

그럼 이메일을 확인해 달라고 합니다.

처음에 가입할 때 입력한 이메일을 확인합니다.

![]({{ site.img_url }}/github_gui/6.png)

이메일을 보면 링크가 하나 있습니다.

Verify email address 를 눌러도 되고 아래에 있는 https://github.com~~를 눌러도 됩니다.

그럼 위에서 봤던 화면이 다시 나옵니다.

![]({{ site.img_url }}/github_gui/7.png)

이까지가 회원가입이였습니다.

이제 GitHub를 사용하러 가보도록 하겠습니다.

### 2. GitHub 사용하기

GitHub에서 제공하는 파일이 있기에 이를 이용할 것입니다.

[GUI 다운로드](https://desktop.github.com/) 에서 다운받습니다.

![]({{ site.img_url }}/github_gui/8.png)

다운로드가 완료되면 실행시켜 줍니다.

이미 가입을 했으므로 Sign into GitHub.com을 클릭해 줍니다.

![]({{ site.img_url }}/github_gui/9.png)

로그인 화면에서 Username 혹은 email 주소를 입력하고

아래에는 비밀번호를 입력해 줍니다.

![]({{ site.img_url }}/github_gui/10.png)

Name과 Email을 입력해 줍니다.

이는 commit할 때 적용됩니다.

commit은 장소에 변경 내역이 반영하는 것입니다.

![]({{ site.img_url }}/github_gui/11.png)

익명 사용자 정보(anonymous usage data)를 보낼지 여부입니다.

원하시면 체크해 주시면 됩니다.

![]({{ site.img_url }}/github_gui/12.png)

저장소를 만들지 않았기때문에 비어있습니다.

**Create new repository**를 눌러 새 저장소를 만들어 줍니다.

![]({{ site.img_url }}/github_gui/13.png)

저장소의 이름, 위치등을 입력해 줍니다.

![]({{ site.img_url }}/github_gui/14.png)

저장소가 생성되었습니다.

![]({{ site.img_url }}/github_gui/15.png)

이제 파일을 추가해 보겠습니다.

메모장을 열어 문장을 입력한 뒤 저장해 줍니다.

이때 위에서 설정한 저장소 폴더 안에 저장합니다.

(저는 C:\Users\bill\Documents\GitHub)

![]({{ site.img_url }}/github_gui/16.png)

변경된 파일 내역이 보여집니다.

![]({{ site.img_url }}/github_gui/17.png)

Sammary에 commit에 대한 나용을 간단히 적은 뒤 **Commit** 버튼을 눌러줍니다.

Description은 반드시 적지 않아도 됩니다.

![]({{ site.img_url }}/github_gui/18.png)

그러면 Changes에선 사라지고 옆의 History에 가면 변경 내역을 볼 수 있습니다.

![]({{ site.img_url }}/github_gui/19.png)

![]({{ site.img_url }}/github_gui/20.png)

다시 웹브라우저를 열어 Github 홈페이지로 가봅니다.

오른쪽 하단에 보면 내가 만든 Repository(저장소)가 보입니다.

클릭해 봅니다.

![]({{ site.img_url }}/github_gui/21.png)

first.txt가 있는것을 확인할 수 있습니다.

![]({{ site.img_url }}/github_gui/22.png)

여기까지 github GUI 사용법이였습니다.

다음엔 CLI 사용법입니다.

감사합니다.