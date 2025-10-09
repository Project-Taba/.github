# TABA — 급발진 감지 & AI 기반 응급 대처 서비스

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
- [기술 스택](#기술-스택)
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
- 실시간 수집 → 전처리/특징 추출 → 급발진 판별 → **119 API 호출** → 대시보드 기록

<details>
<summary>🧩 아키텍처 다이어그램 (클릭해 열기)</summary>

<img width="1111" height="675" alt="image" src="https://github.com/user-attachments/assets/e23d4671-a34e-48cb-bcf6-749782c0d92a" />


</details>

<details>
<summary>📱 앱 화면 (클릭해 열기)</summary>
  <img width="1459" height="553" alt="image" src="https://github.com/user-attachments/assets/88bcabf6-e3b8-4c77-9363-a9cb76d67684" />
</details>

<details>
<summary>🖥️ 웹 대시보드 (클릭해 열기)</summary>

<img width="1468" height="586" alt="image" src="https://github.com/user-attachments/assets/fcf77724-315e-405f-a826-980e5e073a02" />


</details>

---

## 레포지토리 구조
> 조직: **Project-Taba**

- **Frontend** — 웹 프론트엔드 (Vue / JavaScript)  
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

## 데이터 & AI 로직
<img width="1123" height="438" alt="image" src="https://github.com/user-attachments/assets/0d8d5783-55ca-42df-be3f-6adea7bc2a9c" />
- **정규화**  
  \[
  x_\text{scaled} = \frac{x - x_\text{min}}{x_\text{max} - x_\text{min}}
  \]
- **속도 변화율(프레임 간 차분)**  
  \[
  v_{\text{shift}} = v_t - v_{t-1}
  \]
- **판별 개념**
  - 엑셀↑ & 브레이크↓ & 속도↑ 패턴의 **동시·급격 변화** 탐지  
  - 임계치/윈도우 기반 특징 + 휴리스틱/ML 조합  

<details>
<summary>📈 실제 AI 이상탐지</summary>
<img width="1156" height="720" alt="AI 이상탐지" src="https://github.com/user-attachments/assets/86a8bcbf-9665-4438-9677-9812b196aba1" />

</details>

---

## 데모
- 앱/웹/AI 시연 영상:
  - https://youtube.com/shorts/9eompbtX2hE  
  - https://youtu.be/OtI3w4VNpLc  
  - https://youtu.be/59zyD-lkC0Y  
  - https://www.youtube.com/watch?v=LInyRZcJ4HU

<details>
<summary>🎞️ 데모 캡처 (클릭해 열기)</summary>

> 데모 장면 캡처 이미지를 첨부해주세요.  
> 예: `/docs/img/demo-*.png`

</details>
