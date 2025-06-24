---
title: "[Makeover Monday] Aid Worker Security Incidents Dashboard"
excerpt: "Makeover Monday 데이터를 통해 Aid Worker Security Incidents Dashboard 만들기①"
date: 2025-06-23T13:13:00+09:00
last_modified_at: 2025-06-23T13:13:00+09:00
categories:
  - Tableau Dashboard
tags:
  - Tableau
  - Makeover monday
layout: single

---

Makeover Monday에서 테이터를 가져와서 Tableau로 대시보드를 만들어보았습니다. 지원봉사자들에 관련된 데이터로, 연도별로 지원봉사자들이 큰 피해을 받은 상위 지역 3개를 구체적으로 보여주는 대시보드입니다.

<div class='tableauPlaceholder' id='viz1750651696925' style='position: relative'>
  <noscript><a href='#'><img alt='대시보드 1 ' src='https://public.tableau.com/static/images/Ai/AidWorkerSecurityIncidentsmakeovermonday/1/1_rss.png' style='border: none' /></a></noscript>
  <object class='tableauViz' style='display:none;'>
    <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> 
    <param name='embed_code_version' value='3' /> 
    <param name='site_root' value='' />
    <param name='name' value='AidWorkerSecurityIncidentsmakeovermonday/1' />
    <param name='tabs' value='no' />
    <param name='toolbar' value='yes' />
    <param name='static_image' value='https://public.tableau.com/static/images/Ai/AidWorkerSecurityIncidentsmakeovermonday/1/1.png' />
    <param name='animate_transition' value='yes' />
    <param name='display_static_image' value='yes' />
    <param name='display_spinner' value='yes' />
    <param name='display_overlay' value='yes' />
    <param name='display_count' value='yes' />
    <param name='language' value='ko-KR' />
  </object>
</div>
<script type='text/javascript'>                    
  var divElement = document.getElementById('viz1750651696925');                    
  var vizElement = divElement.getElementsByTagName('object')[0];                    
  if ( divElement.offsetWidth > 800 ) { 
    vizElement.style.width='100%';
    vizElement.style.height=(divElement.offsetWidth*0.75)+'px';
  } else if ( divElement.offsetWidth > 500 ) { 
    vizElement.style.width='100%';
    vizElement.style.height=(divElement.offsetWidth*0.75)+'px';
  } else { 
    vizElement.style.width='100%';
    vizElement.style.height='3577px';
  }                     
  var scriptElement = document.createElement('script');                    
  scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    
  vizElement.parentNode.insertBefore(scriptElement, vizElement);                
</script>





<!-- <div class='tableauPlaceholder' id='viz1750651696925' style='position: relative'><noscript><a href='#'><img alt='대시보드 1 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ai&#47;AidWorkerSecurityIncidentsmakeovermonday&#47;1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='AidWorkerSecurityIncidentsmakeovermonday&#47;1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ai&#47;AidWorkerSecurityIncidentsmakeovermonday&#47;1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='ko-KR' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1750651696925');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else { vizElement.style.width='100%';vizElement.style.height='3577px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script> -->