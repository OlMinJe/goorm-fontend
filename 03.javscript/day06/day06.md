# 자바스크립트의 객체(Object)와 프로토타입(Prototype)

## ✅ 객체(Object)

### 1. 기본 개념과 생성 방법

> 자바스크립트 객체는 `키-값` 쌍으로 구성된 자료구조로, 다양한 방법을 통해 생성할 수 있다.

1. 객체 리터럴(`{}`)
2. 생성자 함수(`new Object()`, 사용자 정의 생성자)
3. 클래스(`class` 키워드, 내부적으로는 `prototype`) 기반

```javascript
const student = {
  name: 'minje',
  age: 26,
  sad: function () {
    console.log('왜이렇게 아프지');
  },
};
```

### 2. 객체 속성 접근과 메서드 호출

`.`을 사용하여 속성과 메서드에 접근할 수 있다.
위의 코드를 에시로 출력하면, `student.name`, `student.age`는 `minje`, `26`이 출력된다.

### 3. 객체 관련 주요 메서드

| 메서드                          | 설명                              | 예시                                                  |
| ------------------------------- | --------------------------------- | ----------------------------------------------------- |
| `Object.keys(obj)`              | 객체의 키들을 배열로 반환         | `Object.keys(cat) → ["name", "age", "color", "meow"]` |
| `Object.values(obj)`            | 객체의 값들을 배열로 반환         | `Object.values(cat) → ["이설이", 2, "흰색", ƒ]`       |
| `Object.entries(obj)`           | [키, 값] 쌍을 배열로 반환         | `Object.entries(cat)`                                 |
| `Object.assign(target, source)` | 객체 복사/합치기                  | `Object.assign({}, cat)`                              |
| `Object.freeze(obj)`            | 객체를 동결하여 수정 방지         | `Object.freeze(cat)`                                  |
| `Object.seal(obj)`              | 속성 추가/삭제는 막고 수정만 허용 | `Object.seal(cat)`                                    |
| `Object.hasOwnProperty(key)`    | 객체에 해당 키가 직접 있는지 확인 | `cat.hasOwnProperty("name")`                          |
| `Object.getPrototypeOf(obj)`    | 객체의 프로토타입 반환            | `Object.getPrototypeOf(cat)`                          |

## ✅ 프로토타입(Prototype)

**객체는 언제나 함수(Function)로 생성된다.**

```javascript
function Person() {} // 함수

let personObject = new Person(); // 함수로 객체를 생성
```

일반 객체 생성도 똑같다.

```javascript
let obj = {};
```

### 기본 개념과 활용 방안

자바스크립트는 프로토타입 기반 언어이며, 객체는 자신의 부모 객체(프로토타입)을 가리키는 `__proto__` 속성을 통해 상속 구조를 가진다.

> **📌 프로토타입이 뭔데**
>
> 자바스크립트는 클래스 기반이 아니라 프로토타입 기반의 언어이다.
> 이 말은 객체 간에 상속이나 공통 기능 공유가 프로토타입 체인이라는 방식으로 이루어진다는 의미!
>
> ### ✅ 정리해보자
>
> - `prototype`은 객체가 상속받는 부모 역할을 하는 객체이다.
> - 모든 객체는 내부에 `[[Prototype]]`이라는 숨겨진 속성을 가지고 있고, 이걸 개발자는 `__proto__`로 접근하여 볼 수 있다.
> - 생성자 함수에는 `prototype`이라는 속성이 있고, 이 생성자로 만들어진 객체들이 공유할 공통 속성이나 메서드를 넣을 수 있는 공간이다.
>
> ### ✅ 왜 필요한가?
>
> 객체를 여러 개 만들 때, 중복 없이 메서드를 공유할 수 있기 떄문이다.
> 즉, 생성자 함수의 `prototype` 속성을 이용해 공통 메서드를 공유할 수 있다.
>
> ### ✅ 프로토타입 체인이란?
>
> 객체에서 어떤 속성이나 메서드를 찾을 때
>
> 1. 자기 자신에서 먼저 찾고
> 2. 없으면 `__proto__`가 가리키는 부모 객체에서 찾고
> 3. 계속 위로 올라가다 끝까지 가면 `null`에서 멈춘다.
>
> 이렇게 연결된 구조를 프로토타입 체인이라고 한다.

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.hello = function () {
  console.log(`안녕, 나는 ${this.name}이고 ${this.age}살이야!`);
};
```

- 프로토타입 체인으로 상위 객체의 속성과 메서드를 참조할 수 있다.
- `Object.getPrototypeOf()` 및 `Object.setPrototypeOf()`를 통해 명시적으로 프로토타입 조작이 가능하다.(직접 조작[`__proto__`]은 비권장)

### ❓ 화살표 함수는 왜 생성자 함수로 사용할 수 없을까?

1. 화살표 함수는 `this` 바인딩 방식이 다르기 때문이다

   - 일반 함수는 호출 방식에 때라 `this`가 바뀌지만,
   - 화살표 함수는 자신이 선언된 위치의 `this`를 렉시컬(정적)하게 고정한다.

2. 생성자 함수는 `new` 키워드를 통해 새로운 객체를 생성하고 `this`를 그 객체로 바인딩하는 형식

- 반면에, 화삺표 함수는 `this`를 직접 바인딩하지 않는다.

  > 🔍 왜 화살표 함수는 `this`를 바인딩하지 않을까?
  >
  > ### ✅ 일반 함수의 this 바인딩
  >
  > 일반 함수는 함수 호출 방식에 따라 this가 결정된다.
  >
  > ```javascript
  > function regular() {
  >   console.log(this); // 호출 방식에 따라 this가 달라짐
  > }
  > ```
  >
  > - 메서드로 호출되면 해당 객체가 `this`, 그냥 호출하면 전역(`window` / `undefined in strict mode`)
  > - `new`를 쓰면 새 객체가 `this`
  >
  > ### ❌ 화살표 함수는 this를 고정한다
  >
  > - 화살표 함수는 자신이 선언된 시점의 외부 스코프의 `this`를 그대로 사용한다.
  >   즉, `this`를 바인딩할 수 없으며 `call`, `apply`, `bind`, `new` 같은 메서드로도 `this`를 변경할 수 없다.
  >
  > ```javascript
  > const obj = {
  >   name: '이설이',
  >   regularFunc: function () {
  >     console.log('regular:', this); // this → obj
  >   },
  >   arrowFunc: () => {
  >     console.log('arrow:', this); // this → 외부 스코프(여기선 전역)
  >   },
  > };
  > obj.regularFunc(); // obj
  > obj.arrowFunc(); // window (또는 undefined)
  > ```
  >
  > ### 그래서 new와 함께 쓸 수 없다
  >
  > 생성자 함수는 호출 시 내부적으로 `this = {}`를 만들고 바인딩한다.
  > 하지만 화살표 함수는 그 바인딩 과정을 전혀 수행하지 않기 때문에, `new`를 사용할 수 없다.
  >
  > ```javascript
  > const Foo = () => {
  >   this.value = 10;
  > };
  >
  > new Foo(); // TypeError: Foo is not a constructor
  > ```

## ✅ DOM 객체의 프로토타입 구조

브라우저 환경에서 DOM 객체들도 게층적인 프로토타입 구조를 가지고 있다.

```javascript
console.log(Object.gerPrototypeOf(document.body)); // HTMLBodyElement
```

`window` 객체의 경우

- `Window.prototype` > `EventTarget.prototype` > `Object.prototype` > `null`
