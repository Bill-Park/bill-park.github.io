---
layout: post
title:  "스마트미러 - 공공데이터 api 사용하기(날씨편)"
category: making
---

스마트미러에 표시할 데이터가 필요하기에 이를 가져와 보도록 하겠습니다.

먼저 기상청의 날씨와 미세먼지 데이터를 가져옵니다.

이는 공공데이터 포털을 이용하여 가져올 수 있습니다.

[www.data.go.kr](https://www.data.go.kr/)에 접속합니다.

![]({{ site.img_url }}/smart_mirror/weather_api/1.png)

아이디가 없다면 회원가입을, 있다면 로그인을 해줍니다.

가운데 검색창에 **동네예보**를 입력합니다.

![]({{ site.img_url }}/smart_mirror/weather_api/2.png)

나오는 목록중 **오픈API**에 있는 **동네예보정보조회서비스**를 클릭합니다.

![]({{ site.img_url }}/smart_mirror/weather_api/3.png)

API 사용신청을 해야합니다.

저는 일반 - 참고자료를 선택했습니다.

![]({{ site.img_url }}/smart_mirror/weather_api/4.png)

어떤 기능의 API를 사용할 것인지 선택해 줍니다.

동네예보를 사용하므로 동네예보에 체크해 줍니다.(전부 체크해도 상관 없습니다.)

그리고 맨 밑 **동의합니다**에 체크해 줍니다.

![]({{ site.img_url }}/smart_mirror/weather_api/5.png)

**신청**를 눌러주면 완료됩니다.

![]({{ site.img_url }}/smart_mirror/weather_api/6.png)

우측 위의 **마이페이지**를 누르면 신청한 목록을 볼 수 있습니다.

승인된 **동네예보정보조회서비스**를 클릭하여 들어갑니다.

![]({{ site.img_url }}/smart_mirror/weather_api/7.png)

**일반 인증키 받기**를 클릭하여 인증키를 신청합니다.

![]({{ site.img_url }}/smart_mirror/weather_api/8.png)

받은 인증키는 최장 1시간 뒤 사용이 가능합니다. 조금만 기다려 주세요.

(인증키 목록이 기상청서버로 1시간마다 전송된다고 합니다.)

![]({{ site.img_url }}/smart_mirror/weather_api/9.png)

스크롤을 밑으로 내려 테스트를 해봅니다.

**실맹**을 눌러 요청변수창을 띄운 뒤 각 값을 넣어줍니다.

ServiceKey :  위에서 받은 **일반 인증키**

base_data : 발표 일자(최근 24시간 데이터만 제공됩니다.)

base_time : 발표 시각(02, 05, 08, 11, 14, 17, 20, 23시에 발표됩니다.)

nx : 예보지점 x좌표값(같이 제공되는 엑셀에서 확인 가능합니다.)

ny : 예보지점 y좌표값(같이 제공되는 엑셀에서 확인 가능합니다.)

numOfRows : 한 페이지 결과 수(높으면 많은 값이 한번에 옵니다.)

pageNo : 페이지 번호입니다.

_type : 받는 값입니다. 기본은 xml이나 json이 조금 더 편해서 json으로 받습니다.

![]({{ site.img_url }}/smart_mirror/weather_api/10.png)

칸을 다 채운 뒤 미리보기를 클릭하면

요청한 api에 대해 응답이 옵니다.

![]({{ site.img_url }}/smart_mirror/weather_api/11.png)

이 과정을 python에서 진행해주어야 합니다.

먼저 api에 요청할 url을 만들어 줍니다.

위에서 사용한 요청변수에 기본 url이 추가된 형태입니다.

기본 url은 **http://newsky2.kma.go.kr/service/SecndSrtpdFrcstInfoService2/ForecastSpaceData?** 입니다.

여기에 각종 값들을 덧붙여주는데 구분은 &로 해주면 됩니다.

예를들어보면

key : abc

date : 20170629

time : 0500

nx : 1

ny : 1

numOfRows : 100

type : json 

일 때 url은 아래와 같습니다.

http://newsky2.kma.go.kr/service/SecndSrtpdFrcstInfoService2/ForecastSpaceData?serviceKey=abc&base_date=20170629&base_time=0500&nx=1&ny=1&numOfRows=100&_type=json

이를 python 코드로 만들어 보겠습니다.

### get_weather_data 함수
~~~
import urllib.request
import json

def get_weather_data() :
    api_date, api_time = get_api_date()
    url = "http://newsky2.kma.go.kr/service/SecndSrtpdFrcstInfoService2/ForecastSpaceData?"
    key = "serviceKey=" + bill.key
    date = "&base_date=" + api_date
    time = "&base_time=" + api_time
    nx = "&nx=97"
    ny = "&ny=76"
    numOfRows = "&numOfRows=100"
    type = "&_type=json"
	api_url = url + key + date + time + nx + ny + numOfRows + type

    data = urllib.request.urlopen(api_url).read().decode('utf8')
    data_json = json.loads(data)
	print(data_json)
~~~

bill.key는 key값(노출을 피해야함)인 관계로 변수를 사용했습니다.

만약 코드를 공개하는 것이 아니라면(github등에 올리지 않는다면) 바로 넣어주어도 됩니다.

예를들어 key값이 "abc"일 경우

~~~
key = serviceKey=abc
~~~

로 해주시면 됩니다.

api_date와 api_time은 매번 바뀌기에 변수로 넣어주었습니다.

이 변수를 가져오는 함수롤 만들어 보겠습니다.

### get_api_date 함수
~~~
import datetime
import pytz

def get_api_date() :
    standard_time = [2, 5, 8, 11, 14, 17, 20, 23] #api response time
    time_now = datetime.datetime.now(tz=pytz.timezone('Asia/Seoul')).strftime('%H') #get hour
    check_time = int(time_now) - 1 
    day_calibrate = 0
	#hour to api time
    while not check_time in standard_time :
        check_time -= 1
        if check_time < 2 :
            day_calibrate = 1 # yesterday
            check_time = 23

    date_now = datetime.datetime.now(tz=pytz.timezone('Asia/Seoul')).strftime('%Y%m%d') #get date
    check_date = int(date_now) - day_calibrate

    return (str(check_date), (str(check_time) + '00')) #return date(yyyymmdd), tt00
~~~

YYYYmmdd, tt+00 형태로 반환됩니다.

예를들어 2017년 6월 30일 오후 17시 발표기준이라면

20170630, 1700 이 반환됩니다.

이제 api에 요청하고 받은 json 데이터를 파싱해 보겠습니다.

파싱을 위해 다음 사이트를 참조합니다.

[http://json.parser.online.fr](http://json.parser.online.fr)

파싱되지 않은 데이터를 넣으면 좀 더 보기 편하게 해줍니다.

![]({{ site.img_url }}/smart_mirror/weather_api/12.png)

난잡하던 데이터가 정리가 됬습니다.

이제 python에서 이를 파싱하고 코드를 합쳐보겠습니다.



### get_api.py

##### [gist에서 보기](https://gist.github.com/Bill-Park/be0c141886a24663325657a437ed4ba4)
~~~
import datetime
import pytz
import urllib.request
import bill
import json

def get_api_date() :
    standard_time = [2, 5, 8, 11, 14, 17, 20, 23]
    time_now = datetime.datetime.now(tz=pytz.timezone('Asia/Seoul')).strftime('%H')
    check_time = int(time_now) - 1
    day_calibrate = 0
    while not check_time in standard_time :
        check_time -= 1
        if check_time < 2 :
            day_calibrate = 1
            check_time = 23

    date_now = datetime.datetime.now(tz=pytz.timezone('Asia/Seoul')).strftime('%Y%m%d')
    check_date = int(date_now) - day_calibrate

    return (str(check_date), (str(check_time) + '00'))

def get_weather_data() :
    api_date, api_time = get_api_date()
    url = "http://newsky2.kma.go.kr/service/SecndSrtpdFrcstInfoService2/ForecastSpaceData?"
    key = "serviceKey=" + bill.key
    date = "&base_date=" + api_date
    time = "&base_time=" + api_time
    nx = "&nx=97"
    ny = "&ny=76"
    numOfRows = "&numOfRows=100"
    type = "&_type=json"
    api_url = url + key + date + time + nx + ny + numOfRows + type

    data = urllib.request.urlopen(api_url).read().decode('utf8')
    data_json = json.loads(data)
	
    parsed_json = data_json['response']['body']['items']['item']

    target_date = parsed_json[0]['fcstDate']  # get date and time
    target_time = parsed_json[0]['fcstTime']

    date_calibrate = target_date #date of TMX, TMN
    if target_time > '1300':
        date_calibrate = str(int(target_date) + 1)

    passing_data = {}
    for one_parsed in parsed_json:
        if one_parsed['fcstDate'] == target_date and one_parsed['fcstTime'] == target_time: #get today's data
            passing_data[one_parsed['category']] = one_parsed['fcstValue']

        if one_parsed['fcstDate'] == date_calibrate and (
                one_parsed['category'] == 'TMX' or one_parsed['category'] == 'TMN'): #TMX, TMN at calibrated day
            passing_data[one_parsed['category']] = one_parsed['fcstValue']

    return passing_data

if __name__ == '__main__':
    print(get_weather_data())
~~~

출력되는 값은 아래 형태입니다.

~~~
{'S06': 0, 'R06': 1.9, 'PTY': 1, 'VEC': 213, 'T3H': 24, 'TMN': 23.0, 'SKY': 4, 'VVV': 1.4, 'POP': 60, 'REH': 90, 'TMX': 30.0, 'WSD': 1.7, 'UUU': 0.9}
~~~

각 값의 의미는 아래와 같습니다.

~~~
POP 강수확률 %-1 %
PTY 강수형태 코드값-1
R06 6시간 강수량범주 (1 mm)-1 mm
REH 습도 %-1 %
S06 6시간 신적설범주(1 cm)-1 cm
SKY 하늘상태 코드값 -1
T3H 3시간 기온 ℃-50 ℃
TMN 아침 최저기온 ℃-50 ℃
TMX 낮 최고기온 ℃-50 ℃
UUU 풍속(동서성분) m/s-100 m/s
VVV 풍속(남북성분) m/s100 m/s
WAV 파고 M-1 m
VEC 풍향 m/s-1
WSD 풍속1-1
~~~

TMX와 TMN은 13시(오후 1시)이후의 데이터일 경우 다음날 값을 받아오도록 해주었습니다.

print된 값을 보면 순서가 섞여있는 것을 볼 수 있습니다.

여기서 원하는 데이터를 얻기 위해 dict 타입으로 값을 저장했습니다.

dict타입에 대한 설명과 이용은 다음시간을 기대해 주세요.
