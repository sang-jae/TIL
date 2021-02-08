# Bootstrap

CDN (Content Delivery (Distribution) Network)

컨텐츠(CSS, JS, Image, Text 등) 을 효율적으로 전달하기 위해 여러 노드에 가진 네트워크에 데이터를 제공하는 시스템.

개별 end-user 의 가까운 서버를 통해 빠르게 전달 가능 (지리적 이점) 외부 서버를 활용함으로써 본인 서버의 부하가 적어짐.

CDN으로 가져옴

### **spacing (Utilities - spacing)**

margin padding 설정 가능

class naming : `{property}{sides}-{breakpoint}-{size}` 형식

property : m (margin) p (padding)

sides : t (top) b (bottom) s (left in LTR right in RTL) e (right in LTR left in RTL)

​			x (x축 left right 둘다) y (y축 top bottom 둘다) 비워둠 (전부 다)  

size : 0 ~ 5. `1: 0.25 rem`, `2: 0.5 rem`, `3: 1 rem`, `4: 1.5 rem`, `5: 3 rem`

​			 root인 `<html>`의 root 글꼴 크기는 16px. 따라서 1의 경우 4px

 			auto 도 들어갈 수 있음. mx-auto의 경우 수평 중앙정렬 된다.

### **color**

부트스트랩의 색상 이름과 색상을 매칭할 수 있어야 한다.

blue - primary / grey - secondary / green - success / red - danger / yellow - warning / 청록(?) - info / 밝은 회색(흰색에 가까운) - light / 검은색 - dark / 흰색 - white / 투명 - transparent



### **flexbox**

CSS에서의 명령어와 Bootstrap에서의 차이.

`display: flex;`   →   `class="d-flex"`



### **Responsive Web**

**Grid System**

flex-box로 제작됨

container rows column 으로 컨텐츠를 배치하고 정렬

반드시 기억할 것 2가지 : column 은 12개! / grid breakpoint 는 6개!

homeworkshop 4개는 꼭 다시 보기 베껴서 냈다고 생각하지 마시고..?

서술형이 아닌 문제는 주관식 단답형. 거기에 해당하는 답만 적으면 된다.