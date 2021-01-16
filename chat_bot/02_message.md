# Chat_bot Basic

나에게 챗봇이 메세지를 보내도록 만드는 과정을 배웠다.

(내가 보낸 내용과 상관 없이, 주소를 실행 시키면 나에게 메세지가 오도록 하는 방법까지 진행)



Bot API에서 사용한 주요 기능

1. making requests

   봇에서 어떤 명령을 내릴지 정하기 위해서는 앞서 setting 에서 언급한 token과 making requests에 적힌 url이 필요하다.

   `url = f'https://api.telegram.org/bot{token}/getMe'`

   여기 token 자리에 발급 받은 토큰을 입력하고, getMe 부분에 아래 기능들을 바꾸어가면서 넣어서 기능을 구현했다.

   

2. getting updates - getUpdates

   봇이 나에게 메세지를 보내기 위해서는 봇이 내 아이디를 알아야 한다.

   getUpdates 를 위 url의 getMe 부분에 넣고, 그 페이지에 들어가면 user_id를 확인할 수 있다.

   

3. available methods - sendMessage

   해당 설명 페이지에 들어가면, 표가 하나 있다.

   그 표에 적힌 규칙대로 하면 대답해줄게~ 라고 하는 기능들이 적혀있는데, 그 중 required 에 yes 가 되어 있는 것들은 **필수요소**이다.

   ​	chat_id : 어떤 chat_id에다가 보낼지

   ​	text : 어떤 내용을 보낼지

   url의 getMe 자리에 sendMessage로 변경한 후, 뒤에는 **필수요소**에 대한 정보를 넣어야 한다.

   url의 규칙 상, 기본 주소가 끝난 후, `?` 이후는 위 요소들에 대한 정보가 들어간다.

   예를 들어, `https://api.telegram.org/bot{token}/sendMessage`뒤에 `?`를 넣고, 
   
   `parameter name = 정보 & parameter name = 정보 & ...`같은 형식으로 진행된다.
   
   이 경우에는 `https://api.telegram.org/bot{token}/sendMessage?chat_id={chat_id}&text={text}`의 형식으로 구성되게 된다.



### message.py 코드

```python
import requests                             # 요청을 보낼 라이브러리 호출
import random								# 로또 번호 추출을 위해 랜덤 라이브러리 호출
from bs4 import BeautifulSoup				# html을 이쁘게 가져오기 위한 라이브러리

token = '비밀'
url = f'https://api.telegram.org/bot{token}/sendMessage'
#sendMessage가 들어간 method_name 구간은 기능에 따라서 변경된다.
chat_id = 비밀

\# 로또 번호 뽑기
\# numbers = range(1, 46)
\# pick = random.sample(numbers, 6)
\# text = pick

\#코스피 정보 가져오기
kospi_url = 'https://finance.naver.com/sise/'
res = requests.get(kospi_url).text # html 코드
soup = BeautifulSoup(res, 'html.parser') #html 코드를 가공
text = soup.select_one('#KOSPI_now').text #.text를 안붙이면 크롬 f12의 한줄

message_url = f'{url}?chat_id={chat_id}&text={text}'
\# print(f'{url}?chat_id={chat_id}&text=안녕하세요')

requests.get(message_url) #저 message_url 위치에 요청 보내줘
```

