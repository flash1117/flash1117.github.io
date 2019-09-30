---
layout: post
title:  "python with Flask (3)"
date:   2019-09-30 08:00:59
author: mollangzzang
categories: Web
tags:	backend Flask Python
cover:  "/assets/Flask.png"
---

# Flask

**Main.py**
```
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/')
def index():
    html = render_template('index.html')
    return html

#GET 방식으로 요청시 파라미터 추출
@app.route('/result1')
def result1() :
    a1 = request.args.get("a1")
    a2 = request.args.get("a2")
    a3 = request.args.get("a3")

    # 존재하지 않는 parameter
    a4 = request.args.get("a4")
    # 존재 하지 않는 파라미터일 경우 기본값 세팅
    a5 = request.args.get("a5", 1000)
    # 타입을 지정하면 형변환 해서 반환한다.
    a6 = request.args.get("a6", 0, int)

    print(f'a1 : {type(a1)}') 
    print(f'a6 : {type(a6)}')

    html = render_template('result1.html', a1=a1,a2=a2,a3=a3, a4=a4, a5=a5, a6=a6)
    return html

@app.route('/result2', methods =['get', 'post'])
def result2() :
    a1 = request.form['a1']
    a2 = request.form['a2']
    # a3 = request.form['a3']

    html = render_template('result1.html', a1=a1, a2=a2)
    return html

@app.route('/result3', methods = ['get', 'post'])
def result3() :
    a1 = request.values.get('a1')
    a2 = request.values.get('a2')
    a3 = request.values.get('a3', 300)
    a4 = request.values.get('a4', 0, int) # get post 상관없이 전부 처리 가능

    print(f'a4 {type(a4)}')

    html = render_template('result1.html', a1=a1, a2=a2, a3=a3, a4=a4)
    return html

app.run('0.0.0.0', port=3000, debug=True)

```

`print(f'a1 : {type(a1)}') ` 도메인 주소의 숫자들은 문자열이며, 이를 확인 하기 위한 출력문이다.

**index.html**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <a href="/result1?a1=100&a2=200&a3=300&a6=600">get</a>
    <hr/>
    <form action="/result2" method="post">
        <input type="text" name="a1"/><br/>
        <input type="text" name="a2"/><br/>
        <button type="submit">post</button>

    </form>

    <hr/>
    <a href="result3?a1=100&a2=200&a4=400">get</a>
    <hr/>
    <form action="result3" method="post">
        <input type = "text" name = "a1"/><br/>
        <input type = "text" name = "a2"/><br/>
        <input type = "text" name = "a4"/><br/>
        <button type = "submit">post</button>
    </form>
</body>
</html>
```

위 html 코드를 보면 알겠지만 있는 변수로는 a1, a2, a4 가 있는데 a3은 존재하지 않는다. request 로 a3의 값을 받아오려고 할 때 오류는 뜨지 않고 값을 출력을 받으면 None 값이 뜬다. None 값 대신 존재 하지 않는 값을 위 코드 처럼 입력해 놓을 수 있다.

**result1.html**
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h3>a1 : {{a1}}</h3>
    <h3>a2 : {{a2}}</h3>
    <h3>a3 : {{a3}}</h3>
    <h3>a4 : {{a4}}</h3>
    <h3>a5 : {{a5}}</h3>
    <h3>a6 : {{a6}}</h3>


</body>
</html>
```

단순히 값을 출력 받기 위한 html 파일이다.

