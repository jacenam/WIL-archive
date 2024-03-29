# 참조에 의한 전달과 함수 외부 상태의 변경

**Table of Contents**

- [함수에서 원시 값의 전달](#함수에서-원시-값의-전달)
- [함수에서 객체 값의 전달](#함수에서-객체-값의-전달)
- [순수 함수와 함수형 프로그래밍의 개념](#순수-함수와-함수형-프로그래밍의-개념)

<br>

## 함수에서 원시 값의 전달 

앞서 원시 값이 할당된 변수를 다른 변수에 할당하면 원본의 원시 값이 복사되어 복사본에 전달된다고 했으며, 이를 ‘[값의 의한 전달’(Pass by Value)]()이라 했다. 그리고 원본과 복사본 모두 각각의 메모리 공간에 원시 값을 저장하기 때문에, 복사본에 새로운 원시 값을 재할당해도 원본의 원시 값이 동일하게 변경되지 않는다

```javascript
// 원시 값의 할당 및 전달
var original = 100; 
var copy = original; 

console.log(original, copy); // → 100 100

// 복사본 원시 값의 재할당 및 전달
var original = 100; 
var copy = original; 

copy = 200; 

console.log(original, copy); // → 100 200
```

함수에서는 어떻게 동작할까? 매개변수 `copy`에 원본 변수 `original`을 할당해보았다. 그리고 매개변수 `copy`의 원시 값을 `200`으로 재할당했다. 그러나 원본 변수 `original`의 값은 변하지 않는다

```javascript
var original = 100; 

function passValue(copy) {
  copy = 200; 
}

passValue(original); 

console.log(original); // → 100
```

함수는 객체 타입이기 때문에 객체 타입의 저장 및 전달 방식을 따라야 한다고 생각할 수 있다. 그러나 위에 언급했듯이, 매개변수는 함수 내부에서만큼은 일반 변수와 동일하게 취급되기 때문에 매개변수에 인수를 통해 원시 값을 할당(전달)하게 되면 원시 값의 방식에 의해 값을 저장 및 전달하게 된다. 따라서 외부에 있는 원시 값 원본은 함수 내부의 변경에 의해 변경되지 않는다

<img width="100%" src="https://user-images.githubusercontent.com/92138751/207498469-8244b17a-2884-474e-ac39-3b458558f575.png">

<br>

## 함수에서 객체 값의 전달

객체 값이 할당된 변수를 다른 변수에 할당하면 원본의 객체 값이 저장된 메모리를 가리키는 참조 값이 복사되어 복사본에 공유된다 했으며, 이를 [참조에 의한 전달(Pass by Reference)]()이라 했다. 따라서 원본 혹은 복사본 둘 중 하나의 객체 값을 변경했을 때 다른 한쪽의 객체 값도 변경된다 

```javascript
var original = { name: "Jace", age: 30 }; 
var copy = original; 

console.log(original === copy); // → true

// 마침표 프로퍼티 접근 연산자를 통한 프로퍼티의 변경
original.name = "Ju Hyung"; // 이미 존재하는 프로퍼티의 값 갱신 
copy.residence = "Seoul"; // 새로운 프로퍼티의 동적 생성

console.log(original === copy); // → true
```

함수에서도 매개변수에 객체 값이 할당되면 함수 외부와 동일하게 참조에 의한 전달 방식을 통해 값을 전달한다. 따라서, 함수 내부 매개변수 `copy`의 객체 값을 변경했을 때 함수 외부 변수 `original`의 객체 값 또한 변경된다

```javascript
var original = { name: "Jace", age: 30 }; 
var copy = original; 

function referValue(copy) {
  copy.name = "Ju Hyung"; 
  copy.residence = "Seoul"; 
}

referValue(original);

console.log(original); // → ▸ {name: "Ju Hyung", age: 30, residence = "Seoul"}
```

즉, 원본의 객체 값을 가진 인수(복사본)는 참조 값이 원본의 변수와 공유되기 때문에 함수 내부에서 일어난 객체 값이 변경은 외부의 객체 값 원본에도 영향을 끼친다

<img width="100%" src="https://user-images.githubusercontent.com/92138751/207499422-d102f1bc-8aea-4259-9573-fa145c5e79b2.png">

여기서 주의해야 할 부분이 있다. [객체 값의 전달]() 파트에도 기술한 내용인데, 함수 내부에서 객체 값을 변경할 때도 [프로퍼티 접근 연산자(`.` 혹은 `[ ]`]()를 사용해서 객체 값을 변경해야 한다. 그렇지 않으면 변수 `original`의 객체 값이 변경되지 않는다. 아래 예제를 살펴보자. 마지막 줄 `console.log(original === copy)`의 결과는 어떻게 반환될까? 

```javascript 
var original = {name: "Jace", age: 30}; 

function referValue(copy) {
  copy = {name: "Jace", age: 30};  
}

referValue(original);

console.log(original); // ???
console.log(copy); // ???
console.log(original === copy) // ??? 
```

정답은 `false`다. 위 예제 코드를 풀어서 기술하자면 아래와 같다: 

```javascript
referValue(original) => copy = original => copy = {name: "Jace", age: 30} 
```

함수 `referValue`의 호출을 통해 매개변수 `copy`에 변수 `original`을 전달해서 변수 `original`과 매개변수 `copy`는 동일한 참조 값을 공유하게 된다. 그러나 매개변수 `copy`에 새로운(전혀 다른) 객체를 할당함으로서 변수 `original`과 더 이상 같은 참조 값을 공유하지 않게 되므로 `original === copy`의 평가 결과는 `false`다

<br>

## 순수 함수와 함수형 프로그래밍의 개념

객체 값은 이처럼 함수 내외부의 변경사항에 따라서 변수와 매개변수 등 객체 값의 상태 변화를 추적하는 것이 어려워진다. 이는 객체 값이 참조 값에 의해 저장되고 전달되는 방식으로 인해 생기는 부작용이라고 할 수 있다. 한 두가지의 변수 혹은 매개변수가 아니라, 여러 변수 혹은 매개변수가 참조 값을 공유하고 있다면 하나의 변경이 전체적인 버그로 번질 수 있다는 의미다

```javascript
var original = {name: "Jace", age: 30}; 

function referValue(copy) {
  copy.name = "Ju Hyung"; 
  copy.residence = "Seoul"; 
  console.log(copy); 
}

referValue(original); 

original = {msg: "Have been changed. Is it Easy to track?"}; 

console.log(original); // → ▸ {msg: "Have been changed. Is it Easy to track?"}; 
```

객체의 변경을 추적하려면 옵저버 패턴(Observer Pattern) 등을 통해 객체의 참조 값을 공유하는 모든 이들의 변경 사항을 인지하고 대처할 수도 있다. 문제의 해결 방법으로 객체를 불변 객체(Immutable Object)로 사용할 수도 있다. 이러한 외부 상태 변경에 영향을 받지도 않고, 외부 상태에 의존하지도 않는 함수를 순수 함수라고 부른다. 순수 함수를 통해 부작용을 최대한 억제해서 오류를 피하고 프로그램의 안정성을 높이는 프로그래밍 패러다임을 함수형 프로그래밍이라 부른다. 이에 대해서는 [순수 함수와 비순수 함수]()를 참고하자

<br>

## 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)

