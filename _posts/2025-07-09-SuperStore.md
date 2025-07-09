---
title: "SuperStore 대시보드"
excerpt: "SuperStore 데이터를 가지고 주제에 맞게 대시보드를 설계해보자"
date: 2025-07-09T11:00:00+09:00
last_modified_at: 2025-07-09T11:00:00+09:00
toc: true
toc_label: "목차"
toc_sticky: true
categories:
  - SuperStore
tags:
  - Tableau
  - POC
layout: single

---
<div class="tableauPlaceholder" id="vizResponsive"
     style="position: relative; width: 100%; padding-bottom: 62.5%; height: 0;">
  <noscript>
    <a href="#">
      <img alt="대시보드 1"
           src="https://public.tableau.com/static/images/Su/SuperStore_17507472822680/sheet0/1_rss.png"
           style="border: none" />
    </a>
  </noscript>
  <object class="tableauViz"
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
    <param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F" />
    <param name="embed_code_version" value="3" />
    <param name="site_root" value="" />
    <param name="name" value="SuperStore_17507472822680" />
    <param name="tabs" value="no" />
    <param name="toolbar" value="yes" />
    <param name="static_image" value="https://public.tableau.com/static/images/Su/SuperStore_17507472822680/sheet0/1_rss.png" />
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

해당 대시보드는 주어진 주제를 기반으로, 상황을 구체적으로 가상 설정한 후 그에 맞춰 SuperStore 데이터를 활용하여 대시보드를 설계하였습니다.

# 1. 대시보드 주제
본 대시보드는 **경영진(C-level)**이 전사 매출 실적을 주간 및 월간 단위로 신속하게 파악하고, 주요 이슈를 조기에 인지할 수 있도록 설계되었습니다.

1페이지: 전사 매출 요약
- 매출, 이익, 이익률 등의 주요 지표를 중심으로 전월·전년 대비 증감률을 시각적으로 표현
- 추세선, 비교 막대그래프 등을 활용하여 전체 실적 흐름을 한눈에 파악

2페이지: 지역/카테고리별 상세 분석
- 지역(Region/State) 및 제품 카테고리 기준으로 매출·이익 비교
- 상위/하위 실적 항목 강조 및 정렬 기능 포함으로 Drill-down 분석 지원

또한, 고객 수, 주문 수, 할인율, 고객당 매출 등 추가 지표를 포함하여 보다 심층적인 분석이 가능하도록 구성하였습니다.

# 2. 대시보드 구성
## 0. 기본
- 해당 대시보드는 왼쪽 바가 있어서 개요와 고객 버튼으로 대시보드를 이동할 수 있습니다.
- 바 하단에는 PDF, PNG로 저장할 수 있도록 버튼을 생성하였습니다.

## 개요
### 1. KPI
- 매출, 수익, 수익률, 고객수에 관련된 지표를 보여준다.
- 해당 지표들은 주 단위로 볼 수 있어, 기준연월과 주를 선택하면 해당 달의 주에 따른 지표를 보여준다

※'주' 필터에 대한 주의사항※

해당 필터는 기준 연월의 주차를 나타내며, 1부터 5까지의 숫자로 구성됩니다:
1: 기준 연월의 1주차
2: 기준 연월의 2주차
2: 기준 연월의 2주차
4: 기준 연월의 4주차
5: 기준 연월의 5주차

단, 1주차와 5주차는 해당 월의 시작일 또는 종료일에 따라 7일이 아닌 더 적은 일수를 포함할 수 있으므로, 이로 인해 해당 주차의 지표가 다른 주차에 비해 낮게 나타날 수 있습니다.

### 2. 캘린더
- 해당 시트는 매출/수익 값을 매개변수를 통해 선택할 수 있다.
- 캘린더 차트로 일별로 매출/수익값을 보여준다

### 3. 일별 추이
- 해당 시트는 매출/수익 값을 매개변수를 통해 선택할 수 있다.
- 라인그래프는 **당월**, 영역그래프는 **전월**을 보여준다.
- 당월과 전월을 비교 할 수 있도록 이중축으로 구성하였다

