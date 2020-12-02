---
layout: post
title:  "python with Flask (4)"
date:   2019-10-06 13:01:59
author: mollangzzang
categories: Web
tags:	backend Flask Python
cover:  "/assets/Flask.png"
---

## **HTTP URL 접근 방식**

1. GET - 브라우저가 어떤 페이지에 저장된 정보를 단지 얻기 위해 서버에 요청하고 서버는 그 정보를 보내는 형식으로써 가장 일반적인 메소드이다.

2. HEAD - 브라우저가 어떤 페이지에 저장된 내용이 아니라 헤더라 불리는 정보를 요청한다. 어떤 어플리케이션이 GET 요청을 받은 것 처럼 처리하나, 실제 내용이 전달 되지는 않는다.

3. POST - 브라우저는 서버에게 새로운 정보를 전송하도록 특정 URL에 요청하고 그 정보가 오직 한번 저장되는 것을 보장하도록 한다. 이것이 보통 HTML 폼을 통해서 서버에 데이터 전송하는 방식이다.

4. PUT - POST 와 유사하지만 , 서버가 오래된 값들을 한번 이상 덮어쓰면서 store procedure를 여러번 실행할 수 있다. 전송시 연결을 잃어버리는 경우는 생각해보면, 브라우저와 서버사이에서 정보의 단절없이 요청을 다시 안전하게 받을 수도 있다. POST는 단 한번 요청을 제공하기 떄문에 이런 방식이 불가능하다.

5. DELETE - 주어진 위치에 있는 정보를 제거한다.

6. OPTIONS - 클라이언트에게 요청하는 URL이 어떤 메소드를 지원하는지 알려준다. Flask 0.6 version 부터 이 기능은 자동적으로 구현이 된다.

## **HTTP status code**

400 - bad request
401 - unauthorized
402 - payment required
403 - forbidden
404 - not found
500 - internal server error
501 - not implemented
503 - service unavailable

## error 처리

### error catch
```
@app.errorhandler(403)
def page.forbidden(error):
    print 'not allow this page'
```

### error throw

```
@app.route('/show_infos')
def show_infos():
    if not user.login_in:
        abort(401)

```

## error abort 로 throw

```
from flask import Flask, abort, jsonify

app=Flask(__name__)

@app.route('/abort', methods = ['GET'])
def get_task():
    return abort(404)

if __name__ == '__main__':
    app.run(debug = True)


```

## error abort throw 한 것 잡고 처리

```
from flask import Flask, abort, jsonify, make_response

app = Flask(__name__)

@app.route('/abort', methods =['GET'])
def get_task():
    return abort(404)

@app.errorhandler(404)
def not_found(error):
    return make_response(jsonify({'error':'Notfound'}), 404)

if __name__ == '__main__' :
    app.run(debug=True)
```
