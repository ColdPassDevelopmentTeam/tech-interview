# Tech Interview 스터디 기여 규칙 (Contribution Guide)

이 문서는 스터디 멤버들이 원활하게 협업하고, 일관성 있는 학습 자료를 함께 만들어나가기 위한 규칙입니다. 기여하시기 전에 꼭 읽어주세요!

---

## 기여 절차 (Git Workflow)

모든 기여는 **Fork & Pull Request** 방식으로 진행합니다.

1.  **Fork**: `co2plant/tech-interview` 레포지토리를 자신의 GitHub 계정으로 Fork 합니다.(만약 Fork없이 작업하고 싶은 경우 레포지토리를 `co2plant/tech-interview` 레포지토리로 유지한채 3번으로 넘어가세요)
2.  **Clone**: Fork한 개인 레포지토리를 로컬 환경으로 Clone 합니다.
    ```bash
    git clone [https://github.com/Your-Username/tech-interview.git](https://github.com/Your-Username/tech-interview.git)
    ```
3.  **Branch 생성**: 새로운 작업을 위한 브랜치를 생성합니다. 브랜치 이름은 작업 내용을 알 수 있도록 작성합니다.
    -   `feat/네트워크-http-개념-정리` (새로운 내용 추가)
    -   `fix/자료구조-오타-수정` (기존 내용 수정)
    ```bash
    git checkout -b fix/자료구조-오타-수정
    ```
4.  **작업 및 Commit**: 내용을 수정하거나 추가한 뒤, 아래의 **커밋 메시지 컨벤션**에 맞춰 커밋합니다.
5.  **Push**: 작업한 브랜치를 자신의 원격 레포지토리(origin)에 Push 합니다.
6.  **Pull Request (PR) 생성**: GitHub에서 `co2plant/tech-interview` 레포지토리로 Pull Request를 생성합니다. PR 내용은 아래 **PR 템플릿**을 참고하여 작성합니다.

---

## 커밋 메시지 컨벤션

커밋 메시지는 다음 형식을 따릅니다: `<타입>: <제목>`

-   **타입**:
    -   **`docs`**: 문서 내용 추가, 수정, 삭제 (가장 많이 사용)
    -   **`feat`**: 새로운 주제나 폴더 구조 추가
    -   **`fix`**: 오타 수정, 잘못된 내용 바로잡기
    -   **`style`**: 코드 블록, 마크다운 스타일 등 형식 수정
    -   **`chore`**: 기타 잡다한 변경 사항 (예: 파일 이동, 폴더 구조 변경 등)
-   **제목**: 변경 내용을 요약한 한 줄 설명

**예시)**
- `docs: 트랜잭션 격리 수준 내용 보강`
- `fix: 프로세스와 스레드 오타 수정`
- `feat: Network 카테고리 추가`

---

## Pull Request(PR) 템플릿 예시

해당 템플릿은 예시로 반드시 지켜야하는 항목은 아닙니다. 필요에 의해서 얼마든지 바꿀 수 있습니다.

```markdown
## 어떤 작업을 하셨나요?
예: 데이터베이스 파트의 '정규화'에 대한 내용을 추가했습니다.

## ✅ 체크리스트
- [ ] 커밋 컨벤션을 지켰나요?
- [ ] 오타나 잘못된 내용은 없나요?

Closes #이슈번호 (해결한 이슈가 있다면)
```
