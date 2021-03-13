## ES Analysis ( 6 ~ 8)

### ES6
---
#### arrows (화살표 함수)
: function 키워드 대신 화살표(=>)를 사용하여 보다 간략한 방법으로 함수를 선언할 수 있다.
~~~~
// ES5
var pow = function (x) { return x * x; };
console.log(pow(10)); // 100
~~~~
~~~~
// ES6
const pow = x => x * x;
console.log(pow(10)); // 100
~~~~


: 콜백 함수로 사용
~~~~
// ES5
var arr = [1, 2, 3];
var pow = arr.map(function (x) { // x는 요소값
  return x * x;
});

console.log(pow); // [ 1, 4, 9 ]
~~~~
~~~~
// ES6
const arr = [1, 2, 3];
const pow = arr.map(x => x * x);

console.log(pow); // [ 1, 4, 9 ]
~~~~


#### classes (클래스)
: 혼잡했던 생성자와 상속 코드가 깔끔해짐.  
: 이전에 function Object() {}로 만들던 생성자 객체를 이제 class로 만들 수 있다.   
: 복잡했던 상속을 extends로 간단하게 처리할 수 있다. super로 부모 호출  
~~~~
class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
~~~~

#### enhanced object literals (object 메소드 선언 및 속성(동적) 선언)
: 기존 자바스크립트에서 사용하던 객체 정의 방식을 개선한 문법  
: 자주 사용하던 문법들을 좀 더 간결하게 사용할 수 있도록 객체 정의 형식을 수정  
- 함수
: 익명함수명 생략
~~~~
// es5 : 프로퍼티 : 익명함수명() { 함수바디 }
var obj = {
	property1 : 100,
    function1 : function() {
    	console.log('call function1');
    }
};
obj.property1; //100
obj.function1(); //call function1
~~~~
~~~~
// es6 : 프로퍼티명() { 함수바디 }
var obj = {
    function1() {
    	console.log('call function1');
    }
};
obj.function1(); //call function1
~~~~


- 변수
: 속성명과 함수명이 일치한다면 생략
~~~~
// es5
var property1 = 100;
var obj = {
	property1 : property1,
};
property1; 		//100
obj.property1; 	//100
~~~~
~~~~
// es6
var property1 = 100;
var obj = {
	property1
};
property1; 		//100
obj.property1; 	//100
~~~~

#### template strings (템플릿 문자열)


#### destructuring (구조분해할당)


#### default + rest + spread (default 파라미터, rest 파라미터, 전개연산자)


#### let + const (let, const block level 스코프 변수선언)


#### iterators + for..of


#### generators


#### unicode


#### modules


#### module loaders


#### map + set + weakmap + weakset


#### proxies


#### symbols


#### subclassable built-ins


#### promises (비동기 프로그래밍)


#### math + number + string + array + object APIs


#### binary and octal literals


#### reflect api


#### tail calls (꼬리 물기 최적화)






### ES7
---
#### Array.prototype.includes()
#### 지수 연산자(**) 




### ES8
---
#### Async Functions (async ~ await)
#### Shared memory and atomics 
: (공유된 메모리와 원자 / SharedArrayBuffer 객체와 Atomics 객체를 사용한 메모리 공유)




## VueJS LifeCycle
