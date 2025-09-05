---
title: "[개인] Retail Rocket ABtest 대시보드 - 대시보드 설계"
excerpt: "생성한 데이터를 가지고 대시보드를 설계해보자"
date: 2025-09-02T12:00:00+09:00
last_modified_at: 2025-09-02T12:00:00+09:00
toc: true
toc_label: "목차"
toc_sticky: true
categories: [Prodject,Retail Rocket]
tags: [ecommerce,PostgreSQL, python, ABtest, CTV, Funnel 분석, Path 분석]
layout: single

---
## 개요
- 총 3장의 대시보드 설계
- 보고서 형식으로 구성하였으며, 영어글 삽입
- 대략적인 지표 내용과 가설검정 결과를 보여주는 대시보드로 제작

---

## 1. 대시보드 임베딩
<!-- 수정된 코드: 큰 화면은 원래대로, 노트북만 가로휠 방지 -->
<style>
/* 큰 화면 (800px 이상) - 데스크톱/큰 모니터 (원래대로) */
@media (min-width: 800px) {
  #vizResponsive { 
    height: 1700px !important; 
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
     style="position: relative; width: 100%; height: 1700px; margin: 1em 0;">
  <noscript>
    <a href="https://public.tableau.com/views/ABtestwithRetailRocketdata/CVR">
      <img alt="AB Test with Retail Rocket - CVR"
           src="https://public.tableau.com/static/images/AB/ABtestwithRetailRocketdata/CVR/1_rss.png"
           style="border: none; width: 100%; height: 100%; object-fit: contain;" />
    </a>
  </noscript>
  <object class="tableauViz"
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
    <param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F" />
    <param name="embed_code_version" value="3" />
    <param name="site_root" value="" />
    <!-- 워크북명/시트명 -->
    <param name="name" value="ABtestwithRetailRocketdata/CVR" />
    <param name="tabs" value="no" />
    <param name="toolbar" value="yes" />
    <param name="static_image" value="https://public.tableau.com/static/images/AB/ABtestwithRetailRocketdata/CVR/1_rss.png" />
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

---

## 2. 대시보드 설명
### 1. CTV
- KPI
  - 매개변수를 통해 기간을 정할 수 있음
  - KPI와 파이차트, 막대그래프를 통해 CTV에 대한 대략적인 지표 수치 및 추이를 볼 수 있음
  - A,B group간의 차이를 잘 보일 수 있도록 설정함

- category
  - 매우 많은 카테고리 종류로 인해 구매자 수가 많은 상위 10위에 있는 카테고리만 추출하여 보여주고 있으며, A/B group 수치를 같이 보여주고 있음
  - 카테고리 표에 있는 카테고리를 클릭시 해당 카테고리 정보를 보여주도록 원 차트에 반영함
  - 클릭한 카테고리ID가 어떤 것인지 알 수 있도록 따로 표현함

- 가설검정
  - CTV에 대한 가설검정 결과를 보여주는 내용으로 표는 가설검정과 관련된 수치를 문장은 해당 가설검정 결과에 해당하는 내용을 담고 있음
  - 기간에 따라 결과가 바뀐다면 내용도 바뀌도록 설정

### 2. Funnel Analysis
- KPI
  - 매개변수를 통해 기간을 정할 수 있음
  - 막대그래프와 표를 통해 A,B의 수치를 비교하면서 볼 수 있도록 설정
  - 표에 따로 표시하지는 않았지만, view->cart와 cart ->purchase 이렇게 두가지로 나눠서 생각 (글에는 언급)

- category
  - A,B에 따른 수치 변화를 같이 보여주며, 특정 카테고리를 클릭시 해당 카테고리 정보로 바뀜
  - 수치를 단계적으로 보여주기 위해 점점 줄어드는 시각화를 선택, 표에서 정확한 수치 파악 가능

- 가설검정
  - 총 2가지의 경우로 나누어서 결과를 보여주며, 가설검정과 관련된 수치와 가설검정 결과를 보여주고 있음
  - 기간에 따라 결과가 바뀐다면 내용도 바뀌도록 설정

### 3. path
- KPI
  - 경로 분석의 전체적인 그림을 보여주는 사다리 느낌으로 표현함
  - 해당 대시보드도 기간에 따른 수치를 보여주고 있음
  - view->purchase를 Direct, view->cart->purchase는 viacart로 표현하고 있음

- category
  - Direct와 Viacart를 서로 구별하여 보여주고 있으며, 표도 따로따로 작용하여 Direct 표에 있는 카테고리를 선택시 Direct부분만 Viacart 표에 있는 카테고리를 선택시 viacart에만 작용됨
  - 또한 게이지차트를 통해 A,B 비율을 볼 수 있음
  - 선택한 카테고리id는 서로 구별하여 표현함

- 가설검정
  - 총 2가지의 경우로 나누어서 결과를 보여주며, 가설검정과 관련된 수치와 가설검정 결과를 보여주고 있음
  - 기간에 따라 결과가 바뀐다면 내용도 바뀌도록 설정

### 4. 공통사항
- 모두 기간에 따른 수치를 보여줌
- 하단 오른쪽의 삼각형 화살표를 클릭하면 다음장으로 넘어가도록 설정
- 제목 밑에는 모두 해당 대시보드에 대한 간략한 설명을 담고 있음
- 필터의 경우는 3개의 대시보드 모두 카테고리 표에만 존재함