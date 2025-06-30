---
title: "[Data+ Movies] IMDB Dashboard"
excerpt: "Tabeau에서 제공하는 IMDB 데이터를 가지고 대시보드 만들기①"
date: 2025-06-30T13:13:00+09:00
last_modified_at: 2025-06-30T13:13:00+09:00
toc: true
toc_label: "목차"
toc_sticky: true
categories:
  - Data+
tags:
  - Tableau
  - Data+ Movies
layout: single

---
<div class="tableauPlaceholder" id="vizResponsive"
     style="position: relative; width: 100%; padding-bottom: 62.5%; height: 0;">
  <noscript>
    <a href="#">
      <img alt="대시보드 1"
           src="https://public.tableau.com/static/images/Da/DataMoviesStarterDashboard_17446391842830/sheet0/1_rss.png"
           style="border: none" />
    </a>
  </noscript>
  <object class="tableauViz"
          style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
    <param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F" />
    <param name="embed_code_version" value="3" />
    <param name="site_root" value="" />
    <param name="name" value="DataMoviesStarterDashboard_17446391842830/sheet0" />
    <param name="tabs" value="no" />
    <param name="toolbar" value="yes" />
    <param name="static_image" value="https://public.tableau.com/static/images/Da/DataMoviesStarterDashboard_17446391842830/sheet0/1_rss.png" />
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

이번 대시보드는 Tableau 주최 Data + Movies 챌린지를 통해 제작되었으며, IMDB 영화 데이터를 기반으로 시각화를 진행하였습니다.

# 1. 대시보드 주제
총 4개의 대시보드를 제작하였으며, 각각 Actor(+Director), Year, Genre, Movie를 주제로 구성하였습니다.
이러한 주제를 선정하게 된 배경은, 영화를 볼 때 사람마다 궁금해하는 포인트가 다르다고 생각했기 때문입니다.
어떤 사람은 ‘이 영화에 나온 배우가 누구지?’라고 궁금해하고, 어떤 사람은 감독, 제작 연도, 장르, 혹은 영화가 전반적으로 어떤 내용을 담고 있는지에 더 관심을 가질 수 있습니다.

이처럼 다양한 궁금증을 하나의 대시보드 안에서 모두 해결할 수 있도록 구성하고자 하였고, 메인 페이지는 영화관 분위기를 연출하며 관객들이 각자 다른 궁금증을 품고 있는 장면처럼 디자인하였습니다.
사용자가 자신과 같은 궁금증을 가진 사람을 클릭하면, 그에 맞는 정보를 제공하는 대시보드로 자연스럽게 이동할 수 있도록 설정하였습니다.

# 2. 대시보드 구성
왼쪽 사이드바
장르에 대해 궁금했던 사용자가 중간에 배우나 감독이 궁금해졌을 때, 사이드바에서 Actor 버튼을 클릭하면 해당 대시보드로 바로 이동할 수 있습니다.

모든 영화 추천은 투표 수가 100,000명 이상인 영화만을 대상으로 하여, 보다 신뢰할 수 있는 영화들 위주로 정보를 제공합니다.

## 1. Actor & Director
### ① 시계열 차트
- 상단에 두 개의 시계열 차트를 배치하였고, 왼쪽은 특정 배우(또는 감독)의 영화 수, 오른쪽은 해당 인물의 영화 평균 평점을 보여줍니다.
- 10년 단위로 나누었으며, 가장 최근 수치는 포인트 색으로 강조하였습니다.
- 2020년대는 2023년까지의 데이터만 포함되어 있어 수치가 낮을 수 있습니다.

### ② 장르
- 하단 왼쪽에 위치하며, 해당 배우(또는 감독)가 자주 찍은 장르를 보여주고, 가장 많이 참여한 장르에는 포인트 색을 설정했습니다.
- 오른쪽에는 장르별 평점을 시각화하여, 평점이 7점을 넘는 경우 하이라이트로 표시하였습니다.
- 장르 클릭 시 Genre 대시보드로 이동합니다.

### ③ Award
- 수상 이력과 후보 등재 횟수를 시각화하여, 얼마나 많은 상을 받았고 어떤 상을 받았는지를 한눈에 볼 수 있게 구성했습니다.

### ④ 영화 추천
- 해당 인물과 관련된 영화만 추출하여, 평점 순으로 정렬한 표를 제공하며, 오른쪽 상단의 화살표를 클릭하면 순위를 넘겨볼 수 있습니다.
- 영화 제목 클릭 시 Movie 대시보드로 이동됩니다.

## 2. Year
### ① KPI & 지도
- 특정 연도 또는 시대에 개봉된 영화 수, 평균 평점, 개봉국가 및 사용 언어 등 다양한 정보를 요약하여 보여줍니다.

### ② Award
- 해당 시대에 어떤 배우(또는 감독)가 어떤 상을 수상했는지를 보여주며, 클릭 시 해당 인물의 Actor 대시보드로 이동합니다.

