# flask 사용법

일단 flask를 import 해야겟죠? ㅎㅎ

`import flask`

그 다음은 여러 가지 경우의 수를 나눠서 

- ##### 기본함수로 return하기(@app.route("/~~/") )

```python
@app.route("/")
# 해당 url에 다른 요청이 없이 최상단(/)으로 요청했을 경우를 이야기한다.
def helle():
    return "웹페이지는 처음이지?"
```

※주의※ 

local 컴퓨터가 아니라 cloud9은 외부컴퓨터이기 때문에 서버를 reload해줘야 해요

- ##### html 문서를 받아서 return하기

```python
@app.route("/html_file")
def html_file():
    return render_template("file.html")
```

여기선 미리 가상환경 내에 약속한(제가 한게 아니라 원래이렇게 쓰기로 했대요 ㅎㅎ)template 이라는 폴더에 html문서를 만들어 놓으면 render_template() 메소드에서 직접 그 폴더를 찾아준대요 참 편하네요 편~안~

1. flask의 render_template이라는 library를 일단 import한다
2. ` return render_template("<html문서>") `

- ##### html문서에서 입력받은 값을 변수로 사용하여 return하기

  - python코드

    ```python
    def hello_p(name):
        return render_template("hello.html",user_name = name)
    ```

  - html코드

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <h1>방가방가 {{user_name}}</h1>
    </body>
    </html>
    ```



위와 같이 파이썬 코드에서 선언한 <변수>를

HTML파일에서 {{변수}} 의 형식으로 사용할 수 있다.

- ##### html문서에 사진올리는 방법 

  - python코드

    ```python
    @app.route("/lunch_p")
    def lunch_p():
        menu = ["감자","고구마","스파게티","김밥"]
        picture = {"감자":"https://s-i.huffpost.com/gen/3940536/thumbs/o-3-570.jpg?7",
                   "고구마":"https://img1.daumcdn.net/thumb/R720x0/?fname=http://t1.daumcdn.net/liveboard/realfood/bee4ea5e3e8c491d8353e531be0aaec4.jpg",
                   "스파게티":"http://recipe1.ezmember.co.kr/cache/recipe/2015/06/08/a2464362f70de9c32b802926d178cb5a.jpg",
                   "김밥":"http://recipe1.ezmember.co.kr/cache/recipe/2015/04/04/0461907459756bc3a56472da407a1a9d1.jpg"}
        today_menu = random.choice(menu)
        today_picture = picture[today_menu]
        return render_template("lunch.html",text = today_menu, image = today_picture)
    ```

  - HTML코드

    ```HTML
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <h1>오늘의 메뉴는 {{text}} 입니다.</h1>
        <img src={{image}} alt = "음식사진" width = "300" height = "300" >
    </body>
    </html>
    ```

꿀팁은 !누르고 TAB누르면 기본 태그가 생성된다.

img는 닫는 태그가 없어요 더 자세한 내용은 w3school 홈페이지에 예시를 참고하세요 ㅎㅎ

- ##### 검색페이지 엮어서 사용하기(feat. naver)

  - python코드

    ```python
    @app.route("/naver")
    def naver():
        return render_template("naver.html")
    
    ```

  - HTML코드

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <h1>네이버 검색</h1>
        <form action = "https://search.naver.com/search.naver">
            <input type="text" name="query"/> 
            <input type ="submit">
        </form>
    </body>
    </html>
    ```


`<form action = "url">`
 `<input type = "text" name ="query"`
 ?의 전반부인 데이터를 인풋을 받으면 해당 url에
 ?의 후반부인 매개변수(query)에 넣을 text(input)를 받는다.는 의미로 해석할 수 있겠습니다.

그래서 실제 입력창에 검색어를 치면 

`<form action = "url">    `에서 url뒤에 해당 매개변수(query)에 input을 value로 집어넣는다는 의미에요 :-)

- ##### 지금까지 배운 flask를 총망라한 오늘의 미션 제안하기

보기와 같이 input을 받고 actino url경로로 보내기 위한위한 HTML 문서를 먼저 작성했습니다.

  미션을 위해 이름을 받는 아주 간단한 html입니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>오늘 미션 드림 빨리 이름 ㄱㄱ</h1>
    <form action = "/chucheon">
        <input type="text" name="name"/>
        <input type="submit" value="Submit"/>
    </form>
</body>
</html>
```

이건 input을 받기 위한 경로와 미션을 추천해주기 위한 output경로를 작성한 python코드입니다. 

```python

```

심심하신 분들은 밑에 가서 한번 해보세요

(위에 보고 예상하셨겠지만 엄청 재미없어요 ㅎㅎ)

[오늘의미션]("http://ubuntuuu-jackpot2.c9users.io:8080/dododo")





오늘은 flask 기초 사용법에 대해 학습했습니다.

1. @app.route("/~")로 경로 만들기

2. 경로로 직접 return하지 않고 html으로 return하기

   여기서는 render_template("<html문서>") 를 사용

3. 사진 올리는 태그(<img src ="")도 배움

4. 다른 싸이트 엮어서 사용(<form action = "url")

5. html문서에서 매개변수 사용까지!!!

정말 엄청 다양한 걸 배웠던 하루였습니다. 그럼 다들 ㅂㅇㅂㅇ

p.s 

롤충이었던 제게 op.gg사이트를 크롤링해서 했던게 하나 더 있지만 그건 나중에 올리겠습니다. ㅎㅎㅎ

