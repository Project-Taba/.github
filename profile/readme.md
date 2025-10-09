# TABA — 급발진 감지 & AI 기반 응급 대처 서비스
<div align="center">
   <img width="600" height="250" alt="image" src="https://github.com/user-attachments/assets/5011f9cb-7453-47d2-89c3-944e2c62d9f7" />
</div>

> **타봐! Triggered Acceleration Block Application**  
> 엑셀/브레이크 압력과 속도 데이터를 분석해 급발진을 **판단**하고, **자동으로 119에 신고**하는 스마트 모빌리티 안전 서비스.

---

## 목차(바로가기)
- [프로젝트 개요](#프로젝트-개요)
- [시스템 아키텍처](#시스템-아키텍처)
- [핵심 기능](#핵심-기능)
- [AI 로직](#ai-로직)
- [실험 및 시연 영상](#실험-및-시연-영상)
- [레포지토리 구조](#레포지토리-구조)
---

## 프로젝트 개요

- 운전자가 직접 입증해야 하는 **급발진 사고의 구조적 한계**를 데이터로 보완
- 센서 데이터(엑셀/브레이크 압력, 속도)의 **상관관계 분석**을 통해 **브레이크 오작동 여부 판단**
- 이상 징후(브레이크 오작동) 시 **AI가 즉시 119 신고 및 위치·상태 전송**으로 **골든타임 확보**

---

## 시스템 아키텍처
- **App(Flutter)** ↔ **Server(Spring Boot)** ↔ **AI(Keras)**  
- 실시간 수집 → 전처리/특징 추출 → 이상 탐지(급발진) 판별 → **119 호출** → 대시보드 기록
### 🧩 아키텍처 다이어그램

<div align="center">
<img width="1000" height="400" alt="image" src="https://github.com/user-attachments/assets/e23d4671-a34e-48cb-bcf6-749782c0d92a" />
</div>

### 📱 모바일 앱 기능 요약

<div align="center">
<img width="1000" height="400" alt="image" src="https://github.com/user-attachments/assets/88bcabf6-e3b8-4c77-9363-a9cb76d67684" />
</div>

### 🖥️ 웹 대시보드 기능 요약

<div align="center">
<img width="1000" height="400" alt="image" src="https://github.com/user-attachments/assets/e768dc56-4e9a-4f79-8402-c88947384274" />
</div>

---

## 핵심 기능

<details>
<summary>🚗 내비게이션 </summary>

<br/>
   
<div align="left">

기능 요약
1. 목적지 키워드 기반 검색
2. 목적지 최단 거리 폴리라인
3. 운행 엑셀·브레이크·속도 실시간 데이터를 통한 시각화 
   
<br/>

![Image](https://github.com/user-attachments/assets/a44ce901-8b81-4592-bf66-81dc4599b280)
<img width="280" height="500" alt="image" src="https://github.com/user-attachments/assets/aaf66319-2c86-4fa4-853e-3df636a5426f" />
</div>

</details>

<details>
<summary>🆘 AI 기반 응급 대처 </summary>

<br/>
   
<div align="left">

기능 요약
1. 모든 사용자를 위한 페달 압력 캘리브레이션(Min-Max Scaling 정규화)
2. 브레이크 오작동 감지시 119 자동 호출
3. 웹 대시보드에서 사용자 위치/상태 실시간 확인
   
<br/>

<img src="https://github.com/user-attachments/assets/f9b88307-25b6-4d23-bec2-12269a6c3ed9" width="260" height="480" />
<img src="https://github.com/user-attachments/assets/f43ac1e0-b753-474e-82d6-f80aee28236c" width="260" height="480" />
<img src="https://github.com/user-attachments/assets/b0f8fddf-a43d-40a6-aab3-db31dd54a95c" width="260" height="480" />


<img width="400" height="210" alt="image" src="https://github.com/user-attachments/assets/848d43ed-d521-406b-9fd4-99cfe19bfa0e" />
<img width="400" height="210" alt="image" src="https://github.com/user-attachments/assets/d457b3fd-9d99-467d-8dcd-c8995e393971" />

</div>

</details>


<details>
<summary>📊 이상 탐지 데이터 관리</summary>

<br/>
   
<div align="left">

기능 요약
1. 이상 탐지 전후 차량 데이터만 DB 저장  
2. 모바일 앱에 해당 데이터 차트로 제공  
3. 웹 대시보드에서 엑셀파일 다운로드  

<br/>

<img src="https://github.com/user-attachments/assets/bc65908d-2df2-4f31-ad52-2f0826b694f2" width="280" height="500" style="border-radius:10px; margin-right:10px;" />
<img src="https://github.com/user-attachments/assets/7fb6a8b4-44f4-45aa-be98-9e718d7c4a64" width="540" height="360" style="border-radius:10px;" />

</div>

</details>


<details>
<summary>⚙️ 운전 습관 측정 </summary>

<br/>
   
<div align="left">

기능 요약
1. 페달 압력, 차량 속도 기반 양발 운전·급출발·급정거 습관 제공
2. 운행 폴리 라인, 운행시간, 운행거리 제공
   
<br/>


<img src="https://github.com/user-attachments/assets/7bf0ead1-1ab6-4e45-b4a6-bed720cea792" width="280" height="500" style="border-radius:10px; margin-right:10px;" />
<img src="https://github.com/user-attachments/assets/57ddd83d-a260-41e3-bd23-ff1868c2ff7c" width="280" height="500" style="border-radius:10px; margin-right:10px;" />

</div>

</details>

---


## AI 로직

<img width="800" height="300" alt="AI Logic Diagram" src="https://github.com/user-attachments/assets/0d8d5783-55ca-42df-be3f-6adea7bc2a9c" />

### ⚙️ 모델 개요
- 기존 운전 데이터(`엑셀 압력`, `브레이크 압력`, `속도 변화량`)을 기반으로 **LSTM 모델**을 학습  
- 각 입력은 모두 **Min-Max Scaling** 정규화를 거친 후 학습에 사용  
- 시계열 특성을 반영하여, **이전 5초간 데이터(5개 샘플)** 를 통해 **다음 속도 변화량**을 예측

### 🚗 이상 탐지 로직
1. 1초마다 새로운 데이터 `[엑셀 압력, 브레이크 압력, 속도]` 수집  
2. 최근 5개의 데이터를 유지하며, LSTM 모델로 **다음 속도 변화량** 예측  
3. 예측값과 실제 속도 변화량의 차이가 **8 이상**이면 `급발진`으로 판단  
   - 22,000건의 학습 데이터에서 **정규화 후 이상값이 10 이하**로 수렴  
   - 국제교통포럼(OECD·ITF) 보고서 기준, **10km/h 차이만으로도 사고 위험률 20% 감소**

### 💡 설계 배경
- 동일한 압력이라도 **도로 기울기, 타이어 마모, 제동 환경** 등에 따라 속도 변화가 달라짐  
- 이러한 물리적 환경을 직접 측정하기 어려워, **"정해진 윈도우(5초) 값들의 패턴"으로 이상 여부를 판단**하도록 설계  
- 시계열 예측에 적합한 **LSTM 기반 딥러닝 구조**를 채택  

### 📈 실제 AI 이상탐지 결과
<img width="1100" height="500" alt="AI 이상탐지" src="https://github.com/user-attachments/assets/86a8bcbf-9665-4438-9677-9812b196aba1" />


---

## 실험 및 시연 영상

### 🚘 하드웨어 제품 및 주행 실험
> 실제 주행 환경에서 센서·앱·AI의 연동을 검증하기 위해 실차 테스트를 진행했습니다.  

<div align="center">
   <img width="900" alt="제품 및 실험" src="https://github.com/user-attachments/assets/5fd5165a-29f7-4582-918e-9e7f7a678721" />
   <p align="center"><em>차량 내 센서 설치 및 TABA 앱 실시간 연동 장면</em></p>
</div>

<div align="center">
   <img width="800" height="300" alt="image" src="https://github.com/user-attachments/assets/95b45571-2908-4b1a-88f3-45ebb6fcb7d0" />
   <p align="center"><em> 실제 이상 탐지 감지 DB 기록 내역</em></p>
</div>

---

### 🎬 시연 영상 (App / Web / AI 통합)

| 구분 | 설명 | 링크 |
|------|------|------|
| 📱 **앱 데모** | Flutter 기반 실시간 주행 데이터 시각화 | [YouTube](https://www.youtube.com/watch?v=LlnyRZcJ4HU) |
| 🖥️ **웹 대시보드 데모** | AI 응급대응 및 위치 모니터링 관리 화면 | [YouTube](https://www.youtube.com/watch?v=aK-eYY0P0hw) |
| ⚙️ **페달 캘리브레이션 측정** | 자동차 페달 압력 센서 값 측정 및 보정 | [YouTube Shorts](https://youtube.com/shorts/9eompbtX2hE?feature=share) |
| 🚨 **급발진 상황 감지 (앱 + AI)** | 급발진 발생 시 AI 이상 탐지 및 자동 신고 | [YouTube](https://youtu.be/Otl3w4VNpLc?si=G6EXhFz4sbFQ5sRj) |
| 🚗 **TMap & TABA 앱 동시 실행** | 실제 차량 주행 중 실시간 센서·속도 연동 시연 | [YouTube Shorts](https://youtube.com/shorts/BzHTwrxtZ7Q?feature=share) |


> **시연 요약**  
> 실제 차량 환경에서 페달 센서 입력값을 기반으로 **급발진 탐지 AI 모델**을 구동하고,  
> 감지 시 **119 API 호출 → 웹 대시보드 알림 → MongoDB 데이터 기록 → 앱 실시간 시각화**까지  
> 전 과정을 통합적으로 시연했습니다.

---

## 레포지토리 구조
- **functional_specification_web** — 웹 기능 명세  
  `https://github.com/Project-Taba/functional_specification_web`
- **functional_specification_app** — 앱 기능 명세  
  `https://github.com/Project-Taba/functional_specification_app`
- **Frontend** — 웹 대시보드 (React / JavaScript)  
  `https://github.com/Project-Taba/Frontend`
- **Frontend_App** — 사용자 모바일 앱 (Flutter / Dart)  
  `https://github.com/Project-Taba/Frontend_App`
- **Server** — 백엔드 서버 (Spring Boot / Java)  
  `https://github.com/Project-Taba/Server`
- **AI** — 모델/분석 (Python / Jupyter Notebook)  
  `https://github.com/Project-Taba/AI`
