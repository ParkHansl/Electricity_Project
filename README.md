# LS 전력 예측 프로젝트

**LS 빅데이터 스쿨 4기 팀 프로젝트**

LS 전력 데이터를 활용하여 대시보드를 제작하는 팀 프로젝트입니다.

[프로젝트 대시보드 바로가기 링크]()

<br>

---

## 팀원 소개

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/bokyung13">
        <img src="https://github.com/bokyung13.png" width="100px;" alt="bokyung13"/>
        <br />
        <sub><b>김보경</b></sub>
      </a>
      <br />
      EDA / 데이터 전처리<br />
      streamlit p.2 <br />
      배포
    </td>
    <td align="center">
      <a href="https://github.com/yewon-kim-alt">
        <img src="https://github.com/yewon-kim-alt.png" width="100px;" alt="yewon-kim-alt"/>
        <br />
        <sub><b>김예원</b></sub>
      </a>
      <br />
      EDA / 데이터 전처리<br />
      streamlit p.1
    </td>
    <td align="center">
      <a href="https://github.com/wonjeongnam">
        <img src="https://github.com/wonjeongnam.png" width="100px;" alt="wonjeongnam"/>
        <br />
        <sub><b>남원정</b></sub>
      </a>
      <br />
      EDA / 데이터 전처리<br />
      streamlit p.1
    </td>
    <td align="center">
      <a href="https://github.com/ParkHansl">
        <img src="https://github.com/ParkHansl.png" width="100px;" alt="ParkHansl"/>
        <br />
        <sub><b>박한슬</b></sub>
      </a>
      <br />
      데이터 분석<br />
      streamlit 보조
    </td>
  </tr>
</table>

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/JunKane">
        <img src="https://github.com/JunKane.png" width="100px;" alt="JunKane"/>
        <br />
        <sub><b>양현준</b></sub>
      </a>
      <br />
      EDA / 데이터 전처리<br />
      streamlit p.2 <br />
      **조장**
    </td>
    <td align="center">
      <a href="https://github.com/tjdud2604">
        <img src="https://github.com/tjdud2604.png" width="100px;" alt="leechanghyuk"/>
        <br />
        <sub><b>편서영</b></sub>
      </a>
      <br />
      EDA / 데이터 전처리<br />
      발표
    </td>
     <td align="center">
      <a href="https://github.com/godfuf">
        <img src="https://github.com/godfuf.png" width="100px;" alt="godfuf"/>
        <br />
        <sub><b>홍주형</b></sub>
      </a>
      <br />
      모델링 전담<br />
    </td>
    
  </tr>
</table>

<br />

---

## 데이터 설명

모델 훈련 및 실시간 모니터링에 사용되는 주요 컬럼은 다음과 같습니다:

| 컬럼명                    | 설명                                                                                                 |
| ------------------------- | ---------------------------------------------------------------------------------------------------- |
| **id**                    | 고유 관측 식별자                                                                                     |
| **측정일시**              | 전력 계측 시각 (YYYY-MM-DD HH:MM 형태의 타임스탬프)                                                  |
| **전력사용량(kWh)**       | 실제 소비된 유효 전력량 (킬로와트시)                                                                 |
| **지상무효전력량(kVarh)** | 유도성(Inductive) 무효 전력량 (킬로바트-무효시)                                                      |
| **진상무효전력량(kVarh)** | 용량성(Capacitive) 무효 전력량 (킬로바트-무효시)                                                     |
| **탄소배출량(tCO₂)**      | 전력 사용으로 발생한 이산화탄소 배출량 (톤 단위)                                                     |
| **지상역률(%)**           | 인덕티브 부하 상태에서의 전력 계수(역률) (%)                                                         |
| **진상역률(%)**           | 용량성 부하 상태에서의 전력 계수(역률) (%)                                                           |
| **작업유형**              | 부하 유형 구분<br>- `Light_Load` : 경부하<br>- `Medium_Load` : 중부하<br>- `Maximum_Load` : 최대부하 |
| **전기요금(원)**          | 해당 시점 전력 사용 요금 (원 단위, 모델의 예측 대상)                                                 |

> **참고**
>
> - `지상역률`, `진상역률`은 전력회사의 요금 체계에서 중요한 역률 기준이며, 이를 이진화(`지상역률_이진`, `진상역률_이진`)해 실시간 경고에 활용합니다.
> - `탄소배출량`은 전력 사용량에 비례하여 산출된 추정치이며, 친환경 지표로 함께 모니터링됩니다.

---

## 실시간 전기요금 예측 시스템

Streamlit 기반의 **“실시간 전기요금 예측 시스템”** 은 AI 예측 모델을 활용해  
전력 사용량·요금·역률·SHAP 기반 변수 기여도를 실시간으로 모니터링할 수 있는 대시보드입니다.

### 🔧 주요 기능

- **실시간 스트리밍**: ▶️ 시작 / ⏸️ 정지 / 🔄 리셋
- **누적 KPI 카드**:
  - 전기요금(원), 전력사용량(kWh), 지상무효·진상무효전력(kVarh), 탄소배출량(tCO₂)
