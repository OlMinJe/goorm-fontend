# 📚 10일차 학습일지 — 자바스크립트 주요 표준 내장 객체 & ES3 이후 문법

## 🕒 Date — 날짜/시간 객체

- **역할:** 현재 또는 특정 날짜와 시간을 표현/조작
- **주요 메서드:**
  - `getFullYear()` : 연도
  - `getMonth()` : 월 (0~11)
  - `getDate()` : 일
  - `toISOString()` : 표준 문자열 변환

```js
const now = new Date();
const birthday = new Date('2005-10-15');
console.log(birthday.getFullYear()); // 2005
```

## ❗ Error — 에러 객체

- **역할**: 예외 상황 정보 전달
- `throw new Error(message)`로 발생 가능
- `try...catch` 블록에서 처리

```javascript
try {
  throw new Error('문제 발생!');
} catch (err) {
  console.error(err.name, err.message);
}
```

## 🚫 TypeError — 타입 에러

- **역할**: 잘못된 타입 사용 시 발생
- Error의 하위 클래스

```javascript
function shout(text) {
  if (typeof text !== 'string') {
    throw new TypeError('문자열만 입력하세요');
  }
  return text.toUpperCase();
}
```

### 🗺️ Map — 키-값 자료구조

- 모든 타입을 키로 사용 가능
- 입력 순서 보장
- 주요 메서드: `set`, `get`, `has`, `delete`

```javascript
const m = new Map();
const objKey = { id: 1 };
m.set(objKey, 'value');
console.log(m.get(objKey)); // value
```

객체(`{}`)와 달리 키 순서 보장 + 객체/심볼 등 다양한 타입을 키로 사용 가능

### 🧺 Set — 중복 없는 값 집합

- 값이 중복되면 자동 제거
- 배열 중복 제거에 활용

```javascript
const unique = [...new Set([1, 2, 2, 3])]; // [1, 2, 3]
```

## 2. ES3 이후 주요 문법 학습

### ✅ 옵셔널 체이닝 (`?.`) & 널 병합 연산자 (`??`)

- 옵셔널 체이닝: 안전한 중첩 속성 접근
- 널 병합: `null`/`undefined`일 때만 기본값 사용

```javascript
user?.profile?.name ?? '이름 없음';
```

### ✅ 모듈 시스템 (import / export)

- 코드 분리와 재사용성 향상
  -Barrel pattern: 여러 모듈을 한 파일에서 재수출

### ✅ 구조 분해 할당 (Destructuring)

- 객체/배열의 특정 속성을 변수로 추출

```javascript
const { name, age } = user;
const [a, b] = [1, 2];
```

### ✅ Rest 문법

- 나머지 속성/요소를 한 변수에 모음

```javascript
const { id, ...rest } = user;
```

### ✅ Spread 문법

- 객체/배열 값 펼치기, 복사/병합

```javscript
const merged = { ...obj1, ...obj2 };
```

### ECMAScript 버전별 주요 기능 요약

| 버전     | 주요                                                          | 기능 |
| -------- | ------------------------------------------------------------- | ---- |
| ES5      | `use strict`, 배열 고차함수, `JSON.parse`                     |
| ES6      | `let`/`const`, 화살표 함수, `class`, `Map`/`Set`, 모듈 시스템 |
| ES7      | 지수 연산자 `**`, `includes()`                                |
| ES8      | `async/await`, `Object.entries()`                             |
| ES9      | 객체 rest/spread, `Promise.finally()`                         |
| ES10     | `flat()`, `flatMap()`                                         |
| ES11     | BigInt, `??`, `?.`                                            |
| ES12     | `replaceAll()`, `Promise.any()`                               |
| ES13     | `at()`, 클래스 프라이빗 필드                                  |
| ES14     | `toSorted()`, `findLast()`                                    |
| ES15     | `groupBy()`                                                   |
| ES16(안) | `Promise.try()`, `Array.fromAsync()`                          |

## 정리

- Map은 모든 타입 키 가능, 순서 보장
- Object는 문자열/심볼 키만 가능, 숫자 키 정렬됨
- Set으로 배열 중복 제거가 간단해짐
- 옵셔널 체이닝과 널 병합으로 안전한 데이터 접근 가능
- Spread와 Rest는 문법은 같지만 역할이 반대
