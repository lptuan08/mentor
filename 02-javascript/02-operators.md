# Một số toán tử quan trọng trong JavaScript

Các mục trong mục này:
- [1. So sánh](#1-so-sánh)
- [2. typeof](#2-typeof)
- [3. Truthy và Falsy](#3-truthy-và-falsy)
- [4. Toán tử logic](#4-toán-tử-logic)
- [5. Sự kỳ cục trong JavaScript](#5-sự-kỳ-cục-trong-javascript)

## 1. So sánh:

Đối với so sánh hai dấu bằng '==', JavaScript sẽ chỉ thực hiện **so sánh giá trị**
của hai biến bất kể chúng có cùng kiểu dữ liệu hay không. Tức là JavaScript sẽ đưa 2
biến về cùng một kiểu dữ liệu trước khi thực hiện so sánh.

```js
console.log(2 == "2"); // true
console.log(1 == true); // true
console.log(0 == ""); // true

console.log(1 == "true"); // false,JS không thể convert string "true" thành boolean true
```

Đối với so sánh ba dấu bằng '===', JavaScript sẽ **so sánh kiểu dữ liệu** rồi sau đó
mới **so sánh giá trị**. Nghĩa là lần này, JS không chuyển đổi về cùng một kiểu dữ liệu.

```js
console.log(2 === "2"); // false, number vs string
console.log(1 === true); // false, number vs boolean

console.log(1 === 1); // true, number vs number
console.log('name' === 'name'); // true, string vs string
```

Chú ý rằng, **nên luôn luôn sử dụng toán tử 3 dấu bằng '==='** để dễ dàng hơn trong
việc debug.

## 2. `typeof`

Có thể kiểm tra kiểu dữ liệu của một biến trong JavaScript bằng toán tử `typeof`,
toán tử này trả về một **string** là kiểu dữ liệu của biến đó.

```js
console.log(typeof 2); // number
console.log(typeof 'string'); // string
console.log(typeof true); // boolean
console.log(typeof function() {}); // function
console.log(typeof { a: 1, b:2 }); // object

console.log(typeof undefined); // undefined
console.log(typeof null); // object

console.log(typeof 'name' === 'string'); // true
```

## 3. Truthy và Falsy:

Truthy:
- number khác 0
- string khác rỗng (khác "")
- boolean `true`
- mọi array và object khác `null` (**nghĩa là [] và {} đều là truthy**)

Falsy:
- number 0
- string rỗng ""
- boolean `false`
- `undefined`
- `null`

## 4. Toán tử logic:

Hai toán tử logic `||` và '&&' có thể được dùng khi gán biến. Xét các ví dụ sau:

** Toán tử ||:

Trường hợp biến đầu trả về *falsy*:

```js
const someVariableFromApi = undefined;
const variable = someVariableFromApi || 'default variable'; // default variable
```

Trường hợp biến đầu trả về giá trị khác *falsy*:

```js
const someVariableFromApi = 'variable from api';
const variable = someVariableFromApi || 'default variable'; // variable from api
```

Có thể giải thích đơn giản đoạn code trên rằng, nếu biến đầu tiên trả về *falsy*, biến sau đó sẽ được chọn để gán mặc định.

** Toán tử &&:

Trường hợp biến đầu trả về *falsy*:

```js
const someVariableFromApi = undefined;
const variable = someVariableFromApi && 'default variable'; // undefined
```

Trường hợp biến đầu trả về giá trị khác *falsy*:

```js
const someVariableFromApi = 'variable from api';
const variable = someVariableFromApi && 'default variable'; // default variable
```

Giải thích đơn giản đoạn code trên, nếu biến đầu tiên trả về *falsy*, thì `variable` sẽ được
gán bằng chính biến đó. Nếu biến đầu tiên trả về *truthy*, biến sau sẽ được gán đến `variable`.

## 5. Sự kỳ cục trong JavaScript

Lưu ý những điều kỳ cục dưới đây, cũng chính mấy thứ này làm nên đặc trưng cho JavaScript và nó gây bối rối kể cả cho Junior hay Senior JavaScript Developer 🤣

```js
console.log(1 + "1"); // 11 chứ không phải bằng 2, tương tự "1" + "1"
console.log(1 - "1"); // 0, tương tự 1 - 1
console.log(true + false); // 1, tương tự 1 + 0
console.log([1,2] + [3,4]); // 1, 23, 4 - ??????? 😰
console.log(0.1 + 0.2); // 0.30000000000000004, cái này đa số ngôn ngữ đều thế
10, 2, 3; // 3,  gõ trực tiếp trên console, cơ bản là nó đang đếm số phần tử
console.log(1/0); // Infinity
console.log(-1/0); // - Infinity
console.log(0/0); // NaN - Not a Number
```

Phần này đọc thêm để hiểu sự kỳ quặc của JavaScript, nó được xem như là ngôn ngữ lập trình
"ngu học" nhất thế giới.