
## 1. 느슨한 타입(loosely typed)의 동적(dynamic) 언어

:  자바스크립트의 변수는 어떤 특정 타입과 연결되지 않으며 모든 타입의 값으로 할당(및 재할당 가능하다
  느슨한 타입의 동적 언어이기 때문에 변수생성시 원시 변수의 타입을 미리 선언하지 않아도 된다는 장점이 있음

 --------------------------
 
 

## 2. JavaScript 형변환

자바스크립트의 형변환은 두가지 입니다

 
```
1. 암시적 변환 : 자바스크립트 엔진이 필요에 따라 자동으로 데이터타입을 변환시키는것

➾산술 연산자 : 더하기(+) 연산자는 숫자보다 문자열이 우선시 되기 때문에, 숫자형이 문자형을 만나면 문자형으로 변환되어 연산

➾다른 연산자(-,*,/,%) : 숫자형이 문자형보다 우선시되기 때문에 더하기와 같은 문자형으로의 변환이 일어나지 않는다 

➾ 동치비교 : 엄격하지 않은 동치 ‘==‘ 비교 ( ‘===‘비교와 혼동되지 않도록 해아함 )

```

```

2. 명시적 전환 : 개발자가 의도를 가지고 데이터 타입을 변환시키는것

✔다른 자료형 -> Number Type으로 변환하는 방법

   Number() , parseInt(),  paprseFloat()

 

➾parseInt()

parseInt()는 정수형의 숫자로 변환한다. 만약 문자열이 ’숫자 0’으로 시작하면 8진수로 인식하고(구형브라우저 O, 신형브라우저X),

 ‘0x, 0X’로 시작한다면 해당 문자열을 16진수 숫자로 인식한다. 또한 앞부분 빈 공백을 두고 나오는 문자는 모두 무시되어 NaN을 반환한다.

 

➾paprseFloat()

parseFloat()는 부동 소수점의 숫자로 변환한다. parseInt()와는 달리 parseFloat()는 항상 10진수를 사용하며 parseFloat() 또한 앞부분 빈 공백을 두고 나오는 문자는 모두 무시되어 NaN을 반환한다.

 

✔다른 자료형-> String Typed으로 변환하는 방법

String(), toString(), toFixed()

 

➾toString()

toString()는 인자로 기수를 선택할 수 있다. 인자를 전달하지 않으면 10진수로 변환한다.

 

➾toFixed()

toFixed()의 인자를 넣으면 인자값만큼 반올림하여 소수점을 표현하며 소수점을 넘치는 값이 인자로 들어오면 ()안의 숫자길이를 맞춘 문자열을 반환한다.

 

✔다른자료형 -> Boolean Type

➾Boolean()
```
 ------------------------------------------



## 3. ==, ===

 ‘==‘ 와 ‘===‘ 연산자의 주된 차이점은 ‘==‘는 연산자를 이용하여 서로 다른 유형의 두 변수값이 비교가 가능하지만 

’ ===‘는 a === b 라고 할때, 값과 값의 종류(Data Type)가 모두 같은지를 비교해서, 같으면 true, 다르면 false로 표시 

 

숫자와 불리언 비교 

 ✔ 0값은 false와 동일하므로 -> true 출력

0 == false // true 

 

 ✔ 두 피연산자의 유형이 다르기 때문에 ->false

```
0 === false // expected output: false 

console.log(typeof 0); // expected output: “number”

console.log(typeof false); // expected output: “boolean”
```

 
-------------------------------------
 

## 4. 느슨한 타입(loosely typed)의 동적(dynamic) 언어의 문제점은 무엇이고 보완할 수 있는 방법에는 무엇이 있을지 생각해보세요.

 

➾ 문제점 : 변수 생성시 원시 변수의 타입을 미리 선언하지 않아도 된다는 장점으로 인해 타입이 올바른지 체크하는것이 굉장히 까다롭기 때문에 배포 시 예상치 못한 문제와 직면 할수 있다

 

✔ 타입 스크립트란? 타입 스크립트는 자바스크립트에 타입을 부여한 정적 타입 언어 

만약 타입 스크립트를 브라우저에서 실행하려면 파일을 변환하는 트랜스 파일 과정을 거쳐서 사용함 (공식적으로는 트랜스 파일이 아닌    컴파일된다고 표현)

컴파일의 경우 한 언어로 작성된 소스 코드를 다른 언어로 변환하는 것을 뜻하는 반면, 

트랜스 파일의 경우 한 언어로 작성된 소스 코드를 비슷한 수준의 다른 언어로 변환한다는 차이가 있음

예를 들어 Java를 컴파일하면 bytecode 코드가 출력되지만, C++를 트랜스 파일 하면 C가 출력되며 Typescript를 트랜스 파일 하면 Javascript가 출력됨 ( 하지만 공식적으로 컴파일된다고 표현하기 때문에 컴파일이란 용어를 사용하겠습니다 )

이런 정적 타입 언어는 런타임 이전에 타입이 올바른지에 대한 검사를 시행하며, 동적 타입 언어는 런타임에 프로그램의 타입이 올바른지에 대한 검사를 실행하고  만약 래퍼런스 오류를 유발하는 코드가 존재한다면 정적 언어는 컴파일하는 과정에서 오류를 출력하는 반면 동적 언어는 해당 구문이 실행되는 시점에서 오류를 출력하게 됨

 

➾ 보완방법 : 이 부분을 보완하려면 정적 타입 체크와 강력한 문법을 추가한 타입스크립트를 사용하여 보완하면 가능 하다
( 타입 스크립트는 동적언어 타입으로 구분되며 타입 스크립트는 자바스크립트에 타입을 부여한 정적 타입 언어입니다 )

 -----------------------------
 

## 5.undefined와 null의 미세한 차이들을 비교해보세요.

 

➾ undefined : var 키워드로 선언한 변수는 암묵적으로  undefined로 초기화가 됨 

변수선언에 의해 확보된 메모리 공간을 처음 할당이 이뤄질 때까지 빈 상태로 내버려두지 않고 자바스크립트 엔진이  undefined로 초기화 됨. 즉, 변수를 선언한 이후 값을 할당하지 않은 변수를 참고하면  undefined가 반환 되게 됨.

자바스크립트 엔진이 변수를 초기화하는 데 사용하는 undefined를 개발자가 의도적으로 변수에 할당한다면 ndefined의 본래 취지와 어긋날뿐더러 혼란을 줄수 있이므로 권장하지 않는다. 값이 없다는걸 명시하고 싶을땐  undefined가 아닌 null을 할당해야 함.



➾ null: null은 값이 없다는걸 의도적으로 명시할 때 사용. 변수에 null을 할당하는것은 변수가 이전에 참조하던 값을 더 이상 참조하지 않겠다는 의미. 즉 이는 이전에 할당되어 있던 값에 대한 참조를 명시적으로 제거 하는것을 의미.

