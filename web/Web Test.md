# Web Test

## Homework

### 1-1. HTML 정의

> 아래의 보기 중, HTML의 본딧말을 고르시오.

Hyper Text Markup Language



### 1-2. HTML 개념

> HTML에 대해 T or F

**F 1) 웹 표준을 만드는 곳은 Mozilla 재단이다.**
		W3C.

​		vs WHATWG



**F** **2) 표(table) 을 만들 때에는 반드시 `<th>` 태그를 사용해야 한다.**
		`<th>`태그는 테이블 헤더 태그인데, 가장 위에 들어가고 default 값은 굵은 글씨에 가운데 정렬이다.
		실질적으로 안쓰는 사람이 훨씬 많다. 대부분 `<tr>`태그를 활용하여 테이블 헤더를 만든다.
		table
		ㄴ	table header `<th>` : 표의 제목 셀.
		ㄴ	table row `<tr>` : 표의 행.
		ㄴ	table data `<td>` : `<tr>`태그의 하위
		
		ㄴ	`<thead>` : 표의 제목 영역. `<table>` 하위, `<tr>` 상위
		ㄴ	`<tbody>` : 표의 본문 영역. `<thead>` 와 같은 위치


​		ㄴ	구조
​				ㄴ `<table>`
​						ㄴ `<thead>` , `<tbody>` , `<tfooter>`
​								ㄴ `<tr>`
​										ㄴ `<th>` , `<td>`



**T** **3) 제목(Heading) 태그는 제목 이외에는 사용하지 않는 것이 좋다.**
		시멘틱 태그에 대해 설명하면서 말했음. 사용하면 안된다고 한게 아니라서 T가 맞다.
		권장하는 수준. h1 h2 태그들 말하는 듯??



**F** **4) 리스트를 나열하기 위해서는 `<ul>` 태그만 사용 할 수 있다.**
		`<ul>`: 순서가 필요 없는 목록
		`<ol>` : 순서가 있는 목록
		`<dl>` : 사전처럼 용어를 설명하는 목록
		`<li>` : `<ol>`과 `<ul>`의 각 항목들을 나열할 때 사용하는 태그

**F** **5) HTML의 태그는 반드시 별도의 닫는 태그가 필요하다.**
		필요 없는 것도 있다.
		`<input type="date">`
		그 외 img, link 도 닫는 태그 없음.



### 1-3. CSS 정의

> CSS의 본딧말

Cascading Style Sheets



### 1-4. CSS 개념

> T or F

**T** **1) HTML과 CSS는 각자 문법을 갖는 별개의 언어이다.**

​		HTML 마크업 언어.

​		CSS는 Style sheet 언어.

​		다른 언어는 맞지만 , CSS는 HTML 없이는 존재할 수 없다.

**T** **2) 웹 브라우저는 내장 기본 스타일이 있어 CSS가 없어도 작동한다.**

​		부트스트랩할 때 한번 살펴볼 예정.

​		브라우저 마다 스타일이 조금 씩 다르다.	

**F** **3) 자식 요소 프로퍼티는 부모의 프로퍼티를 모두 상속 받는다.**

​		'모두' 가 틀렸다. box model 관련 요소 (width  height  margin  padding 등은 상속되지 않는다.)

​		다 외울 필요는 없고 , PPT에 나온거 정도는 숙지할 것.

**F** **4) 디바이스마다 화면의 크기가 다른 것을 고려하여 상대 단위인 %를 사용한다.**

​		vp를 사용하는게 맞음.

​		그거까지 반영된 그리드 시스템을 할 예정

**T** **5) id 값은 유일해야 하므로 중복되어서는 안된다.**

​		중복이 될 수는 있지만, 왠만하면 중복 되면 안된다.



### 1-5. CSS 우선순위

!important : 가장 중요

Inline style :