### 4. 상위/하위 매출 고객
- 이 차트는 고객을 상위 10%, 상위 20%, 하위 10%, 하위 20%, 해당 없음의 다섯 집단으로 분류하여 시각화한 것입니다.
- 여기서 10%, 20%는 매출/수익 값에 대한 백분위수를 구해 설정하였다.
- X축은 선택한 매개변수(매출 또는 수익)에 따른 고객 순위를 나타내며, 오른쪽으로 갈수록 순위가 높습니다.
- Y축은 임의로 생성된 값으로, 실제 수치와는 무관합니다.
- 각 동그라미는 한 명의 고객을 의미하며, 마우스를 올리면 해당 고객의 상세 정보를 확인할 수 있습니다.
※ 만약 매개변수로 집단을 변경할 경우 설정한 집단에 따라 고객과 순위가 변경됩니다

### 5. 고객별 최근 1년동안의 구매일자 
- 기준연월 기준으로 상품을 구매한 사람들을 대상으로 그 전에도 구매를 한 이력이 있는지 볼 수 있는 시각화입니다.
- 고객의 이름과 재구매 횟수 그리고 언제 구매를 했는지 월단위로 나타나 있으며, 원에 마우스 오버를 하면 디테일하게한 정보를 알 수 있습니다.
- 마우스오버를 할 시, 해당월에 고객이 언제, 무엇을, 얼마나 구매했는지 알 수 있으며, 환불 여부도 알 수 있습니다.

## 고객
### 1. 지도
- 지도는 오른쪽 표의 필터의 개념으로 대륙을 클릭하면 드릴다운 형식으로 해당 대륙의 도시들이 뜨도록 만들었다.
- 해당 대륙과 지역을 클릭하면 오른쪽 표가 필터링되며, 어떤 값이 필터링 되었는지는 가운데 **필터확인** 공간에서 확인할 수 있다.
- 마우스오버를 하면 해당 영역의 매출/수익을 볼 수 있으며, 도시들도 마우스 오버 하면 해당 도시의 매출/수익값과 함께 도시 맵을 볼 수 있다.

### 2. 카테고리
- 카테고리도 지도와 마찬가지로 오른쪽 표의 필터의 개념으로 상위 카테고리를 클릭하면 드릴다운 형식으로 해당 상위 카테고리의 하위 카테고리들이 뜨도록 만들었다.
- 해당 카테고리들을 클릭하면 오른쪽 표가 필터링되며, 어떤 값이 필터링 되었는지는 가운데 **필터확인** 공간에서 확인할 수 있다.
- 마우스오버를 하면 해당 영역의 매출/수익을 막대그래프로 볼 수 있다.

### 3. 필터 및 정렬 확인 바
- 왼쪽 지역과 카테고리에서 선택된 즉, 필터링 된 값을 보여주는 영역이다.
- 정렬은 해당 값이 가장 위에 뜨도록 설정하였으며, 상위 10%, 상위 20%, 해당없음, 하위 20%, 하위 10% 순서는 유지되도록 설정하였다.
- ex) 만약 정렬 우선순위가 상위 20%라면 정렬 순서는 상위 20% -> 상위 10% -> 해당없음 -> 하위 20% -> 하위 10% 이다.

### 4. 고객 표
- 해당 표는 오른쪽 지역과 카테고리 항목이 필터링 된 고객 명단을 보여주며, 고객 이름, 세그먼트, 이번달 매출/수익, 최근 N 동안 재구매율, 매출 상위/하위 집단을 보여준다.
- 최근 N 은 사용자가 선택할 수 있으며, 6개월, 1년, 2년 중 하나를 선택하여 볼 수 있다.
- 매출 상위/하위 집단은 매출/수익의 백분위수를 구하여 집단을 설정하였으며, 필터링 된 고객에 맞춰 집단이 변경된다.

# 3. 결론
해당 대시보드는 정해진 주제와 정해진 상황에 따라 설계된 비즈니스 대시보드로 최대한 주제에 적합하게 구성하였으며, **고객**을 중심으로 해당 지표와 정보들을 알 수 있도록 설계되었습니다.


# 💬 분석 피드백
- 너무 정보를 덜어내서 더 많은 인사이트와 정보를 보여줄 수 있도록 추가하면 좋을듯





