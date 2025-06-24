---
title: "[Makeover Monday] Who Spends the Most Time on Social Media?"
excerpt: "Makeover Monday 데이터를 통해 Who Spends the Most Time on Social Media? 대시보드 만들기①"
date: 2025-06-23T13:13:00+09:00
last_modified_at: 2025-06-23T13:13:00+09:00
categories:
  - Makeovermonday
tags:
  - Tableau
  - Makeovermonday
layout: single

---
<div class='tableauPlaceholder' id='vizResponsive' style='position: relative; width: 100%; height: 0; padding-bottom: 62.5%;'>
  <noscript>
    <a href='#'>
      <img alt='대시보드 1' src='https://public.tableau.com/static/images/Ai/WhoSpendstheMostTimeonSocialMediamakeovermonday/1/1_rss.png' style='border: none' />
    </a>
  </noscript>
  <object class='tableauViz' style='position: absolute; top: 0; left: 0; width: 100%; height: 100%;'>
    <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' />
    <param name='embed_code_version' value='3' />
    <param name='site_root' value='' />
    <param name='name' value='WhoSpendstheMostTimeonSocialMediamakeovermonday/1' />
    <param name='tabs' value='no' />
    <param name='toolbar' value='yes' />
    <param name='static_image' value='https://public.tableau.com/static/images/Ai/WhoSpendstheMostTimeonSocialMediamakeovermonday/1/1.png' />
    <param name='animate_transition' value='yes' />
    <param name='display_static_image' value='yes' />
    <param name='display_spinner' value='yes' />
    <param name='display_overlay' value='yes' />
    <param name='display_count' value='yes' />
    <param name='language' value='ko-KR' />
  </object>
</div>
<script type='text/javascript'>
  var divElement = document.getElementById('vizResponsive');
  var vizElement = divElement.getElementsByTagName('object')[0];
  vizElement.style.width = '100%';
  vizElement.style.height = '100%';
  var scriptElement = document.createElement('script');
  scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';
  vizElement.parentNode.insertBefore(scriptElement, vizElement);
</script>
Makeovermonday에 올라온 11월 1주차 주제인 Individuals using the Internet (% of population) 에 관한 대시보드를 구축하였다. 데이터셋은 Makeovermonday 사이트에 올라온 데이터를 사용하여 대시보드를 구축하였다.

<!-- ## 1. 목표 및 니즈 파악

전 세계적으로 자원봉사와 지원 활동에 종사하는 이들의 희생은 점점 더 큰 사회적 문제로 부각되고 있습니다.  
매년 특정 국가에서 지원활동종사자 희생자 수가 급증하며, 경각심을 고취하기 위해 시각적 데이터 분석 도구인 **대시보드**를 기획하고자 합니다.

해당 대시보드는 매년 지원활동종사자의 희생자 수를 한눈에 파악할 수 있도록 설계되었습니다.  
주요 목표는 다음과 같습니다:

- 희생자 수의 **연도별 증가 및 감소 추세**를 확인한다.
- **특정 국가**에서 발생하는 희생자들을 파악한다.
- 데이터를 **시각적으로 명확히 표현**하여 인사이트를 쉽게 전달한다.

## 2. 대시보드 기획
#### 1. 지도 시각화:
전 세계 국가별 희생자 수를 지도에 표시하여 전체적인 희생자 지표를 윈의 크기로 볼 수 있도록 구상하였다. 
또한, 빨간색 원의 크기를 통해 희생자 수의 대략적인 규모를 직관적으로 확인할 수 있으며, 희생이 많이 발생한 국가가 지도에서 두드러지게 보이도록 설계한다.

#### 2. 주요 피해 국가 순위:
총 희생자 수(죽음, 부상, 납치 포함)가 많았던 상위 3개 국가를 대시보드에 별도로 강조하였다. 이들 국가의 희생자 규모와 관련된 구체적인 데이터를 추가로 제공하였다.

#### 3. 기타 국가 데이터 시각화:
나머지 국가들의 희생자 수는 막대 그래프로 표현하여 연도별 희생 규모를 쉽게 비교할 수 있도록 하였다.

#### 4. 연도별 필터 제공:
사용자는 연도별로 데이터를 필터링하여 특정 시점에서 가장 피해가 많았던 국가와 피해량을 확인할 수 있다.

#### 5. 디자인 테마:
대시보드의 전반적인 분위기는 희생의 무게감을 전달하기 위해 어두운 배경을 사용한다. 빨간색과 흰색을 강조색으로 사용하여 데이터를 돋보이게 하였다.

## 3. 대시보드 구현
#### - 지도
  - 원의 크기를 Total affect 값의 크기로 설정하여 피해인원을 보이고자 했으며, 지도는 어둡게 원의 색은 빨간색으로 설정하여 무거운 이미지를 보이도록 구상했다.
  - ountry 이름은 원이 밑에 레이블 표시가 되도록 설정하였고, 해당 지도는 대시보드의 배경처럼 깔리게 설정하였다.

