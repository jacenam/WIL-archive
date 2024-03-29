# 즉시 실행 함수

**Table of Contents**

- [즉시 실행 함수](#즉시-실행-함수)
  - [익명 함수와 기명 함수](#익명-함수와-기명-함수)
  - [즉시 실행 함수와 그룹 연산자](#즉시-실행-함수와-그룹-연산자)
  - [값의 반환과 인수 전달](#값의-반환과-인수-전달)
- [즉시 실행 함수를 사용하는 이유](#즉시-실행-함수를-사용하는-이유)

<br>

## 즉시 실행 함수

함수는 함수를 정의한 후 메모리에 함수를 저장하고 식별자를 통해 함수를 호출해서 실행하는 과정을 거친다. 반면, 즉시 실행 함수(Immediately Invoked Function Expression)는 함수를 정의하자마자 즉시 호출한다

```javascript
(function () {
  var x = 3;
  var y = 5; 
  var z = 7;
  return x + y + z;
})(); // → 15
```

### 익명 함수와 기명 함수

즉시 실행 함수는 [그룹 연산자(`()`)]() 내에 익명 함수를 위치해 사용한다. 기명 함수는 왜 사용하지 않는 것일까?

<img width="100%" src="https://user-images.githubusercontent.com/92138751/233101296-d364a7a9-bfdb-4653-8511-dfa27ada2e4a.png">

위 예제에서 그룹 연산자의 피연산자는 함수이며 그룹 연산을 위해 함수는 값으로 평가가 가능한 표현식이어야 한다. 다시 말해, 그룹 연산자 내의 함수 정의는 함수 선언문이 아니라 함수 표현식으로 인식된다는 의미다. 따라서 위 예제의 함수 정의는 함수 표현식으로 인식되는 함수 리터럴로서 값을 생성한다. 그리고 함수가 즉시 호출되어 생성된 값은 메모리에 저장된다. [리터럴을 통해 값이 생성되어 메모리에 저장되는 메커니즘]()을 복기해보자. 이해가 훨씬 쉬워진다. 아래와 같이 변수 혹은 함수 식별자가 없어도 생성된 값은 메모리에 저장된다.

<img width="100%" src="https://user-images.githubusercontent.com/92138751/233101576-dcc4b1eb-4fb9-4cb1-80ee-f55dbb742fc6.png">

그렇다면 기명 함수를 사용하면 식별자를 통해 즉시 실행 함수도 재차 호출해서 재사용이 가능하지 않을까?

```javascript
(function sum() {
  var x = 3; 
  var y = 5; 
  var z = 7; 
  return x + y + z;
})(); // → 15

sum(); // → ReferenceError: sum is not defined
```

정답은 ‘재사용이 불가능하다’이다. 기명 함수도 그룹 연산자 내에 위치한다면 위 예제와 동일하게 함수 선언문이 아닌 함수 표현식으로 JS 엔진에 의해 인식된다. 그렇기에 메모리에는 (즉시 실행 함수의) 함수 표현식과 즉시 호출되어 생성된 숫자 값 `15`가 저장된다

따라서 [함수 표현식의 내부 동작]()에서 언급했듯이, 함수 표현식에서는 함수가 저장된 메모리의 참조 값을 가리키는 식별자가 암묵적으로 생성되지 않아 함수 몸체 외부에서 함수를 함수 이름(식별자)으로 함수를 참조할 수 없다. 즉, 그룹 연산자 내의 기명 함수도 즉시 실행 함수를 다시 호출할 수 없다. 기명 함수를 사용해도 즉시 실행 함수를 재사용할 수 없기 때문에, 즉시 실행 함수에서는 일반적으로 익명 함수를 사용하는 것이다

<img width="100%" src="https://user-images.githubusercontent.com/92138751/233104155-36c44897-a766-4820-b04a-2789aeb82d4f.png">

### 즉시 실행 함수와 그룹 연산자

즉시 실행 함수는 반드시 그룹 연산자(`(...)`)로 감싸야 하며 함수 선언문 뒤에는 함수 호출 연산자(`()`)가 필요하다. 만약 그룹 연산자로 즉시 실행 함수를 감싸지 않으면 아래 코드 예제는 함수 선언문으로 인식되며, 함수 선언문의 형식(기명 함수)에 부합하지 않기 때문에 에러가 발생한다

```javascript
function () {
}(); // → SyntaxError: Function statements require a function name
```

기명 함수로 함수를 정의해 그룹 연산자 없이 즉시 실행하고자 했을 때에도 에러가 발생한다. JS 엔진이 함수 코드블록(함수 몸체)이 끝나는 ‘닫는 중괄호’(`}`) 뒤에 암묵적으로 세미콜론(`;`)을 자동으로 추가하기 때문이다

```javascript
// 예제 코드 원래의 상태
function sum() {
  var x = 3; 
  var y = 5; 
  return x + y; 
}(); // → SyntaxError: Unexpected token ')'

// 세미콜론이 자동 삽입된 상태
function sum() {
  var x = 3;
  var y = 5;
  return x + y;
};();
```

원시 값과 객체를 생성하는 리터럴 표현식과는 달리, 함수는 코드블록문(제어문, 함수선언문 등)의 종료를 명시하기 위해 세미콜론을 뒤에 붙이지 않는 것이 일반적이지만, 사실 세미콜론을 붙여도 에러가 발생하지는 않는다. 그렇다면 위 예제는 어째서 오류가 발생하는 것일까? 함수 코드 블록 뒤에 함수 호출 연산자가 위치해서 그런가?

```javascript
function sum() {
  var x = 3;
  var y = 5; 
  return x + y; 
}; // 세미콜론을 함수 코드 블록 뒤에 붙여도 에러가 발생하지 않는다

console.log(sum()); // → 8
```

아래 예제를 풀어서 쓴 코드를 보면, 함수 코드 블록 뒤에 괄호(`()`)가 함수 호출 연산자가 아니라 그룹 연산자로 인식되며, 그룹 연산자의 피연산자가 없기 때문에 문법 에러가 발생하는 것이다. 따라서 즉시 실행 함수는 그룹 연산자로 꼭 감싸야한다

<img width="100%" src="https://user-images.githubusercontent.com/92138751/233105529-2d71b773-4cf7-4041-9364-b000e90ce166.png">

```javascript
=> function sum() {
  var x = 3; 
  var y = 5; 
  return x + y;
}; 

(); // → SyntaxError: Unexpected token ')'
```

### 값의 반환과 인수 전달

앞서 즉시 실행 함수는 함수 정의 직후 함수 호출이 실행되어 결과 값을 반환한다 했다. 즉시 실행 함수의 결과 값은 일반 함수처럼 변수에 할당하거나 반환이 가능하다

```javascript
// 일반 함수
function sum(x, y) {
  return x + y;
}

sum(3, 5); // → 8

// 즉시 실행 함수
var result = (function () {
  var x = 3;
  var y = 5; 
  return x + y;
})(); 

console.log(result); // → 8
```

또한 즉시 실행 함수에도 일반 함수처럼 매개변수에 전달할 인수를 지정할 수도 있다

```javascript
var result = (function (x, y) {
  return x + y;
})(3, 5); 

console.log(result); // → 8
```

<br>

## 즉시 실행 함수를 사용하는 이유 (추후 정리 필요)

즉시 실행 함수는 왜 사용하는 것일까? 즉시 실행 함수 내에 함수 코드를 모아 두면 혹시 있을 수도 있는 변수나 함수 이름의 충돌을 방지할 수도 있다. 이 전역 변수의 부작용으로 인해 야기되는 문제들을 방지할 수 있는 방법이기도 하다. 이에 대해서는 [전역 변수의 사용을 억제하는 방법]()을 참고하자

<br>

## 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)
- [즉시실행함수(IIFE)](https://jongminfire.dev/java-script-%EC%A6%89%EC%8B%9C%EC%8B%A4%ED%96%89%ED%95%A8%EC%88%98-iife)
- [즉시호출함수, 즉시실행함수 IIFE](https://jongminfire.dev/java-script-%EC%A6%89%EC%8B%9C%EC%8B%A4%ED%96%89%ED%95%A8%EC%88%98-iife)
- [함수, 즉시실행함수](https://beomy.tistory.com/9)

