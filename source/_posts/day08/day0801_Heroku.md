---
title: "Heroku"
categories:
- Development Settings
output:
 html_document:
   keep_md: true
date: '2022-08-01'
---

### 설치

- 사이트에서 설치 : [https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli](https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli)

![Untitled](/images/day08/day0801_Heroku/Untitled.png)

- github에서 레포만들기
    - 헤로코를 쓰기위해 깃허브에서 레포를 만들때 ‘_’사용금지
    - 모든사람의 레포의 이름이 달라야 한다
    
    ![Untitled](/images/day08/day0801_Heroku/Untitled%201.png)
    
    ![Untitled](/images/day08/day0801_Heroku/Untitled%202.png)
    
- VScode에서 가상환경 만들기

![Untitled](/images/day08/day0801_Heroku/Untitled%203.png)

- 가상환경 접속 후 설치

![Untitled](/images/day08/day0801_Heroku/Untitled%204.png)

![Untitled](/images/day08/day0801_Heroku/Untitled%205.png)

### 배포를 위한 세팅

- 배포할때 requirements.txt파일도 같이 배포해줘야하기 때문에 생성해준다
    
    ![Untitled](/images/day08/day0801_Heroku/Untitled%205.png)
    
- 코드작성

```python
# -*- coding:utf-8 -*-

from flask import Flask

app = Flask(__name__)

@app.route("/") #Rest API 구축
def index():
    return "Hello World!"
```

- 터미널창에서 명력어 실행
    
    ```python
    export FLASK_APP=app
    # 코드상 내가 입력해준 이름
    ```
    
    ```python
    export FLASK_ENV=development
    ```
    
    ```python
    flask run
    ```
    
    ![Untitled](/images/day08/day0801_Heroku/Untitled%206.png)
    
- app.py에 코드추가 작성

```python
if __name__ == '__main__':
    app.run(port=5000)
```

- Procfile 파일생성 후 코드작성

```python
web: gunicorn wsgi:app
```

- [wsgi.py](http://wsgi.py) 파일 생성 후 코드작성

```python
from app import app

if __name__ == "__main__":
    app.run()
```

- 파이썬 버전체크

```python
python -V
```

![Untitled](/images/day08/day0801_Heroku/Untitled%207.png)

- runtime.txt 파일생성

```python
python-3.9.12
```

- git push하기
- 헤로쿠에 로그인

```python
heroku login
```

![Untitled](/images/day08/day0801_Heroku/Untitled%208.png)

```python
heroku create 폴더명
```

![Untitled](/images/day08/day0801_Heroku/Untitled%209.png)

```python
git add .
git commit -m 'updated'
git push
git push heroku main
```

![Untitled](/images/day08/day0801_Heroku/Untitled%2010.png)

### 업그레이드

- Procfile, requirements,runtime,wsgi는 건들지 말라
- app.py파일에 import에 render_template 추가

```python
from flask import Flask, render_template
```

![Untitled](/images/day08/day0801_Heroku/Untitled%2011.png)

- index함수에서 return값 변경

![Untitled](/images/day08/day0801_Heroku/Untitled%2012.png)

- templates 폴더생성
    - index.html 파일 생성
        
        ![Untitled](/images/day08/day0801_Heroku/Untitled%2013.png)
        
    - 코드작성
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>FlaskBlog</title>
    </head>
    <body>
       <h1>aaaaa</h1>
    </body>
    </html>
    ```
    
- static폴더 생성
    - css폴더 생성
        - style.css 파일생성
        
        ![Untitled](/images/day08/day0801_Heroku/Untitled%2014.png)
        

```css
h1 {
    border: 2px #eee solid;
    color: brown;
    text-align: center;
    padding: 10px;
}
```

- index.html에서 <head>에 추가

```html
<link rel="stylesheet" href="{{ url_for('static', filename= 'css/style.css') }}">
```

![Untitled](/images/day08/day0801_Heroku/Untitled%2015.png)