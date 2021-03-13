# 첫번째 주 내용 정리

## 1. ES6 ~ ES8 핵심 파악

- 🤝 `Promise`

  - Javascript의 `Callback Hell`로부터 코더를 구원할 새로운 **비동기 객체**
  - `Pending` (대기), `Fullfilled` (이행/완료), `Rejected` (실패) 총 3가지 상태를 갖고 있다.
    - `Pending`, `Promise` 객체를 생성하여 호출하면 대기 상태가 된다. 대기 상태는 곧 요청을 한 상태이고 완료되거나 실패했을 경우 다시 대기 상태로 돌아오게 된다.
    - `Fullfilled`, 요청에서 `Promise.resolve`를 호출하여 요청을 이행한 상태가 된다. `then`을 사용하여 요청에 대한 결과를 받을 수 있다.
    - `Rejected`, 요청에서 `Promise.reject`가 호출하여 요청을 실패한 상태가 된다. `catch`를 사용하여 요청에 대한 실패 결과를 받을 수 있다.
    ```js
    // 회원 정보를 조회하는 비동기 함수
    const getUserInfo('bolam')
      .then((response) => console.log(response))
      .catch((error) => console.error(error));
    ```
    > `then`, `catch`의 후속 처리 메소드를 연속으로 체이닝(`chaining`)하여 여러 개의`Promise`를 연결하여 사용할 수 있다.

- 🏹 `Arrow function`

  - 기존의 함수 선언(`fuction foo()`) 대신에 화살표(`=>`)를 사용하여 간략하게 표현할 수 있도록 해주는 화살표 함수.
  - 화살표 함수는 익명 함수로만 사용할 수 있고 이를 호출하기 위해서는 함수 표현식을 사용한다.

    ```js
    const getUserInfo = (userId) => {
      /** 대충 아이디로 회원 조회하는 함수 */
    };

    console.log(getUserInfo('bolam'));
    ```

  - 자바스크립트의 경우 호출 방식에 의해 `this`에 바인딩할 객체가 동적으로 결정된다. 그러나 화살표 함수는 함수를 선언할 때 `this`에 바인딩할 객체가 정적으로 결정된다. 이때 결정되는 바인딩 객체는 화살표 함수의 상위 스코프의 `this`를 가리킨다.

  - 기존에 작성되던 함수 작성 방법보다 간결하고 가독성이 뛰어나 많이 채택되어 사용되고 있다. 그러나 일부 상황(메소드 정의, `prototype`, 생성자 함수 등)에서는 일반 함수 작성 방법을 채택하여야 한다.

- 📃 `Template Literal`

  - 기존에 사용하던 `'`, `"` 대신 백틱(`)을 사용하여 문자열을 구현한다.
  - 문자열 내 변수를 작성하고 싶은 경우 `${foo}`로 작성할 수 있다.
  - 엔터(줄바꿈)가 그대로 적용되기 때문에 `\n`(줄바꿈)을 따로 적을 필요가 없다.

    ```js
    const username = 'bolam';
    const sentence = `Hello, ${username}.`;

    console.log(sentence); // Hello, bolam.
    ```

- 🎫 `const`, `let`

  - 기존 ES5까지는 변수 선언을 오직 `var`로만 할 수 있었다. 그러나 `var`의 경우 변수 `Hoisting`을 발생시키며 `Function scoped`의 전역 변수 이기 때문에 변수 선언을 중복으로 할 수 있으며 이로 인해 어느 부분에서든 접근할 수 있다.
  - 이를 방지하기 위해 ES6에서는 한 번 선언하면 재선언이 불가능한 `const`와 재선언이 가능한 `let`이 있다.

    ```js
    var name = 'foo';

    console.log(name); // foo

    var name = 'bar';

    console.log(name); // bar
    ```

    ```js
    const name = 'foo';

    console.log(name); // foo

    const name = 'bar';

    console.log(name); // Uncaught SyntaxError: Identifier 'name' has already been declared
    ```

- `rest`, `spread`

  1. `rest`

     - `rest` 파라미터는 구문이 정해지지 않은 수의 인수를 배열로 나타낼 수 있다.
     - 함수의 마지막 파라미터 앞에 `...`를 붙여 모든 나머지 인수를 배열로 대체한다.

       ```js
       function foo(...rest) {
         console.log(rest);
       }

       foo(1, 2, 3, 4, 5); // [1, 2, 3, 4, 5]
       ```

  2. `spread`

     - `spread` 연산자는 전개 연산자로써 배열 혹은 순회가 가능한 객체의 요소를 하나씩 분리하여 전개한다.
     - `ES5`에서는 `concat`을 사용했었으나 `spread` 연산자를 사용하여 대체할 수 있다.

       ```js
       const array1 = [1, 2, 3, 4, 5];
       const array2 = [6, 7, 8];

       console.log([...array1, ...array2]); // [1, 2, 3, 4, 5, 6, 7, 8]
       ```

- 구조 분해 할당(`Destructuring`)

  - 구조 분해 할당은 구문은 배열이나 객체의 속성은 해체하여 그 값을 변수에 담을 수 있게하는 표현식이다.

    ```js
    const userInfo = {
      name: 'bolam',
      age: '22',
    };

    const { name, age } = userInfo;

    console.log(`${name} is ${age} years old.`); // bolam is 22 years old.
    ```

- `async`, `await`

  - `ES8`에서 제공한다. 함수 앞에 `async`를 붙이게 되면 해당 함수는 항상 `Promise` 객체를 반환합니다. `Promise`가 아니더라도 이행 상태에서 `Proimse`로 값을 감싸면 이행된 `Promise`를 반환된다.

    ```js
    // 1. 일반 함수
    async function foo() {
      await bar();
    }

    // 2. 화살표 함수
    const foo = async () => {
      await bar();
    };

    foo().then(/** */).catch(/** */);
    ```

  - 위 예제처럼 `async`가 붙은 함수는 `Promise` 객체를 반환하기 때문에 후속 처리 메소드를 사용해서 핸들링할 수 있다.
  - 일반적으로 `then()`, `catch()`를 통해 핸들링을 하며 그러지 않을 경우 `try/catch`문으로 감싸서 핸들링할 수 있다.
  - `await`의 경우 비동기 함수를 동기함수처럼 보여지게 하며 비동기 함수의 가독성을 높인다.
