# 수업내용메모
* 형제레벨의 블록이 서로 겹칠때 overflow: hidden으로 서로 독립적인 컨텍스트를 생성가능하다.
* 컨텐츠 모델상 인터렉티브 모델 안에 또 다른 인터렉티브 모델을 쓸 수 없다. (예를들어 a href안에 또 다른 a href)
* 이미지의 대체텍스트인 alt를 생략하면 스크린 리더가 경로를 읽는다. alt가 필요없는 경우라 하더라도  빈칸으로 남겨둔다. (예를들어 figure안에 figcaption이 있는경우)
* IR 기법 (텍스트를 이미지에 숨기는 기법)
* 텍스트인덴트와 박스사이징
* 강조에 쓰이는 텍스트 속성 : strong, em
* 특성 및 구분됨을 보여주는 텍스트 속성 : bold, i
* sprite -> 텍스트의 마진을 박스의 높이만큼 주게되면 밖으로 밀려나게되는데 그때 overflow:hidden 사용
* 윈도우 11은 justify-content: space-evenly 지원안함 (대신 between 사용)


# 수업 내용
  1. 새소식 마크업 순서
    * 제목 새소식 (h2.news-heading, span)
    * W3C 사이트가 리뉴얼 되었습니다. (h3.news-item-heading)
    * 날짜정보 (time.news-item-date)
    * 기사본문 (p.news-item-brief)
    * 썸네일 (figure.news-item-thumbnail, img, figcaption)
    * 더보기 
    * h3, time, p, figure, img, figcaption 부분들은 article로 마크업(article.news-item) 한 뒤에 a로 마크업 (그러기전에 a테그안의 모든 요소들을 block요소로 만들어야함 -> 인라인요소안에 블록 요소가 오면 안좋으므로)
  2. 신규이벤트 마크업 순서
    * 신규이벤트 (h2.event-heading, span)
    * 이벤트 내용 (div #event-detail,p.event-thumbnail, p.event-brief)
    * 이전/다음 (div.btn-event, btn-prev, btn-next)
  3. 관련 사이트 마크업 순서
    * 제목 관련사이트 (related-heading, span)
    * 관련사이트 목록 (ul.related-list, li, a)
