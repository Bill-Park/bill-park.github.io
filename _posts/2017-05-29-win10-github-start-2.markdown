---
layout: post
title:  "Github 시작하기 - CLI 사용하기"
category: coding
---

[GUI 사용하기]({{site.url}}/coding/2017/05/28/win10-github-start-1.html)

git 파일이 있는 곳을 확인해야 합니다.

저번시간에 GUI를 설치하였으므로 환경변수만 추가해 주면 됩니다.

### 1. 환경변수 추가하기

바탕화면의 아이콘을 우클릭하고 **파일 위치 열기**를 클릭합니다.

![1](https://goo.gl/yXHhvk)

GitHubDesktop 폴더가 열립니다.

![2](https://goo.gl/uXTTaU)

**app~**로 들어갑니다.

![3](https://goo.gl/0GdcJL)

**resources**로 들어갑니다.

![4](https://goo.gl/kqS5jO)

**app**으로 들어갑니다.

![5](https://goo.gl/Sb5fcB)

**git**으로 들어갑니다.

![6](https://goo.gl/5SIuem)

**cmd**로 들어갑니다.

![7](https://goo.gl/CiBv2J)

안에 **git**파일이 있습니다.

우클릭 - 속성을 클릭합니다.

![8](https://goo.gl/181eRM)

**위치**를 드래그하여 복사(Ctrl + C)합니다.

![9](https://goo.gl/QcDZvn)

왼쪽에 있는 **내 PC**를 우클릭 - 속성을 클릭합니다.

![10](https://goo.gl/MGskOL)

나오는 화면에서 **고급 시스템 설정**을 클릭합니다.

![11](https://goo.gl/e2Io9q)

**환경 변수**를 클릭합니다.

![12](https://goo.gl/YV7UhG)

**시스템 변수의 Path**를 누른 뒤 **편집**을 클릭합니다.

![13](https://goo.gl/4k4Euj)

**새로 만들기**를 클릭합니다.

![14](https://goo.gl/tsSJkt)

위에서 복사했던 **git** 파일의 위치를 붙여넣고 **확인**을 누릅니다.

![15](https://goo.gl/M3x9Fl)

### 2. 명령 프롬프트에서 git 명령어 사용하기

윈도우키를 누른 뒤 cmd를 입력하여 명령 프롬프트를 실행합니다.

혹은 실행(Ctrl + R)을 누른 뒤 cmd를 입력해도 됩니다.

![16](https://goo.gl/a86mWu)

**git**을 입력하여 경로설정이 잘 되었는지 확인해줍니다.

![17](https://goo.gl/3Hnlis)

cd 명령어를 이용하여 지난 시간에 만든 저장소(repository)가 있는 폴더로 이동합니다.

![18](https://goo.gl/smw5JJ)

git status를 입력하여 현재 상태를 확인합니다.

이는 GUI에서 스크린상에 뜨는 내용입니다.

![19](https://goo.gl/i8q4A4)

메모장을 이용하여 테스트용 파일을 하나 만들어 줍니다.

저장은 저장소가 있는 위치에 해줍니다.

실제 소스코드로 테스트해도 괜찮습니다.

![20](https://goo.gl/FSSAN8)

**git status**를 입력하여 변경된 파일이 있는지 확인합니다.

![21](https://goo.gl/2bRz6X)

**git add .**을 입력하여 변경된 파일을 추가합니다.

GUI에서 commit할 파일을 마우스로 클릭하는 것과 같습니다.

![22](https://goo.gl/yBTfgk)

**git commit -m "commit 내용"**을 입력하여 commit합니다.

commit 내용을 입력하기 위해서 **-m**이 반드시 붙어있어야 합니다.

![23](https://goo.gl/Q5iYM9)

**git push origin master**를 입력하여 저장소에 업로드합니다.

이때 push시 사용하는 User-name과 e-mail을 입력해 주어야 합니다.

![24](https://goo.gl/gI3esJ)

이상으로 CLI에서 사용하는 것까지 알아보았습니다.

이외에도 더 많은 명령어가 있지만 위에서 사용한

status, add, commit, push 이 4가지만 알아도 git을 시작하기에 무리가 없다고 생각합니다.

중간중간 나오는 에러는 검색을 통하여 쉽게 답을 얻을 수 있습니다.(구글링!)

감사합니다.