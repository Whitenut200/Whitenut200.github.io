---
title: "[Makeover Monday] Who Spends the Most Time on Social Media?"
excerpt: "Makeover Monday 데이터를 통해 Who Spends the Most Time on Social Media? 대시보드 만들기②"
date: 2025-06-25T13:13:00+09:00
last_modified_at: 2025-06-25T13:13:00+09:00
toc: true
toc_label: "목차"
toc_sticky: true
categories:
  - Makeovermonday
tags:
  - Tableau
  - Makeovermonday
layout: single

---
<!-- 업데이트된 Minimal Mistakes 테마 breakpoint 맞춤 반응형 CSS -->
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

<!-- Tableau 대시보드 임베드 -->
<div class="tableauPlaceholder" id="vizResponsive"
     style="position: relative; width: 100%; height: 700px; margin: 1em 0;">
  <noscript>
    <a href="#">
      <img alt="대시보드 1"
           src="https://public.tableau.com/static/images/Ai/WhoSpendstheMostTimeonSocialMediamakeovermonday/1/1_rss.png"
           style="border: none; width: 100%; height: 100%; object-fit: contain;" />
    </a>
  </noscript>
  <object class="tableauViz"
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
    <param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F" />
    <param name="embed_code_version" value="3" />
    <param name="site_root" value="" />
    <param name="name" value="WhoSpendstheMostTimeonSocialMediamakeovermonday/1" />
    <param name="tabs" value="no" />
    <param name="toolbar" value="yes" />
    <param name="static_image" value="https://public.tableau.com/static/images/Ai/WhoSpendstheMostTimeonSocialMediamakeovermonday/1/1_rss.png" />
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

이번 대시보드는 MakeoverMonday 11월 1주차 주제인 "Individuals using the Internet (% of population)" 데이터를 기반으로 제작하였다.
데이터는 MakeoverMonday 공식 웹사이트에서 제공된 데이터를 사용하였으며, Tableau를 활용해 시각화하였다.

## 1. 목표 및 니즈 파악

이 대시보드는 여러 국가들의 인터넷 사용 비율을 다양한 관점에서 한눈에 파악할 수 있도록 구성되었다.
특히, 시간이 지남에 따라 국가별 변화, 소득 수준별, 지역별 패턴을 쉽게 비교하고 분석할 수 있도록 설계하였다.
주요 목표는 다음과 같습니다:

- 각 국가의 연도별 인터넷 사용 시간을 살펴보자
- 상위 10%, 하위 10% 국가들을 연도별로 구분하여 순위를 살펴보자
- 소득 수준(Income Group) 및 **지역(Region)**별로 상위·하위 국가들을 비교하고, 각 그룹에서 상위(Top N)에 위치한 국가들의 특징을 파악해보자

## 2. 대시보드 기획 및 구현
### 1. 달리기 시각화 (Running Visualization)
- 국가별 Social Media 사용 시간을 달리기 형태로 시각화하였다.
- 맨 위 Finish Line에 가까울수록 사용 시간이 많고, Starting Line에 가까울수록 사용 시간이 적은 국가로 배치됩니다.
- 많은 국가들이 존재하기 때문에:
  - 상위 10% 국가들은 최상단
  - 하위 10% 국가들은 최하단에 위치시켰다.
- 1명당 1국가가 배정되며, 해당 도형을 클릭하면 Finish Line과 Starting Line에 위치한 레이블이 해당 국가의 정보로 동적으로 변경됩니다.

### 2. 지도 (Map)
- 데이터에 포함된 국가들을 지도상에 표시하였다.
- 색상은 Social Media 사용 시간이 많을수록 진하게, 적을수록 연하게 표현하였다.
- 이를 통해 전 세계적으로 지역 간 격차를 한눈에 파악할 수 있다.

### 3. 소득 수준별 그룹 (Income Group)
- 국가별 소득 수준을 기준으로 4개의 그룹으로 분류하였다:
  - High income
  - Upper middle income
  - Lower middle income
  - Low income
- 각 그룹의 평균 Social Media 사용 시간을 색상으로 표현하였으며, 진할수록 사용 시간이 많은 그룹을 나타낸다.
- 각 박스의 레이블은 해당 소득 그룹의 전체 사용 시간 합계를 나타낸다.

### 4. 지역별 비율 (Region)
- 총 7개의 지역(Region)을 기준으로 파이차트를 구성하였다.
- 각 지역이 차지하는 Social Media 사용량의 비율을 색상과 크기로 확인할 수 있다.
- 가운데 레이블에는 Social Media 사용 시간이 가장 많은 지역과 그 값을 강조하였으며, 우측에는 색상 범례를 함께 제공한다.

