#  Weekly Review - 도서 관리 시스템 (CRUD Service)

이번 주에 학습한 DOM 조작과 JavaScript 배열을 활용하여 도서 관리 시스템을 구현하고 배포하였습니다.

---

##  Deployment
* **Vercel 배포 URL**: https://2026ossassign05-sandy.vercel.app/


---

## Key Learning

### 1. CRUD Service 구현
* **서비스 주제**: 도서 정보(제목, 저자, 카테고리, 가격)를 관리하는 웹 애플리케이션
* **사용 데이터 Field**: 
  * `id` (고유 번호, 자동 증가)
  * `title` (도서 제목)
  * `author` (저자)
  * `category` (카테고리: Web, 책 등)
  * `price` (가격)
* **C R U D 구현 방법**:
  * **Create**: `form`의 `submit` 이벤트를 받아 입력값을 객체로 만든 뒤, `books.push()`를 통해 배열에 추가
  * **Read**: `render()` 함수를 만들어 `books` 배열을 순회(`forEach`)하며 동적으로 HTML 테이블(`<tr>`, `<td>`) 생성
  * **Update**: 수정 버튼 클릭 시 기존 데이터를 입력폼에 채워넣고(`editBook`), 저장 시 `findIndex`로 해당 아이템을 찾아 값 갱신
  * **Delete**: 삭제 버튼 클릭 시 `confirm` 창을 띄운 후 `splice()` 메서드로 배열에서 해당 인덱스 데이터 제거

### 2. 주요 JavaScript 기능
* `document.getElementById()`: DOM 요소를 자바스크립트 객체로 가져오기
* `addEventListener("submit", ...)`: 폼 제출 이벤트 감지 및 처리
* `e.preventDefault()`: 폼 제출 시 페이지가 새로고침되는 기본 동작 차단
* `Array Methods (`push`, `findIndex`, `splice`, `find`)`: 배열 데이터 추가, 검색, 삭제 처리
* `Template Literals (``) & innerHTML`: 동적 HTML 문자열을 조합하여 테이블 렌더링

---

## AI / Search Usage

이번 과제를 진행하면서 다음과 같은 문제 해결을 위해 AI(Gemini)와 검색을 활용했습니다.

1. **JavaScript 배열 데이터 렌더링(`render`) 로직 구성**
   * **문제**: 배열에 담긴 데이터를 화면의 HTML 테이블에 동적으로 반복 출력하는 구조를 설계하는 데 어려움을 겪음.
   * **적용**: `forEach` 반복문 안에서 템플릿 리터럴과 `innerHTML`을 활용해 테이블 행(`<tr>`)을 동적으로 생성하고 누적하는 코어 로직을 참고하여 구현.
   * **새롭게 이해한 내용**: DOM 요소를 하나씩 직접 생성하는 방식보다 문자열 템플릿을 조합해 한 번에 주입하는 방식이 코드가 훨씬 직관적이고 관리하기 편하다는 점을 알게 됨.
2. **폼 데이터 저장 오류 트러블슈팅**
   * **문제**: 카테고리에 새로운 항목을 추가하고 저장했을 때 데이터가 제대로 반영되지 않는 현상 발생.
   * **적용**: AI 진단을 통해 `<select>` 태그 내부의 `<option value="Web">` 값이 중복 설정되어 있던 원인을 파악하고, 각 옵션의 `value`를 올바르게 분리(`value="Web"`, `value="책"`)하여 해결.

---

## Problem & Solution

* **Issue : `<select>` 카테고리 선택 값 누락 및 저장 불가**
  * **원인**: 새롭게 추가한 '책' 옵션의 `value` 속성이 기존 'Web'과 동일하게 들어가 있어 자바스크립트가 올바른 값을 읽어오지 못함.
  * **해결**: HTML에서 `<option value="책">책</option>`으로 값을 명확히 분리하여 정상 작동 확인.


---

## Reflection

이번 과제를 통해 프론트엔드에서 서버(DB) 없이 **JavaScript 배열 메모리만으로도 완벽한 CRUD 로직을 구현**할 수 있다는 점을 실습할 수 있었습니다. 특히 화면을 다시 그려주는 `render()` 함수의 구조와 이벤트 기본 동작(`preventDefault`)의 중요성을 몸소 느꼈으며 폼 태그의 `value` 설정 미스가 데이터 처리 오류로 이어질 수 있다는 점을 배우는 좋은 계기가 되었습니다.