#### - 메인차트
  - 가장 많은 Total affect값을 가진 순서대로 순위를 매겨 1-3위 국가들의 구체적인 정보를 보여주고자 하였다.
  - 일단 1위에 해당하는 부분을 만들고 복제하여 2위 3위가 나오도록 rank 의 수를 조정하였다.

#### - 국가 이름과 순위
  - 국가 이름을 제일 왼쪽에 두어 잘 보이도록 설계하였고, 그 옆에 순위를 보여주어 강조하였다.
  - 'year>' 해당 레이블 뒤에는 연도 필터에 따라 달라지며, 만약 필터에 **전체** or **두 개이상의 연도**가 클릭 되었을 때는 'Two or more years' 라고 뜨고, **한 개의 연도**만 클릭 되어있을 때는 해당 연도가 뜨도록 설정하였다.

#### - KPI
  - Killed, Wounded, Kidnapped 의 값이 보이도록 설정하였다.
  - 3개의 지표를 합쳐서 Total affect 값을 만들었으며, 3개 지표 각각 의미가 크다고 판단하여 kPI로 강조하였다.
  
#### - 성별
  - 성별의 따른 피해인원 수를 보여주기 위해 만들었다.

#### - 자원봉사자 유형
  - 피해자들의 유형을 보여주는 것으로 대체로 위에 있는 원이 national, 아래 있는 원이 internationals이며 두 개의 위치는 피해인원 수에 따라 바뀐다
  - national과 internationals의 수를 보여주며, 두 유형의 비율 차이도 따로 레이블로 표시하였다.
  
#### - 상위 4-15위 국가
  - 상위 4-15위 국가들의 연도별 피해인원수를 보여주며, 연도는 2016~2024년까지 보이도록 설정하였다.
  - 참고로 2024년은 8월까지의 데이터까지 반영되었다.

#### - 필터 & 동작
  - 1,2,3위의 시트에 마우스오보하면 지도에 해당 국가가 하이라이트 되도록 설정하였다.
  - info시트를 이용하여 전체적인 대시보드이 설명을 담아놓았다.


## 4. 결론

- **연도별 희생자 분포:**
특정 연도에 지원활동종사자의 희생자 수가 집중된 국가와 해당 피해 규모를 확인할 수 있다.
예를 들어, 2024년(8월까지 집계)은 2023년을 제외한 다른 연도와 유사한 희생 규모를 보인다. 

- **피해 추세 분석:**
연도별 데이터를 통해 희생자 수가 점차 증가하고 있다는 점을 알 수 있다. 이는 자원봉사자들이 직면하는 위험이 점점 커지고 있음을 시사한다.

- **주요 피해 국가 파악:**
매년 희생자 수가 가장 많았던 국가 TOP3와 그 세부 데이터를 분석할 수 있다. 특히 특정 국가가 지속적으로 상위 3위 안에 포함된다면, 해당 국가의 위험 요인을 분석하고 대응 방안을 마련할 필요성이 강조된다.

이 대시보드는 단순히 데이터를 시각화하는 것을 넘어, 자원봉사자와 지원활동종사자들이 직면한 위험을 보다 명확히 알리고, 국제사회와 관련 단체가 이를 경각심을 가지고 대처할 수 있도록 설계되었다. 특히, 특정 국가에서 지속적으로 희생이 발생한다는 점은 해당 지역의 문제를 국제사회가 보다 심각하게 받아들여야 할 필요성을 보여준다.
희생이 늘어나는 현실은 자원봉사자들에게만 책임을 전가할 수 없는 문제다. 국제적 차원에서 더 강력한 보호 체계를 마련하고, 위험이 도사리는 지역에서의 자원봉사 활동에 대한 대책을 고민해야 할 시점이라고 생각한다.

## 💬 분석 피드백

- 성별 차틀르 굳이 막대로 표현한 것이 너무 평범해보이며, **파이나 다른 차트**로 나타내면 좋을 것으로 판단됨
- 막대그래프를 2016~2024년으로 고정시킨 것이 별로이며, 필터를 움직이면 연도도 **최근 10년**으로 바뀌게 설정하면 좋을 듯
- 그리고 **상위 4-15위까지의 국가**라고 따로 표기해야 이해하기 편할듯 -->

<!-- <div class='tableauPlaceholder' id='viz1750651696925' style='position: relative'><noscript><a href='#'><img alt='대시보드 1 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ai&#47;AidWorkerSecurityIncidentsmakeovermonday&#47;1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='AidWorkerSecurityIncidentsmakeovermonday&#47;1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ai&#47;AidWorkerSecurityIncidentsmakeovermonday&#47;1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='ko-KR' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1750651696925');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else { vizElement.style.width='100%';vizElement.style.height='3577px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script> -->