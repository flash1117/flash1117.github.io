---
layout: post
title:  "python with Flask (2)"
date:   2019-09-30 08:00:59
author: mollangzzang
categories: Web
tags:	backend Flask Python
cover:  "/assets/Flask.png"
---

**Main.py**
```
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/")
def index() :
    html = render_template("index.html")
    return html

# 127.0.0.1 : 3000 / second
# methods : 받아들일 요청 방식을 셋팅. 생략시 get만 받아들임
@app.route("/second", methods=['get', 'post']) # get과 method 방식 둘다 받겠다.
def second() :
    return request.method

app.run('0.0.0.0', port = 3000, debug = True)
```

method 를 전달 받는 방법은 GET 과 POST 두가지 방법이 있는데, 파라미터 방식과 URL 변수 방식이다.

파라미터 방식은 `https:// 주소.com/v1/v2/v3?a1=100&a2=200&a3=300` 과 같이 값마다 이름을 붙인다. 장점으로는 서버쪽에서 이름을 붙여서 도메인을 보내기 때문에 관리하기 용이하다. 다만 단점으로는 URL 변수 방식에 비해 변수등의 이름과 값으로 인해 추측하기가 더 쉬워서 공격에 취약하다는 단점이 있다.

URL 변수 방식은 `https://주소.com/100/200/300`에서 볼 수 있듯이 도메인 주소가 짧다. cilent 쪽에서 도메인이 결정되기 때문에 트래픽이 줄어서 서버의 부담을 줄인다는 장점이 있다.다만 개발자가 변수의 이름이 없고 값만 보이기 떄문에 저 숫자들의 순서에 대해 기억을 하고 있지 않으면 관리하기 힘들다. 또한 파라미터 방식에 비해서 보안이 더 뛰어나다. 저런 특성을 이용하여 숫자 더미값을 추가로 넣기도 한다.

위와 같은 특성을 제외하고 서라도 GET과 POST가 나뉘는 가장 큰 이유는 서버 개발을 할 때 사용한 언어가 지원을 하는가 안하는가의 차이이며, Python은 둘다 사용 가능하다. 다만 html에서 방식에 따라 값을 어떻게 받는지는 약간 차이가 있다.

**index.html**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    {# get 방식 요청 #}
    <a href="/second">get 요청</a>

    {# post 방식 요청 #}
    <form action="/second" method="post">
        <button type="submit">post 요청</button>
    </form>
</body>
</html>
```





