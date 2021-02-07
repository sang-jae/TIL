# HTML

> Hyper Text Markup Language



- 최초의 웹사이트 : https://info.cern.ch  > CERN에서 



- Hyper Text

  정보가 동일 선상에 있어서 책장을 넘기는 거 처럼 한장한장 이어지는 것이 아니라!

  다중으로 연결되어 한 문서에서 다른 문서들로 자유롭게 이동할 수 있는 구조.

  링크에 따라 그 차례가 바뀌는 임의적인 구조를 가진다.

  

- Markup

  단순 텍스트 정보에 구조와 의미를 더하는 것. (태그의 역할. 제목 목차 등)



- HTML

  웹컨텐츠의 의미와 구조를 정의

  확장자는 .html

  CSS를 해제하면 이상하게 텍스트 정보들만 나온다.



### HTML 기본 구조

- 기본 구조

  html 태그 내, head와 body가 들어온다.

  ```html
  <! DOCTYPE html>
  <html lang="ko">
  <head>
  	<meta charset="UTF-8">
  	<title>Document</title>
  </head>
  <body>
  </body>
  </html>
  ```

  **html 요소**

  html 문서의 최상위 요소로 문서의 root를 뜻한다.

  **head**

  문서제목, 문자코드(인코딩)와 같이 해당 문서의 정보를 담고 있으며, 브라우저에 나타나지 않는다.

  CSS선언 및 외부 로딩 파일 지정 등도 작성한다.

  Open Graph Protocol : HTML 문서의 메타데이터를 통해 문서의 정보를 전달하는 규약.

  **body**

  브라우저 화면에 나타나는 정보로 실제 내용에 해당한다.

  

  **DOM (Document Object Model) 트리** : HTML 문서의 프로그래밍 interface

  DOM은 구조화된 표현(structured representation)을 제공하며 그들이 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는다.

  **요소 (Element)**

  (여는/시작)태그  ———————————— (닫는/종료) 태그

  HTML의 요소는 태그와 내용(contents)로 구성되어 있다.

  **속성 (attribute)**

  여는 태그의 태그 뒤에 들어간다.

  ```html
  <a href="<https://google.com>"></a>
  ```

  태그별로 사용할 수 있는 속성은 제각기 다르다.

  속성을 호출할 때 쓰이는 '=' 주변에는 공백을 줄 수 없고, 주소에는 쌍따옴표를 ("") 사용해야 한다.

  a태그 안에 href는 당연히 있어야 한다. 왜냐면 a태그는 href가 없으면 기능을 못한다.

  모든 HTML 요소가 공통으로 사용할 수 있는 속성 : id, class, hidden, lang, style, tabindex, title 등

  일부 요소에는 아무 효과가 없을 수도 있음

  **시맨틱 태그**

  의미론적 요소를 담은 태그.

  header / nav / aside / section / article / footer 등

  단순히 구역을 나누는 것이 아니라, 의미를 가지는 태그를 활용하기 위한 노력

  non semantic 요소 : div, span

  semantic 요소 : h1, table 등

  ### **HTML 문서 구조화**

  인라인 / 블록 요소 : CSS 에서 다룸

  **태그 - 그룹 컨텐츠**

  - `<p>` : paragraph의 P / 단락, 문단, 절

  - `<hr>` : 단락 구분. 문서의 구분선
  - `<ol>` : ordred list. 순서가 있고, 앞에 넘버링이 붙는다.
  - `<ul>` : unordered list. 순서가 없고, 앞에 기호가 붙는다.
  - `<pre>` :
  - `<blockquote>` :
  - `<div>` : division의 약자. 문서 영역이나 섹션의 분할을 정의.

  **태그 - 텍스트 관련 요소**

  - `<a>` : ahchor. 링크 연결. ( href="link" )
  - `<b>` : bold. 진하게. 의미없이 진하게 표시할 때
  - `<strong>` : 내용의 강조를 위해 진하게 표시하는 경우.
  - `<i>` : italic. 기울임. 의미 없이 기울임꼴로 표시할 때
  - `<em>` : 내용의 강조를 위해 기울임꼴로 표시하는 경우.
  - `<span>` : 아무 의미 없이. 문서 영역이나 섹션의 분할을 정의. `<div>`와의 차이는 `<div>`는 줄바꿈이 있고, `<span>`은 줄바꿈이 없다.
  - `<br>` : 줄바꿈. 닫는 태그가 없다.
  - `<img>` : 이미지를 넣는 태그. 태그 하나 당 1개의 이미지
  - 기타 등등

  **태그 - table**

  - `<tr>`
  - `<td>`
  - `<th>`
  - `<thead>`
  - `<tbody>`
  - `<tfoot>`
  - `<caption>`
  - 셀 병합 속성 : colspan, rowspan
  - scope 속성
  - `<col>`
  - `<colgroup>`

  **태그 - form**

  - 서버에서 처리될 데이터를 제공하는 역할
  - 기본속성 : action / method

  **태그 - input**

  - 다양한 타입을 가지는 입력 데이터 필드
  - `<label>` : 서식 입력 요소의 캡션
  - 

  form은 넘어가도 됨.

  무슨 태그를 사용할 수 있는지 정도를 알아두면 되겠다.