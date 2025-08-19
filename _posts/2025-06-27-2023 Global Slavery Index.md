---
title: "[Makeover Monday] 2023 Global Slavery Index"
excerpt: "Makeover Monday 데이터를 통해 2023 Global Slavery Index 대시보드 만들기④"
date: 2025-06-25T17:13:00+09:00
last_modified_at: 2025-06-25T17:13:00+09:00
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
           src="https://public.tableau.com/static/images/Gl/GlobalSlaveryindex2023/1/1_rss.png"
           style="border: none" />
    </a>
  </noscript>
  <object class="tableauViz"
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
    <param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F" />
    <param name="embed_code_version" value="3" />
    <param name="site_root" value="" />
    <param name="name" value="GlobalSlaveryindex2023/1" />
    <param name="tabs" value="no" />
    <param name="toolbar" value="yes" />
    <param name="static_image" value="https://public.tableau.com/static/images/Gl/GlobalSlaveryindex2023/1/1_rss.png" />
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

이번 대시보드는 MakeoverMonday 12월 1주차 주제인 "Global Slavery Index" 데이터를 기반으로 제작하였다.
데이터는 MakeoverMonday 공식 웹사이트에서 제공된 데이터를 사용하였으며, Tableau를 활용해 시각화하였다.

## 1. 목표 및 니즈 파악

이 대시보드는 여러 국가들의 Slavery 수 현황을 한눈에 파악할 수 있도록 구성되었다.
특히, 종합점수를 통해 국가 간 비교가 가능하며, 특정 국가를 디테일하게 볼 수 있도록 설계하였다.
주요 목표는 다음과 같다:

- 2023년 전체 국가적으로 Slavery 수, 종합점수(최저, 평균, 최고)에 대해서 알아보자
- 특정 국가의 수치를 디테일하게 알아보자
- 취약성 점수와 정부 대응 점수를 전체 평균과 특정 국가를 비교해보자

## 2. 대시보드 기획 및 구현
### 1. 메인 KPI
- 2023년 전체 국가들의 수치를 합산한 내용으로 다음과 같은 요소를 포함한다:
  - 전체 국가 수
  - Slavery 수
  - 평균 종합점수
  - 최저종합점수
  - 최고종합점수 들을 알 수 있는 KPI 이다.

- 여기서 종합점수는 취약성 점수와 정부 대응 점수를 종합한 것으로, **취약성 종합점수에는 0.6의 가중치**를, **정부 대응 점수에는 0.4의 가중치**를 부여하여 산출하였다.
- 해당 KPI는 필터에 따라 바뀌는 동적인 시각화가 아닌 정적인 정보로 구성하였다.

### 2. 지도 (Map)
- 국가별로 위치 아이콘을 배치해 클릭을 유도하였고, 왼쪽 하단에는 직접 기준 종합점수를 입력할 수 있어 입력 시 아이콘 색이 변하도록 설정하였다.
- 마우스 오버 시 범례 내용이 툴팁으로 표시되며, 국가를 클릭하면 해당 국가의 정보가 아래에 뜨도록 구성하였다.

### 3. 특정 국가 종합 KPI
- 클릭한 특정 국가의 정보가 나오는 KPI 영역으로, 해당 국가의 인구, 노예 수, 종합점수 등을 디테일하게 확인할 수 있다.

### 4. 취약점 & 정부 대응 점수
- 취약성 점수와 정부 대응 점수를 막대그래프로 표현하였고, 전체 평균과 특정 국가의 점수를 나란히 배치하여 비교할 수 있도록 설계하였다.
- 전체와 특정 국가를 구분할 수 있도록 색상을 다르게 설정하였고, 범례도 차트 위에 표시하였다.
- 취약성 점수는 부정적인 수치로 높을수록 안 좋은 상태, 정부 대응 점수는 긍정적인 수치로 높을수록 좋은 대응력을 의미한다.
- 전체적인 변수 명은 해당 막대를 마우스오버하면 보인다.

## 3. 대시보드 상호작용
- 상호작용은 지도에만 설정되어 있다. 
- 지도에서 국가 아이콘을 클릭하면, 아래 특정 국가 종합 KPI와 막대차트가 선택 국가 기준으로 바뀌어 전체와 비교할 수 있도록 구성하였다.

## 4. 결론
- **2023년의 Slavery 현황**
이번 대시보드를 통해 2023년 전 세계의 노예 수 현황을 한눈에 볼 수 있으며, 종합점수를 기준으로 각 국가 간 상대적 위치를 비교해볼 수 있다.
또한 지도에서 관심 있는 국가를 클릭하면 해당 국가의 구체적인 수치를 확인할 수 있고, 전 세계 평균과의 비교도 가능하다.

- **특정 국가의 Slavery 현황**
특정 국가의 인구 대비 노예 수, 종합점수, 취약성 점수, 정부 대응 점수를 전 세계 평균과 나란히 확인하면서 해당 국가가 어떤 위치에 있는지 파악할 수 있다.
특히, 취약성 점수는 높고 정부 대응 점수는 낮은 국가는 제도적 개선이나 국제적 지원이 필요한 곳일 수 있으며, 반대로 대응 점수가 높은 국가는 적극적인 정책이 시행되고 있음을 보여준다.


이번 대시보드는 단순한 정보 전달을 넘어서, 글로벌 노예제 문제의 구조적 현실과 국가 간 격차를 함께 조명하고자 하였다.
취약성 점수는 각 국가가 안고 있는 사회·경제적 문제의 심각도와 제도적 취약함을 반영하며,
정부 대응 점수는 해당 국가가 이 문제에 대해 얼마나 적극적으로 정책적 대응을 하고 있는지를 나타낸다.

특히 지도 기반 상호작용을 통해 사용자는 관심 있는 국가의 현황을 직접 선택하고 비교할 수 있고,
전 세계 평균과의 비교를 통해 상대적인 위치와 대응 수준을 보다 명확하게 파악할 수 있다.

이번 시각화를 통해 우리는 단순히 '노예 수'나 '점수 차이'에 주목하는 데 그치지 않고,
이를 통해 드러나는 인권의 불균형, 제도의 불완전성, 사회적 안정성의 격차라는 더 큰 화두를 함께 바라볼 수 있다.

## 💬 분석 피드백

- 시계열적으로 볼 수 있으면 더 좋을듯
- 지도 말고도 전체적인 국가 현황을 볼 수 있는 시각화를 추가해도 좋을듯
- 막대 그래프의 변수 이름을 다 보이도록 설정할 아이디어가 필요해보임

<!-- <div class='tableauPlaceholder' id='viz1751245444120' style='position: relative'><noscript><a href='#'><img alt='대시보드 1 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Gl&#47;GlobalSlaveryindex2023&#47;1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='GlobalSlaveryindex2023&#47;1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Gl&#47;GlobalSlaveryindex2023&#47;1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='ko-KR' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1751245444120');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1600px';vizElement.style.height='927px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1600px';vizElement.style.height='927px';} else { vizElement.style.width='100%';vizElement.style.height='2577px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script> -->