### 5. TOP N 국가
- Social Media 사용 시간이 많은 국가들을 순위별로 나열한 표입니다.
- 사용자가 직접 보고 싶은 순위 개수(N) 를 지정할 수 있으며, Income Group 및 Region 필터를 통해 원하는 조건에 맞는 상위 국가를 확인할 수 있습니다.
- 예: High income과 South Asia를 선택하고 N=6으로 설정하면, 해당 조건에 맞는 상위 6개 국가가 출력됩니다.

## 3. 대시보드 필터 및 상호작용
- Income Group과 Region 차트에 필터 기능을 설정해, 원하는 그룹이나 지역만 필터링할 수 있도록 구성하였다.
- 달리기 시각화는 하단 시각화들과는 필터 연동이 되지 않으며, 오직 도형 및 레이블 간 상호작용만 가능합니다.
- TOP N 표는 선택한 필터 조건에 따라 자동으로 갱신되어, 보다 정밀한 분석이 가능합니다.

## 4. 결론
- **연도별 사용 추이 분석**
대시보드를 통해 국가별 Social Media 사용 시간이 매년 증가하는 추세임을 확인할 수 있습니다. 디지털 접근성이 향상되면서 많은 국가들이 더 많은 시간을 온라인에 소비하고 있는 흐름을 보여줍니다.

- **국가 간 격차 확인**
소득 수준이나 지역에 따라 Social Media 사용 시간의 차이가 뚜렷하게 나타납니다. 고소득 국가일수록 사용 시간이 높은 경향이 있으며, 일부 지역은 여전히 낮은 수준에 머물러 있어 디지털 격차(Digital Divide) 문제를 시사합니다.

- **상위/하위 국가 탐색 가능**
TOP N 표와 달리기 시각화를 통해 Social Media 사용 시간이 가장 많은 국가와 가장 적은 국가를 한눈에 파악할 수 있습니다.
특히 특정 국가가 지속적으로 상위권에 머무는 경우, 사회적, 문화적 요인을 분석해볼 수 있는 출발점이 됩니다.

이번 대시보드는 단순한 정보 전달을 넘어서, 국가 간 디지털 소비 행태의 차이, 소득 및 지역별 사용 특성, 그리고 변화 추세를 함께 이해할 수 있도록 설계되었다.
사용자들은 대시보드를 통해 단편적인 수치 이상의 인사이트를 얻고, 나아가 디지털 접근성과 균형 있는 정보 소비의 중요성을 되짚어볼 수 있다.

Social Media는 이제 단순한 소통 수단을 넘어 사회, 정치, 경제에 큰 영향을 미치는 플랫폼으로 자리 잡고 있다.
그 사용 양상을 살펴보는 일은 단지 트렌드를 이해하는 것이 아니라, 디지털 사회 속 국가 간 불균형과 사회 구조를 이해하는 중요한 창이 될 수 있다.

## 💬 분석 피드백

- 색이 너무 다양하게 너무 정신없어보임
- 지도 시각화의 효과가 미미해보이며, 해당 시각화보다 더 여러 효과를 집어 넣어 **여러 인사이트를 보이는 차트**로 변경하는 게 좋아보임
- 예를 들어, 지역을 선택했을 때 해당 지역만 차트에 보이게 하고 그 지역에 해당하는 국가들이 **필터링** 되게 설정하거나 Income Group을 클릭하면 해당 집단에 맞는 국가들이 **하이라이트**되게 하는 방법
- 달리기 시각화를 좀 더 달리고 있는 모습이 보이도록 디자인하고 **상위10%, 하위 10%**에 해당하는 차트라고 **따로 표기**하는 것이 좋아보임
- 간단한 파이, 막대 차트가 아닌 좀더 **차이를 효율적으로 보일 수 있는 차트**를 선택하는 것이 좋아보임

<!-- <div class='tableauPlaceholder' id='viz1750651696925' style='position: relative'><noscript><a href='#'><img alt='대시보드 1 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ai&#47;AidWorkerSecurityIncidentsmakeovermonday&#47;1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='AidWorkerSecurityIncidentsmakeovermonday&#47;1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ai&#47;AidWorkerSecurityIncidentsmakeovermonday&#47;1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='ko-KR' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1750651696925');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else { vizElement.style.width='100%';vizElement.style.height='3577px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script> -->