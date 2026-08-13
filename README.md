# **3D Learning Atlas**

### AI 융합형 중·고등 3D 학습 플랫폼 — ICT 통합 설계 경진대회 제출작 (팀 코드톡톡)

3D 모델로 과학 개념을 학습하고, AI 챗봇에 질문하며, 북마크와 질문 기록을 바탕으로 **나만의 복습 노트를 AI와 함께 정리**하는 통합 학습 플랫폼입니다.

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat&logo=sqlite&logoColor=white)

🔗 **소스코드** : https://github.com/Sanduduck/ICT-Innovation-Project-Competition

---

## 📌 프로젝트 소개

* 중·고등학생이 **평면 그림만으로 이해하기 어려운 개념**(세포 구조, 분자 결합, 지각판, 천체 운동, 입체도형 등)을 3D 모델로 직접 조작하며 학습하는 웹 플랫폼입니다.
* 핵심 문제의식은 **"학생이 실제로 개념을 이해하고 있는가?"**. 초기엔 3D 모델 카탈로그만 구상했지만, 학생은 *자료를 보는 것*에서 끝나지 않고 *질문하고 → 저장하고 → 복습 정리*한다는 점에 주목해, 이 전체 흐름을 하나의 플랫폼으로 연결했습니다.
* **배경 근거:** 선행 연구에 따르면 3D·애니메이션 기반 학습은 2D 대비 흥미 지표가 높고(첫 수업 직후 약 +10%p), 전체 통과율도 73% → 87%로 개선되는 것으로 보고됩니다. 이를 근거로 3D 시각화 + AI 학습 보조를 결합했습니다.
* **설계 철학: "AI는 초안, 학습은 학습자."** AI가 완성 답안을 대신 쓰는 게 아니라, 학생이 수정·보완하는 1차 초안을 제공합니다.

---

## 📖 목차

