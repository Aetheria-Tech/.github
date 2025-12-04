### 📝 커밋 메시지 구조 (Structure)

기본적으로 커밋 메시지는 **헤더(Header)**, **본문(Body)**, **꼬리말(Footer)** 세 부분으로 구성하며, 각 부분 사이는 빈 줄로 구분합니다.

```text
<Type>(<Scope>): <Subject>   <-- 헤더 (필수)

<Body>                        <-- 본문 (선택)

<Footer>                      <-- 꼬리말 (선택/Breaking Change 시 필수)
```

-----

### 📋 커밋 메시지 작성 규칙 (Convention Rules)

| 항목 (Component)       | 설명 (Description) | 작성 규칙 (Rules)                                                                                                             | 예시 (Example)                                                   |
|:---------------------|:-----------------|:--------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------|
| **Type**             | 커밋의 종류           | • **소문자**만 사용<br>• 아래의 [Type 키워드 리스트] 준수                                                                                  | `feat`, `fix`, `refactor`                                      |
| **Scope**            | 변경된 범위 (선택)      | • **소문자** 사용, 괄호 `()`로 감싸기<br>• 모듈명, 패키지명 등을 명시                                                                           | `(auth)`, `(ui)`, `(db)`                                       |
| **Subject**          | 제목 (요약)          | • **50자 이내**로 간결하게<br>• **명령문/현재 시제** 사용 (\~함(X), \~했음(X), \~하라/한다(O))<br>• 첫 글자 대문자는 선택 (보통 소문자)<br>• **끝에 마침표(`.`) 금지** | `add login logic`<br>`fix typo in user controller`             |
| **Body**             | 본문 (상세)          | • **무엇을, 왜** 변경했는지 설명 (How보다는 Why)<br>• 한 줄당 **72자** 내외로 줄 바꿈<br>• 제목과 구분하기 위해 한 줄 띄우고 작성                                 | `기존 로그인 방식의 보안 취약점 해결을 위해`<br>`JWT 토큰 만료 시간을 단축함.`             |
| **Breaking Changes** | 중요 변경 사항         | • API 호환성이 깨지는 경우 필수 작성<br>• 본문 또는 꼬리말 시작에 `BREAKING CHANGE:` 명시                                                          | `BREAKING CHANGE: The graph API version 1.0 has been removed.` |
| **Footer**           | 이슈 추적 (선택)       | • **이슈 트래커 ID**를 참조 (`Closes`, `Fixes` 등)<br>• Breaking Change 정보 포함 가능                                                   | `Closes #123`<br>`Fixes #45`                                   |

-----

### 🔖 Type 키워드 리스트 (Type Cheatsheet)

`Type` 란에 들어갈 수 있는 표준 키워드입니다.

| Type         | 설명 (Description) | 비고                                                       |
|:-------------|:-----------------|:---------------------------------------------------------|
| **feat**     | 새로운 기능 추가        | 사용자에게 새로운 기능을 제공할 때                                      |
| **fix**      | 버그 수정            | 사용자에게 영향을 주는 버그를 고칠 때                                    |
| **docs**     | 문서 수정            | README.md, 주석 등 코드 변화 없이 문서만 수정                          |
| **style**    | 코드 포맷팅, 세미콜론 누락  | 비즈니스 로직 변경 없음 (오타 수정, 탭 들여쓰기 등)                          |
| **refactor** | 코드 리팩토링          | 기능 변경 없이 코드 구조만 개선 (성능 개선 포함 가능)                         |
| **test**     | 테스트 코드           | 테스트 코드 추가, 수정, 삭제 (프로덕션 코드 변경 없음)                        |
| **chore**    | 기타 변경 사항         | 빌드 설정 수정, 패키지 매니저 설정 등 (소스 코드 변경 없음)                     |
| **ci**       | CI 설정 파일 수정      | GitHub Actions, Jenkins 설정 파일 변경 등                       |
| **perf**     | 성능 개선            | 기능 변경 없이 성능(Performance)만 향상시켰을 때 (예: 쿼리 튜닝, 캐싱 적용)      |
| **build**    | 빌드 시스템/의존성       | chore에서 분리. npm, gradle, dockerfile 등 빌드 도구 및 라이브러리 업데이트 |
| **revert**   | 커밋 되돌리기          | 이전 커밋을 Revert(롤백) 할 때 사용                                 |
| **security** | 보안 이슈 수정         | 치명적인 취약점 해결이나 인증 로직 강화 등 보안 관련 사항                        |


-----

### ✅ 좋은 커밋 메시지 예시 (Full Example)

**1. 기능 추가 (Feature)**

```text
feat(auth): add google social login

사용자 유입을 늘리기 위해 구글 소셜 로그인 기능을 추가함.
OAuth 2.0 기반으로 구현되었으며 기존 회원가입 로직과 통합됨.

Closes #102
```

**2. 버그 수정 (Fix)**

```text
fix(payment): handle negative value in discount logic

할인 금액이 결제 금액보다 클 경우 마이너스가 되는 현상 수정.
이제 결제 금액이 0원 미만으로 내려가지 않도록 0원으로 고정함.

Fixes #45
```

**3. 호환성 변경 (Breaking Change)**

```text
refactor(api): switch to graphQL for user data

기존 REST API의 오버페칭 문제를 해결하기 위해 GraphQL로 전환함.

BREAKING CHANGE: GET /api/v1/users 엔드포인트가 삭제되었습니다.
대신 /graphql 엔드포인트를 사용해야 합니다.
```