### ③ Genre
- 오른쪽 상단에 위치하며, 시대별로 자주 제작된 장르와 평점을 보여줍니다. 평점 6점 이상은 하이라이트 처리하였습니다.
- 장르 클릭 시 Genre 대시보드로 이동합니다.

### ④ Color
- 컬러 영화와 흑백 영화의 비율을 통해, 시대별 영화 색채 트렌드를 확인할 수 있습니다.

### ⑤ 영화 추천
- 해당 시대의 영화 중 평점이 높은 작품을 추천하며, 영화 제목 클릭 시 Movie 대시보드로 이동합니다.

## 3. Genre
### ① 시계열 차트
- 월별로 해당 장르가 얼마나 자주 개봉되었는지, 평균 평점은 어느 정도였는지를 확인할 수 있습니다.

### ② 영화 추천
- 해당 장르에 속하는 영화 중 평점이 높은 영화들을 표로 정렬해 보여주며, 좌측에는 순위별 영화 정보를 요약해 하이라이트하였습니다.

### ③ Award
- 특정 장르의 영화가 전체 수상 영화 중 얼마나 큰 비중을 차지하는지를 시대별로 시각화하였으며, 주황색으로 해당 장르를 강조하였습니다.

### ④ Actor
- 특정 장르에 가장 많이 참여한 배우 또는 감독을 보여주며, 하이라이트된 이름 클릭 시 Actor 대시보드로 이동합니다.
- 매개변수 필터를 통해 배우 또는 감독을 선택할 수 있게 하였습니다.

## 4. Movie
### ① 영화 사진
- 선택한 영화의 포스터가 자동으로 반영되며, 마우스오버를 통해 이미지가 변경됩니다.
- 아래에는 영화 설명과 태그, 장르가 함께 제공되며, 주요 장르는 하이라이트 처리하였습니다.

### ② KPI
- 평점, 투표 수, 개봉일, 개봉 국가 및 언어 등의 핵심 정보를 간결하게 제공하는 영역입니다.

### ③ Job Category
- 감독과 배우의 실명과 극중 이름을 함께 보여주는 표 형태의 시각화입니다.

### ④ Award
- 해당 영화가 수상한 내역과 수상 비율, 수상 시기를 함께 확인할 수 있도록 구성하였습니다.

### ⑤ 영화 추천
- 비슷한 영화를 평점 기준으로 추천해주며, 사용자가 필터를 조정하면 그에 맞는 상위 3개의 영화를 보여줍니다.
- 영화 클릭 시 자동으로 매개변수가 변경되며, 해당 영화의 상세 정보가 표시됩니다.


# 3. 결론
이 대시보드는 총 4가지 관점(Actor & Director, Year, Genre, Movie)을 통해 IMDB 데이터를 보다 풍부하게 탐색할 수 있도록 구성하였습니다.
사용자는 각자의 궁금증에 따라 대시보드를 선택해 정보를 확인할 수 있으며, 각 대시보드 간의 연결을 유기적으로 설계하여 궁금증이 생길 때마다 자연스럽게 다른 시트로 이동할 수 있도록 구성하였습니다.

특히, 시각화 구성에 있어 단순히 정보를 나열하기보다는 사용자의 탐색 여정을 고려한 인터랙티브한 흐름을 설계한 점에서 큰 의의를 갖습니다.
영화를 사랑하는 사람, 데이터를 좋아하는 사람 모두에게 의미 있는 인사이트를 제공할 수 있도록 설계된 이 대시보드는, 단순한 시각화를 넘어 사용자의 호기심을 따라가는 데이터 스토리텔링을 생각하여 설계해보았습니다.


# 💬 분석 피드백
- 여러 주제를 담으려고 하다가 산으로 가는 느낌이 있음
- 하나의 구체적인 주체를 가지고 더 디테일한 정보를 볼 수 있는 대시보드도 한번 만들어보면 좋을 것
- 웹의 느낌을 내려고 했지만 데이터가 커서 그런지 이동하는 딜레이시간이 매우 길어짐
- 대시보드 전반적으로 디테일한 설명이 부족해보임
- Movie 대시보드에 이미지 처리하는 방법을 다시 생각해봐야될듯 (지금은 뒤에 url만 띄여진 시트를 넣어놓고 이미지 시트를 앞에 부동으로 띄여놔서 뒤에 url 시트에 마우스 오버를 할 때 이미지가 바뀌는 형태)

<!-- <div class='tableauPlaceholder' id='viz1751260123178' style='position: relative'><noscript><a href='#'><img alt='표지 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Da&#47;DataMoviesStarterDashboard_17446391842830&#47;sheet0&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='DataMoviesStarterDashboard_17446391842830&#47;sheet0' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Da&#47;DataMoviesStarterDashboard_17446391842830&#47;sheet0&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='ko-KR' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1751260123178');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1680px';vizElement.style.height='1027px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1680px';vizElement.style.height='1027px';} else { vizElement.style.width='100%';vizElement.style.height='727px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script> -->