---
title: "[개인] Retail Rocket ABtest 대시보드 - 가설검정 "
excerpt: "산출한 지표를 통해 가설검정을 실시하자"
date: 2025-08-29T12:00:00+09:00
last_modified_at: 2025-08-29T12:00:00+09:00
toc: true
toc_label: "목차"
toc_sticky: true
categories: [Project,Retail Rocket]
tags: [ecommerce,PostgreSQL, python, ABtest, CVR, Funnel 분석, Path 분석]
layout: single

---

# 1. 가설검정 실시
[![Hypothesis-Testing.py](https://img.shields.io/badge/code-Hypothesis--Testing.py-blue?logo=github)](https://github.com/Whitenut200/Retail-Rocket-ecommerce-ABtest/blob/main/code/Hypothesis-Testing.py)

- 귀무가설 (H₀): A와 B 사이의 <지표>에는 유의미한 차이가 없다.

- 대립가설 (H₁): A와 B 사이의 <지표>에는 유의미한 차이가 있다.

<!-- ============================== -->
<!-- N일 이내의 구매전환율 (CVR)   -->
<!-- ============================== -->
<h2>N일 이내의 구매전환율 (CVR)</h2>
<p>- 주지표에 해당함</p>

<table>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 1일</b>
      <table>
        <tr><th>Group</th><th>Conversions</th><th>Non-Conversions</th><th>CVR</th></tr>
        <tr><td><b>A</b></td><td>6,568</td><td>797,980</td><td>0.0082</td></tr>
        <tr><td><b>B</b></td><td>7,613</td><td>801,504</td><td>0.0094</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 7일</b>
      <table>
        <tr><th>Group</th><th>Conversions</th><th>Non-Conversions</th><th>CVR</th></tr>
        <tr><td><b>A</b></td><td>6,927</td><td>797,621</td><td>0.0086</td></tr>
        <tr><td><b>B</b></td><td>7,965</td><td>801,152</td><td>0.0098</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
  </tr>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 14일</b>
      <table>
        <tr><th>Group</th><th>Conversions</th><th>Non-Conversions</th><th>CVR</th></tr>
        <tr><td><b>A</b></td><td>7,027</td><td>797,521</td><td>0.0087</td></tr>
        <tr><td><b>B</b></td><td>8,092</td><td>801,025</td><td>0.0100</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 30일</b>
      <table>
        <tr><th>Group</th><th>Conversions</th><th>Non-Conversions</th><th>CVR</th></tr>
        <tr><td><b>A</b></td><td>7,096</td><td>797,452</td><td>0.0088</td></tr>
        <tr><td><b>B</b></td><td>8,183</td><td>800,934</td><td>0.0101</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
  </tr>
</table>

<hr/>

<!-- ============================== -->
<!-- Funnel: View → Cart           -->
<!-- ============================== -->
<h2>Funnel 분석 — View → Cart</h2>
<p>- 보조지표에 해당됨</p>

<table>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 1일</b>
      <table>
        <tr><th>Group</th><th>View→Cart</th><th>No Cart</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>18,027</td><td>786,521</td><td>0.0224</td></tr>
        <tr><td><b>B</b></td><td>19,363</td><td>789,754</td><td>0.0239</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 7일</b>
      <table>
        <tr><th>Group</th><th>View→Cart</th><th>No Cart</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>19,000</td><td>785,548</td><td>0.0236</td></tr>
        <tr><td><b>B</b></td><td>20,380</td><td>788,737</td><td>0.0252</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
  </tr>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 14일</b>
      <table>
        <tr><th>Group</th><th>View→Cart</th><th>No Cart</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>19,189</td><td>785,359</td><td>0.0239</td></tr>
        <tr><td><b>B</b></td><td>20,563</td><td>788,554</td><td>0.0254</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 30일</b>
      <table>
        <tr><th>Group</th><th>View→Cart</th><th>No Cart</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>19,306</td><td>785,242</td><td>0.0240</td></tr>
        <tr><td><b>B</b></td><td>20,715</td><td>788,402</td><td>0.0256</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
  </tr>
</table>

<hr/>

<!-- ============================== -->
<!-- Funnel: Cart → Purchase       -->
<!-- ============================== -->
<h2>Funnel 분석 — Cart → Purchase</h2>

<table>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 1일</b>
      <table>
        <tr><th>Group</th><th>Purchase</th><th>No Purchase</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>5,558</td><td>12,469</td><td>0.3083</td></tr>
        <tr><td><b>B</b></td><td>6,545</td><td>12,818</td><td>0.3380</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 7일</b>
      <table>
        <tr><th>Group</th><th>Purchase</th><th>No Purchase</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>6,250</td><td>12,750</td><td>0.3289</td></tr>
        <tr><td><b>B</b></td><td>7,250</td><td>13,130</td><td>0.3557</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
  </tr>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 14일</b>
      <table>
        <tr><th>Group</th><th>Purchase</th><th>No Purchase</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>6,357</td><td>12,832</td><td>0.3313</td></tr>
        <tr><td><b>B</b></td><td>7,382</td><td>13,181</td><td>0.3590</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 30일</b>
      <table>
        <tr><th>Group</th><th>Purchase</th><th>No Purchase</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>6,429</td><td>12,877</td><td>0.3330</td></tr>
        <tr><td><b>B</b></td><td>7,472</td><td>13,243</td><td>0.3607</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0000)</p>

    </td>
  </tr>
</table>

<hr/>

<!-- ============================== -->
<!-- Path: View → Purchase (Direct)-->
<!-- ============================== -->
<h2>Path 분석 — View → Purchase (Direct)</h2>

<table>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 1일</b>
      <table>
        <tr><th>Group</th><th>Direct Purchase</th><th>No Direct</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>597</td><td>5,558</td><td>0.0970</td></tr>
        <tr><td><b>B</b></td><td>616</td><td>6,545</td><td>0.0860</td></tr>
      </table>
      <p><b>Result:</b> A &gt; B (p=0.0282)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 7일</b>
      <table>
        <tr><th>Group</th><th>Direct Purchase</th><th>No Direct</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>645</td><td>6,282</td><td>0.0935</td></tr>
        <tr><td><b>B</b></td><td>681</td><td>7,254</td><td>0.0858</td></tr>
      </table>
      <p><b>Result:</b> A &gt; B (p=0.1030, not significant)</p>

    </td>
  </tr>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 14일</b>
      <table>
        <tr><th>Group</th><th>Direct Purchase</th><th>No Direct</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>654</td><td>6,363</td><td>0.0932</td></tr>
        <tr><td><b>B</b></td><td>698</td><td>7,388</td><td>0.0863</td></tr>
      </table>
      <p><b>Result:</b> A &gt; B (p=0.1396, not significant)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 30일</b>
      <table>
        <tr><th>Group</th><th>Direct Purchase</th><th>No Direct</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>660</td><td>6,435</td><td>0.0930</td></tr>
        <tr><td><b>B</b></td><td>703</td><td>7,479</td><td>0.0859</td></tr>
      </table>
      <p><b>Result:</b> A &gt; B (p=0.1245, not significant)</p>

    </td>
  </tr>
</table>

<hr/>

<!-- ============================== -->
<!-- Path: View → Cart → Purchase  -->
<!-- ============================== -->
<h2>Path 분석 — View → Cart → Purchase (Via cart)</h2>

<table>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 1일</b>
      <table>
        <tr><th>Group</th><th>Cart Path</th><th>Non-Cart Path</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>5,558</td><td>597</td><td>0.9030</td></tr>
        <tr><td><b>B</b></td><td>6,545</td><td>616</td><td>0.9140</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.0282)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 7일</b>
      <table>
        <tr><th>Group</th><th>Cart Path</th><th>Non-Cart Path</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>6,255</td><td>645</td><td>0.9065</td></tr>
        <tr><td><b>B</b></td><td>7,254</td><td>681</td><td>0.9142</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.1030, not significant)</p>

    </td>
  </tr>
  <tr>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 14일</b>
      <table>
        <tr><th>Group</th><th>Cart Path</th><th>Non-Cart Path</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>6,363</td><td>654</td><td>0.9068</td></tr>
        <tr><td><b>B</b></td><td>7,388</td><td>698</td><td>0.9137</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.1396, not significant)</p>

    </td>
    <td style="padding:10px; vertical-align:top;">

      <b>📅 30일</b>
      <table>
        <tr><th>Group</th><th>Cart Path</th><th>Non-Cart Path</th><th>Rate</th></tr>
        <tr><td><b>A</b></td><td>6,435</td><td>660</td><td>0.9070</td></tr>
        <tr><td><b>B</b></td><td>7,479</td><td>703</td><td>0.9141</td></tr>
      </table>
      <p><b>Result:</b> B &gt; A (p=0.1245, not significant)</p>

    </td>
  </tr>
