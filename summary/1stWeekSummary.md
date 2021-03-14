

# 1. ES5

## filter()

조건결과가 true인 요소만 남긴 새로운 배열을 반환합니다.

<pre>
<code>
[0, 1, 2, 3, 4, 5, 6]
    .filter(function (val, idx, array) {
        return val <= 3;
    })
    .forEach(function (val, idx, array) {
        console.log(val);
    });
//
// will print
// 0, 1, 2, 3
</code>
</pre>

## reduce()
개수세기!!
<pre>
<code>
const array = [1, 1, 1, 9];
const count = array.reduce(function (acc, val, idx, array) {
    if (acc[val] === undefined) {
        acc[val] = 0;
    }
    acc[val]++;
}, new Object());

console.log(count);
//
// will print
// {
//     1 : 3,
//     9 : 1,
// }
</code>
</pre>


## 비구조화 할당
<pre>
<code>
const [cat, dog, tiger] = ["CAT", "DOG", "TIGER"];
console.log(cat); // CAT
console.log(dog); // DOG
console.log(tiger); // TIGER
</code>
</pre>


# 2. es6
## 넘나 편한 백틱
<pre>
<code>
hello = () => {
    return "Hello, World!";
};

const message = `
        Hi, ${name}!
        Hello, ${name}!
        `;
</code>
</pre>

# 3. es7
## .includes()
<pre>
<code>
const list = ["1", 2, 3, 4, 5];
list.includes(1); // false
list.includes(2); // true
list.includes(2, 2); // false
</code>
</pre>

# 4.es8
## 프로미스
<pre>
<code>
function getAsyncRandomValue() {
    return new Promise((resolve, reject) => {
        resolve(Math.random());
    });
}

function main() {
    getAsyncRandomValue()
        .then(onSuccess_1)
        .then(onSuccess_2)
        .then(onSuccess_3)
        .catch(onFailure);
}
</code>
</pre>