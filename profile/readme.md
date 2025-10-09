# TABA — 급발진 감지 & AI 기반 응급 대처 서비스
<img width="1057" height="476" alt="image" src="https://github.com/user-attachments/assets/5011f9cb-7453-47d2-89c3-944e2c62d9f7" />

> **Triggered Acceleration Block Application**  
> 엑셀/브레이크 압력과 속도 데이터를 분석해 급발진을 **입증**하고, 사고 시 **자동으로 119에 신고**하는 스마트 모빌리티 안전 서비스.

---

## 목차(바로가기)
- [프로젝트 한눈에 보기](#프로젝트-한눈에-보기)
- [핵심 기능](#핵심-기능)
- [시스템 아키텍처](#시스템-아키텍처)
- [레포지토리 구조](#레포지토리-구조)
- [데이터 & AI 로직](#데이터--ai-로직)
- [데모](#데모)
- [팀](#팀)

---

## 프로젝트 한눈에 보기
- 운전자가 직접 입증해야 하는 **급발진 사고의 구조적 한계**를 데이터로 보완
- 센서 데이터(엑셀/브레이크 압력, 속도)의 **상관관계 분석**을 통해 **급발진 여부 자동 판단**
- 이상 징후 시 **AI가 즉시 119 신고 및 위치·상태 전송**으로 **골든타임 확보**

<details>
<summary>🔎 프로젝트 요약 이미지 (클릭해 열기)</summary>
<img width="1201" height="719" alt="image" src="https://github.com/user-attachments/assets/0149f378-f5e6-4c39-b287-402e795dcbff" />

> 여기 프로젝트 썸네일 / 문제정의 / 핵심가치 이미지를 첨부해주세요.  
> 예: `/docs/img/summary.png`

</details>

---

## 핵심 기능
- **실시간 감지**: 엑셀·브레이크·속도 스트리밍 수집/분석으로 급발진 판단
- **AI 응급대응**: 사고 감지 즉시 **119 자동 호출**, 위치/상태 데이터 동봉
- **데이터 증거화**: 사고 전후 **시계열 로그**와 **입증 리포트** 자동 생성
- **웹/앱 통합**: 운전자 앱(알림/수동 신고), 웹 대시보드(시각화/로그 열람)

---

## 시스템 아키텍처
- **App(Flutter)** ↔ **Server(Spring Boot)** ↔ **AI(Python/Jupyter)**  
- 실시간 수집 → 전처리/특징 추출 → 이상 탐지(급발진) 판별 → **119 호출** → 대시보드 기록
### 🧩 아키텍처 다이어그램
<img width="1111" height="675" alt="image" src="https://github.com/user-attachments/assets/e23d4671-a34e-48cb-bcf6-749782c0d92a" />


### 📱 모바일 앱 주요 기능
<img width="1400" height="600" alt="image" src="https://github.com/user-attachments/assets/88bcabf6-e3b8-4c77-9363-a9cb76d67684" />

### 🖥️ 웹 대시보드 주요 기능
<img width="1400" height="600" alt="image" src="https://github.com/user-attachments/assets/e768dc56-4e9a-4f79-8402-c88947384274" />

---

## 레포지토리 구조
> 조직: **Project-Taba**

- **Frontend** — 웹 프론트엔드 (React / JavaScript)  
  `https://github.com/Project-Taba/Frontend`
- **Frontend_App** — 모바일 앱 (Flutter / Dart)  
  `https://github.com/Project-Taba/Frontend_App`
- **Server** — 백엔드 서버 (Spring Boot / Java)  
  `https://github.com/Project-Taba/Server`
- **AI** — 모델/분석 (Python / Jupyter Notebook)  
  `https://github.com/Project-Taba/AI`
- **functional_specification_web** — 웹 기능 명세  
  `https://github.com/Project-Taba/functional_specification_web`
- **functional_specification_app** — 앱 기능 명세  
  `https://github.com/Project-Taba/functional_specification_app`

---

## 🧠 데이터 & AI 로직

<img width="100" height="400" alt="AI Logic Diagram" src="https://github.com/user-attachments/assets/0d8d5783-55ca-42df-be3f-6adea7bc2a9c" />

### ⚙️ 모델 개요
- 기존 운전 데이터(`엑셀 압력`, `브레이크 압력`, `속도 변화량`)을 기반으로 **LSTM 모델**을 학습  
- 각 입력은 모두 **Min-Max Scaling** 정규화를 거친 후 학습에 사용  
- 시계열 특성을 반영하여, **이전 5초간 데이터(5개 샘플)**를 통해 **다음 속도 변화량**을 예측  

\[
x_\text{scaled} = \frac{x - x_\text{min}}{x_\text{max} - x_\text{min}}, \quad
v_{\text{shift}} = v_t - v_{t-1}
\]

---

### 🚗 이상 탐지 로직
1. 1초마다 새로운 데이터 `[엑셀 압력, 브레이크 압력, 속도]` 수집  
2. 최근 5개의 데이터를 유지하며, LSTM 모델로 **다음 속도 변화량** 예측  
3. 예측값과 실제 속도 변화량의 차이가 **10 이상**이면 `급발진`으로 판단  
   - 20,000건의 학습 데이터에서 **정규화 후 이상값이 10 이하**로 수렴  
   - OECD·ITF 보고서 기준, **10km/h 차이만으로도 사고 위험률 20% 감소**

---

### 💡 설계 배경
- 동일한 압력이라도 **도로 기울기, 타이어 마모, 제동 환경** 등에 따라 속도 변화가 달라짐  
- 이러한 물리적 환경을 직접 측정하기 어려워,  
  **“이전 값들의 패턴”을 학습해 이상 여부를 판단**하도록 설계  
- 시계열 예측에 적합한 **LSTM 기반 딥러닝 구조**를 채택  

---

<details>
<summary>📈 실제 AI 이상탐지 결과 (클릭해 보기)</summary>
<img width="1156" height="720" alt="AI 이상탐지" src="https://github.com/user-attachments/assets/86a8bcbf-9665-4438-9677-9812b196aba1" />
</details>


---

## 데모
- 앱/웹/AI 시연 영상:
1. 설명용 앱 데모: https://www.youtube.com/watch?v=LlnyRZcJ4HU
2. 설명용 웹 데모: https://www.youtube.com/watch?v=aK-eYY0P0hw

<details>
<summary>🎞️ 데모 캡처 (클릭해 열기)</summary>

> 데모 장면 캡처 이미지를 첨부해주세요.  
> 예: `/docs/img/demo-*.png`

</details>
