# 자바스크립트

## 호이스팅과 TDZ는 무엇일까?

### 스코프
- 변수가 선언되는 범위에 따라서 참조할 수 있는 구역이 나누어지는 것
- 예) 전역 스코프(전역 변수)는 어디서든 참조 가능, 지역 스코프(지역 변수)는 함수 자신과 하위 함수에서 참조 가능
```(javascript)
// test1은 아래 function안에서도 참조 가능
const test1 = '전역 변수';
function temp() {
  //test2는 function 바깥쪽에서는 참조 불가능
  let test2 = '지역 변수';
  };
```

### 호이스팅(hoisting)
- 함수의 코드를 실행하기 전에 변수와 함수의 메모리 공간을 선언 전에 미리 할당하여 변수의 선언을 최상단으로 끌어올리는 것
- 예) 함수가 선언되기 전에 호출하는 코드를 먼저 배치하지만, 정상적으로 실행되는 것을 볼 수 있다.
```(javascript)
name1('상진'); // '제 이름은 상진입니다.'
function name1(name2) {
  console.log('제 이름은 '+ name2 +'입니다.');
  }
```
- 이는 변수 선언 형식에 따라 달라진다.
- var : 호이스팅 시 undefined로 변수를 초기화
- function : 선언된 위치와 상관없이 동일하게 호출됨
- let, const : 호이스팅 시 변수를 초기화하지 않음. (호이스팅 대상은 맞음)
- 예)
```(javascript)
console.log(test1); // 호이스팅한 var 선언으로 인해 undefined 출력
var test1; // 선언
test1 = 'test1' // 초기화

console.log(test2); // ReferenceError : test2 is not defined
let test2 = 'test2'

name1('상진'); // '제 이름은 상진입니다.'
function name1(name2) {
  console.log('제 이름은 '+ name2 +'입니다.');
  }
```

### TDZ(Temporal Dead Zone, 일시적 사각지대)
- 변수 선언 전에 변수를 사용하는 것을 허용하지 않는 개념상의 공간
- 영향을 받는 구문 : const, let, class
- 예)
```(javascript)
name; // TDZ의 영향으로 ReferenceError
// -- 개념상의 TDZ 공간 --
const name = '상진'; // 선언
name; // => '상진'
```
- var는 의도하지 않은 중복선언과 재할당으로 문제가 생길 수 있기 때문에 사용하지 않는 편이 좋음

### const, let, var, function
- var : 중복 선언이 가능하다. 하지만 가장 마지막에 선언된 변수만 저장된다. 변수의 중복선언이 가능하기 때문에 위험하다.
- let : 중복 선언이 불가능하다.(에러 발생) 하지만 값을 재할당 하는 것은 가능하다.(재할당시 let은 생략)
- const : 중복선언이 불가능하며, 값을 재할당 하는 것도 불가능하다. 

### 실행 컨텍스트와 콜 스택
- 실행 컨텍스트(Execution Context)는 자바스크립트의 핵심 개념으로, 코드를 실행하기 위해 필요한 환경이다.
- 더 자세히 말하자면, 실행할 코드에 제공할 환경 정보들을 모아놓은 객체이다.
```(javascript)
// 함수 호출 예제. 순서대로 흘러간다.
// (1)

const a = "hello world!";

const bar = () => { // (5)
    console.log(a)
}; // (6)

const foo = ()=>{ // (3)
	bar() // (4)
}; // (7)

foo(); // (2)

// (8)
```
![images_wonseok2877_post_a6b94e61-7482-408e-976d-43beff496b40_image](https://user-images.githubusercontent.com/85321327/179883152-84208f39-7b41-418a-8b48-2cc2156a6b58.png)
(1) Global Execution Context 생성.

자바스크립트 파일이 열리는 순간(별도의 명령 없이) 전역 실행 컨텍스트가 생성된다. 그리고 global execution context가 가장 먼저 callstack에 push된다. 지금 callstack의 맨 위에는 global execution이 있으므로 자바스크립트 엔진은 이제 전역 실행 컨텍스트 상에서 코드를 읽어내려가기 시작한다.

(2) foo함수 호출.

foo함수를 호출할 때, Global Execution Context는 멈춘다. 왜냐하면 자바스크립트는 싱글 스레드 환경이기 때문에, 한 번에 하나의 코드만을 실행할 수 있기 때문이다.

(3) 자바스크립트 엔진은 foo함수에 대한 환경 정보를 수집해서 foo execution context를 생성한 후, callstack에 push한다. 이제 함수 내부의 코드들이 순서대로 진행된다.

(4) bar함수 호출. foo함수의 Execution Context는 멈춘다.

(5) bar함수의 Execution Context가 생성되고 callstack에 push된다. 읽어내려간다. console.log함수를 실행한다. 전역 변수인 a의 값이 콘솔창에 뜸으로써 console.log함수의 실행이 끝난다.

(6) 더 읽어내려갈 게 없으므로 bar함수의 Execution Context가 종료된다. callstack에서 pop-out된다. 그리고 해당 함수 바로 밑의 Execution Context, 여기에선 foo함수의 Execution Context가 계속된다.

(7) 더 읽어내려갈 게 없으므로 foo함수의 Execution Context가 끝난다.

(8) 더 읽어내려갈 게 없으므로 Global Execution Context가 끝난다.

### 콜 스택
- call은 호출, stack은 출입구가 하나뿐인 깊은 우물 같은 데이터 구조를 의미한다.
- 따라서 callstack은 자바스크립트가 함수 호출을 기록하기 위해 사용하는 우물 형태의 데이터 구조이다.
- 항상 맨 위에 놓인 함수를 우선으로 실행된다. 이런 식으로 자바스크립트 엔진은 가장 위에 쌓여있는 context와 관련 있는 코드들을 실행하는 식으로 전체 코드의 환경과 순서를 보장한다.

### 스코프 체인(Scope Chain), 변수 은닉화
- 스코프를 안에서부터 바깥으로 차례로 검색해 나가는 것
- 여러 스코프에서 동일한 식별자를 선언한 경우에는 무조건 스코프 체인 상에서 가장 먼저 발견된 식별자에만 접근 가능하게 된다.
- 스코프 체인 내부에서 선언된 변수와 전역변수를 동일한 이름으로 선언해도 서로 접근할 수 없는 경우를 변수 은닉화라고 한다.
```(javascript)
var a = 1;
var outer = function() {
  var inner = function() {
    console.log(a); //undefined
    var a = 3;
    } 
    inner();
    console.log(a); // 1
  };
outer();
console.log(a); // 1
```
