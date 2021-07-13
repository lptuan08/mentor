# Khai báo biến trong JavaScript

Các mục trong phần này:
- [1. Các kiểu dữ liệu trong JavaScript](#1-các-kiểu-dữ-liệu-trong-javascript)
- [2. Khai báo biến trong JavaScript:](#2-khai-báo-biến-trong-javascript)
- [3. Scope của biến](#3-scope-của-biến)
- [4. Hoisting](#4-hoisting)
- [5. Best practice](#5-best-practice)

## 1. Các kiểu dữ liệu trong JavaScript:

JavaScript có các kiểu dữ liệu **nguyên thuỷ** sau: Number, String, BigInt, Boolean, Symbol.
Ở phần này khá cơ bản nên ta cần tìm hiểu kỹ hơn về Number, String, Boolean.

Các collection trong JavaScript bao gồm: Array, Object, Set và Map. Chúng ta chỉ cần
tìm hiểu Array và Object trong chương trình này. Còn Set và Map chỉ nói sơ qua định
nghĩa.

Các kiểu dữ liệu trên sẽ được nhắc lại ở những phần sau, hoặc bài sau. Hiện tại, ta cần
tìm hiểu qua hai kiểu `undefined` và `null`. Hai kiểu dữ liệu này rất dễ nhầm lẫn khi
mới tiếp cận

## 2. Khai báo biến trong JavaScript:

JavaScript là một weak-typed programming language (ngôn ngữ lập trình tự định nghĩa
kiểu dữ liệu) nên ta không cần khai báo kiểu dữ liệu khi tạo biến mới. Trước ES6, khi
khai báo biến trong JavaScript chỉ có thể sử dụng từ khoá `var`.

```js
var myName = "Allan Wu";
var myAge = 25;
```

Từ ES6 trở về sau, JavaScript có thêm 2 từ khoá dùng để khai báo biến là `let` và `const`.

Từ khoá `let` được sử dụng để khai báo biến có thể thay đổi giá trị:

```js
let myName = "Harry Potter";
console.log(myName); // Harry Potter
myName = "Hermione Granger";
console.log(myName); // Hermione Granger
```

Từ khoá `const` lại được dùng cho hằng số (giá trị không thể thay đổi)

```js
const PI = 3.14;
console.log(PI); // 3.14
PI = 3; // TypeError: Assignment to constant variable
```

## 3. Scope của biến

Scope của một biến là phần chương trình mà một biến có thể được thấy (see) và sử dụng.
Chúng ta không thể sử dụng biến ở bên ngoài scope của nó.

Có 3 loại scope trong JavaScript: *Global scope*, *Function scope* (trước ES6) và có thêm
*Block scope* (từ ES6). Biến global có thể được truy cập bởi bất cứ nơi nào khác trong
chương trình. Với **Function scope** và **Block scope**, sau khi ra khỏi scope của nó, bộ
nhớ sẽ được giải phóng ngay lập tức và không thể truy cập được từ bên ngoài.

Một biến có Global scope khi được khai báo không nằm trong bất kỳ function nào khác
(không có bất cứ function nào bao lấy biến đó). Ví dụ:

```js
var myName = "Harry Potter";
let myAge = 17;
const PI = 3.14;

function getName() {
    return myName;
}
```

Thế nhưng có sự khác biệt giữa `var` với `let`/`const`. Khi khai báo với từ khoá `var`,
**biến có global scope** sẽ được gán đến *Window Global Object* (trên môi trường browser).

```js
var globalVar = 1;
console.log(window.globalVar); // 1
let globalLet = 2;
console.log(window.globalLet); // undefined
```

Biến được khai báo với `var` sẽ có **Function Scope**, còn với `let`/`const` sẽ có **Block Scope**.
Xét các ví dụ sau:

Với `var`:

```js
function printName() {
    var name = "Nobita";
    console.log(name); // Nobita
}

console.log(name); // undefined
```

Với `let`/`const`:

```js
function printSum() {
    let sum = 0;

    for(let i = 0; i < 10; i++) {
        sum += i; // có thể sử dụng biến i ở đây
    }

    // ra khỏi cặp dấu ngoặc nhọn, i được giải phóng khỏi bộ nhớ

    console.log(i); // ReferenceError: i is not defined
}
```

## 4. Hoisting:

Trong JavaScript, một biến có thể được sử dụng trước khi nó được khai báo. Nghĩa là không cần phải
khai báo biến để sử dụng nó.

```js
name = "Harry Potter";
console.log(name); // Harry Potter
var name;
console.log(name); // Harry Potter

age = 17;
console.log(age); // 17
let age;
console.log(age); // 17
```

Có thể hiểu hoisting theo một cách khác như sau:

```js
name = "Harry Potter";
console.log(name); // Harry Potter
```

Đoạn code trên sẽ tương đương với:

```js
var name = undefined; // dòng này được JavaScript khai báo ngầm lên đầu scope của biến name
name = "Harry Potter";
console.log(name); // Harry Potter
```

Với `var`, ta có thể khai báo lại biến (khai báo đè), nhưng với `let`/`const` thì không thể.

```js
// Khai báo đè với var
var name = "Ron Weasley";
console.log(name); // Ron Weasley
var name = "Harry Potter";
console.log(name); // Harry Potter

// Khai báo đè với let
let age = 17;
console.log(age); // 17
let age = 18; // SyntaxError: Identifier 'age' has already been declared
```

## 5. Best Practice:

Từ khi có từ khoá `let` và `const`, việc khai báo biến với các từ khoá này giúp cho lập trình viên
dễ dàng kiểm soát scope và giá trị của biến. Thế nên, *đừng bao giờ sử dụng từ khoá `var`*.
Nghĩa là *chỉ sử dụng `let` và `const` để khai báo biến*
(luôn luôn sử dụng `const` và chỉ sử dụng `let` trong trường hợp cần gán lại giá trị biến).