---
title: "[개인] Retail Rocket ABtest 대시보드 - 프로젝트 개요 "
excerpt: "Retail Rocket 데이터를 가지고 AB test를 진행해보자"
date: 2025-08-25T12:00:00+09:00
last_modified_at: 2025-08-25T12:00:00+09:00
toc: true
toc_label: "목차"
toc_sticky: true
categories: [Project,Retail Rocket]
tags: [ecommerce,PostgreSQL, python, ABtest, CVR, Funnel 분석, Path 분석]
layout: single

---
## 1. 프로젝트 주제
E-commerce 데이터를 활용해 **기존 UI(A)**와 **리메이크된 UI(B)**가 **구매 전환율에 어떤 영향을 미치는지** A/B 테스트 방식으로 검증하였습니다.  
가설검정을 통해 두 UI 중 더 효과적인 방향에 대한 인사이트를 도출하는 것이 본 프로젝트의 목표입니다.  

---

## 2. 데이터
- **출처**: [Retail Rocket eCommerce Dataset (Kaggle)](https://www.kaggle.com/datasets/retailrocket/ecommerce-dataset)

해당 데이터셋은 실제로 A/B 테스트 변수를 제공하지 않기 때문에, **고객 ID를 기준으로 A/B 그룹을 무작위로 균등 분할**하여 가상의 실험 환경을 설정했습니다.  

- A 그룹: 기존 UI를 본 고객  
- B 그룹: 리메이크된 UI를 본 고객  

이러한 가정을 바탕으로, **각 그룹의 구매 전환율 차이**를 검증하기 위해 프로젝트를 진행했습니다.  

---

## 3. 프로젝트 진행 과정
1. **데이터 전처리** – 고객 ID별로 무작위로 A/B 그룹을 배정  
2. **지표 설계 및 산출** – 전환율, 경로 비율 등 실험 설계에 맞는 지표 도출  
3. **가설검정 (Z-test)** – 각 지표별로 두 그룹 간 유의미한 차이가 있는지 확인  
4. **시각화 (Tableau)** – 지표와 검정 결과를 바탕으로 3개의 대시보드 제작  

<p align="center">
  <img src="/assets/images/ABtest_architecture.png" alt="프로젝트 아키텍처" width="1000"/>
</p>  

---

## 4. 데이터 선정 이유
- **고객 ID**를 활용해 무작위 그룹 배정이 가능  
- **날짜 변수**가 상세하게 기록된 로그 데이터라 "N일 이내"와 같은 시계열 지표 산출이 용이  
- 실제 E-commerce 상황과 유사하게 **구매 경로·전환율 분석**이 가능  

따라서 본 프로젝트의 실험 환경에 적합하다고 판단했습니다.  

---

## 5. 구현 방법
- **PostgreSQL**: 지표 산출 및 데이터 처리  
- **Python**: Z-test 기반 가설검정  
- **Tableau**: 결과 시각화 및 대시보드 제작  

---

## 6. 진행 기간
총 **4주**  
- 주제 선정 및 전처리: 1주  
- 지표 산출: 1주  
- 가설검정 및 결과 해석: 0.5주  
- Tableau 대시보드 제작 및 디자인: 1.5주  

---

## 7. 기여도
**100%** (기획 → 데이터 전처리 → 지표 산출 → 가설검정 → 시각화 전 과정 단독 수행)  

---

## 8. 사용 기술 및 도구
- **언어**: Python  
- **데이터베이스**: PostgreSQL  
- **시각화 도구**: Tableau  

---

## 9. 주요 특징
- 실제 데이터에 **가상의 A/B 테스트 환경**을 구성해 분석 수행  
- **SQL**로 지표 산출, **Python**으로 가설검정, **Tableau**로 시각화 진행  
- **주요 지표**: N일 이내 구매 전환율 (CVR)  
- **보조 지표**:  
  - Path 전환율 (Direct: view→purchase, ViaCart: view→cart→purchase)  
  - Funnel 전환율 (view→cart, cart→purchase)  
- **대시보드 구성**: 총 3개 페이지 (CVR, Path, Funnel)  