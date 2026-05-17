# Contributing to hanpil

hanpil은 EMP 아키텍처를 기반으로 하는 오픈소스 글쓰기 플랫폼입니다.  

### 퀵 스타트: 이슈에서 시작하기

아래의 절차를 통해 첫 PR을 시작해보세요.

1. **이슈 둘러보기**  
   이슈란을 보면 'KoreanSpellChecker에 Naver 맞춤법 API 백엔드 추가' 같은 개발이슈들이 여럿 있을 것입니다.
   
2. **댓글로 참여 의사 표현**  
   '이 이슈는 제가 해결하겠습니다'라고 댓글을 답니다.
   메인테이너가 '네. 진행해주세요'라고 답하면 실제로 개발을 진행합니다.

3. **저장소 준비**  
   - 저장소를 fork하거나 clone합니다.
   - `feature/korean-spellchecker-naver` 같은 새 브랜치를 만듭니다.
   - 프로젝트 루트에서 `pnpm setup`을 실행합니다.
   - 패키지는 pnpm으로 관리되며, `pnpm setup` 한 번으로 필요한 설치가 모두 수행됩니다.

4. **Module 하나만 만들어 보기**  
   예: `KoreanSpellChecker` 인터페이스를 구현하는 새 백엔드 Module을 하나 만듭니다.  
   - `name`: `korean-spellchecker-naver`
   - `author`: `@yourname`
   - `description`: "Naver 맞춤법 API를 사용하는 KoreanSpellChecker 백엔드"

5. **Module PR 체크리스트**  
   - 파일이 500줄 이하인지 확인
   - `metadata`에 `name`, `description`, `version`, `author`, `contributors`가 모두 포함되어 있는지 확인
   - `dependencies`가 필요하면 최소화하고, 순환 의존이 없는지 확인
   - copy로 가져온 코드가 있다면 원본 작성자를 `contributors`에 추가

6. **PR 보내기**  
   PR을 보내는 방법은 저장소를 어떻게 준비했는지에 따라 다릅니다.

   **fork한 경우** (대부분의 외부 기여자):
   - fork한 저장소(`origin`)에 브랜치를 push합니다: `git push origin feature/korean-spellchecker-naver`
   - GitHub에서 "Compare & pull request" 버튼을 클릭합니다.
   - PR할 때, 원본 저장소(upstream)의 `main` 브랜치로 병합되도록 요청합니다.

   **직접 push 권한이 있는 경우** (프로젝트 멤버):
   - `git push`로 브랜치를 origin에 올립니다.
   - GitHub에서 "Compare & pull request" 버튼을 클릭합니다.
   - PR할 때, `main` 브랜치로 병합되도록 요청합니다.

   PR이 승인되면, 메인테이너가 `main` 브랜치에 병합(merge)합니다.  
   PR이 "Merged" 상태가 되었다면 프로젝트에 대한 기여가 끝난 것입니다!

## 더 알아보기

### EMP 아키텍처 핵심 원칙

- Engine → Modules → Project의 단방향 의존을 유지합니다.
- Engine은 Project(브랜드, UI 흐름, 사용자 프리셋)를 알지 못합니다.
- 각 Module은 독립적으로 동작하며, 입출력 스키마만으로 그 기능을 이해할 수 있어야 합니다.
- 모든 파일은 **500줄 이하**로 유지합니다. Engine/Module이 깊게 분해되더라도 파일 단위는 작게 유지하세요. 그래야 후발주자들이 합류하기가 쉽습니다.

### Registry와 Module Metadata

각 Module은 registry에 등록되며, 다음 metadata를 가집니다:

- `name`: Module 이름
- `description`: 간단한 설명
- `version`: 버전
- `author`: 주 작성자 (`@username`, `email`, 또는 `"이름 <email>"`)
- `contributors?`: 추가 기여자 배열 (각 항목은 `@username` / `email` / `"이름 <email>"` 자유 형식)
- `dependencies?`: 의존하는 다른 Module 목록 (가능하면 최소화, 순환 의존은 금지함)

### Module 간 의존

Module 간 의존(`dependencies`)은 **가능하지만, 최소화**하는 것을 권장합니다.

- Module이 서로 얽혀 있으면, Registry에서 개별 Module을 선택하고 조합하기 어려워집니다.
- Benchmark Module로 여러 구현체를 공정하게 비교하기도 복잡해집니다.
- 모듈간 의존이 필요하면 import보다는 필요한 부분만 copy하는 것을 권장합니다.
- 지나치게 많이 copy되는 모듈은 엔진으로 승격 대상이니 이슈로 보고해주세요.
- A → B → A 같은 순환 의존은 금지합니다.

### Contributors 필드

- `@username`, `email`, `"이름 <email>"` 등 원하는 형식으로 자유롭게 기재할 수 있습니다.
- 익명 참여자는 `@anonymous` 또는 빈 값으로도 가능합니다.
- Registry UI는 contributors를 명확히 표시하여, 기여자에게 credit을 부여합니다.

### 동일 기능 다중 구현체와 Benchmark

- 동일 기능에 대한 다중 구현체를 **허용**합니다.
- 사용자는 Registry UI에서 여러 구현체 중 선택할 수 있습니다.
- 동일 기능 다중 구현체 간 경쟁을 위한 벤치마크는 **Benchmark Module**로서 구현합니다.
- Benchmark Module도 registry에 등록되며, author/contributors credit을 받습니다.

### PR 프로세스

- 작은 Module 하나부터 시작하는 것을 추천합니다.
- PR 설명에 "이 Module이 해결하는 문제"와 "contributors에 포함할 이름"을 명확히 적어주세요.
- Engine 변경이나 아키텍처 수정은 이슈에서 먼저 논의한 후 PR을 보내주세요.

### 라이선스

hanpil은 오픈소스 프로젝트입니다. 기여한 코드는 프로젝트 라이선스를 따릅니다.

---

*이 문서는 프로젝트가 성장함에 따라 여러개로 분리(RFC, ADR)될 수 있습니다.*
