<img src="https://ifh.cc/g/DZWNlw.png" style="max-width: 100%" align="center">

### 목차

- [1 객체 리터럴 외의 객체 생성 방식](#1-객체-리터럴-외의-객체-생성-방식) 

- [2 생성자 함수에 의한 객체 생성](#2-생성자-함수에-의한-객체-생성)

  - [2-1 `Object` 생성자 함수](#2-1-Object-생성자-함수)

  
***

<br>

## 1 객체 리터럴 외의 객체 생성 방식

앞서 [객체 리터럴]()에서 언급했듯이, 객체 리터럴을 통해 객체를 가장 간단하게 생성할 수 있었다. 그러나 JS는 프로토타입 기반의 객체지향 언어인만큼 객체 리터럴 이외에도 객체를 생성할 수 있는 여러가지 방법을 지원한다:
- 객체 리터럴
- `Object` 생성자 함수
- 생성자 함수 
- `Object.creat` 메서드 
- 클래스 

자세히 살펴보면 객체 리터럴 외의 나머지 객체 생성 방식은 대대분 함수를 사용해 객체를 생성하는 것이다. 따라서 [함수](), [생성자 함수]()에 대한 개념을 먼저 학습한 후 아래 '생성자 함수에 의한 객체 생성'에 대해 살펴보자

<br>


## 2 생성자 함수에 의한 객체 생성
앞서 언급했듯이, 객체 리터럴은 객체를 가장 쉽게 만들 수 있는 객체 생성 방식 중 하나다. 그러나 복수의 유사 객체를 생성할 때 객체 리터럴보다 생성자 함수를 사용하는 것이 더 편리한 경우가 있다. 먼저 생성자 함수를 사용하여 객체를 생성하는 방식을 살펴본 후 객체 리터럴을 사용해서 객체를 생성하는 방식의 차이와 장단점에 대해 다뤄볼 예정이다

### 2-1 Object 생성자 함수

<br>

***

### 참고

- [모던 자바스크립트 Deep Dive](http://www.yes24.com/Product/Goods/92742567)