# Một số cú pháp mới từ ES6

Các mục trong phần này:
- [1. Khai báo nhiều biến cùng lúc](#1-khai-báo-nhiều-biến-cùng-lúc)
- [2. Destructuring](#2-destructuring)
- [3. Spread Syntax](#3-spread-syntax)
- [4. Template Literal](#4-template-literal)
- [5. Vòng lặp For Of](#5-vòng-lặp-for-of)

## 1. Khai báo nhiều biến cùng lúc

Thay vì khai báo kiểu cũ:

```js
var x = 1;
var y = 2;
var z = 3;
```

Ta sử dụng khai báo cùng lúc:

```js
let x = 1, y = 2, z = 3;
// hoặc
let [x, y, z] = [1, 2, 3];
```

## 2. Destructuring

Destructuring là cú pháp lấy các phần tử trong mảng, hay thuộc tính trong array mà
không cần sử dụng `bracket notation` (cú pháp: `array[index]` hoặc `object[prop]`) hay
`dot notation` (như `object.prop`) nhiều lần.

Array Destructuring:

```js
const nums = [1, 2, 3, 4];
const [a, b, c, d] = nums;
console.log(a, b, c, d); // 1 2 3 4

// có thể bỏ qua những phần tử không dùng đến
const [x,y,,z] = nums;
console.log(x, y, z); // 1 2 4
```

Object Destructuring:

```js
const person = {
    name: 'Harry Potter',
    age: 17,
    profile: {
        image: 'https://image.com/harry'
    }
};

const { name, age } = person;
console.log(name, age); // Harry Potter 17

// sử dụng với tên biến khác
const { name: nameOfPerson } = person;
console.log(nameOfPerson); // Harry Potter

// destructuring ở level sâu hơn
const { profile: { image } } = person;
console.log(image); // https://image.com/harry
console.log(profile); //  error, destructuring không destruct phần này
```

## 3. Spread Syntax

Rest Operator (hoặc Spread Syntax) là cú pháp sử dụng dấu 3 chấm `...` để lấy một dãy các phần tử trong array hay thuộc tính trong mảng còn lại khi sử dụng destructuring. (Khái niệm này còn mơ hồ vì anh không biết viết sao cho rõ nữa, xem code để hiểu hơn).

Xét đoạn code dưới:

```js
// Array
const nums = [1, 2, 3, 4, 5, 6];
const [a, b, ...restNums] = nums;
console.log(a, b, restNums); // 1 2 [3, 4, 5, 6]

// Object
const person = {
    name: 'Hermione Granger',
    age: 17,
    burst: 86,
    waist: 59,
    hip: 86
};

const { name, age, ...measurements } = person;
console.log(measurements); // { burst: 86, waist: 59, hip: 86 }
```

Ngoài ra cú pháp này còn được sử dụng với tham số của một hàm khi số lượng tham số pass đến hàm là chưa thể xác định. Gọi là Rest Parameters.

```js
function sum(...nums) {
    console.log(nums);
    return nums.reduce((acc, curr) => acc+ curr, 0);
}

console.log(sum(1, 2, 3, 4));
// [1, 2, 3, 4]
// 10
```

## 4. Template Literal

Sử dụng dấu backtick (`) để khai báo một template literal. Bằng cách này, ta có thể format một string ngay khi khai báo.

Xét đoạn code dưới

```js
const myAge = 25;
const message = `Today is my ${myAge}th birthday`;
console.log(message); // Today is my 25th birthday
```

## 5. Vòng lặp For Of

Sử dụng for ... of để duyệt mảng thay vì sử dụng for thường như trước ES6

Xét đoạn code dưới:

```js
const nums = [0, 1, 2, 3, 4];

for(let num of nums) {
    console.log(num);
}
```
