## Flask 기초

1. 설치

   ```
   $ sudo pip3 install flask
   ```

2. 기본코드

   ``` python
   # /app.rb  파일이다
   # -*- coding: utf-8 -*-  인코딩 주석이지만 돌아가는 코드가 있다
   from flask import Flask
   app = Flask(__name__)
   
   @app.route("/")
   def hello():
       return "Hello World!"
   ```

3. 서버 실행 명령어

   ```
   $ flask run --host 0.0.0.0 --port 8080
   ```

   * c9 서버에서는 `flask run` 명령어에 host와 port를 직접 설정해줘야한다.

   * 로컬에서 구동시에는 `flask run` 만 해도 되며, 접속 url은 `http://localhost:5000`이 기본이다.

   * `flask run`명령어를 실행할 때, 파일명이 `app.rb`가 아니면 직접 설정해줘야 한다.

     예)만약에 위의 코드가 `application.rb` 로 설정해두었다면 실행코드는 다음과 같다.

     `$ FLASK_APP=hello.py flask run`혹은 `$ export$ FLASK_APP=application.rb`로 환경변수를 설정하고 `$ flask run`을 실행시킨다

4. ` render_template 모듈` 사용하기

   1) render_template 불러오기

   ```python
   # /app.rb
   # -*- coding: utf-8 -*-
   from flask import Flask, render_template
   app = Flask(__name__)
   
   @app.route("/")
   def hello():
       return render_template("index.html")
   ```

   2) `.html`파일 만들기

   ``` html 
   <!-- /templates/index.html -->
   <!Doctype html>
   <html>
       <head>
           <title>프로젝트</title>
       </head>
       <body>
           <h1>안녕!!</h1>
       </body>
   </html>
   ```

   3) python 변수 활용하기

   ```python
   def lunch():
       lunch_box=["멀캠20층", "김밥카페"]
       lunch = random.choice(lunch_Box)
       return render_template("lunch.html", lunch=lunch)
   ```

   ```html
   <!-- /templates/lunch.html -->
   {{lunch}} 꺼내먹어요!
   <hr>
   <p>메뉴 리스트</p>
   {% for menu in lunch_box %}
   	<p>{{menu}}</p>
   {% endfor %}
   ```

5. `layout` 활용하기- `jinja2` 템플릿 활용

   ```html
   <!-- /templates/layout.html -->
   <!Doctype html>
   <html>
       <head>
           <title>{% block title %} {% endblock %}</title>
       </head>
       <body>
       	{% block body %}
   		{% endblock %}
       </body>
   </html>
   ```

   ```html
   <!-- /templates/index.html -->
   {% extends "layout.html" %}
   {% block title %}홈{% endblock %}
   {% block body %}
   	<h1>Hello, world!</h1>
   {% endblock %}
   ```

6. `variable routing`

   ```python
   @app.route('/hello/<string:name>')
   def hello(name):
       return render_template("index.html", name=name) 
   
   @app.route('/cube/<int:num>')
   def cube(num):
       return render_template("cube.html", cube=num*num)
   ```
