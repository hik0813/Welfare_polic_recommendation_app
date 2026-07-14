
---

# 나에게 맞는 복지 찾기

### 맞춤형 복지 추천 웹서비스

**간단한 질문에 답하면 53개의 정부·지자체 복지서비스 중 나에게 적합한 지원사업을 추천하고, 신청 방법과 공식 사이트까지 안내하는 맞춤형 복지 추천 웹서비스입니다.**

### 주요 기능

* 맞춤형 설문(8단계)

  * 나이 → 지역 → 가족 → 소득 → 장애 여부 → 현재 상황 → 관심 분야 → 최종 확인
* 맞춤형 복지 추천

  * 나이, 소득, 장애 여부, 생활 상황 등을 종합적으로 분석하여 적합한 복지서비스 추천
* 추천 사유 제공

  * 추천 이유를 함께 제공하여 서비스 적합성을 쉽게 이해 가능
* 신청 안내

  * 신청 절차와 공식 홈페이지 바로가기 제공
* 접근성 지원

  * 글자 크기 조절
  * 고대비 모드
  * 음성 읽기(TTS)
* 반응형 웹

  * PC, 태블릿, 모바일 환경 지원

---

# 1. 서비스 이용

배포 후 아래 위치에 서비스 주소를 입력합니다.

```
https://<사용자명>.github.io/<저장소명>/
```

또는

```
https://<사이트명>.netlify.app
```

---

# 2. 프로젝트 구조

| 파일                             | 설명                      |
| ------------------------------ | ----------------------- |
| `index.html`                   | 메인 페이지                  |
| `style.css`                    | UI 스타일 및 접근성 디자인        |
| `app.js`                       | 설문 진행, 추천 알고리즘, 결과 출력   |
| `welfare_data.json`            | 복지서비스 데이터               |
| `netlify/functions/explain.js` | AI 추천 설명 생성(Serverless) |
| `netlify.toml`                 | Netlify 배포 설정           |
| `README.md`                    | 프로젝트 설명서                |

---

# 3. 로컬 실행

> **주의**
> `index.html`을 직접 실행하면 브라우저 보안 정책(CORS)으로 인해 데이터를 불러올 수 없습니다.

### 방법 1. Python 서버

```bash
cd Welfare_polic_recommendation_app
python -m http.server 8000
```

접속

```
http://localhost:8000
```

### 방법 2. VS Code Live Server

1. Live Server 설치
2. `index.html` 열기
3. **Go Live** 클릭

---

# 4. 배포

## GitHub Pages

1. GitHub 저장소 생성
2. 프로젝트 업로드
3. **Settings → Pages**
4. Branch : **main**
5. Root : **/**

---

## Netlify

1. GitHub 저장소 연결
2. Publish Directory : `.`
3. (선택) 환경변수 등록

```
ANTHROPIC_API_KEY
```

---

## Vercel

1. GitHub Import
2. Framework : **Other**
3. API 경로 변경 후 배포

---

# 5. AI 추천 설명

추천 설명은 다음 순서로 생성됩니다.

| 우선순위 | 방식                     |
| ---- | ---------------------- |
| 1    | Netlify Serverless API |
| 2    | 사용자 API Key 입력         |
| 3    | 규칙 기반 자동 설명            |

AI를 사용할 수 없는 환경에서도 기본 추천 설명은 항상 제공됩니다.

---

# 6. 복지 데이터 수정

복지 데이터는 `welfare_data.json`에서 관리합니다.

| 항목                  | 설명      |
| ------------------- | ------- |
| id                  | 서비스 번호  |
| name                | 서비스명    |
| category            | 서비스 분류  |
| age_range           | 대상 연령   |
| support_amount      | 지원 내용   |
| income_criteria     | 소득 기준   |
| disability_required | 장애 여부   |
| apply_method        | 신청 방법   |
| summary             | 서비스 요약  |
| url                 | 공식 홈페이지 |
| apply_steps         | 신청 절차   |

새로운 서비스를 추가할 경우 동일한 형식으로 JSON 객체를 추가하면 됩니다.

---

# 7. 유의사항

* 복지 기준 및 지원 금액은 매년 변경될 수 있습니다.
* 실제 신청 전에는 반드시 공식 홈페이지에서 최신 정보를 확인하시기 바랍니다.
* 소득 기준은 예시 데이터를 기반으로 계산되며 실제 심사 결과와 다를 수 있습니다.
* 지자체 사업은 지역별로 지원 내용이 상이할 수 있습니다.
* TTS 기능은 브라우저에서 제공하는 음성 엔진을 사용합니다.

---

# 8. 개발 정보

* HTML, CSS, JavaScript 기반 정적 웹서비스
* 별도의 빌드 과정 없이 실행 가능
* 점수 기반 추천 알고리즘 적용
* 접근성(WCAG) 고려
* 반응형 웹 지원
* AI 추천 설명(Anthropic Claude Sonnet 5) 연동 가능

---
