# Mar 11

> **Django Project**
>
> Create (생성) / Read (읽기) Update (갱신), Delete (삭제) 를 모두 갖춘 프로젝트

### 오늘 한 내용

Django Model을 통해 데이터를 구조화하고 조작하는 페이지를 만듬.

게시물을 만들고, 수정하고, 삭제할 수 있는 페이지를 제작함.



#### 파일 구성

```python
articles # 앱 디렉토리
  templates
    articles
      index.html
      new.html
      detail.html
      edit.html
  urls.py    
  views.py
  models.py
  ...
crud # 프로젝트 디렉토리
  settings.py #
  urls.py
  ...
```



#### settings.py (crud - 프로젝트 디렉토리)

`INSTALLED_APPS`에 앱 디렉토리 명을 추가

`TEMPLATES`의 `'DIRS'`에 `BASE_DIR / 'curd (아마 프로젝트명) ' / 'templates',` 넣기

`TIME_ZONE`에 `'Asia/Seoul'`로 변경



#### urls.py (crud - 프로젝트 디렉토리)

```python
from django.contrib import admin
# articles.urls를 가져오려면 include 함수가 필요
from django.urls import path, include
# urlpatterns에 호출하기 위해서 articles에 views 를 불러온다.
from articles import views

urlpatterns = [
    path('admin/', admin.site.urls),
    # 주소 뒤에 articles를 붙이면 articles.urls 가져오기
    path('articles/', include('articles.urls')),
    # 기본 주소 뒤에 articles를 안붙여도 자동으로 불러오도록
    path('', views.index),
]
```





#### views.py (articles)

> **들어가기 전에, POST와 GET 메소드의 차이점**
>
> POST 방식은 URL이 아니라 BODY에 데이터를 넣어서 보낸다.
>
> GET은 URL을 `https://urls.com?id=id&title=title&content=content` 형식으로 만들어서 보낸다.



```python
from django.shortcuts import render, redirect
# redirect : 그 url로 이동 (render 처럼 context 값을 넘기지는 못함)
from .models import Article 
# 아래코드에서 .은 현재 폴더를 의미. views.py가 있는 현재 폴더 내의 models파일을 불러온다는 의미

# index.html은 모든 게시물들의 목록을 보여주는 페이지이다.
# 따라서 article에 등록된 모든 오브젝트를 context에 넣고 return.
def index(request):
    articles = Article.objects.all()
    context = {
        'articles': articles
    }
    return render(request, 'articles/index.html', context)

# 특정한 context 없이 new.html을 불러오면 되기 때문에 이 함수는 바로 return만 받는다.
def new(request):
    return render(request, 'articles/new.html')
    

def create(request):
    title = request.POST.get('title')
    content = request.POST.get('content')

    article = Article.objects.create(title=title, content=content)

    context = {
        'article': article
    }
    # return render(request, 'articles/create.html', context)
    return redirect('articles:index')

def detail(request, pk):
    article = Article.objects.get(pk=pk)
    
    context = {
        'article': article
    }

    return render(request, 'articles/detail.html', context)

def delete(request, pk):
    article = Article.objects.get(pk=pk)
    article.delete()

    return redirect('articles:index')


def edit(request, pk):
    article = Article.objects.get(pk=pk)

    context = {
        'article': article
    }
    return render(request, 'articles/edit.html', context)

def update(request, pk):
    # 기존의 정보
    article = Article.objects.get(pk=pk)
    # 새로운 정보
    title = request.POST.get('title')
    content = request.POST.get('content')

    # 기존 정보를 수정
    article.title = title
    article.content = content
    article.save()
    
    return redirect('articles:detail', article.pk)
```



#### urls.py (articles)

```python
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('', views.index, name='index'),
    path('new/', views.new, name='new'),
    path('create/', views.create, name='create'),
    path('<int:pk>/', views.detail, name='detail'),
    path('<int:pk>/delete/', views.delete, name='delete'),
    path('<int:pk>/edit/', views.edit, name='edit'),
    path('<int:pk>/update/', views.update, name='update'),
]

```



