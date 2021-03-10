# Mar 09

> Django 실습

### django 프로젝트 만드는 순서

원하는 폴더 만들기

폴더 내에서 vs 코드 실행 후, 터미널 실행

다음 명령어를 통해 프로젝트 디렉토리 생성 ( `django-admin startproject pjt .`)

다음 명령어를 통해 앱 디렉토리 생성 (`python manage.py startapp pages`)

프로젝트 디렉토리의 settings.py 파일에서 `INSTALLED_APPS`내에 앱디렉토리 명을 추가 해줘야 한다.

```
[추가] 서버 실행 명령어 : python manage.py runserver
```



### django 프로젝트 작성 순서

프로젝트 디렉토리의 urls.py

앱단위로 코드가 동작할 수 있도록 하기 위해 `from django.urls import path` 코드 뒤에

`, include`를 추가하여 urls에서 include 함수를 불러온다.



urlpatterns 리스트 내에

`path('pages/', include('pages.urls')),` 를 추가하고

앱 디렉토리에 urls.py 파일을 생성



앱 디렉토리의 urls.py에 코드 작성

```python
from django.urls import path
from . import views

app_name = 'pages' # 앱네임을 쓰는 이유?

urlpatterns = [
    path('index/', views.index, name='index'),
]
```



 









 templates 폴더 안에 base.html 생성

 

pjt폴더의 settings.py 안에 INSTALLED_APPS에 articles 추가





## 느낀점



렉이 너무 심하게 걸리면서 수업을 따라갈 수가 없다.

웹엑스를 다른 노트북으로 틀고 코딩만 하던지 해야할 것 같다.

이번 수업 하나도 못 따라가서 망한 느낌



중간에 다른 노트북으로 웹엑스를 접속하고, 본 노트북으로는 코딩만 진행하니 버벅거리지 않고 잘 진행되었다.



homeworkshop을 통해서 놓친 부분도 일부 되짚을 수도 있어서 좋았던 것 같다.