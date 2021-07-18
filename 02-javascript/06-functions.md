# Function

Các mục trong phần này:
- [1. Khai báo function trong JS](#1-khai-báo-function-trong-js)
- [2. Arrow Function](#2-arrow-function)
- [3. Arguments](#3-arguments)
- [4. No Overloading](#4-nọ-overloading)
- [5. Giá trị tham số mặc định](#5-giá-trị-tham-số-mặc-định)
- [6. Spread Arguments](#6-spread-arguments)
- [7. Keyword `this` trong Function](#7-keyword-this-trong-function)
- [8. Các phương thức của Function](#8-các-phương-thức-của-function)
    + [Function.prototype.bind()](#functionprototypebind)
    + [Function.prototype.apply()](#functionprototypeapply)
    + [Function.prototype.call()](#functionprototypecall)
- [9. IIFE](#9-iife)
- [10. Các khái niệm về function](#10-các-khái-niệm-về-function)
    + [First-Class Function](#first-class-function)
    + [Higher Order Function](#higher-order-function)
    + [Closure](#closure)
    + [Currying Function](#currying-function)

## 1. Khai báo function trong JS:

Có 3 cách để khai báo một function trong JavaScript:

- Function-declaration

```js
function sum(num1, num2) {
    return num1 + num2;
}

console.log(sum(1, 2)); // 3
```

- Function expression (gán function cho một biến)

```js
const sum = function(num1, num2) {
    return num1 + num2
};

console.log(sum(1, 2)); // 3
```

- Sử dụng `Function` constructor (**Đừng dùng cách khai báo này**)

```js
const sum = new Function('num1', 'num2', 'return num1 + num2');
console.log(sum(1, 2)); // 3
```

## 2. Arrow Function

Kể từ ES6, ta có thể khai báo một *function expression* sử dụng `arrow function`.

```js
const sum = (num1, num2) => {
    return num1 + num2;
};

console.log(sum(1, 2)); // 3
```

Arrow function thường được sử dụng trong trường hợp muốn viết một `inline syntax`,
tức là viết trên cùng một dòng để dễ dàng đọc code hơn.

```js
const nums = [1, 2, 3];

const squareNums = nums.map((n) => Math.pow(n, 2));
```

Nếu chỉ có duy nhất một tham số, ta có thể bỏ dấu ngoặc tròn


```js
const nums = [1, 2, 3];

const squareNums = nums.map(n => Math.pow(n, 2));
```

Khi sử dụng với cú pháp destructuring, **phải có dấu ngoặc tròn ở tham số**.

```js
const animals = [
    {
        name: 'Laila',
        type: 'dog'
    },
    {
        name: 'Mark',
        type: 'cat'
    }
];

const animalNames = animals.map(({ name }) => name);
```

## 3. Arguments

Khi một function được khai báo với keyword `function` (tức là không bao gồm *arrow function*),
luôn có thể truy cập đến một object tên là `arguments` trong function. `arguments` là một *like-array object* và có thể truy cập đến các phần tử (tham số) bằng `bracket notation`.

```js
function sum() {
    console.log(arguments);
    return [...arguments].reduce((s, x) => s + x, 0);
}

console.log(sum(1,2,3));
/*
Arguments {
    0: 1,
    1: 2,
    2: 3,
    length: 3,
    ...
}
*/
```

## 4. No Overloading

Function trong JavaScript không thể được *overload* như trong Java hay các ngôn ngữ khác.
Nếu 2 hay nhiều function được khai báo cùng một tên thì **function cuối cùng** sẽ được sử dụng.

```js
function addNumber(num) {
    return num + 100;
}

console.log(addNumber(100)); // 300

function addNumber(num) {
    return num + 200;
}

console.log(addNumber(100)); // 300
```

## 5. Giá trị tham số mặc định

Khi một function được gọi mà không được truyền giá trị tham số, giá trị đó mặc định sẽ
là `undefined`. Giá trị tham số mặc định trong tiếng Anh là *Default Parameter Values*

```js
function printLine(value) {
    console.log(value + '\n');
}

printLine(); // undefined
printLine('Bruce'); // Bruce
```

Từ ES6, ta có thể định một giá trị mặc định nếu tham số không được truyền vào khi gọi hàm.

```js
function sum(num1 = 0, num2 = 0) {
    return num1 + num2;
}

sum(); // 0
sum(1); // 1
sum(1, 2); // 3
```

Tham số trong một hàm được khởi tạo theo thứ tự (từ phải sang trái), nên ta hoàn toàn có thể
định một giá trị mặc định cho tham số phía sau bằng tham số phía trước. Nhưng không thể làm ngược lại

```js
function sum(num1 = 0, num2 = num1) {
    return num1 + num2;
}

console.log(sum(1)); // 2

// Error
function sum(num1 = num2, num2 = 0) {
    return num1 + num2;
}
```

## 6. Spread Arguments

Tương tự `Spread Syntax`, ta có thể sử dụng dấu `...` với function

```js
function sum(...nums) {
    console.log(nums);
    return nums.reduce((s, x) => s + x, 0);
}

console.log(sum(1, 2, 3, 4, 5));
// [1, 2, 3, 4, 5]
// 15
const values = [1, 2, 3, 4, 5];
console.log(sum(...values));
// [1, 2, 3, 4, 5]
// 15

console.log(sum(-1, ...values));
// [1, 2, 3, 4, 5]
// 14
```

`Rest parameter` có thể lấy một dãy các tham số còn lại của một function

```js
function getPost(title, ...postDetails) {
    console.log(title);
    console.log(postDetails);
}

getPost('post title', 'post description', 23, 'James King');
// post title
// ['post description', 23, 'James King']

// SyntaxError: Rest parameter must be last formal parameter
function getPost(...postDetails, author) {
    console.log(postDetails);
    console.log(author);
}
```

## 7. Keyword `this` trong Function

Có một object đặc biệt gọi là `this` trong JS function. Object `this` này sẽ có sự khác nhau
giữa một function chuẩn (function thuần, được khai báo với keyword `function`) và arrow
function.

Trong một function chuẩn, `this` sẽ tham chiếu đến *context* của object chứa nó. Nếu function
được gọi ở `Global Scope` thì object đó chính là `window` (`this` = `window`).

```js
window.color = 'red';

const obj = {
    color: 'blue',
};

function sayColor() {
    console.log(this.color);
}

sayColor(); // red

obj.sayColor = sayColor;
obj.sayColor(); // blue
```

Trong ví dụ trên, function `sayColor` được định nghĩa ở Global Scope. Tuy nhiên, khi hàm chưa
được *invoke* (gọi hàm), giá trị `this` này **chưa được xác định**. Và nó sẽ chỉ được xác định
khi hàm được *invoke* và giá trị đó tuỳ theo `context object`. hay nói cách khác, với function
chuẩn, `this` sẽ trỏ tới **`context object` nơi mà nó được gọi**.

Khi function `sayColor` được ở `Global Scope`, `this` sẽ trỏ tới `window`. Giá trị `color` lúc
này sẽ là giá trị của `window.color`. Giá trị đó là *string* `'red'`.

Sau khi function được gán đến object `obj` và gọi nó với `obj.sayColor`, `this` lúc này sẽ trỏ
tới `obj` và `this.color` chính là `obj.color`. Giá trị đó là *string* `'blue'`.

Bây giờ, ta sẽ thử viết lại đoạn code trên với Arrow Function.

```js
window.color = 'red';

const obj = {
    color: 'blue',
};

const sayColor = () => {
    console.log(this.color);
}

sayColor(); // red

obj.sayColor = sayColor;
obj.sayColor(); // red
```

Có thể thấy kết quả được log ra giữa function chuẩn và arrow function là khác nhau khi gọi
`obj.sayColor`. Lý do cho điều này là arrow function không tự bind `this` và `this` sẽ trỏ tới
**`object context` bao bọc lấy nó khi khai báo**. Ở Global Scope, `this` sẽ trỏ tới `window`.
Trong Function Constructor và Class, `this` sẽ trỏ tới instance khi khai báo instance đó với
từ khoá `new`.

Chính vì vậy, arrow function không nên được sử dụng như là phương thức khi khai báo object
với cú pháp `object literal`.

```js
const person = {
    name: 'Damian',
    age: 17,
    sayName: () => {
        console.log(this);
        console.log(this.name);
    }
};

person.sayName(); // undefined
```

## 8. Các phương thức của Function:

### Function.prototype.bind()

`Function.prototype.bind()` sẽ trả về một function mới với `this` là giá trị được cấp sẵn như
là tham số đầu tiên của phương thức. Các tham số còn lại là **các tham số đầu tiên** của hàm
khi gọi hàm.

```js
window.color = 'red';
const obj = {
    color: 'blue'
};

function sayColor() {
    console.log(this.color);
}

const sayColorBindWindow = sayColor.bind(window); // hoặc bind(this) hoặc chỉ là sayColor
sayColorBindWindow(); // red

const sayColorBindObj = sayColor.bind(obj);
sayColorBindObj(); // blue
```

Đoạn code dưới đây sẽ có các tham số còn lại theo sau `this` khi gọi `Function.prototype.bind()`.

```js
const obj = {
    nums: [1, 2, 3]
};

function printArgs() {
    console.log([...arguments]);
}

const printArgsBindObj = printArgs.bind(obj);
console.log(printArgsBindObj(4)); // [4]

const printArgsBindObjWithLeadingThirtyTwo = printArgs.bind(obj, 32);
console.log(printArgsBindObjWithLeadingThirtyTwo(4)); // [32, 4]
```

### Function.prototype.apply()

`Function.prototype.apply()` sẽ gọi một function với một giá trị `this` cho sẵn và một tham số
`arguments` như là một array.

```js
window.color = 'red';
const obj = {
    color: 'blue'
};

function sayColorAndSaySum() {
    console.log(this.color);
    console.log([...arguments].reduce((s, x) => s + x, 0));
}

sayColorAndSaySum.apply(window, [1, 2, 3]);
// red
// 6

sayColorAndSaySum.apply(obj, [1, 2, 3]);
// blue
// 6
```

### Function.prototype.call()

`Function.prototype.call()` sẽ gọi một function với một giá trị `this` cho sẵn và các tham số
theo sau đó chính là tham số được truyền đến hàm.

```js
window.color = 'red';
const obj = {
    color: 'blue'
};

function sayColorAndSaySum() {
    console.log(this.color);
    console.log([...arguments].reduce((s, x) => s + x, 0));
}

sayColorAndSaySum.call(window, 1, 2, 3);
// red
// 6

sayColorAndSaySum.call(obj, 1, 2, 3);
// blue
// 6
```

## 9. IIFE

Immediately Invoked Function Expression (viết tắt là IIFE) là một *anonymous function* sẽ được thực thi ngay lập tức khi khai báo.

```js
(function () {
    console.log('I am called');
})()
```

Ta có thể truyền các tham số bên ngoài vào IIFE

```js
const name = 'Bruce';
const age = 32;

(function () {
    console.log(name);
    console.log(age);
})(name, age)
```

## 10. Các khái niệm về Function:

### First-Class Function

Khi ta nói một ngôn ngữ có **First-Class Function**, thì có nghĩa ngôn ngữ đó xem các function
như là một biến. Ta có thể dùng nó để truyền vào tham số, return về từ một function khác, hay gán
chúng để lưu trữ một giá trị

**First-Class Function** không phải là một function, mà là một tính năng trong ngôn ngữ.

```js
// Function như là biến
const getObject = () => ({ color: 'red', type: 'product' });

// Function như là tham số
const squareNums = [1, 2, 3].map(x => Math.pow(x));

// Function trả về function khác
const sum = function(a) {
    return function(b) {
        return a + b;
    }
};
```

### Higher Order Function

**Higher Order Function** là function nhận một **function khác như là *tham số*** hoặc ***trả về* một function**, hoặc **cả hai**.

```js
const myFirstHOF = () => {
  return () => {
    const output = 'Returned from a higher order function';
    console.log(output);
  };
};

const mySecondHOF = (func) => {
  func();
};
```

### Closure

**Closure** là những function có thể truy cập các biến từ scope của những function khác. Điều này
đạt được khi ta tạo một function bên trong function khác. Một số tài liệu thì nói Closure là một kỹ thuật trong JavaScript (JavaScript concept).

Hàm bên trong có thể truy cập biến từ scope của hàm bên ngoài. Hàm bên trong gọi là
**inner function**, hàm bọc lấy nó gọi là **outer function**.

```js
const getPerson = () => {
    let name = 'Jane';

    return {
        getName: () => name,
        setName: (_name) => name = _name 
    };
};

const person = getPerson();

console.log(person.name); // undefined

console.log(person.getName()); // Jane
person.setName('Josh');
console.log(person.getName()); // Josh
```

### Currying Function

**Currying Function** là function đã được chuyển đổi một function nhiều tham số thành
một *higher order function* nhận lần lượt từng tham số.

```js
// function nhiều tham số
const sum = (a, b, c) => a + b + c;
console.log(1, 2, 3); // 6

// currying function
const curryingSum = a => b => c => a + b + c;

console.log(curryingSum(1)); // b => c => a + b + c
console.log(curryingSum(1)(2)); // c => a + b + c
console.log(curryingSum(1)(2)(3)); // 6
```

## BÀI TẬP

### Bài 1

Viết một hàm sử dụng keyword `function`, nhận vào nhiều tham số có kiểu dữ liệu `number` có
**2 chữ số thập phân phía sau dấu chấm**, trả về một mảng bao gồm các số đó được làm tròn
xuống (sử dụng hàm `Math.floor()`).

```js
// kết quả mong đợi
numsPowFour(1, 2, 3, 4);
// [1, 16, 81, 256]
```

### Bài 2

Viết một hàm `addOrSubtract`, nhận tham số đầu tiên là một boolean (`true` nếu muốn cộng và
`false` nếu muốn trừ). Các tham số còn lại là các số hạng. Hàm này trả về tổng hoặc hiệu (số
trước trừ số sau) các tham số còn lại phụ thuộc tham số đầu tiên là `true` hay `false`.

```js
// kết quả mong đợi
addOrSubtract(true, 1, 2, 3); // 6 tức là 1 + 2 + 3
addOrSubtract(false, 1, 2, 3); // -4 tức là 1 - 2 -3
addOrSubtract(false, 3, 4, 8); // -9 tức là 3 - 4 - 8
```

### Bài 3

Chạy đoạn code bên dưới và giải thích vì sao vẫn có thể gọi hàm `copyFunc` sau khi ta gán
lại hàm `func` bằng `null`. Gợi ý: sử dụng `Spread Arguments`.

```js
function func() {
    console.log('This is my function');
}

const copyFunc = func;
func = null;
copyFunc();
```

### Bài 4

Nêu sự giống và khác nhau giữa 2 phương thức `Function.prototype.call()` và `Function.prototype.apply()`.

### Bài 5

Cho đoạn code bên dưới, gọi hàm `printInfo` với `this` lần lượt là `window` và `obj`. Gợi ý
có thể sử dụng một trong 3 phương thức: `bind()`, `call()`, `apply()`.

```js
window.info = 'This is message from WINDOW';
const obj = {
    info: 'This is message from OBJ'
};

function printInfo() {
    console.log(this.info)
}
```

### Bài 6

Viết một *IIFE* nhận 2 biến `num1`, `num2` là tham số. Hàm này sẽ log ra màn hình `num1 is
greater than num2` khi num1 lớn hơn num2 và ngược lại, hàm log ra `num1 is less than or
equal to num2`.

### Bài 7

Cho một function `multiply` nhận 3 tham số và trả về tích của chúng. Hãy viết một hàm
 `curryingMultiply` nhận lần lượt từng tham số và có tính năng tương tự. Sử dụng
phần lý thuyết về **Currying Function**.

```js
const multiply = (a, b, c) => a * b * c;
```