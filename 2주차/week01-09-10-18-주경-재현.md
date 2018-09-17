# Today I Learned
## 에이전트 기본스타일 초기화시키기
  ## Reset : 모든 여백을 0으로 만들어놓고 시작
  ## Normalize : 다양한 크로스브라우징 환경에서 좋음 
----
#### 하이퍼링크 스타일

     a:link _ 방문안함 : 파란색
     a:visited _ 방문함 : 보라색
     a:hover_ 마우스 hover  : 빨간색
     a:focus _ 키보드  : 빨간색
     a:active_ 활성화 : 빨간색  (요즘 잘 안씀)


상속과 특정요소에 직접적인 효과를 주었을 때 일어나는 상황에 대해 생각해보기!
겹침, 상속, 우선순위 이슈!

예제에 스타일 적용시키기

        a{
            color: inherit;
            text-decoration: none;
            /* 화면에 출력되고 있었던 밑줄 없앰 */
         }

---

#### Web font적용한 스타일

Google Web font : [web font](https://fonts.google.com/)

* Serif (문자 가로획의 시작이나 끝부분에 붙어있는 장식, 세로기둥과 줄기의 끝부분에 맵시를 내거나 가독성을 높이기 위해 붙인 획이 있는 글꼴)
* Sans-serif (세리프(Serif, 장식)이 없는 글꼴 / 고딕체같은 반듣한 글꼴)

> @import url(‘https://fonts.googleapis.com/css?family=Noto+Sans+KR:400,700’);  / *css시트 맨 위에 추가 _ 요청만 한 상태*/

css 시트에 html에 적용할 수 있게 불러와봅시다
                
        /* 본문스타일 */
        body{
           color: #181818;
           background-color: #fff;
           font-family: “Noto Sans KR”, sans-serif;
           font-weight: 700;
            font-size: 1.4rem;         
            }
# Today I found out
* float에서 상자는 겹치지만 텍스트는 밀려남 
* 한글같은경우 line-height: 1.15 사용 권장
* 전체선택자(*)는 우선순위가 낮고 성능이 저하될 수 있음
* rem은 html을 기준으로 글자크기가 정해진다 (상속되지않음)
* font의 속성은 6가지가 있음 (-style, weight, varient, line-height, size, family) -> font: 'italic' bold 1.2 12px 고딕
* 익스플로러 구버전에서는 해석하지 못하는 속성들을 inline으로 설정함 
* ol테그로 마크업을 하게되면 숫자로 넘버링이 되는데 만일 넘버링이 없어진다면 음성텍스트가 인식하지 못함
* 활성화상태 (마우스와 키보드)의 색도 지정 가능
* 상속값 < 내가 가진 값
* css에서 자주 나오는 버그 : 오타 , 겹침, 상속, 우선순위
* 글꼴 군 : serif, sans-serif(돋움체형)
* 폰트가 안나올경우 : 개발자도구페이지 -> network -> Font -> 응답코드보고 다운받았는지 체크 
* 그리드는 12칼럼이 많이 쓰인다. 
* inline을 이용해서 가로메뉴를 만들때 html 배치에 따라 요소들의 공백이 생길수도있다.(block은 공백이 없음)
* 공백제거를 위해 부모 폰트사이즈는 0으로 그리고 자식요소에게만 폰트사이즈를 주는것으로 사용할 수 있다. 
* inline vs inline-block
* nth-child는 익스플로러8 지원X
* a요소의 기본속성 -> inline
* inline에 block이 포함된건 바람직하지 않다. (키보드 포커싱 작동 X)
* display: none vs visibility: hidden vs position: absolute vs clip: rect(0,0,0,0)

<!-- * 읽어보자 https://www.slideshare.net/wsconf/web-font-wsconfseoul2017-vol2?qid=7b5a4aa2-280e-4834-ba99-6c46749c03c1&v=&b=&from_search=1 -->