1. [팀 구성 & 역할](#-팀-구성--역할)
2. [사용 기술](#️-사용-기술)
3. [주요 기능](#-주요-기능)
4. [🧠 기술적 의사결정](#-기술적-의사결정-technical-decisions) ← *왜 이 기술을 선택했는가 (6건)*
5. [시스템 구조](#-시스템-구조)
6. [API 명세](#-api-명세)
7. [데이터베이스 스키마](#️-데이터베이스-스키마)
8. [설치 및 실행](#-설치-및-실행)
9. [트러블슈팅](#-트러블슈팅)

---

## 👥 팀 구성 & 역할

| 이름 | 역할 |
| --- | --- |
| **박동진 (팀장)** | 프론트엔드 · 백엔드 · AI · 보안 — 기술 설계 총괄 및 전반 구현 |
| **박지호** | 프론트엔드 · 백엔드 · AI |
| **김준영** | 백엔드 · 하드웨어 · 보고서 |
| **오유진** | 백엔드 · AI · 발표 자료 |
| **이찬** | 프론트엔드 · 발표 자료 |

---

## 🛠️ 사용 기술

**Frontend** — HTML / CSS / Vanilla JavaScript (별도 빌드 과정 없이 실행)
**Backend** — Node.js + Express (인증·모델·북마크·노트·대시보드 API), axios
**AI 서버** — Python + FastAPI / Uvicorn
* **의미 검색** — Sentence-Transformers (KoSimCSE) + FAISS 벡터 검색
* **챗봇** — Qwen2.5-0.5B-Instruct (로컬 경량 LLM)
* **피드백** — Anthropic Claude (Sonnet: 심층 피드백 / Haiku: 챗봇 폴백)

**Database** — SQLite3 (사용자·북마크·노트·챗봇 로그) + JSON (3D 모델 메타데이터)
**보안** — bcryptjs 해시, 쿠키 기반 세션, 역할 기반 접근 제어(RBAC)

---

## 🎯 주요 기능

| 기능 | 설명 |
| --- | --- |
| **3D 모델 탐색** | Sketchfab 임베드로 과목별 과학 개념 3D 시각화 |
| **하이브리드 검색** | 문자열 검색 + FAISS 의미 검색 — "세포에서 에너지를 만드는 구조" 같은 문장으로도 탐색 |
| **AI 챗봇** | 중·고등 수준 개념 설명·예시·퀴즈 (과목 맥락 유지) |
| **AI 노트 생성** | 북마크 + 챗봇 질문 기록을 묶어 복습용 1차 노트 초안 자동 생성 |
| **AI 심층 피드백** | 노트 품질 등급(F~S) + 학습 패턴 5차원 분석 |
| **교사 대시보드** | 질문·북마크·노트 수 기반 단원별 관심도·약점 시각화 |
| **관리자 페이지** | 3D 모델 등록·삭제·정렬 (드래그앤드롭) |

---

## 🧠 기술적 의사결정 (Technical Decisions)

단순히 "무엇을 썼는가"보다 **왜 그것을 선택했는가**를 기록합니다. 각 항목은 실제 겪은 문제·팀 논의·성능 제약을 근거로 결정되었습니다.

<details>
<summary><b>1. 웹 서버와 AI 서버를 왜 분리했는가 (Node.js ↔ Python)</b></summary>

<br>

**문제**
AI 기능(문장 임베딩, LLM 추론)은 Python 생태계에 강점이 있고, 웹 서버는 비동기 I/O에 강한 Node.js가 적합했습니다. 이 둘을 한 서버에 묶으면, 무겁고 느린 AI 연산이 이벤트 루프를 점유해 **기본적인 검색·북마크 요청까지 지연**될 위험이 있었습니다.

**선택한 구조**
역할을 두 서버로 분리하고 REST API로 연동했습니다.
* **Node.js Express** — 인증, 3D 모델 관리, 북마크, 노트, 대시보드 API
* **Python FastAPI** — AI 의미 검색, 챗봇 응답 생성

**결과 / 트레이드오프**
AI 서버가 일시적으로 지연되거나 죽어도, **모델 검색·북마크·마이페이지 같은 기본 기능은 그대로 유지**되도록 설계했습니다. 대신 서버 2개를 운영하는 복잡도와 서버 간 통신 설계 비용이 늘었습니다.

</details>

<details>
<summary><b>2. 챗봇 모델을 왜 Qwen과 Claude로 나눴는가</b></summary>

<br>

**문제**
학교 PC처럼 **GPU 없는 환경에서도 로컬 실행 가능한 경량 LLM**이 필요했습니다. 그래서 CPU로 돌아가는 Qwen2.5-0.5B를 도입했는데, 소형 모델이라 **복잡한 JSON 구조화 지시(5차원 피드백 형식)를 제대로 따르지 못하는** 한계가 있었습니다.

**검토·선택 — 작업별 모델 분리**

| 작업 | 모델 | 이유 |
| --- | --- | --- |
| 단순 챗봇 질의응답 | **Qwen2.5-0.5B** | CPU 로컬 실행, 무료, 단순 설명엔 충분 |
| 5차원 심층 피드백 | **Claude Sonnet** | 엄격한 JSON + Chain-of-Thought 지시 이행 필요 |
| 챗봇 폴백 | **Claude Haiku** | Qwen 실패 시, 빠르고 저렴한 대체 |

**결과 / 트레이드오프**
"모든 걸 큰 모델로"도, "모든 걸 로컬로"도 아닌, **작업 성격에 맞춰 비용·성능·지시이행 능력을 배분**했습니다. 심층 피드백은 외부 API 비용이 들지만, 그 품질이 필요한 기능에만 한정했습니다.

</details>

<details>
<summary><b>3. 검색 — 왜 문자열 검색만으로는 부족했는가 (하이브리드 검색)</b></summary>

<br>

**문제**
키워드 검색은 학습자가 **정확한 교과 용어를 알아야만** 자료를 찾을 수 있습니다. "미토콘드리아"라는 단어를 모르는 학생이 *"세포에서 에너지를 만드는 구조"* 라고 검색하면 아무것도 안 나오는 문제가 있었습니다.

**팀 논의 (2026.04.27 회의)**
문자열 검색과 Sentence-BERT 기반 의미 검색을 비교했습니다.
* 문자열 검색 — 빠르지만 표현이 조금만 달라져도 정확도 급락
* 의미 검색 — 유사 개념 탐색 가능, 교육 플랫폼에 더 적합
* **이견:** 일부 팀원이 *"의미 검색이 서버 성능과 구현 난도를 높인다"* 고 우려했으나, 사용자 경험 향상을 위해 도입이 필요하다는 의견이 우세해 채택했습니다.

**선택 — 둘 다**
문자열 검색으로 명확한 키워드 일치를 빠르게 잡고, FAISS 의미 검색으로 개념 간 연관성을 보완했습니다. 사용자는 상단 "AI 검색" 토글로 사용 여부를 직접 선택할 수 있습니다.

**결과 / 트레이드오프**
현재 데이터 규모(100건 이하)에서는 단순 FAISS 인덱스로 충분히 빠릅니다. 규모가 커지면 더 큰 벡터 검색에 맞는 인덱스로 확장이 필요합니다.

</details>

<details>
<summary><b>4. AI 장애에 어떻게 대비했는가 (다단계 폴백)</b></summary>

<br>

**문제**
AI 챗봇·피드백이 핵심 기능이지만, **AI 서버나 외부 API가 죽으면 서비스 전체가 멈출** 위험이 있었습니다.

**선택 — 기능별 폴백 체인**
* **챗봇** — Qwen(로컬) 실패 → Claude Haiku 자동 전환 → 그것도 실패 시 오류 안내
* **피드백** — Claude 실패 → Qwen → **로컬 규칙 기반 계산**(노트 글자 수·챗봇 패턴으로 등급·점수 산출)
* **노트 생성** — AI 실패 → 북마크 제목·설명 기반 **템플릿 초안** 제공

**결과 / 트레이드오프**
테스트 항목에 *"AI 서버 장애 대응"*을 별도로 넣어, **AI 없이도 기본 학습 흐름이 유지되는지** 검증했습니다. 폴백 계층이 늘어난 만큼 로직 복잡도는 커졌지만, 데모·시연 중 AI 장애로 전체가 멈추는 최악을 방지했습니다.

</details>

<details>
<summary><b>5. 동시 AI 요청을 어떻게 감당했는가 (Redis 없는 트래픽 대응 레이어)</b></summary>

<br>

**문제**
AI 호출은 **느리고 비싸며**, 다수 사용자가 동시에 요청을 보내면 AI 서버가 과부하로 죽거나 API 비용이 폭증할 수 있었습니다. 경진대회 데모라 Redis 같은 외부 인프라는 부담이었습니다.

**선택 — 인메모리 자체 구현 5종**

| 장치 | 역할 | 선택 이유 |
| --- | --- | --- |
| **LRU 캐시** | 동일 요청 반복 시 AI 호출 없이 즉시 반환 (TTL 10분) | Redis 없이 인메모리로 |
| **Rate Limiter** | 사용자당 분당 5회 제한 | **슬라이딩 윈도우** — 고정 윈도우의 경계 취약점 회피 |
| **Semaphore** | AI 동시 요청 3개로 제한 | 초과분은 대기열로 순차 처리 |
| **Circuit Breaker** | 연속 5회 실패 시 60초 차단 | 장애 전파 방지 + 자동 복구 |
| **DB Job Queue** | Rate Limit 초과 요청을 DB에 저장 후 처리 | 서버 재시작 후에도 작업 유지 |

**결과 / 트레이드오프**
외부 캐시·큐 인프라 없이 **애플리케이션 레벨에서 트래픽을 보호**했습니다. 대규모 분산 환경에선 Redis 등으로 이관이 필요하지만, 단일 서버 데모 규모에는 과하지 않게 맞췄습니다.

</details>

<details>
<summary><b>6. 데이터 저장 — 왜 SQLite인가, 그리고 왜 WAL을 안 썼는가</b></summary>

<br>

**문제**
경진대회 특성상 **배포·데모가 간편**해야 했습니다. 별도 DB 서버를 구동·운영하는 부담을 피하고 싶었습니다.

**선택**
* **SQLite** — 파일 하나(`data/app.db`)로 동작. 쿼리는 `?` 파라미터 방식으로 통일해 향후 **PostgreSQL 이관도 용이**하도록 작성.
* **3D 모델 메타데이터는 JSON**(`data/models.json`)으로 분리해 관리자 페이지에서 바로 편집.

**겪은 문제 — WAL 모드 미사용**
성능을 위해 SQLite의 WAL 모드를 켰더니, **Windows에서 `-wal`·`-shm` 파일이 추가로 생성돼 DB 파일을 복사·이동할 때 문제**가 발생했습니다. 데모 환경에서 DB를 통째로 옮겨야 하는 경우가 많아, 기본 DELETE 모드로 되돌렸습니다.

**결과 / 트레이드오프**
DB 서버 없이 **즉시 실행·복사 가능한 단순함**을 확보했습니다. 대신 대규모 동시 쓰기가 필요한 실서비스 단계에서는 RDS 등으로의 확장이 필요합니다.

</details>

---

## 🧩 시스템 구조

```
┌─────────────────────────────────────────────────────────┐
│                   클라이언트 (브라우저)                      │
│               HTML / CSS / Vanilla JS                    │
└──────────────────────────┬──────────────────────────────┘
                           │ HTTP (:3000)
┌──────────────────────────▼──────────────────────────────┐
│                Express 서버 (Node.js)                     │
│   인증 · 모델 · 북마크 · 노트 · 대시보드 API               │
│   ┌─────────────┐   ┌──────────────────────────────┐     │
│   │ SQLite      │   │  트래픽 대응 레이어             │     │
│   │ app.db      │   │  LRU / Rate-limit / Semaphore │     │
│   └─────────────┘   │  / Circuit-Breaker / Job Queue│     │
│                     └──────────────────────────────┘     │
└───────────┬───────────────────────────┬─────────────────┘
            │ HTTP (:8000)              │ HTTPS
┌───────────▼──────────────┐  ┌─────────▼───────────────────┐
│  Python AI 서버 (FastAPI) │  │  Anthropic API              │
│  · KoSimCSE (임베딩)      │  │  Claude Sonnet (심층 피드백) │
│  · FAISS (벡터 검색)      │  │  Claude Haiku  (챗봇 폴백)   │
│  · Qwen 0.5B (챗봇)       │  └─────────────────────────────┘
└──────────────────────────┘

── 챗봇 폴백:  Qwen 실패 → Claude Haiku → 오류 안내
── 피드백 폴백: 캐시 HIT 즉시반환 → Claude → Qwen → 로컬 규칙 계산
```

---

## 📡 API 명세

```
# 인증
POST /api/auth/register        회원가입
POST /api/auth/login           로그인 (쿠키 발급)
POST /api/auth/logout          로그아웃
GET  /api/auth/whoami          현재 로그인 사용자

# 챗봇
POST /api/chat                 { message, subject, withQuiz } → { answer, model }

# AI 노트
POST /api/notes/generate       AI 노트 즉시 생성
POST /api/notes/generate/async 큐 등록 후 jobId 반환
GET  /api/notes/jobs/:jobId    작업 상태 폴링
POST /api/notes/:id/feedback   AI 심층 피드백 생성

# 노트 CRUD
GET/POST/PUT/DELETE /api/notes[/:id]

# 북마크 · 모델
POST/DELETE /api/bookmarks/:id
GET/POST/DELETE /api/models[/:id]
```

---

## 🗄️ 데이터베이스 스키마

```sql
users          (id, username, email, password, role, created_at)
models         (id, title, description, url, subject, thumb, created_at)  -- data/models.json
bookmarks      (id, user_id, model_id, created_at)
notes          (id, user_id, title, content, subject, tags, created_at, updated_at)
chat_logs      (id, user_id, message, subject, with_quiz, created_at)
note_feedbacks (id, note_id, user_id, feedback, summary, concept_analysis,
                learning_pattern, next_step, strengths, improvements,
                weak_areas, interest_areas, score, grade, created_at)
note_generation_jobs (id, user_id, model_ids, status, result_note_id,
                      error_msg, ai_used, priority, created_at, updated_at)
```

**AI 노트 품질 등급** — 글자 수 기반 F(~19자)/D/C/B/A/S(1000자~), 등급별 점수 상한을 두어 빈약한 노트에 높은 점수가 나가지 않도록 설계.

---

## 🚀 설치 및 실행

**사전 요구사항** — Node.js 18+, Python 3.9+ (PATH 등록), Anthropic API 키

### Windows
```bash
git clone https://github.com/Sanduduck/ICT-Innovation-Project-Competition.git
cd ICT-Innovation-Project-Competition
copy .env.example .env         # ANTHROPIC_API_KEY 입력
node scripts/db-migrate.js     # DB 초기화 (최초 1회)
start-all.bat                  # 원클릭 실행
```

### Mac / Linux
```bash
git clone https://github.com/Sanduduck/ICT-Innovation-Project-Competition.git
cd ICT-Innovation-Project-Competition
npm install
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env           # ANTHROPIC_API_KEY 입력
node scripts/db-migrate.js
npm run ai &                   # AI 서버 (:8000)
npm start                      # Express (:3000)
```

| 서비스 | URL |
| --- | --- |
| 메인 | http://localhost:3000 |
| 마이페이지 | http://localhost:3000/mypage.html |
| 관리자 | http://localhost:3000/admin |
| AI Swagger | http://localhost:8000/docs |

---

## 🔧 트러블슈팅

<details>
<summary><b>자주 발생하는 오류</b></summary>

<br>

| 오류 | 원인 | 해결 |
| --- | --- | --- |
| `SQLITE_IOERR` | DB 파일 없음/손상 | `node scripts/db-migrate.js` 실행 |
| `'pip'은 내부 명령어가 아닙니다` | pip이 PATH에 없음 | `python -m pip install -r requirements.txt` |
| `npm run ai exited with code 1` | `reload=True` Windows 충돌 | `semantic_search.py`에서 `reload=False`로 변경 |
| AI 피드백이 노트 내용 반복 | Qwen 소형 모델 한계 | `.env`에 `ANTHROPIC_API_KEY` 설정 |
| 챗봇 503 | AI 서버 + Anthropic 모두 실패 | `npm run ai` 실행 후 API 키 확인 |

> **`reload=False` 이유** — Windows에서 `reload=True`는 멀티프로세스가 필요한데, Node.js 자식 프로세스로 실행 시 즉시 종료되는 문제가 있어 비활성화했습니다.

</details>
