# 📘 Web APIs와 DOM 이해

## 1️⃣ Web APIs란?

오늘은 자바스크립트가 웹 브라우저와 어떻게 상호작용하는지를 담당하는 **Web APIs**에 대해 공부했다.
**Web APIs**는 브라우저가 자바스크립트에게 제공하는 기능 모음으로, 단순히 HTML과 CSS를 보여주는 것을 넘어서, 페이지를 동적으로 조작할 수 있게 해준다.

### 대표적인 **Web APIs** 예시

- **DOM API**: 문서 구조를 읽고 수정할 수 있다.
- **Events API**: 사용자 입력 감지 및 반응
- **Fetch API**: 서버와 데이터 주고받기

이러한 API 덕분에 자바스크립트는 정적인 페이지를 동적으로 바꿀 수 있다.

## 2️⃣ DOM과 인터페이스

**DOM(Document Object Model)**은 HTML 문서를 객체로 표현한 구조다.
여기서 중요한 점은 **DOM이 브라우저가 제공하는 인터페이스**라는 것이다.

### ✅ DOM 인터페이스란?

- DOM 인터페이스는 자바스크립트가 HTML 요소를 객체로 다루기 위한 일종의 "청사진"이다.
- 예를 들어, `Document`, `Element`, `HTMLElement` 등은 모두 DOM 인터페이스이다.
- 이 인터페이스들은 자바스크립트 객체처럼 사용할 수 있도록 메서드와 속성을 제공한다.

### 📌 JS에서 인터페이스란?

자바스크립트는 타입스크립트처럼 명시적인 `interface` 키워드는 없지만, 브라우저나 표준 라이브러리에서 제공하는 객체들은 공식적으로 정의된 속성과 메서드를 따르는 일종의 인터페이스로 볼 수 있다.
즉, DOM 객체들은 특정한 메서드 체계를 따르고 있으며, 이. 구조가 바로 "인터페이스"이다

## 3️⃣ DOM 객체 정리

| 객체       | 의미                |
| ---------- | ------------------- |
| `Document` | 전체 HTML 문서      |
| `Element`  | HTML 요소 개별 객체 |

DOM에서 요소에 접근하려면 여러 메서드를 활용한다.

**주요 DOM 접근 메서드**

- `getElementById(id)`
- `getElementsByClassName(class)`
- `querySelector(selector)`
- `querySelectorAll(selector)`

이 외에도 태그 이름, name 속성, 네임스페이스 등을 기준으로 접근하는 다양한 메서드가 있다.

## 4️⃣ Events & addEventListener

브라우저는 사용자와의 상호작용을 위해 **이벤트(Event)**의 개념을 제공한다.

- `click`, `scroll`, `submit` 등 다양한 이벤트가 있따.
- 이벤트는 `addEventListener()` 메서드로 연결한다

```javascript
const btn = document.getElementById('myBtn');
btn.addEventListener('click', () => {
  alert('버튼 클릭!');
});
```

## 5️⃣ 클래스 조작: Element.classList

DOM 요소의 클래스(class)를 조작할 때는 `classList` 속성을 사용하면 편리하다.

```javascript
element.classList.add('active');
element.classList.remove('hidden');
element.classList.toggle('selected');
element.classList.contains('highlighted');
element.classList.replace('old', 'new');
```

`classList`는 내부적으로 DOMTokenList 인터페이스를 따른다.

## 6️⃣ 스타일 조작: HTMLElement.style

HTML 요소의 인라인 스타일을 자바스크립트에서 설정할 수 있다.

```javascript
element.style.backgroundColor = 'blue';
element.style.opacity = '0.8';
button.style.display = 'none';
```

CSS 속성명은 camelCase로 변환해서 사용해야 한다.
예: `margin-top -> marginTop`, `font-size -> fontSize`

## 7️⃣ console 객체 활용

디버깅과 테스트를 위해 자바스크립트에서는 `console` 객체를 자주 활용한다.

### 주요 메서드

| 메서드            | 설명                           |
| ----------------- | ------------------------------ |
| `console.log()`   | 일반 로그 출력                 |
| `console.error()` | 에러 메시지 출력               |
| `console.warn()`  | 경고 메시지 출력               |
| `console.info()`  | 정보 메시지 출력               |
| `console.table()` | 객체나 배열을 표 형식으로 출력 |

```javascript
console.log('버튼이 클릭됨');
console.error('오류 발생!');
console.table([
  { name: '홍길동', age: 20 },
  { name: '김철수', age: 25 },
]);
```

## ✍️ 느낀 점

- 지금까지 자바스크립트를 단순히 코드로만 생각했었는데, 브라우저가 제공하는 **Web API**와 **DOM 인터페이스**를 통해 자바스크립트가 웹과 사화작용하는 방법을 더 잘 이해하게 되었다.
- DOM은 문서를 객체처럼 다루기 위한 기반 구조이며, 각 HTML 요소는 다 **객체(인터페이스)**로 표현된다는 개념이 인상 깊었다.
- `console` 객체를 활용하면 디버깅과 데이터 확인이 훨씬 수월하다는 점도 확인했다.
- 앞으로는 인터페이스의 개념과 객체 구조 이해를 바탕으로 코드를 더 체계적으로 바라볼 수 있을 것 같다.
