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

    ```js
    const username = 'bolam';
    const sentence = `Hello, ${username}.`;

    console.log(sentence); // Hello, bolam.
    ```
