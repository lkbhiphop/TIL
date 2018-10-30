# telegram bot

### install

- telegram 설치

### bot init

- @BotFather 검색
- start 버튼클릭
- /newbot 입력
- 이름을 생성 => 중복가능
- username => `bot`으로 끝나야하고 유니크한 값

이 과정을 통해 나의 챗봇 url을 받을 수 있고, 접근을 위한 token을 받을 수 있다.

 token은 url을 누가 썼는지 확인하기 위한 것이다(있어야 활성화)

- `token`, `url`
- url 클릭하여 봇 활성화

### telegram.py

- user id 가져오기

```python
import requests
token = "봇의 토큰값"
method_name = "getUpdates"
url = 'https://api.telegram.org/bot{0}/{1}'.format(token,method_name)
print(url)
# url을 해당토큰으로 넣고, 내 url을 업데이트해서 받는다!
print(requests.get(url))
# request.get(url)으로 url주소을 가진 서버에 HTML문서요청을 하고 정보를 얻는다.
```

- 유저에게 메세지 보내기

```python
import requests
token = "763337042:AAEjq0JPofKKdu9_oYwVdi5O5L8JGz_xl6E"
method_name = "getUpdates"
url = 'https://api.telegram.org/bot{0}/{1}'.format(token,method_name)

user_id = 'user_id'
method_name = "sendmessage"
msg = "안녕하세요!!!"
msg_url = 'https://api.telegram.org/bot{0}/{1}?chat_id={2}&text={3}'.format(token,method_name,user_id,msg)
print(msg_url)
print(requests.get(msg_url))
```

- id 값을 json에서 가져와봅시다.

```python
import requests
token = "763337042:AAEjq0JPofKKdu9_oYwVdi5O5L8JGz_xl6E"
method_name = "getUpdates"
url = 'https://api.telegram.org/bot{0}/{1}'.format(token,method_name)
update = requests.get(url).json()

user_id = update["result"][0]['message']['from']['id']
# json 파일에서 result키 리스트 0번째 message 키에 from 키에 id키의 value값
method_name = "sendmessage"
msg = "안녕하세요!!!"
msg_url = 'https://api.telegram.org/bot{0}/{1}?chat_id={2}&text={3}'.format(token,method_name,user_id,msg)
# print(msg_url)
# print(requests.get(msg_url))
```

- 코스피 정보 가져오기

```python
import requests
from bs4 import BeautifulSoup
token = "763337042:AAEjq0JPofKKdu9_oYwVdi5O5L8JGz_xl6E"
method_name = "getUpdates"
url = 'https://api.telegram.org/bot{0}/{1}'.format(token,method_name)
update = requests.get(url).json()

user_id = update["result"][0]['message']['from']['id']
method_name = "sendmessage"

url_cos = "https://finance.naver.com/sise/"
html_cos = requests.get(url_cos).text
soup_cos = BeautifulSoup(html_cos, 'html.parser')
# html에 맞게 text parsing하기
select = soup_cos.select_one('#KOSPI_now')
# KOSPI_now라는 key의 value값(증시가격)뽑아내기

msg = select.text
msg_url = 'https://api.telegram.org/bot{0}/{1}?chat_id={2}&text={3}'.format(token,method_name,user_id,msg)
# print(msg_url)
print(requests.get(msg_url))
requests.get(msg_url)
# get을 통해서 해당 url로부터 HTML문서를 요청하고 받는다.??
```