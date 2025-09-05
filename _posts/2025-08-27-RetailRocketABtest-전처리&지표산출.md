---
title: "[개인] Retail Rocket ABtest 대시보드 - 전처리 및 지표산출 "
excerpt: "Retail Rocket 데이터를 전처리하고 주지표, 보조지표를 선정하여 관련 지표를 산출하자"
date: 2025-08-27T12:00:00+09:00
last_modified_at: 2025-08-27T12:00:00+09:00
toc: true
toc_label: "목차"
toc_sticky: true
categories: [Prodject,Retail Rocket]
tags: [ecommerce,PostgreSQL, python, ABtest, CTV, Funnel 분석, Path 분석]
layout: single

---
<script type="text/javascript" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

## 1. 데이터 전처리
[![preprocessing.py](https://img.shields.io/badge/code-preprocessing.py-blue?logo=github)](https://github.com/Whitenut200/Retail-Rocket-ecommerce-ABtest/blob/main/code/preprocessing.py)
[![AB-add.py](https://img.shields.io/badge/code-AB--add.py-blue?logo=github)](https://github.com/Whitenut200/Retail-Rocket-ecommerce-ABtest/blob/main/code/AB-add.py)

### 원본데이터 구성
- **events**
  - 고객행동에 대한 모든 로그데이터
- **category_tree**
  - itemid,categoryid 관계
- **item_properties**
  - part1, part2로 나누어져있으며, category나 item 관련 변경사항 로그데이터

### 전처리 내용

1. 날짜 형식 변경
  - timestamp 형식에서 date형식으로 변경

2. item_properties_part1, item_properties_part2 유니온
  - 같은 내용을 담고 있으므로 서로 유니온처치

3. category_tree와 item_properties 병합
  - item_properties에서 catagoryid에 대한 내용만 가져오기
  - 두 데이터 조인

4. category_item과 events 병합
  - itemid가 서로 같으면 category_item에 존재하는 categoryid 가져오기
  - 근데, 로그데이터여서 서로 date가 존재해서
    - events.itemid의 날짜가 category_item의 날짜보다 더 최신일 경우에 해당 categoryid 가져오기
    - 반대의 경우 nan로 처리하거나 그 전의 값이 존재하다면 그거 가져오기(가장 가까운 과거값)
  - 두 데이터 join

5. A,B할당
  - userid만 추출하여 무작위로 A,B 할당하여 원래 데이터와 조인 (5:5)

## 2. 지표 산출
[![Metric-calculation.sql](https://img.shields.io/badge/code-Metric--calculation.sql-blue?logo=github)](https://github.com/Whitenut200/Retail-Rocket-ecommerce-ABtest/blob/main/code/Metric-calculation.sql)

### 1. 주지표 — N일 이내 구매전환율, N=1,7,14,30
$$
PCR_{7d} = \frac{count(View \rightarrow Purchase\ (within\ 7d))}{total(View)}
$$

---

### 2. 보조지표
#### 2-1. 경로 지표 (Path Composition, N일 이내)

- **View → Cart → Purchase (via_cart)**  

  $$
  \frac{count(View \rightarrow Cart \rightarrow Purchase)}{total(Purchase)}
  $$

- **View → Purchase (Direct, no cart)**  

  $$
  \frac{count(View \rightarrow Purchase\ (no\ Cart))}{total(Purchase)}
  $$

#### 2-2. 퍼널 지표 (Funnel Rates, N일 이내)

- **View → Cart**  

  $$
  \frac{count(View \rightarrow Cart)}{total(View)}
  $$

- **Cart → Purchase**  

  $$
  \frac{count(Cart \rightarrow Purchase\ (within\ 7d))}{total(Cart)}
  $$

---

### 데이터 생성

| 기간 | AB그룹 | 카테고리ID | 구매자수 | 총뷰수 | 전환율  | 평균구매소요일수 | 뷰투카트전환자수 | 총뷰수_퍼널 | 뷰투카트전환율 | 카트투구매전환자수 | 총카트수 | 카트투구매전환율 | 직접구매수 | 카트경유구매수 | 총구매수 | 직접구매비율 | 카트경유구매비율 |
|------|--------|------------|----------|--------|--------|------------------|------------------|-------------|----------------|-------------------|----------|-----------------|------------|----------------|----------|--------------|-----------------|
| 1    | A      | 0          | 3        | 380    | 0.0079 | 0.1071           | 15               | 380         | 0.0395         | 2                 | 15       | 0.1333          | 0          | 2              | 2        | 0            | 1               |
| 1    | A      | 1          | 21       | 2007   | 0.0105 | 0.0322           | 109              | 2007        | 0.0543         | 18                | 109      | 0.1651          | 1          | 18             | 19       | 0.0526       | 0.9474          |
| 1    | A      | 10         | 0        | 1      | 0      | 0                | 0                | 1           | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 100        | 0        | 5      | 0      | 0                | 0                | 5           | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 1000       | 0        | 7      | 0      | 0                | 0                | 7           | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 1001       | 2        | 378    | 0.0053 | 0                | 4                | 378         | 0.0106         | 1                 | 4        | 0.25            | 1          | 1              | 2        | 0.5          | 0.5             |
| 1    | A      | 1002       | 6        | 1222   | 0.0049 | 0.0121           | 24               | 1222        | 0.0196         | 4                 | 24       | 0.1667          | 0          | 4              | 4        | 0            | 1               |
| 1    | A      | 1003       | 1        | 619    | 0.0016 | 0                | 6                | 619         | 0.0097         | 1                 | 6        | 0.1667          | 0          | 1              | 1        | 0            | 1               |
| 1    | A      | 1006       | 5        | 793    | 0.0063 | 0                | 27               | 793         | 0.0340         | 4                 | 27       | 0.1481          | 1          | 4              | 5        | 0.2          | 0.8             |
| 1    | A      | 1007       | 0        | 1745   | 0      | 0                | 0                | 1745        | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 1008       | 0        | 209    | 0      | 0                | 0                | 209         | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 1010       | 0        | 25     | 0      | 0                | 0                | 25          | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 1011       | 5        | 493    | 0.0101 | 0                | 12               | 493         | 0.0243         | 4                 | 12       | 0.3333          | 1          | 4              | 5        | 0.2          | 0.8             |
| 1    | A      | 1013       | 0        | 7      | 0      | 0                | 0                | 7           | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 1014       | 2        | 263    | 0.0076 | 0.0333           | 3                | 263         | 0.0114         | 1                 | 3        | 0.3333          | 0          | 1              | 1        | 0            | 1               |
| 1    | A      | 1015       | 0        | 52     | 0      | 0                | 0                | 52          | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 1016       | 0        | 20     | 0      | 0                | 0                | 20          | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 1017       | 1        | 146    | 0.0068 | 0.1875           | 3                | 146         | 0.0205         | 0                 | 3        | 0               | 1          | 0              | 1        | 1            | 0               |
| 1    | A      | 1018       | 35       | 3062   | 0.0114 | 0.0877           | 109              | 3062        | 0.0356         | 32                | 109      | 0.2936          | 1          | 32             | 33       | 0.0303       | 0.9697          |
| 1    | A      | 1019       | 0        | 14     | 0      | 0                | 0                | 14          | 0              | 0                 | 0        | 0               | 0          | 0              | 0        | 0            | 0               |
| 1    | A      | 102        | 1        | 71     | 0.0141 | 0                | 3                | 71          | 0.0423         | 1                 | 3        | 0.3333          | 0          | 1              | 1        | 0            | 1               |
| 1    | A      | 1020       | 17       | 1037   | 0.0164 | 0.2062           | 32               | 1037        | 0.0309         | 13                | 32       | 0.4063          | 3          | 13             | 16       | 0.1875       | 0.8125          |
| ...  | ...    | ...        | ...      | ...    | ...    | ...              | ...              | ...         | ...            | ...               | ...      | ...             | ...        | ...            | ...      | ...          | ...             |

### 계산 기준

본 A/B 테스트에서는 전환 계산을 엄격하게 정의함

1. **동일 사용자**: user_id가 일치해야 함  
2. **동일 아이템 & 카테고리**: item_id, category_id가 View/Cart/Purchase 간 일치  
3. **시간 제한**: View 또는 Cart 이후 **7일 이내**의 Purchase만 인정  
4. **Direct 정의**: Cart 이벤트 없이 View → Purchase된 경우만 Direct  
5. **Viacart 정의**: View -> Cart -> Purchase된 경우만 
6. **중복 제거**: 동일 사용자·아이템 조합은 **1회 전환만** 집계  

---

### 메모

- 위와 같은 엄격 조건으로 인해 **전환율 수치가 실제보다 낮게 측정**
- 그러나 이는 **A/B 테스트의 내적 타당성**(같은 아이템·카테고리 내 비교)을 높이기 위해 
- 실무에서는 종종 **느슨한 조건**(예: 카테고리만 일치, 세션 범위, 라스트 터치 등)을 사용하지만,  
  본 프로젝트는 **실험 정확성 확보**를 위해 엄격 기준을 채택함