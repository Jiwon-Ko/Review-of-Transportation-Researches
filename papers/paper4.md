# Multisource Methodology for Traffic Analysis Zone Definition
*Based on the fusion of Remote Sensing, OpenStreetMap, and Floating Car Data*  

---

## 📄 기본 정보
- **저널:** *Journal of Transport Geography* (2025)  
- **저자:** Marisdea Castiglione, Federico Gallo, Martina Pastorino, Gabriele Moser, Marialisa Nigro, Nicola Sacco  
- **DOI:** [10.1016/j.jtrangeo.2025.104324](https://doi.org/10.1016/j.jtrangeo.2025.104324)  
- **키워드:** Traffic Analysis Zones (TAZ), Remote Sensing, OpenStreetMap, Floating Car Data, Spatial Clustering  

---

## 🎯 연구 목적
- 교통 수요 모델링에서 핵심 단위인 **교통 분석 구역(TAZ)** 정의 문제 해결.  
- 기존 방식: 행정구역/전문가 경험 의존 → **주관적, 갱신 어려움, 내존 통행 과다**.  
- 새로운 접근: **위성 원격탐사(RS) + OSM + Floating Car Data(FCD)** 융합을 통한 **데이터 기반 자동 TAZ 정의 방법론** 제안.  

---

## 🧩 방법론 개요
1. **입력 데이터**
   - Sentinel-2 위성영상 (NDVI 계산)
   - ESA WorldCover 토지피복 지도
   - OpenStreetMap (건물, 도로, 시설)
   - Floating Car Data (약 150만 건 차량 이동 기록)  

2. **단계별 절차**
   - **BSU 생성 (Basic Spatial Units)**  
     - NDVI 기반 **워터셰드 세그멘테이션**으로 균질 소구역 자동 분할  
     - 형태학적 연산으로 경계 매끈화 및 잡영역 제거  
   - **TAZ 집합 정의**  
     - BSU 특성(OSM + 토지피복)으로 **계층적 클러스터링**  
     - 실루엣 계수로 최적 클러스터 수 결정  
     - 공간 연속성 확보 → 불연속 영역 수정  
   - **보정 단계 (선택)**  
     - FCD 기반 OD 매트릭스 분석  
     - **내존 통행 최소화**를 위한 경계 재조정  

---

## 📊 주요 결과
- 사례지역: **로마 EUR 지구**  
- 결과 TAZ는:  
  - **토지이용/활동/도로망 동질성 확보**  
  - **자연적·인공적 경계(강, 녹지, 주요도로)**를 잘 반영  
  - 기존 행정구역 기반 TAZ보다 **내존 통행 비율↓, OD 매트릭스 정확도↑**  
- 자동화로 인해 **정기적 업데이트 가능**, 다른 도시에도 손쉽게 적용 가능  

---

## 🚦 결론 및 기여
1. **최초의 RS+OSM+FCD 융합 기반 TAZ 정의 프레임워크** 제시  
2. 전문가 의존적 절차를 보완할 **데이터 기반·자동화된 구역 설정 도구** 제공  
3. 교통 수요예측, 도시계획, 스마트 모빌리티 연구에 활용 가능  
4. 향후 빅데이터·스마트시티 기반 교통 모델링에 확장 가능  

---

## 📌 구조 요약
- **1절 Introduction:** TAZ 정의의 중요성과 기존 한계 제시  
- **2절 Literature Review:** 기존 방법론(통계·GIS·빅데이터·RS 응용) 검토, 연구 공백 확인  
- **3절 Methodology:** RS 세그멘테이션으로 BSU 생성 → OSM/토지피복 기반 군집화 → FCD 기반 내존통행 최소화  
- **4절 Case Study:** 로마 EUR 지구 사례 검증, 기존 대비 OD 품질 개선 확인  
- **5절 Conclusion:** 제안 기법의 장점·보편성 강조, 향후 교통계획·정책 활용 가능성 제시  

