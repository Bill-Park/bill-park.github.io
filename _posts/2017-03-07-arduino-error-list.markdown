---
layout: post
title:  "아두이노 에러 리스트(Arduino Error list)"
category: avr_arm
---

아두이노에 업로드 하는 방법에는 여러가지가 있습니다.

최근에는 웹상에서 바로 업로드가 가능하기도 하며 Visual Studio, eclipse 등의 IDE, 그리고 대표적이라 할 수 있는 Arduino IDE가 있습니다.


Arduino IDE는 여러 기능을 갖추고 있으며 그중 하나인 에러 출력이 있습니다.

컴파일과정, 업로드과정등에서 에러가 발생했을 경우 에러코드를 보여줌으로써 디버깅에 편의를 돕습니다.


다만 에러코드는 대부분 영어로 출력되며 의미심장한 말이 많습니다.


구글링을 해도 무슨 말인지 모르는 경우가 많으며 업로드 에러(upload error)의 경우 너무 포괄적인 내용을 담고 있습니다.

그래서 에러의 내용, 해결 방법등을 한글로 정리해보고자 합니다.

에러의 내용은 계속 추가될 것이며 문의사항이 있으시면 하단의 메일로 알려주시기 바랍니다.


본 문서는 Windows 7 Arduino IDE 1.6.8을 기준으로 작성되었습니다.

에러코드의 의미 설명중 번역이 매끄럽지 않을 수 있습니다. 더 좋은 설명이 있다면 제안해 주시기 바랍니다.


## 컴파일 에러


### 1. setup 에러  
~~~
C:\Program Files\Arduino\hardware\arduino\avr\cores\arduino/main.cpp:43: undefined reference to `setup'

collect2.exe: error: ld returned 1 exit status

exit status 1

Error compiling for board Arduino/Genuino Uno..
~~~
**의미** : 해당 경로에 'setup'이 없습니다.

**설명** : 코드에서 기본적으로 있어야 할 setup(C의 main에 해당)이 없을 경우 발생하는 에러

void setup() {} 를 추가해주면 해결된다.

 

### 2. loop 에러  
~~~
C:\Program Files\Arduino\hardware\arduino\avr\cores\arduino/main.cpp:46: undefined reference to `loop'

collect2.exe: error: ld returned 1 exit status

exit status 1

Error compiling for board Arduino/Genuino Uno.
~~~
**의미** : 해당 경로에 'loop'가 없습니다.

**설명** : loop가 없을경우 발생하는 에러

위의 setup에러와 비슷하다 void loop() {}를 추가해주면 해결된다.

 

### 3. ;(세미콜론, semicolon) 에러  
~~~
sketch_apr30a:3: error: expected ',' or ';' before 'void'