</table>


# 2. 데이터 생성
- 해당 결과를 통합한 시각화용 데이터를 생성

| 기간 | 검정이름        | P-VALUE     | Z통계량   | 신뢰구간_min | 신뢰구간_max | 효과크기   |
|------|----------------|-------------|-----------|--------------|--------------|-----------|
| 1    | CVR            | 0           | 8.4755    | 0.000957     | 0.001533     | 0.001245  |
| 1    | Cart→Purchase  | 8.61E-10    | 6.1333    | 0.020209     | 0.039192     | 0.029700  |
| 1    | Cart경로        | 0.0282      | 2.1940    | 0.001170     | 0.020775     | 0.010973  |
| 1    | Direct경로      | 0.0282      | -2.1940   | -0.020775    | -0.001170    | -0.010973 |
| 1    | View→Cart      | 1.22E-10    | 6.4367    | 0.001060     | 0.001989     | 0.001525  |
| 7    | CVR            | 2.22E-16    | 8.1983    | 0.000939     | 0.001529     | 0.001234  |
| 7    | Cart→Purchase  | 2.17E-08    | 5.5976    | 0.017412     | 0.036175     | 0.026794  |
| 7    | Cart경로        | 0.1030      | 1.6303    | -0.001548    | 0.016860     | 0.007656  |
| 7    | Direct경로      | 0.1030      | -1.6303   | -0.016860    | 0.001548     | -0.007656 |
| 7    | View→Cart      | 9.69E-11    | 6.4717    | 0.001096     | 0.002048     | 0.001572  |
| 14   | CVR            | 0           | 8.3525    | 0.000970     | 0.001564     | 0.001267  |
| 14   | Cart→Purchase  | 6.43E-09    | 5.8053    | 0.018355     | 0.037067     | 0.027711  |
| 14   | Cart경로        | 0.1396      | 1.4771    | -0.002249    | 0.016009     | 0.006880  |
| 14   | Direct경로      | 0.1396      | -1.4771   | -0.016009    | 0.002249     | -0.006880 |
| 14   | View→Cart      | 1.49E-10    | 6.4063    | 0.001085     | 0.002042     | 0.001563  |
| ...   | ...      | ...    | ...    | ...     | ...     | ...  |