---
title: "[Makeover Monday][Remake] Who Spends the Most Time on Social Media?"
excerpt: "Makeover Monday 데이터를 통해 Who Spends the Most Time on Social Media? 대시보드 만들기③ - Remake"
date: 2025-06-27T13:13:00+09:00
last_modified_at: 2025-06-27T13:13:00+09:00
toc: true
toc_label: "목차"
toc_sticky: true
categories: [Project,Makeovermonday]
tags:
  - Tableau
  - Makeovermonday
layout: single

---

<!-- 수정된 코드: 큰 화면은 원래대로, 노트북만 가로휠 방지 -->
<style>
/* 큰 화면 (800px 이상) - 데스크톱/큰 모니터 (원래대로) */
@media (min-width: 800px) {
  #vizResponsive { 
    height: 1000px !important; 
  }
}

/* 중간 화면 (720px ~ 799px) - 노트북 (가로휠 방지) */
@media (min-width: 720px) and (max-width: 799px) {
  #vizResponsive { 
    height: 700px !important; 
    width: 100% !important;
    max-width: 100% !important;
    overflow-x: hidden !important;
  }
  #vizResponsive .tableauViz {
    transform: scale(0.95) !important;
    transform-origin: top left !important;
  }
}

/* 작은 화면 (600px ~ 719px) - 태블릿 */
@media (min-width: 600px) and (max-width: 719px) {
  #vizResponsive { 
    height: 550px !important;
    width: 100% !important;
    max-width: 100% !important;
    overflow-x: hidden !important;
  }
  #vizResponsive .tableauViz {
    transform: scale(0.9) !important;
    transform-origin: top left !important;
  }
}

/* 모바일 (600px 미만) - 스마트폰 */
@media (max-width: 599px) {
  #vizResponsive { 
    height: 400px !important;
    width: 100% !important;
    max-width: 100% !important;
    overflow-x: hidden !important;
  }
  #vizResponsive .tableauViz {
    transform: scale(0.85) !important;
    transform-origin: top left !important;
  }
}
</style>
<div class="tableauPlaceholder" id="vizResponsive"
     style="position: relative; width: 100%; height: 700px; margin: 1em 0;">
  <noscript>
    <a href="#">
      <img alt="대시보드 1"
           src="https://public.tableau.com/static/images/Wh/WhoSpendstheMostTimeonSocialMediamakeovermondayRemake/1/1_rss.png"
           style="border: none" />
    </a>
  </noscript>
  <object class="tableauViz"
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
    <param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F" />
    <param name="embed_code_version" value="3" />
    <param name="site_root" value="" />
    <param name="name" value="WhoSpendstheMostTimeonSocialMediamakeovermondayRemake/1" />
    <param name="tabs" value="no" />
    <param name="toolbar" value="yes" />
    <param name="static_image" value="https://public.tableau.com/static/images/Ai/WhoSpendstheMostTimeonSocialMediamakeovermondayRemake/1/1.png" />
    <param name="animate_transition" value="yes" />
    <param name="display_static_image" value="yes" />
    <param name="display_spinner" value="yes" />
    <param name="display_overlay" value="yes" />
    <param name="display_count" value="yes" />
    <param name="language" value="ko-KR" />
  </object>
</div>

<script type="text/javascript">
  window.addEventListener('DOMContentLoaded', function () {
    var divElement = document.getElementById('vizResponsive');
    var vizElement = divElement.getElementsByTagName('object')[0];
    if (vizElement) {
      var scriptElement = document.createElement('script');
      scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';
      vizElement.parentNode.insertBefore(scriptElement, vizElement);
    }
  });
</script>



이번 대시보드는 Makeover Monday 11월 1주차 주제인 "Individuals using the Internet (% of population)" 데이터를 기반으로 제작하였다.
과거에도 동일한 주제로 2024년에 대시보드를 만든 경험이 있지만, 최근 변화한 나의 분석 성향과 향상된 시각화 역량을 반영하여 새롭게 리메이크하였다.

## 대시보드 구성 설명
### 1. Region 합계/평균 비교
   - 매개변수(Parameter)를 활용하여 합계와 평균 값을 자유롭게 전환하여 확인할 수 있도록 설정
   - 원의 크기와 막대의 높이를 함께 활용해, 각 지역의 상대적인 값 크기를 직관적으로 비교 가능
   - 특정 지역을 클릭하면 필터링되어 해당 지역 데이터만 하위 시트에 반영


### 2. Income 그룹별 비교
   - 국가들을 High / Upper Middle / Lower Middle / Low의 4개 소득 그룹으로 분류
   - 각 그룹 제목 옆에는 소속 국가 수와 해당 국가들의 평균값을 표시
   - 각 원은 한 국가를 나타내며, 그룹마다 서로 다른 색상으로 구분
   - 원 클릭 시 해당 국가가 아닌 소속된 전체 소득 그룹이 필터링되어 그룹별 패턴 분석이 가능
   - **Y축, 즉 높은 곳에 있을 수록 값이 크다는 것을 의미하며, X축의 위치는 의미 없음**


### 3. Country Rank (상위/하위 국가 분포)
   - 상단에는 상위 그룹(1~10%), 하단에는 하위 그룹(1~10%) 국가들이 표시됨
   - 위쪽은 왼쪽부터 순서대로 상위 1~3%, 3~5%, 5~8%, 8~10%
   - 아래쪽은 반대로 하위 8~10%, 5~8%, 3~5%, 1~3%
   - 한 사람 모양 아이콘 = 하나의 국가, 전체적으로 달리기 경기 트랙처럼 구성하여 왼쪽 상단이 결승선, 오른쪽 하단이 출발점처럼 보이도록 시각화
   - 같은 색은 같은 순위 그룹에 속한 국가들을 의미



<!-- <div class='tableauPlaceholder' id='viz1751010377736' style='position: relative'><noscript><a href='#'><img alt='대시보드 1 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Wh&#47;WhoSpendstheMostTimeonSocialMediamakeovermondayRemake&#47;1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='WhoSpendstheMostTimeonSocialMediamakeovermondayRemake&#47;1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Wh&#47;WhoSpendstheMostTimeonSocialMediamakeovermondayRemake&#47;1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='ko-KR' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1751010377736');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1600px';vizElement.style.height='927px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1600px';vizElement.style.height='927px';} else { vizElement.style.width='100%';vizElement.style.height='4327px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script> -->