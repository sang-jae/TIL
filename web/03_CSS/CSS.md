# CSS

> CSS 는 HTML을 꾸미는 언어.

예시 ↓

```css
h1 {
	color: blue;
	font-size: 15px;
}
```

h1 : **선택자**. HTML의 태그를 기준으로도 가능하고 .을 활용하여 class를 기준으로도 가능.

color: blue; : **선언**. 속성: 수치 로 구성된다.

**CSS 정의 방법**

1. inline : 태그 내에 style 속성을 적용해서 정의

   ```html
   <h1 style="color: blue; font-size: 100px">HELLO</h1>
   ```

2. 내부참조 `<head>`태그 내에 `<style> `: head태그 내 style태그를 만들어 그 안에 정의

   ```html
   <head>
   	<style>
   		h1 {
   			color: blue;
   			font-size: 100px;
   		}
   	</style>
   </head>
   ```

3. 외부참조 분리된 CSS 파일 : CSS 파일을 따로 만들고 head태그 내에 link하여 만들어둔 CSS파일을 정의

   ```html
   <head>
   	<link rel="stylesheet" href="mystyle.css">
   </head>
   ```



**CSS 선택자**

CSS 를 통해 "어떤 것" 을 "어떤 형태"로 변경하려고 하면, "어떤 것"을 선택해주는 개념.

homework에 비교하는 문제 확인해볼 것

클래스 선택자(.class {}) , 아이디 선택자 (#id {}) , 속성 선택자 (div {})

중복으로 적용시키고 싶을 때 결합자를 사용

'div > a {}' or 'div span {}' 같은 자손결합자, 자식결합자 homework확인할 것

개발자 도구에서 카피 셀렉터를 하면 된다.



**CSS 적용 우선순위**

!Important 가 가장 중요!!!!

그 후, 인라인 / id 선택자 / class 선택자 / 요소 선택자

homework 확인

퀴즈를 통해서 어떤게 적용이 될지 확인했었음



**CSS 상속**

CSS 상속은 모두 되는 것은 아니다.

즉, "CSS는  상속을 통해 부모 요소의 속성을 모두 자식에게 상속한다." 같은 말은 틀린 것.

상속 되는 예시 : Text 관련 요소 (font color text-align) opacity visibility 등

상속 안되는 예시 : box model 관련 요소 (width height margin padding border box-sizing display) position 관련 요소 (position top right bottom left z-index) 등



**CSS 단위**

크기 5개의 단위 (pixel % em rem viewport 기준 단위) 가 어떻게 다른지?

색상 단위 (RGB (red green blue) 조합 전부 섞이면 흰색.) #16진수로 / rgb() 함수로

```
      (HSL 색상 채도 명도 기준 - 별로 안중요한지 언급 안하심)
```

RGB 색상의 경우. 색상명을 입력한 후, 색상 박스를 클릭하여 나오는 팝업으로 변경 가능

CSS문서 표현 - 패스하심



**CSS Box Model**

모든 요소는 네모 box로 구성되어 있고

content padding border margin으로 구성된다.

박스 사이징은 별로 중요하진 않은 것 같다. 한방에 다 넘어 가셨다.(그래도 한번만 보기)

103~121페이지.

CSS Page layout technique



**CSS Display**

display: block

화면 크기 전체의 가로 폭을 차지. 줄 바꿈이 일어나는 요소이다.

display: inline

content 너비 만큼 가로 폭을 차지. 줄 바꿈이 일어나지 않는 행의 일부 요소.

display: inline-block

두가지를 다 가지고 있다.

속성에 따른 수평정렬하는 방법 (margin-left: auto;)



**CSS Position**

static

absolute

relative

셋의 차이를 파악할 것.

fixed까지 추가

CSS Float

잘 안쓰인다.

뭔지 정의정도만 알면 될 것 같고, 시험문제에도 잘 안나올 것 같다.

float라는게 있구나 정도로만 정의만 알고 있자.

CSS Flexbox

flexbox를 만들기 위해서는 축이 중요하다.

부모 요소에 display: flex; 를 적용시키면서 시작한다.

flex에 적용하는 속성 (각각 안에 어떤 요소들이 있었는지)

flex-direction

justify-content

start / end / between / center / around /

align-items ( align-self / align-content )

Bootstrap

CDN (Content Delivery (Distribution) Network)

컨텐츠(CSS, JS, Image, Text 등) 을 효율적으로 전달하기 위해 여러 노드에 가진 네트워크에 데이터를 제공하는 시스템.

개별 end-user 의 가까운 서버를 통해 빠르게 전달 가능 (지리적 이점) 외부 서버를 활용함으로써 본인 서버의 부하가 적어짐.

CDN으로 가져옴

**spacing (Utilities - spacing)**

margin padding 설정 가능

class naming : `{property}{sides}-{breakpoint}-{size}` 형식

property : m (margin) p (padding)

sides : t (top) b (bottom) s (left in LTR right in RTL) e (right in LTR left in RTL)

​			x (x축 left right 둘다) y (y축 top bottom 둘다) 비워둠 (전부 다)  

size : 0 ~ 5. `1: 0.25 rem`, `2: 0.5 rem`, `3: 1 rem`, `4: 1.5 rem`, `5: 3 rem`

​			 root인 `<html>`의 root 글꼴 크기는 16px. 따라서 1의 경우 4px

 			auto 도 들어갈 수 있음. mx-auto의 경우 수평 중앙정렬 된다.

**color**

부트스트랩의 색상 이름과 색상을 매칭할 수 있어야 한다.

blue - primary / grey - secondary / green - success / red - danger / yellow - warning / 청록(?) - info / 밝은 회색(흰색에 가까운) - light / 검은색 - dark / 흰색 - white / 투명 - transparent

**flexbox**

CSS에서의 명령어와 Bootstrap에서의 차이.

`display: flex;`   →   `class="d-flex"`



**Responsive Web**

Grid System

flex-box로 제작됨

container rows column 으로 컨텐츠를 배치하고 정렬

반드시 기억할 것 2가지 : column 은 12개! / grid breakpoint 는 6개!

homeworkshop 4개는 꼭 다시 보기 베껴서 냈다고 생각하지 마시고..?

서술형이 아닌 문제는 주관식 단답형. 거기에 해당하는 답만 적으면 된다.