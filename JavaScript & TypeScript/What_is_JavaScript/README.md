중, 고등학교 때 컴퓨터를 제대로 배워본 적이 없이 컴퓨터 공학과에 들어온 학생들의 대다수는

코딩을 제대로 할 줄 모르는 게 현실입니다. 저도 그렇구요.

그래서 접하기 가장 쉬우면서 실습해보기도 쉬운 **JavaScript** 에 대해 다뤄보려고 합니다.

주의. Java와 JavaScript는 Oracle에서 등록한 상표이지만, 문법 체계와 사용 방법은 전혀 다릅니다.

<br></br>

### JavaScript 의 개념

---

> 개념적인 부분이기 때문에 참고 정도로만 읽어보아도 좋습니다.

<img src="./es6-icon.jpg" width="133" >

JavaScript(이하 JS) 는 **가벼운 인터프리터 언어**이며, **일급 함수**를 지원합니다.

여기서 일급 함수란 함수를 변수와 동일하게 다루는 언어의 특성을 일컫습니다.

일급 함수에 대한 특징은 다음에 구체적으로 다뤄보겠습니다.

```
const foo = function() {
	console.log('Hello World!');
}

// 변수를 이용해 호출
foo();

// 결과값 : Hello World!
```

웹 페이지의 스크립트 언어로서 제일 유명하지만 **비 브라우저 환경**에서도 사용하고 있습니다.

> Node.js, Aache CouchDB, Adobe Acrobat 등...

또한 프로토타입 기반, 다중 패러다임 스크립터 언어이며, 동적이고 명령어, 객체 지향, 함수 프로그래밍 스타일을 지원합니다.

중요한 건 JS라는 언어로 많은 것들을 할 수 있다는 점입니다.

JavaScript는 ES5부터 지금까지 바뀌면서 많은 변화가 생겼습니다.

그에 대한 변화도 추후에 따로 정리하면서 알아보도록 하겠습니다.

참고: [https://developer.mozilla.org/ko/docs/Web/JavaScript](https://developer.mozilla.org/ko/docs/Web/JavaScript)

<br></br>

### JavaScript 의 동작원리

---

<img src="./chrome-v8-engine.jpeg" width="176" >

JavaScript는 인터프리터 언어입니다.

> 인터프리터는 **작성된 소스 코드를 바로 실행하는 컴퓨터 프로그램 또는 환경**

이 JavaScript로 짜여진 코드를 해석하고 실행하는 인터프리터가 바로   
**JavaScript Engine** 입니다.

그리고 JavaScript Engine 은 JIT Compile 유형의 인터프리터 입니다.

> Jist-In-Time compilation 은 프로그램을 실제 실행하는 시점에 기계어로 번역해주는 컴파일 기법

이러한 JavaScript Engine은 브라우저가 가지고 있으며, JavaScript 코드를 웹에 올릴 시,

해당 **브라우저의 엔진**(e.g. V8)이 **코드를 해석하고 실행**합니다.

그래서 ES6, ES7 이 발표되어도 IE 같은 브라우저에서는 *새로운 문법을 해석할 수 없는 엔진*이기 때문에 사용할 수 없습니다.

따라서 이런 문제를 해결하기 위해 **Babel**과 같은 transpiler를 이용하여 ES6로 작성된 코드를 ES5로 변환시킨 후 사용합니다.

이런 변환 과정을 거치면서 까지도 ES6, 그 이후의 문법들을 사용하는 이유는

**아름다운 코드를 만들기 위해서 입니다.**

아름다운 코드는 **짧고** **간결**하며 **직관적**이어야 합니다. 하지만 이런 목적을 가지고 만드는 코드들이 쉽게 나올리가 없습니다.

이 때, ES6 문법들을 활용한다면 훨씬 나은 코드로 만들어 줄 수 있습니다.

> 해당 문법들을 활용한 깔끔한 코드들은 이 후, ECMAScript 관련 포스팅에서 보여드리겠습니다.

<br></br>

### JavaScript 기본 문법

---

**변수 선언**

1.  var : 변수를 선언, 동시에 값을 초기화
2.  let : 블록 범위 지역 변수로 선언. 추가로 동시에 값을 초기화
3.  const : 블록 범위 읽기 전용 상수를 선언

```
var a;
console.log("a 값은 " + a);	// "a 값은 undefined"로 로그가 남음
```

> 값을 초기화 해주지만, 제대로 된 입력값이 없는 상태에서는 'undefined'를 출력  
> 개인적으로 var, let 보다는 const를 선호. 함수형 프로그래밍의 개념에 있어 constant는 필수

변수를 선언할 때의 특징은 선언 종류가 세 가지로만 존재한 다는 것입니다.

각 선언에 대한 분류는 변수의 자료형이 아닌 특징을 중심으로 나뉩니다.

<img src="./typescript-icon.jpeg" width="108" >

> 자료형이 없는 데 얘가 뭔지 어떻게 알지라는 의문이 든다면 이 후 TypeScript에 대한 게시글을  
> 보시면 될 것 같습니다.

**6가지 원시 데이터형**

1.  Boolean. true, false
2.  null. null 값을 나타내는 특별한 키워드
3.  undefined. 값이 저장되어 있지 않은 최상위 속성
4.  Number. 정수 또는 실수형 숫자
5.  String. 문자열
6.  Symbol. 인스턴스가 고유하고 불변인 데이터 형 (거의 사용하지 않습니다.)

**Object**

객체와 함수는 언어의 다른 기본 요소

- 객체: 값을 위한 컨테이너
- 함수: 어플리케이션이 수행할 수 있는 절차

---

여기까지 JavaScript에 대한 기본 정보에 대해 다루어 보았습니다.

언어 자체가 어렵다기 보다는 새로운 데이터 형, 변수 선언 형, 그리고 함수를 운용하는 방식일 것입니다.

기본적으로 언어에 대해 구사하기 위해서는 당연히 기초를 다지는 과정이 필요합니다.

이 포스팅에서는 언어를 어떻게 다루는 지에 대한 방법보다는 간단하게 개념을 다지고 시작하는 곳이 되었으면 좋겟습니다.

언어를 배울 때, 개인적으로 추천하는 사이트로는 프로그래머스에서 알려주는 자바스크립트 입문 과정입니다.

[https://programmers.co.kr/learn/courses/3](https://programmers.co.kr/learn/courses/3)

이 후에는, JavaScript에서 ES5부터 다루며, 여러 가지 함수들에 대해 배워보고,

이를 효율적으로 사용하는 방법은 어떤 게 있을 지 알아보도록 하겠습니다.