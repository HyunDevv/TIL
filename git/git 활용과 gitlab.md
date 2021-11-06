# gitlab 활용

---

## 좋은 git 커밋 메시지

1. 제목과 본문을 한 줄 띄워 분리하기
2. 제목은 영문 기준 50자 이내로
3. 제목 첫글자를 대문자로
4. 제목 끝에 `.` 금지
5. 제목은 `명령조`로 : 첫 단어를 `동사원형`으로 작성
6. 본문은 영문 기준 72자마다 줄 바꾸기
7. 본문은 `어떻게` 보다 `무엇을`, `왜`에 맞춰 작성하기

---

https://blog.ull.im/engineering/2019/03/10/logs-on-git.html

- 동명사보다 명사를 사용

- 관사는 사용하지 않습니다

- 부정문 `Don't`를 사용합니다

- 오타 수정은 `Fix type` 로 입력

- 좋은 커밋 메시지를 위한 영어 단어 목록

  - Fix
    - Fix A
    - Fix A in B
    - Fix A which B : B절인 A를 수정합니다
    - Fix A to B : B를 위해 A를 수정합니다
    - Fix A so that B : A를 수정해서 B가 되었습니다
    - Fix A where B : B처럼 발생하는 A를 수정했습니다
    - Fix A when B : B일 때 발생하는 A를 수정했습니다
  - Add
    - Add A
    - Add A for B : B를 위해 A를 추가했습니다
    - Add A to B : B에 A를 추가했습니다
  - Remove
    - Remove A
    - Remove A form B : B에서 A를 삭제합니다
  - Use
    - Use A
    - Use A for B : B에 A를 사용합니다
    - Use A to B : B가 되도록 A를 사용합니다
    - Use A in B : B에서 A를 사용합니다
    - Use A instead of B : B 대신 A를 사용합니다
  - Refactor : 전면 수정이 있을 때 사용합니다
  - Simplify A : A를 단순화합니다
  - Update : 개정이나 버전 업데이트가 있을 때 사용,  수정,추가,보완을 한다는 개념,  코드보다는 문서나 리소스, 라이브러리 등에 사용
    - Update A to B : A를 B로 업데이트 합니다
  - Improve A : A를 향상시킵니다
  - Make : 기존 동작의 변경을 명시
    - Make A B : A를 B하게 만듭니다
  - Implement
    - Implement A : A를 구현합니다, Add에 비해 더 큰단위의 코드에 추가, 모듈이나 클래스 단위에 사용
    - Implement A to B : B를 위해 A를 구현합니다
  - Revise A : A 문서를 개정합니다
  - Correct : 주로 문법의 오류나 타입의 변경, 이름 변경 등에 사용합니다
    - Correct A : A를 고칩니다
  - Ensure A : A가 확실히 보장 되도록 수정했습니다
  - Prevent A : A하지 못하게 막습니다
    - Prevent A form B : A를 B하지 못하게 막습니다
  - Avoid
    - Avoid A : A를 회피합니다
    - Avoid A if B : B인 상황에서 A를 회피합니다
  - Move A to B : A를 B로 옮깁니다
  - Rename A to B : A를 B로 이름 변경합니다
  - Allow A to B : A가 B를 할 수 있도록 허용합니다
  - Verify A : A를 검증합니다
  - Set A to B : A를 B로 설정합니다
  - Pass A to B : A를 B로 넘깁니다

  

- 자주 쓸거 같은 단어 : Add, Remove, Fix, Update,,,  Use, Make



---

## Merge Request (병합 요청)

### [GitLab 이슈를 활용한 Git Branch Strategy](https://waspro.tistory.com/710)

https://waspro.tistory.com/710



---

## Label

https://forge.etsi.org/rep/help/user/project/labels.md