void setup() {

^

exit status 1

expected ',' or ';' before 'void'
~~~
**의미** : 'void'이전에 ',' 혹은 ';'가 예상됩니다.

**설명** : C계열의 프로그램에서 끝을 표현하기 위해 사용하는 ;(세미콜론)이 없을경우 발생하는 에러

해당하는 줄에 에러가 발생하는 것이 아니라 다음줄을 기점으로 에러가 발생한다.

위의 경우 void setup() { 이전 문장을 살펴보면 문제를 찾을 수 있다.

 

### 4. :(콜론, colon) 에러  
~~~
sketch_apr30a:1: error: expected ',' or ';' before ':' token

int a = 1 :

^

exit status 1

expected ',' or ';' before ':' token
~~~
**의미** : ':' 이전에 ',' 혹은 ';'가 예상됩니다.

**설명** : ;(세미콜론)대신 :(콜론)을 사용하였을 경우 발생하는 에러

:(콜론)을 ;(세미콜론)으로 바꿔주면 해결된다.

 

### 5. {. } (중괄호) 에러  
~~~
sketch_apr30a:11: error: expected initializer before '}' token

}

^

sketch_apr30a:11: error: expected declaration before '}' token

exit status 1

expected initializer before '}' token

sketch_apr30a.ino: In function 'void loop()':

sketch_apr30a:9: error: expected '}' at end of input

void loop() {

^

exit status 1

expected '}' at end of input
~~~
**의미** : '}' 이전에 생성자 초기화가 예상됩니다.
  끝에 '}'가 예상됩니다.

**설명** : '}' 함수등의 시작이나 끝에 { 혹은 } (중괄호)가 없을 경우 발생하는 에러.

{로 열어주거나 }로 닫히는 부분을 추가해 주시면 됩니다.

 

### 6. 선언되지 않은 변수 또는 함수  ###  사용  
~~~
sketch_apr30a.ino: In function 'void setup()':

sketch_apr30a:3: error: 'a' was not declared in this scope

a = 1 ;

^

exit status 1

'a' was not declared in this scope

sketch_apr30a:6: error: 'func' was not declared in this scope

func(1, 2) ;

^

exit status 1

'func' was not declared in this scope
~~~
**의미** : 'a'는 현재 범위에서 선언되어 있지 않습니다.
  'func'는 현재 범위에서 선언되어 있지 않습니다.

**설명** : 선언되어 있지 않을 경우 발생하는 에러

해당 변수(또는 함수)를 선언해주면 해결된다.

오타로 인하여 자주 발생하는 에러

 

### 7. 헤더파일(또는 라이브러리)을 찾을 수 없음  
~~~
sketch_apr30a.ino:1:17: fatal error: abc.h: No such file or directory

#include <abc.h>

^

compilation terminated.

exit status 1

Error compiling for board Arduino/Genuino Uno.
~~~
**의미** : abc.h : 파일이나 폴더를 찾을 수 없습니다. 컴파일이 종료되었습니다.

**설명** : 헤더파일(또는 라이브러리)을 찾을 수 없을 경우 발생하는 에러

Arduino 폴더 내의 libraries에 헤더파일(또는 라이브러리)을 추가해 주거나 아두이노 도구메뉴의 Sketch - Include Library - Add .ZIP Library... 를 클릭하여 추가해주면 된다.

 

### 8. 함수 사용 실수  
~~~
sketch_apr30a.ino: In function 'void setup()':

sketch_apr30a:11: error: too few arguments to function 'void func(int, int)'

func(1) ;

^

sketch_apr30a.ino:4:6: note: declared here

void func(int a, int b) {

^

exit status 1

too few arguments to function 'void func(int, int)'


sketch_apr30a.ino: In function 'void setup()':


sketch_apr30a:11: error: too many arguments to function 'void func(int)'


func(1, 2) ;


^


sketch_apr30a.ino:4:6: note: declared here


void func(int a) {


^


exit status 1

too many arguments to function 'void func(int)'
~~~
**의미** : 'void func(int, int)'에 너무 적은 인수(arguments)가 사용되었습니다.
  'void func(int, int)'에 너무 많은 인수(arguments)가 사용되었습니다.

**설명** : 함수 사용시에 인수의 개수가 맞지 않을 경우 발생하는 에러

넘겨주어야 할 인수의 개수가 맞는지 살펴본다.

Arduino IDE에서는 Default Parameters(디폴트 매개변수) 사용이 가능하기에 반드시 인자(Parameter, 함수에서 사용)의 개수와 인수(arguments, 함수 호출시 사용)의 개수가 같지는 않다.

### 9. 변수 중복 에러

~~~
exit status 1
conflicting declaration 'int i = 1'
~~~
 
변수가 중복 선언되었을 경우 발생한다.

이미 선언된 변수가 아닌지 확인해 본다.


## 업로드 에러  

 

### 1. 포트 에러  
~~~
avrdude: ser_open(): can't open device "\\.\COM1": 지정된 파일을 찾을 수 없습니다.

Problem uploading to board.  See http://www.arduino.cc/en/Guide/Troubleshooting#upload for suggestions.
~~~
**의미** : 보드에 업로드 중 문제가 발생하였습니다.

**설명** : 해당 포트(위에선 COM1)에서 아무것도 찾지 못하였을 경우 발생하는 에러

USB, 보드가 재대로 연결되어 있는지 확인한다.

정상이라면 COMxx가 재대로 설정되어 있는지 Tools - Port 에서 확인한다.

만약 Tools - Port에서 나오지 않는다면 장치관리자 창에서 드라이버등이 재대로 설치되어 있는지, 케이블등에 문제가 있는것은 아닌지 확인한다.

 

### 2. not in sync 에러  
~~~
avrdude: stk500_getsync(): not in sync: resp=0x00  
~~~
**의미** : sync가 맞지 않습니다. (보드가 응답하지 않습니다.)

**설명** :업로드 과정에서 제일 골치아픈 또 많이 발생하는 에러

보드가 응답하지 않을 경우 발생하는 에러로 원인은 아래와 같다.

1. 드라이버가 재대로 설치되지 않음 - 장치관리자에서 드라이버 제거 후 보드에 맞는 드라이버를 다시 설치한다.

2. USB선, 보드의 USB 포트등의 불량으로 재대로 연결되지 않음 - 다른 보드 혹은 USB로 테스트해본다.

3. 올바르지 않은 보드를 선택한 경우 - Tools - Boards에서 사용중인 보드에 맞게 설정한다.

4. Rx, Tx 바뀜 - USB를 사용할 경우 극히 드문 현상이나 중간 Level Converter(3.3V에 업로드할 경우, 기본적으로 USB는 5V)등을 사용할 경우 종종 발생하는 에러 - 결선이 올바른지 확인한다.

5. 부트로더 깨짐 - 부트로더를 다시 설치한다.

6. FT232, CH340등의 USB - UART 변환장치의 불량 - Arduino Pro mini등 별도의 구성으로 되어있을 경우(Uno, Nano등의 대부분이 내장) 다른 장치로 바꿔 사용해 본다.