# Feb 04

> HTML, CSS, Bootstrap 실습

### 요약

practice와 homeworkshop을 통해서 bootstrap을 적용시키는 실습을 했다. 거의 하루 종일 실습.

### 느낌

실습을 통해 하니 bootstrap을 사용하기 위해 어떤 클래스를 사용하고 적용해야 하는지는 알 것 같은데, HTML에서 어떤 태그를 써야 제일 적합하게 작동할지에 대한 확신은 아직 안생겼다.

이론적인 공부도 조금 하면서 (과목평가 대비) 내 프로필 사이트를 만들면서 공부해야겠다.

### 공부내용

> 공부하면서 중간중간 기록한 내용. 오늘은 실습 위주였기에, 중간 중간에 몰랐던 내용들을 기록해뒀다.

bootstrap 사이트 - Get started - CSS 와 JS를 불러오는 코드를 각각 head와 body 끝에 추가

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-giJF6kkoqNQ00vy+HMDP7azOuL0xtbfIcaT9wjKHr8RbDVddVHyTfAAsrekwKmP1" crossorigin="anonymous">
</head>
<body>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-ygbV9kiqUc6oa4msXn9868pTtWMgiQaeYH7/t7LECLbyPA2x65Kgf80OJFdroafW" crossorigin="anonymous"></script>
</body>
</html>
```

모든 요소를 container 안에 넣는다고 생각하자.

but container안에 안넣는 예외가 있다. 네비게이션 바나 footer같은 애들



**Bootstrap 사이트의 components 탭에서 자주 쓰는 기능들**

0) 공통 색상?

`primary` : 파란색 / `secondary` : 연한회색 / `success` : 초록색 / `danger` : 빨간색 / `warning` : 노란색 / `info` : 청록색(?) / `light` : 흰색 / `dark` : 검은색, 진한 회색



1) alerts

갖고 있는 class : `alert` / `alert-primary`



2) buttons

button tags 를 알아야 함.

a태그에 btn 클래스 부여.

input 태그에도 btn 클래스 부여. - input은 데이터를 넣을 수 있는 공간일 뿐 링크가 아니라 박스의 형태만 바꾼 거

​	type="submit" 으로 바꾸면 됨.

근데 button은 많이 안쓰일거임.

a 태그는 링크로 가는 기능을 갖고 있고, input은 다른 입력내용을 받아주는 기능을 갖고 있다.

하지만 button 태그는 기능이 따로 없다??



3) Cards

추후에 많이 사용하게될 컴포넌트 중 하나

깔끔한 모습을 갖고 있음

이미지를 넣는 부분. 내용을 넣는 부분. 버튼이 포함된 컴포넌트.

style에 18rem을 지우면, 오른쪽부터 왼쪽까지 전체를 차지하게 된다. 그말은 블럭 속성이라는 것임

인터넷의 이미지를 그대로 가져오려면 주소 복사해서 붙여넣으면 됨



3개를 넣고 가로로 정렬하는 방법?

div.row 에 3개 코드를 넣는다.

```html
    <div class="row">
      <div class="card col-3">
        <img src="..." class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          <a href="#" class="btn btn-primary">Go somewhere</a>
        </div>
      </div>
      <div class="card col-5">
        <img src="..." class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          <a href="#" class="btn btn-primary">Go somewhere</a>
        </div>
      </div>
      <div class="card col-4">
        <img src="..." class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
          <a href="#" class="btn btn-primary">Go somewhere</a>
        </div>
      </div>
    </div>
```





4) Carousel (회전목마)

옆으로 누르면 사진이 넘어가는 기능.

id 값



5) Modal

클릭하면 팝업이 뜨고 display를 none 에서 block으로?????????다시 보기

id값

버튼과 모달의 2개 영역을 구분한다. id 값으로 버튼의 타겟을 모달로 본다. 그 다음 fade라는 속성이 안보이도록 하는건데 show라는 클래스를 추가하면서 보이도록 만들어준다.





6) Navs and tabs

d-flex

justify-content-around





7) Navbar



8) pagination