- **예측 요금 추이**: 10초 간격으로 업데이트되는 Plotly 라인 차트
- **누적 SHAP 분석**:
  - 변수별 평균 |SHAP| 막대차트 → 모델 해석성 확보
- **실시간 원본 데이터 테이블**:
  - 페이징(8행씩) → 최신 `측정일시`, 주요 피처, 예측 타겟 확인
- **최근 SHAP 기여도**:
  - 마지막 인스턴스별 변수별 양·음영 색상 막대차트

### 🎨 UI & 스타일링

- **Wide 레이아웃**: `layout="wide"`
- **Custom CSS**:
  - Noto Sans KR 폰트, 카드·테이블·차트 컨테이너 일관된 화이트 테마
  - KPI 카드·정보 카드·상태 인디케이터 디자인
- **Plotly & Streamlit 컴포넌트** 활용

### ⚙️ 사이드바 제어판

- **시스템 제어**:
  - Start / Stop / Reset 버튼
  - 상태 인디케이터(🟢 실행 중 / 🔴 정지됨)
- **버튼 스타일**: 호버·활성화 애니메이션

---

## 과가 전기 요금 분석대시보드

Streamlit 기반의 **“통합 전력 분석 시스템”** 은 실시간 전력 사용량·요금·역률 등을 한눈에 볼 수 있도록 설계된 대시보드입니다.

### 🎨 UI & 스타일링

- **Wide 레이아웃**: `st.set_page_config(layout="wide")`
- **Custom CSS**: Google-font(Noto Sans KR) 적용, 헤더·카드·테이블·차트 등 일관된 디자인
- **Matplotlib & Plotly** 시각화 모두 지원

### 🔧 사이드바 필터

- **분석 기간**: 월별 / 일별 전환
- **지표 선택**: 전력사용량, 전기요금, 탄소배출량, 역률 등 두 축 비교
- **보고서 생성**: `.docx` 포맷으로 자동 문서화 및 다운로드

### 📊 주요 컴포넌트

- **메인 지표 카드**
  - 총 전력(kWh), 전기요금(원), 평균 단가(원/kWh), 탄소배출량(tCO₂)
- **주·야간 역률 카드**
  - 전일 대비 변화량에 따른 신호등 표시(🟢🟡🔴)
- **듀얼 축 차트**
  - Plotly로 두 지표를 X축(시간/날짜) 기준 병렬 비교
- **스택형 막대 & 도넛 차트**
  - 작업유형별 시간대별 요금·사용량 분포

### 📄 맞춤형 보고서 생성

- **Word(.docx)** 라이브러리 사용
- 문서 테두리, 헤더 정보, 분석 요약, 차트(영어 레이블) 포함
- “보고서 생성” 버튼 클릭으로 즉시 다운로드

---

## 모델 설명

**완전한 통합 모델 – 딥러닝 5-fold CV 개선 버전**  
기존의 고급 머신러닝 모델과 딥러닝 모델을 결합하여 5-fold 시계열 교차검증을 통해 더욱 안정적인 예측을 수행하고, 최종적으로 스태킹 앙상블로 예측값을 결합합니다.

1. **머신러닝 모델 (Traditional)**

   - RandomForestRegressor (n_estimators=500, max_depth=15)
   - XGBoostRegressor (n_estimators=800, max_depth=6, learning_rate=0.05)
   - LightGBMRegressor (n_estimators=800, max_depth=7, learning_rate=0.05)
   - CatBoostRegressor (iterations=800, depth=6, learning_rate=0.05)

2. **딥러닝 모델 (Deep)**

   - **LSTM**
     - 2-layer LSTM (128→64 units), BatchNorm, Dropout
   - **GRU**
     - 2-layer GRU (128→64 units), BatchNorm, Dropout
   - _(Transformer, CNN-LSTM 등은 주석 처리하여 사용하지 않음)_

3. **데이터 파이프라인**

   - **특징 생성**  
     시계열 및 정적 피처 1) 기본 시간 피처 2) 예측 대상 전력 변수 예측 3) 고급 조합·라그·롤링 피처 4) 비선형 및 상호작용 피처
   - **딥러닝용 시퀀스 제작**
     - `sequence_length = 48` (15분 단위 데이터 기준 약 12시간)
     - 과거 48행을 입력으로, 다음 시점 전기요금 예측
   - **스케일링**
     - 시계열 피처, 정적 피처, 타깃 모두 StandardScaler 적용

4. **5-fold 시계열 교차검증 (TimeSeriesSplit)**

   - 각 모델별로 5회 분할 학습 → Fold별 MAE 기록
   - **평균(MAE_avg)** 과 **최소(MAE_min)** 방식으로 두 결과 저장

5. **완벽한 스태킹 앙상블**

   - Level-1: 모든 모델의 CV 예측값을 메타 피처로 생성
     - 전통 모델은 실제 CV 예측, 딥러닝 모델은 전통 모델 평균에 노이즈(딥러닝 MAE 기반) 추가
   - Level-2: Ridge 메타 모델 학습 → 최종 스태킹 예측

6. **최종 앙상블 전략**
   - **가중 평균**: CV MAE 기반 역수 가중치
   - **스태킹**: Meta-Ridge 결과
   - 두 방법 MAE 비교 후 더 우수한 쪽 선택

---