id 선택자 (#)

class 선택자 (.)

요소 선택자 (태그div 등)

소스 순서



### 2-1. Semantic Tag

> 보기 중, 콘텐츠의 의미를 명확히 하기 위해 HTML5에서 새롭게 추가된 시맨틱(semantic) 태그를 모두 고르시오.
>
> `div` , `header` , `h1` , `section` , `footer` , `a` , `form` , `span`

`header` `section` `footer`  (시맨틱 태그 `h1`)



### 2-2. input Tag

> 로그인 Form 생성하는 HTML 코드 작성. 

```html
<div>
  <label for="id">USERNAME : </label>
  <input type="text" id="id" placeholder="아이디를 입력 해 주세요." autofocus>
</div>
<div>
  <label for="pwd">PWD : </label>
  <input type="password" id="pwd" autofocus>
  <input type="submit" value="로그인">
</div>
```

어차피 코드를 작성하라는 문제는 나오지 않는다.

글자 클릭하면 자동으로 input에 focusing 되는 기능 : autofocus 인 듯 하고

label 태그와 input 태그를 활용하였다.

input 태그의 type에는 text와 password submit이 있는데, 각 type에 대해서 input 창에 표시되는 형식이 다른 것 같다.



### 2-3. 크기 단위

> 크기 단위 em은 요소에 지정된 상속된 사이즈나 기본 사이즈에 대해 상대적인 사이즈를 설정한다. 즉, 상속의 영향으로 사이즈가 의도치 않게 변경될 수 있는데 이를 예방하기 위해 HTML 최상위 요소의 사이즈를 기준으로 삼는 크기 단위는?

rem



### 2-4. 선택자

> 다음 예제를 통해 '자손 결합자'와 '자식 결합자' 의 차이를 설명하시오.

```css
div p {
  color: crimson;
}
div > p {
  color: crimson;
}
```

자손 결합자 : div 아래의 모든 p에 대해서

자식 결합자 : div 바로 아래인 p에 대해서 



### 3-1.2.3. Components

1. button
2. navbar
3. pagination



### 3-4. Login Page

text-decoration-none -> text에 있는 밑줄 등의 효과를 없앰. 특히 a태그에서는 파란색 글자에 밑줄이 생기는데 밑줄을 없애준다.



### 4-1. CSS flex-direction

display: flex;

flex-direction: row;

flex-direction: row-reverse;

flex-direction: column;

flex-direction: column-reverse;



### 4-2. Bootstrap flex-direction

d-flex

flex-row

flex-row-reverse

flex-column

flex-column-reverse



### 4-3. Align-items (row direction 기준)

align-items: flex-start;	위로 붙임

align-items: flex-end;	아래로 붙임

align-items: center;		가운데 정렬

align-items: stretch;		늘린다.

![2021-02-08 03;12;55](C:\Users\sangj\OneDrive\바탕 화면\SSAFY\2021-02-08 03;12;55.PNG)



### 4-4. Flex-flow

flex-flow: row wrap;

flex-direction flex-wrap: row wrap;



flex-wrap : flex-item 요소들이 강제로 한 줄에 배치되게 할 것인지 또는 가능한 영역 내에서 벗어나지 않고 여러행으로 나누어 표현할 것인지 결정하는 속성. nowrap / wrap / wrap-reverse



### 4-5. Bootstrap Grid System

(a) container

(b) row 

(c) col-md-3



breakpoints 정리

none	576px 미만

sm		576px 이상

md		768px 이상

lg			992px 이상

xl			1200px 이상

xxl			1400px 이상





## Workshop

### 1-1.2. 파일 경로

절대경로.

```html
<img src="C:\Users\sangj\homeworkshop\homeworkshop\image\web_01_workshop_01.png" alt="ssafy">
```

상대경로.

```html
<img src="..\image\web_01_workshop_01.png" alt="ssafy">
```



### 1-3. Hyper Link





### 1-4. 선택자

`#ssafy > p:nth-child(n)` : 부모 엘리먼트의 '모든' 자식 중, n 번째

​	id가 ssafy인 요소의 자식 요소 중, 2번째를 찾아! 그리고 p태그이면 아래 명령을 수행해

`#ssafy > p:nth-of-type(n)` : 부모 엘리먼트의 'p' 태그 중, n 번째

​	id가 ssafy인 요소의 자식 요소 중, p 태그 중 2번째를 찾아! 그리고 아래 명령을 수행해



### 2-1. Semantic Tag

