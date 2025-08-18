# 📌 금융 데이터 고객 이탈 예측 및 세분화 분석
> 팀 프로젝트 (3인 공동 진행, 2025)  
> *클러스터링 설계·시각화 및 인사이트 도출에 주도적 기여*

---

## 📄 프로젝트 개요

- **목표**: 금융 고객 데이터를 활용해 **이탈 예측 모델**을 구축하고, **세분화 기반 맞춤형 리텐션 전략**을 제안  
- **데이터**: Kaggle 공개 신용카드 고객 데이터 (가공·전처리 후 사용)  
- **기간**: 2025.07 ~ 2025.08 (1개월) 
- **형태**: 팀 프로젝트 (3인 공동 진행, 전 과정 협업)  
- **기여도**: 
  - 전 과정(전처리 → EDA → 모델링 → 세분화 → 전략 도출)을 팀원과 공동 수행  
  - **클러스터링(세분화) 설계·시각화** 주도  
  - **인사이트 도출 및 전략 제안** 담당
---

## 📂 파일 구성

```
project_churn/
├─ README.md              # 프로젝트 소개 문서
├─ credit-card-churn_analysis.ipynb   # EDA → 모델링 → 세분화 → 인사이트 전체 코드
└─ data/
   └─ sample_BankChurners.csv    # 원본 데이터 일부 샘플 (10행 정도만 추출)                 
```
## 📄 데이터 출처
- 원본 데이터: [Kaggle - Bank Churn Dataset](https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers)  
- 본 Repo에는 **재현 목적의 샘플 데이터(sample_BankChurners.csv)**만 포함되어 있습니다.  
- 전체 데이터는 Kaggle 링크에서 직접 다운로드 후, `data/BankChurners.csv` 경로에 두고 실행하시면 됩니다.

---

## 📄 분석 및 모델링 과정
1. **데이터 전처리**
   - 데이터 크기: 10,127행 × 21열  
   - Null 값 및 이상치 없음  
   - `CLIENTNUM`: 고객 고유 번호 → 분석 불필요하여 제거  
   - `Attrition_Flag`: 파생 변수 `is_churned` 생성 (0: 유지, 1: 이탈)  
   - 범주형 변수 인코딩 및 Unknown 값 처리  

<br>

2. **탐색적 데이터 분석 (EDA)**
   - 타깃 분포: 이탈 고객 약 16%  
   - Numeric 변수(거래 건수, 총 거래액, 신용한도 등) 분포 확인  
   - Categoric 변수(성별, 카드 유형 등)과 이탈 여부 관계 탐색    

<br>

3. **모델링**
   - Logistic Regression, SVM, Random Forest, LightGBM, CatBoost 비교  
   - **최종 선택: CatBoost (튜닝 후 성능 최적화)**  
   - **불균형 데이터 처리**: Class Weight 적용, Threshold 조정  
   - **평가 지표**: Recall 중심 (이탈 탐지율 최우선)  

<br>

4. **세분화 (Clustering)**
   - 유지 고객을 대상으로 KMeans 군집화 수행 (최적 K=7)  
   - T-SNE/PCA 기반 군집 구조 시각화  
   - ‘이탈 고위험군(Cluster 4)’을 Target으로 지정 후, 저위험군과 비교  
   - **고위험군이 안정 고객군에 근접할 수 있는 전략 도출**

---

## 📄 주요 결과
- 최적 모델: **CatBoost (Optuna 기반 파라미터 조정)**  
- **평가 기준**: 이탈 고객을 최대한 포착하기 위해 Recall을 최우선 지표로 설정  

| 모델         | Recall | F1-score | ROC-AUC |
|-------------|--------|----------|---------|
| CatBoost    | **0.92** | **0.89** | **0.99** |

- Precision 일부 손실이 있었지만, Recall을 크게 향상시켜 **이탈 고객을 놓치지 않는 방향**으로 최적화됨



- 주요 Feature 중요도:  
  - `Total_Trans_Ct` (총 거래 건수)  
  - `Total_Trans_Amt` (총 거래 금액)  
  - `Total_Revolving_Bal` (리볼빙 잔액)  

---

## 📄 인사이트 & 기대 효과
- **이탈 고위험군(Target)** → 거래 활성화 / 잔고 활용 유도 전략 필요  
- **예상 효과 (추정치)**  
  - 단기: 약 **846만 원** 매출 유지 (이탈률 10%p 감소 시)  
  - 중기: 최대 **4.4억 원** 매출 유지 (저위험군 중 대표 Cluster ‘Low3’ 수준 도달 시)  
  - 장기: LTV 극대화 및 고객 기반 안정화  

---

## 📄 기술 스택
- Python (Pandas, NumPy, Scikit-learn, LightGBM, CatBoost)  
- Visualization (Matplotlib, Seaborn)  
- Jupyter Notebook  
- Git/GitHub  

---

## 📄 참고
- 데이터 출처: Kaggle [Bank Churn Dataset]  
- 본 프로젝트는 **학습·포트폴리오 목적**으로 진행되었으며, 실제 금융사 데이터가 아님을 명시합니다.
