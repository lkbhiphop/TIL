# HTML

텍스트를 연결시켜주는 링크를 하이퍼링크라한다!

HTML문서는 박스형태로 이루어져있다. 

> 웹페이지를 만들기 위한 언어, 웹브라우저(크롬,파이어폭스,익스플로어X) 위에서 동작

1. #### HTML 형식

      ```html
      <태그명 속성="속성값" 속성2="속성값2 속상값2-1">정보</태그명>
      ```

```HTML
<span id="KOSPI_now" class="num num2">1,996.05</span>
```

트리형태로 이루어져있다(폴더 구조로 존재한다)

결국 HTML문서도 큰 태그안에 태그들이 존재하면서 구성된다.

2. #### HTML 문서의 구조

HTML태그가 모든 태그를 감싸고 있고

head와 body가 안에 들어있다.

meta charset ="utf-8"  이 코드로 한글이 사용이 가능해진다.

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset = "utf-8">
        <title>웹페이지 제목</title>
    </head>
    <body>
    </body>
</html>
```

3. ####  태그

   - link : 문서에 필요한 다른 파일을 가져올 때 사용

   - h1(1~6) : 문서의 제목을 나타냄

     (보통 가장 중요한 레벨을 h1으로 사용함)

   - a : 문서와 문서를 연결시켜주는 주소를 넣는 것! 

     --> 하이퍼링크를 걸어줄것이다

   - div : 여러가지 태그를 하나의 그룹으로 묶음(네모네모)

```html
<link> # 닫는 tag가 필요없는 친구들이다:) 닫는 태그 사이에 정보가 들어갈 필요가 없는 애들이다.

```

# CSS

박스영역에서 이것 저것에 속성을 줄 수 있다. 

1. HTML에서 CSS 사용하기 

​       - 태그안에 넣기

      ```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset = "utf-8"
    </head>
    <body>
        <p style ="background-color:red">안녕하슈</p>
        <h1>반가워유</h1>
        <style>
            h1{background-color:blue}
        </style>
    </body>
</html>
      ```

파일눌러서 preview로 볼 수 있다.

전체박스영역을 차지한다는 것을 볼 수 있다.

