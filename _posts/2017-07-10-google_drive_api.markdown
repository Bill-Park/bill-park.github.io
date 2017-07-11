---
layout: post
title:  "python 구글 드라이브 api로 파일 업로드하기"
category: coding
---

Upload file to google drive using api with python

파이썬과 google drive api를 이용하여 구글 드라이브에 파일을 업로드해 보도록 하겠습니다.

api를 사용하기 위해 권한을 받아야 합습니다.

[https://console.developers.google.com/flows/enableapi?apiid=drive](https://console.developers.google.com/flows/enableapi?apiid=drive)

위 링크에 접속합니다.

![enable_api](https://goo.gl/dVqmTt)

**Create a project**를 선택한 후 **Continue**를 클릭합니다.

![credential](https://goo.gl/1Je92a)

Google Drive Api를 사용할 수 있게 되었습니다.

**Go to credentials**를 클릭합니다.

Cancel을 눌러 빠져나옵니다.

![oauth](https://goo.gl/Mu11tR)

**OAuth consent screen**을 클릭합니다.

![oauth_make](https://goo.gl/x7hMAB)

Email을 확인하고 Product name을 적어줍니다.

save를 눌러 저장해 줍니다.

![credential](https://goo.gl/zMcq23)

Credentials로 돌아와 Create credentials - OAuth client ID를 클릭합니다.

![create_client_id](https://goo.gl/gEJSNE)

Other를 선택하고 Create를 클릭합니다.

![download_json](https://goo.gl/Ajurcy)

나오는 결과창은 OK를 눌러 닫은 뒤 다운로드 마크를 눌러 Json파일을 다운받습니다.

다운받은 json파일은 client_secret_~~~~~~~~~~.json 으로 되어있을 것입니다.

이를 **client_secret_drive.json** 로 바꿔줍니다.

![folder](https://goo.gl/84drra)

작업할 폴더를 만들고(저는 F:\python\drive_api) 안에 json파일을 넣어줍니다.

위와 같은 폴더에 python 스크립트를 만듭니다.

저는 upload_file.py로 하였습니다.

스크립트 작성 전에 pip를 이용하여 패키지를 설치해 줍니다.

~~~
pip install --upgrade google-api-python-client
~~~

스크립트 작성 전 폴더안에 hello.txt라는 파일을 만들어 줍니다.

안의 내용은 아무거나 넣어도 상관없습니다.

python 코드는 아래와 같습니다.

### upload_file.py
~~~
from googleapiclient.discovery import build
from httplib2 import Http
from oauth2client import file, client, tools

try :
    import argparse
    flags = argparse.ArgumentParser(parents=[tools.argparser]).parse_args()
except ImportError:
    flags = None

SCOPES = 'https://www.googleapis.com/auth/drive.file'
store = file.Storage('storage.json')
creds = store.get()

if not creds or creds.invalid:
    print("make new storage data file ")
    flow = client.flow_from_clientsecrets('client_secret_drive.json', SCOPES)
    creds = tools.run_flow(flow, store, flags) \
            if flags else tools.run(flow, store)

DRIVE = build('drive', 'v3', http=creds.authorize(Http()))

FILES = (
    ('hello.txt'),
)

for file_title in FILES :
    file_name = file_title
    metadata = {'name': file_name,
                'mimeType': None
                }

    res = DRIVE.files().create(body=metadata, media_body=file_name).execute()
    if res:
        print('Uploaded "%s" (%s)' % (file_name, res['mimeType']))
~~~

실행시키면 다음과 같은 창이 뜰 것입니다.

![select_google_id](https://goo.gl/X79Ssn)

여러 아이디가 로그인 되어있다면 로그인 할 아이디를 선택해 줍니다.

![api_allow](https://goo.gl/sTJRUL)

허용을 눌러줍니다.

![api_success](https://goo.gl/hwEUj9)

api 사용을 위한 준비가 완료되었습니다.

폴더안에 storage.json이라는 파일이 생성됩니다.

이 파일은 token값등 구글 계정의 권한을 일부 가지고 있으므로 외부 공개를 주의해 주시기 바랍니다.

![upload_end](https://goo.gl/sUihVe)

업로드가 완료되면 위와 같이 출력될 것입니다.

![google_drive](https://goo.gl/hCbXXH)

구글드라이브에 들어가보면 위와같이 업로드가 완료된 것을 볼 수 있습니다.

이상 **python에서 google drive api 사용하여 파일 업로드하기** 입니다.


