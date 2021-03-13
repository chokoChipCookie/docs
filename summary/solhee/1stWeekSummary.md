# 1stWeekSummary by 토리

### 📝 ES6의 주요 문법에 대해서 알아보자
<br />
<br />

# let & const

> ## let

```` JS
let a = 10;
let a = 20; // 오류
````
### ☞ let 예약어는 한번 선언하면 재선언이 불가합니다.
<br />

>## const

```` JS
const b = 10;
b = 20; // 오류
````
### ☞ const 예약어는 할당한 값의 변경이 불가합니다.

<br />
<br />

# 화살표 함수 (Arrow Function) 

> ## 기존의 함수 선언 방식
<br />

### 1. 함수 선언문

```` JS
func();

function func() {
    console.log("Hello World!");
}
````

### 2. 함수 표현식

```` JS
func(); // 오류

var func = function() {
    console.log("Hello World!");
};

func(); // 정상적으로 실행
````
#### ☞ 익명함수를 함수 변수 func을 통해 호출할 수 있습니다. 
#### ☞ 호이스팅(함수가 정의되기 전에 호출)이 불가능합니다.
#### ☞ 클로저 및 콜백으로 유용하게 사용됩니다.
<br />

### 클로저
```` JS
const outer = function(x) {
    let y = 2;

    return function(z){
        y = 100;
        return x + y + z;
    };
}

const excuteInner = outer(1); // 클로저에 x,y값이 저장됨
console.log(excuteInner(3)); // 1+100+3 = 104
````
#### ☞ 외부함수의 실행이 끝난 이후에도 내부함수가 외부함수의 context에 접근이 가능합니다.
<br />

>## 새로운 함수 정의 방식
```` JS
var func = () => {
    console.log("Hello World!");
};

func();
````
<br />

### 간소화 된 문법
```` JS
const func = (x, y) => {return x*y};
console.log(func(10,20));

const func_1 = x => {return x*10};
console.log(func_1(10));
````
#### ☞ parameter를 한 개만 받을 경우 소괄호를 생략할 수 있습니다.
<br/>