# 변수

**Table of Contents**

- [변수란](#변수란)
- [변수의 동작 원리](#변수의-동작-원리)
- [JS 변수의 특징](#JS-변수의-특징)
- [변수 이름과 식별자](#변수-이름과-식별자)
- [변수 선언](#변수-선언)
- [호이스팅](#호이스팅)

<br>

## 변수란

모든 소프트웨어 프로그램은 데이터를 입력(Input)받아 처리하고 결과를 출력(Output)한다. 컴퓨터 연산(데이터의 입력 → 처리 → 출력)에 필요한 데이터(값)는 모두 메모리에 저장되므로, CPU는 메모리부터 연산되어야 할 값을 불러와(참조) 연산을 실행한다. '변수(Variable)'란 프로그래밍 언어에서 이러한 메모리 내의 데이터들을 관리하기 위한 핵심 개념이다

> 컴퓨터(Computer)는 단어 의미 그대로 연산을 하는 기기다. 컴퓨터는 연산(CPU)과 기억(메모리)을 수행하는 하드웨어가 나뉜다. CPU, 메모리 등 컴퓨터 구조와 연산 방식에 대해서는 [컴퓨터 공학 기초]()를 참고하자

<br>

## 변수의 동작 원리

변수는 왜 필요할까? 변수와 메모리의 관계를 살펴보자. 아래 예제는 `10 + 20`이라는 JS 코드를 실행했을 때 컴퓨터 내부에서 발생하는 일을 나타낸다!

연산될 숫자 값(피연산자) `10`과 `20`은 메모리 상의 임의의 메모리 위치(주소)에 저장되고 CPU는 이 값을 읽어들여(참조) `+` 연산을 수행한다. 연산 결과로 생성된 숫자 값 `30`도 메모리 상의 임의의 위치에 저장된다. 각 메모리 셀은 고유의 메모리 주소를 갖는다. 메모리 주소는 메모리 공간의 위치를 나타낸다

<img src="https://velog.velcdn.com/images/jacenam/post/6606a44c-5911-46c1-8222-0366da14a3b9/image.png" width="100%">

만약 결과 값 `30`이 저장된 메모리의 위치를 식별할 수 없게 된다면 `30`이 저장된 메모리 공간에 직접 접근하는 방법 외에는 결과 값을 재사용할 수 없다. 그러나 메모리 주소를 통해 값에 직접 접근하는 것은 컴퓨터 혹은 운영체제 상의 치명적 오류를 발생시킬 수 있기에, JS는 개발자의 직접적인 메모리 제어를 허용하지 않는다.

따라서 저장하고 싶은 값을 메모리에 저장하고 저장된 값을 읽어 들여 재사용하기 위해 변수라는 메커니즘이 제공된다.`result`라는 이름을 가진 변수에는 메모리에 저장된 결과 값 `30`의 메모리 주소 정보가 저장되어 있기 때문에 변수 `result`를 활용해 결과 값 `30`을 재사용할 수 있게 된다

<img src="https://velog.velcdn.com/images/jacenam/post/222bafb8-f943-409c-9421-0567a2734860/image.png" width="100%" align="center">

변수는 메모리 상에 값의 위치(메모리 주소) 정보를 가리키는 포인터의 개념이자 메모리 주소를 기억하고 있는 식별자라고 보면 된다. 다시 말해, 결과 값(`30`)은 변수에 저장되는 것이 아니라 메모리에 저장되며 변수는 실제 값이 저장된 메모리 주소를 기억하고 있는 식별자다

변수 `result`를 호출(참조)했을 때 `result`가 가리키는 `0x00000004` 메모리 주소를 기억해내 메모리 안에 저장된 숫자 값 `30`을 반환하는 것이다. 이에 개발자는 변수를 통해 값을 한번만 사용하거나 직접 메모리에 접근하여 값을 저장하고 참조할 필요 없이 안전하게 값들을 재사용할 수 있다

<img src="https://velog.velcdn.com/images/jacenam/post/1aa59a04-82d7-4e61-9ac4-53507663a923/image.png" width="100%" align="center">

<br>

## JS 변수의 특징

JS는 [매니지드(Managed) 언어이자 동적 언어(Dynamically Typed Language)]()으로 다른 언어에 비해 쉽고 안전한 메모리 관리 기능을 제공한다. 따라서 JS에서는 값이 저장될 메모리를 직접적으로 관리하지 않아도 되고 성능을 준수한 상태로 관리해 준다. 또한, 프로그래밍 언어에서 데이터를 관리하기 위해 쓰이는 [데이터 타입]()을 변수에 할당할 때 일일히 의도적으로 지정해 줄 필요가 없기 때문에 코드 작성면에서도 편리하다

변수는 보통 메모리에 저장될 값 한 개만을 식별한다

```javascript
var userId = 1;
var userName = "Jace";
```

여러 개의 값을 메모리에 저장하려면 여러 개의 변수를 사용해서 메모리를 다수 확보해야하지만, 배열이나 객체와 같은 자료 구조를 사용하면 연관성있는 여러 개의 값을 하나의 변수 값처럼 사용해 메모리를 보다 효율적으로 사용이 가능하다

```javascript
// 객체 구조
var userInfo = {
  id: 1,
  name: "Jace",
};

// 배열 구조
var users = [
  { id: 1, name: "Jace" },
  { id: 2, name: "Ju Hyung" },
];
```

<br>

## 변수 이름과 식별자

변수 이름을 식별자로고도 한다. 메모리 공간에 특정 값을 저장하고 참조하여 값을 재사용하기 위해 해당 값이 저장되어 있는 메모리 주소를 사람이 이해할 수 있는 언어의 이름으로 지정하는 것이다

<img src="https://velog.velcdn.com/images/jacenam/post/94d2722f-0800-4f0b-bc1c-834a29321026/image.png" width="100%" align="center">

식별자는 변수 이름에만 국한해서 사용하지 않는다. 예를 들어, 변수, 함수, 클래스 등의 사람이 이해할 수 있는 언어로 이름을 지정한 것은 모두 식별자다. 값이 저장된 메모리에 접근해서 값을 재사용하고 싶다면 식별자의 이름을 지정해서 '[선언](#5-변수-선언)'을 통해 JS 엔진에 식별자의 존재를 알려야 한다. 변수, 함수, 클래스 등의 식별자 이름은 [식별자 네이밍 규칙]()을 준수해서 선언해야 한다

```javascript
var userAge = 30;

function sayHello(name) {
  console.log(`Hello, ${name}`);
}
```

식별자 네이밍 규칙을 준수하는 것은 단순히 식별자 선언만을 위한 것이 아니라, 실무에서 원활한 소통과 협업을 위해 식별자의 이름은 식별자의 목적이나 의미를 직관적으로 파악할 수 있도록 쉽게 네이밍하는 것이 중요하기 때문이다

<br>

## 변수 선언

변수 선언(Declaration)이란 변수를 생성해서 JS 엔진에 변수 식별자의 존재를 알리는 것을 의미한다. 다시 말해, 값을 메모리에 저장하기 위해 메모리 공간을 확보하고 변수 이름과 확보된 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 것이다. 변수 선언에 의해 확보된 메모리 공간은 해제가 되기 전까지 해당 공간을 사용할 수 없다

변수를 선언할 때는 `var`, `let`, `const`의 식별자 선언 키워드를 사용한다. 변수는 물론 모든 식별자는 사용하기 위해 반드시 선언이 필요하다

> 키워드란 JS 엔진이 수행할 동작을 규정한 일종의 명령어다. 코드로 입력된 키워드를 JS 엔진이 인지한 순간, JS 엔진은 자신이 수행해야 할 규정된 동작을 실행한다. 변수 선언 키워드는 총 세 가지로, 이들의 차이에 대해서는 [스코프]()를 참고하자

```javascript
// 선언되지 않은 식별자를 통해 값에 접근하고자 하면 JS 엔진은 해당 식별자를 찾을 수 없기 때문에 에러가 발생한다
userName; // → Uncaught ReferenceError: userName is not difined
```

변수 선언 키워드를 사용해 변수를 선언할 경우 JS 엔진은 다음과 같은 작업들을 단계별로 수행한다:

<img src="https://velog.velcdn.com/images/jacenam/post/0ecc1140-7057-4dec-8d9c-ecca2be362b7/image.png" width="100%" align="center">

1. `var userName` 새로운 변수를 선언하는 단계:

   - 변수 이름을 [실행 컨텍스트]()에 등록해서 JS 엔진에 새로운 변수의 존재를 알린다

2. `undefined` 메모리 확보를 위한 초기화 단계:

   - 변수가 식별할 값을 메모리에 저장하기 위해 메모리 공간을 확보하고 디폴트로 `undefined`를 메모리에 해당 메모리 공간 내의 데이터를 초기화한다

     ```javascript
     // 변수에 값을 할당하지 않았을 때
     var userName; // → undefined
     
     // 변수에 값을 할당했을 때도 undefined가 항상 반환된다. undefined 할당 후 30을 메모리에 할당한다
     var userAge = 30; // → undefined
     ```

   - 이는 값을 저장하기 위해 확보된 메모리 공간 내 이전에 사용되었던 데이터(쓰레기 값, Garbage Value)를 초기화하는 것으로, JS에서는 식별자 선언 시 JS 엔진이 항상 `undefined`를 값으로 자동 할당하는 JS 언어만의 독특한 특징이다

이처럼 변수는 데이터의 저장, 사용 등 데이터 관리의 필수적인 장치다. 변수를 많이 사용하면 할수록 메모리를 그만큼 많이 사용하게 된다. 따라서 변수는 필요한 경우에 한해 제한적으로 사용해야 한다. 실제로 코딩 테스트 시 특정 메모리 용량만큼만 사용을 제한하는 경우도 필요한 만큼의 식별자만을 사용해서 최대의 효율성을 지닌 코드 짜는 방식이 중요하기 때문이다.

<br>

## 호이스팅

[호이스팅]()이란 식별자 키워드(`var`, `let`, `const`, `function`, `class` 등)를 사용해서 선언하는 모든 식별자가 소스코드(작성한 코드)의 선두로 끌어 올려진 것처럼 동작하는 JS 언어의 고유 특징을 의미힌다. 추후에도 매우 중요한 개념이나 현재는 간단히 이해만 하고 넘어가자

JS 소스코드는 인터프리터(Interpreter)에 의해 한 줄씩 순차적으로 실행되는 [인터프리터 언어]()다

```javascript
// 콘솔에 2, 4, ReferenceError가 순차적으로 반환된다
console.log(1 + 1); // → 2
console.log(2 + 2); // → 4
console.log(userName); // → Uncaught ReferenceError: userName is not defined
```

아래 예제를 살펴보자. 앞서 JS 소스코드는 순차적으로 실행된다 했다. 변수 `userName`를 참조하는 `console.log(userName);` 참조문이 변수 선언문보다 먼저 위치해 있다. 그렇다면 변수가 선언되어 JS 엔진에 존재를 알리기 전에 변수 `userName`을 참조하고자 했으니 `Uncaught ReferenceError: userName is not difined`가 나오게 될까?

```javascript
console.log(userName); // → ?
var userName; // → undefined (변수에 어떠한 값도 할당하지 않고 선언만 했다)
```

정답은 변수 `userName`이 정상적으로 참조되어 `undefined`가 반환된다. 변수 선언문 `var userName`이 먼저 실행되고 난 뒤 변수 `userName`의 참조문인 `console.log(userName);`이 실행되기 때문이다. JS 엔진은 식별자 선언이 소스코드의 어디에 위치해 있든 상관 없이 다른 코드보다 먼저 실행한다

즉, 소스코드가 한 줄씩 순차적으로 실행되는 시점인 런타임(Runtime)에 앞서 JS 엔진은 소스코드의 평가 과정을 거치면서 식별자 선언을 찾고 먼저 실행하기 때문에, 식별자 선언이 소스코드 내 어디에 있어도 선언된 식별자를 참조할 수 있게 되는 것이다

```javascript
console.log(hoisting); // → undefined
1 + 1;
2 + 2;
3 + 3;

("Jace");
var hoisting;
```

그러나 주의해야 할 점이 있다. 각각의 식별자 키워드(`var`, `let`, `const`, `function`, `class` 등)마다 호이스팅되는 방식이 다소 다르다. 식별자 키워드별 호이스팅 시점에 대해서는 [스코프]()를 참고하자.

<br>

## 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)