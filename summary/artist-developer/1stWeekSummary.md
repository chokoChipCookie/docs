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

#### destructuring (구조분해할당)
: 좌변은 값을 넣을 변수, 우변에는 값이 되는 변수
~~~~
var a, b, rest;
[a, b] = [1, 2];
console.log(a); // 1
console.log(b); // 2 

[a, b, ...rest] = [1, 2, 3, 4, 5];
console.log(a); // 1
console.log(b); // 2
console.log(rest); // [3, 4, 5]
~~~~
~~~~
var a, b;
[a, b] = [1, 2];
console.log(a); // 1
console.log(b); // 2
~~~~

#### default + rest + spread
- default
: 기본값
~~~~
function inc(number, increment=1) {
  return number + increment;
}
console.log(inc(2, 2)); // 4
console.log(inc(2));    // 3
~~~~

- rest
: ... 연산자
~~~~
function sort(...numbers){
    return numbers.sort(function(a,b){return a-b;});
}
 
console.log(sort(10,2,6,4));           //[ 2, 4, 6, 10 ]
console.log(sort(9,8,7,100,20,15,17)); //[ 7, 8, 9, 15, 17, 20, 100 ]
~~~~

- spread
: 전개연산자
~~~~
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5]
var arr3 = [...arr1];

var arr2.push(...arr1);

console.log(arr3);    // [0, 1, 2]
console.log(arr4);    // [0, 1, 2, 3, 4, 5]
~~~~
: 내장함수 사용 없이 전개 연산자를 활용하여 배열 복사


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
: Array.prototype.includes()으로 배열의 value 확인
~~~~
// es6
let numbers = [1, 2, 3, 4];
if(numbers.indexOf(2) !== -1) { console.log('Array contains value');}
~~~~
~~~~
// es7
if(numbers.includes(2)) { console.log('Array contains value');}
~~~~

#### 지수 연산자(**)
: 거듭제곱. Math.pow()와 유사
~~~~
let base = 10;
let exponent = 3;
result = base**exponent; // 1000
~~~~


### ES8
---
#### Async Functions (async ~ await)
: 직관적이고 단순해 개발자가 익숙한 기존의 동기식 코드 형식으로 비동기식 처리 코드를 작성 가능
~~~~
function awaitFunction() {
  return new Promise((resolve, reject) => {
  setTimeout(() => resolve('success'), 1000);
  // setTimeout(() => reject('fail'), 1000);
  });
}

async function asyncFunction() {
  try {
    const msg = await awaitFunction();
    console.log(msg); // awaitFunction에서 resolve가 호출 될 때 resolve의 인자값 'success'
  } catch (e) {
    console.log(e); // awaitFunction에서 reject가 호출 될 때 reject의 인자값 'fail' 
  }
}

asyncFunction();
~~~~
: async 함수에서는 await를 사용 가능  
: await는 async 함수에서만 사용 가능  
: await는 Promise와 함께 사용되어야 한다.  
: Promise가 종료 될 때까지 함수 실행이 일시 정지 + Promise가 종료되면 함수 실행 다시 진행  

#### Shared memory and atomics 
: (공유된 메모리와 원자 / SharedArrayBuffer 객체와 Atomics 객체를 사용한 메모리 공유)  
  
- shared memory  
: 길이가 고정된(fixed-length) 바이너리 데이터 버퍼  
: 에이전트들 간의 데이터 공유  

- Atomics  
: SharedArrayBuffer와 함께 사용  
: 에이전트는 다른 에이전트의 데이터 쓰기 작업이 끝날 때까지 대기 큐에 포함되며 'sleep' 상태로 대기  
: Atomics.wait()로 깨어나는 조건 발생 시까지 대기, Atomics.load()로 특정 지점 값 read  

~~~~
// 1024바이트 크기의 버퍼 생성
var sab = new SharedArrayBuffer(1024);

// shared typedArray 객체 생성
var int32 = new Int32Array(sab);

// 읽기 스레드가 typedArray 객체의 인덱스 번호가 '0'인 위치의 값이 '0'인지 테스트한다. 'true'가 반환되면 'sleep' 상태에서 대기한다.
// 대기 타임아웃을 지정할 수 있다(기본값: Infinity).
Atomics.wait(int32, 0, 0);

// 쓰기 스레드가 새로운 값을 저장하면 깨어나 새로운 값을 반환한다.
console.log(int32[0]); // 123  
~~~~
  
    
## VueJS LifeCycle
: 참고 - https://kr.vuejs.org/v2/guide/instance.html#%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%EB%8B%A4%EC%9D%B4%EC%96%B4%EA%B7%B8%EB%9E%A8  
### create 
: 라이프 사이클들 중에 가장 먼저 실행  
: create 단계에서 실행되는 라이프 사이클 훅(hook)들은 컴포넌트가 DOM에 추가 되기 전이기 때문에, DOM에 접근하거나 this.$el을 사용할 수 없다.  


- beforeCreate  
: 가장 먼저 실행 되는 훅  
: 인스턴스가 초기화된 직후에 발생.  
: 데이터 관찰 및 이벤트, watcher 설정 전에 호출 - data, methods에 접근할 수 없다.  

- created  
: 인스턴스가 생성된 후 동기적 발생.  
: mounted가 시작되지 않았으므로 $el 속성을 사용하지 못한다.  


### Mounting (DOM Insertion)
: mounting 클래스를 사용하면 첫 번째 렌더링 전 / 후에 컴포넌트에 즉시 접근할 수 있다.  
: 초기 렌더링 직전 또는 직후, 구성 요소의 DOM에 접근하거나 수정해야할 때 사용한다.  


- beforeMount  
: mounting이 시작되기 전에 호출  
: 초기 렌더링이 발생하기 전 / 템플릿 또는 렌더함수가 컴파일 된 후에 실행  
: 가상 DOM이 생성되어있으나, 실제 DOM에는 mount 되지 않은 상태  

- mounted
: 인스턴스가 마운트된 후 el이 호출되며, 새로 작성된 인스턴스vm.$el로 대체된다.  
: 가상 DOM의 내용이 실제 DOM에 부착되고 난 이후에 실행되므로 data, computed, methods, watch등 모든 요소에 접근이 가능  
: 주의! 현재 컴포넌트가 mount 되었다고 해서 모든 하위 구성요소도 mount 된 것을 보장하지 않는다.  


### Updating
: 업데이트는 컴포넌트의 변화 또는 re-render되는 발생 원인에 대해 민감하게 반응하여 수행된다.  
: 주로 디버깅이나 프로파일링을 위해 컴포넌트들이 언제 다시 렌더링 될 지 알고 있을 때 사용.  


- beforeUpdate  
: DOM이 패치(patch)되기 전, 데이터가 변경될 때 호출  
: 업데이트 전에 기존 DOM에 엑세스 가능  

- updated  
: 데이터 변경 후 호출되어 가상 DOM이 다시 렌더링 되고 patch될 때 호출  
: 구성요소의 DOM이 업데이트 되므로 이 때 DOM에 종속된 동작을 수행할 수 있다.  
: updated 또한 mounted처럼 모든 하위 구성요소의 렌더링을 보장하지 않는다.  


### Destruction (Teardown)  
: destruction은 cleanup 또는 analytics sending과 같이, 컴포넌트가 파괴될 때 수행  
: 컴포넌트가 해체되어 DOM에서 제거되면 실행


- beforeDestroy  
: 인스턴스가 삭제되기 전에 호출  
: 인스턴스는 여전히 작동한다.  

- destroyed  
: 스턴스가 제거된 후에 호출  




