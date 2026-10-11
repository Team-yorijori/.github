# 🧊 Team-yorijori

> 냉장고 속 재료를 사진 한 장으로 등록하면, 소비기한이 임박한 재료부터 쓰는 레시피를 추천해 음식물 쓰레기를 줄여 주는 웹 서비스 **냉장고를 부탁해 (요리조리)**

경성대학교 팀 프로젝트 (3명) · 2026년 2학기

## 저장소

| 저장소 | 내용 |
|---|---|
| [yorijori](https://github.com/Team-yorijori/yorijori) | 서비스 전체 — Spring Boot 서버·화면, AI 재료 인식, 레시피 데이터, 문서 |

## 팀

| 역할 | 담당 |
|---|---|
| 팀장 · 백엔드 | 회원·인증, DB, REST API, 스케줄러, 배포 |
| 백엔드 · 프론트엔드 · AI | 재료 인식 모델, 영수증 인식, 레시피 데이터, 추천 로직 |
| 프론트엔드 · 디자인 | Figma 화면 설계, Thymeleaf 템플릿, CSS, 애니메이션 |

## 주요 기능

- 📸 재료 사진·영수증으로 냉장고 등록 (브라우저 안에서 인식, 서버로 사진 전송 없음)
- ⏰ 재료별 소비기한 자동 안내, 임박 재료 강조
- 🍳 임박 재료를 먼저 쓰는 레시피 추천 (공공데이터 레시피 560건)
- ✅ 요리 완료 시 재료 자동 차감, 만든 요리 보관·기록
- 🛒 장보기 목록과 최저가 안내

## 기술 스택

`Java 17` `Spring Boot 3` `Spring Security` `JPA` `Thymeleaf` `MySQL` `Flyway` `YOLO26 → ONNX` `onnxruntime-web` `tesseract.js` `GitHub Actions`

## 진행 상황

| 단계 | 기간 | 상태 |
|---|---|---|
| 기획 · 데모 v1~v9 · Spring 뼈대 | 2026-09-29 ~ 10-12 | ✅ |
| 개발 (화면↔API 연결, DB·서버 구축, 모델 v5) | 2026-10-13 ~ 11-30 | 🔧 |
| 테스트 · 배포 · 발표 | 2026-12-01 ~ 12-14 | 📅 |

## 현재 실행 방법 (2가지)

### 처음 실행하기 (서버 + 화면)

**준비물**

| 필요한 것 | 확인 방법 | 없으면 |
|---|---|---|
| JDK 17 이상 | 터미널에서 `java -version` | [Temurin JDK 21](https://adoptium.net) 설치 |
| Git | `git --version` | [git-scm.com](https://git-scm.com) 설치 |
| 인터넷 | — | 처음 실행 때 Gradle·라이브러리 다운로드 |

MySQL은 없어도 됨. 기본 실행은 H2 메모리 DB를 자동으로 만들어서 사용

**1. 코드 받기** (처음 한 번)

```bash
cd C:\Users\본인계정\IdeaProjects        # 원하는 폴더
git clone https://github.com/Team-yorijori/yorijori.git
cd yorijori
```

**2. 서버 실행**

```bash
cd backend
gradlew.bat bootRun        # 윈도우
./gradlew bootRun          # 맥·리눅스
```

- 처음 실행은 Gradle·라이브러리를 받느라 몇 분 걸림. 두 번째부터는 금방 뜸
- 로그 마지막에 `Started YorijoriApplication`이 보이면 실행 완료
- IntelliJ로 실행할 때 : `backend` 폴더 열기 → Gradle 불러오기 끝날 때까지 대기 → `YorijoriApplication` 의 ▶ 버튼

**3. 접속**

| 주소 | 내용 |
|---|---|
| http://localhost:8080 | 서비스 화면 |
| http://localhost:8080/h2-console | DB 확인 (JDBC URL `jdbc:h2:mem:yorijori`, 사용자 `sa`, 비밀번호 없음) |

**4. 동작 확인 (5분)**

1. 회원가입 → 로그인 → 상단에 닉네임 표시
2. 냉장고에 재료 입력, 초성 검색 `ㅇㅍ` → 양파
3. 레시피 추천 목록 → 상세 → 요리 완료
4. 재료 사진 스캔 (localhost는 카메라 허용됨)

**5. 끄기** : 터미널에서 `Ctrl + C`

> **현재 상태 주의**
> - 회원·로그인은 서버(H2)에 저장되지만, H2는 메모리 DB라 **서버를 끄면 초기화**
> - 냉장고·만든 요리·장보기는 아직 **브라우저(localStorage)에 저장**. 서버 저장으로 바꾸는 작업이 #7
> - 서버를 꺼도 데이터를 남기려면 아래 MySQL 실행 사용 (#5)