#### base.html

> Bootstrap nav-bar를 상단에 추가

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-BmbxuPwQa2lc/FVzBcNJ7UAyJxM6wuqIj61tLrc4wSX0szH/Ev+nYRRuWlolflfl" crossorigin="anonymous">
</head>
<body>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
     <a class="navbar-brand" href="{% url 'articles:index' %}">Home</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <a class="nav-link" href="{% url 'articles:new' %}">New</a>
          <a class="nav-link" href="#">Features</a>
          <a class="nav-link" href="#">Pricing</a>
          <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
        </div>
      </div>
    </div>
  </nav>
  <div class="container">
    {% block content %}
    {% endblock content %}
  </div>


  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/js/bootstrap.bundle.min.js" integrity="sha384-b5kHyXgcpbZJO/tY9Ul7kGkf1S0CWuKcCD38l8YkeH8z8QjE0GmW1gYU5S9FOnJ0" crossorigin="anonymous"></script>
</body>
</html>
```



#### index.html

> Bootstrap 의 table 을 활용하여 리스트 구성

```html
{% extends 'base.html' %}

{% block content %}
  <h1>index</h1>
  <table class="table">
    <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">Title</th>
        <th scope="col">-</th>
      </tr>
    </thead>
    <tbody>
      {% for article in articles %}
        <tr>
          <th scope="row">{{ article.id }}</th>
          <td>{{ article.title }}</td>
          <td><a class="btn btn-primary" href="{% url 'articles:detail' article.pk %}">detail</a></td>
        </tr>
      {% endfor %}
      
    </tbody>
  </table>
{% endblock content %}
```

![CRUD_index_page](C:\Users\sangj\homeworkshop\homeworkshop\workshop\etc\django_03,04_workshop\crud\CRUD_index_page.PNG)

#### new.html

```html
{% extends 'base.html' %}

{% block content %}
  <form action="{% url 'articles:create' %}" method="POST">
    {% csrf_token %}
    <div class="mb-3">
      <label for="title" class="form-label">Title</label>
      <input name="title" type="text" class="form-control" id="title" placeholder="제목을 입력해주세요">
    </div>
    <div class="mb-3">
      <label for="content" class="form-label">Content</label>
      <textarea name="content" class="form-control" id="content" rows="3" placeholder="내용을 입력해주세요"></textarea>
    </div>
    <input type="submit" class="btn btn-primary">
  </form>
  
{% endblock content %}
```

![CRUD_new_page](C:\Users\sangj\homeworkshop\homeworkshop\workshop\etc\django_03,04_workshop\crud\CRUD_new_page.PNG)

#### detail.html

```html
{% extends 'base.html' %}

{% block content %}
  <h2>{{ article.title }}</h2>
  <hr>
  <p>{{ article.content }}</p>
  <a class="btn btn-danger" href="{% url 'articles:delete' article.pk %}">삭제</a>
  <a class="btn btn-warning" href="{% url 'articles:edit' article.pk %}">수정</a>
{% endblock content %}
```

![CRUD_detail_page](C:\Users\sangj\homeworkshop\homeworkshop\workshop\etc\django_03,04_workshop\crud\CRUD_detail_page.PNG)

#### edit.html

```html
{% extends 'base.html' %}

{% block content %}
  <form action="{% url 'articles:update' article.pk %}" method="POST">
    {% csrf_token %}
    <div class="mb-3">
      <label for="title" class="form-label">Title</label>
      <input value="{{ article.title }}" name="title" type="text" class="form-control" id="title" placeholder="제목을 입력해주세요">
    </div>
    <div class="mb-3">
      <label for="content" class="form-label">Content</label>
      <textarea name="content" class="form-control" id="content" rows="3" placeholder="내용을 입력해주세요">{{ article.content }}</textarea>
    </div>
    <input type="submit" class="btn btn-primary">
  </form>
  
{% endblock content %}
```

![CRUD_edit_page](C:\Users\sangj\homeworkshop\homeworkshop\workshop\etc\django_03,04_workshop\crud\CRUD_edit_page.PNG)

