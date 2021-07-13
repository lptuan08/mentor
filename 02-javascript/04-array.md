# Array

Phần này chỉ giới thiệu một số method thường dùng của JavaScript Array chứ chưa
phải toàn bộ (rất nhiều method).

Các mục trong phần này:
- [1. Array.prototype.map](#1-arrayprototypemap)
- [2. Array.prototype.filter](#2-arrayprototypefilter)
- [3. Array.prototype.find](#3-arrayprototypefind)
- [4. Array.prototype.findIndex](#4-arrayprototypefindindex)
- [5. Array.prototype.reduce](#5-arrayprototypereduce)
- [6. Array.prototype.flat](#6-arrayprototypeflat)
- [7. Array.prototype.concat](#7-arrayprototypeconcat)
- [8. Array.prototype.forEach](#8-arrayprototypeforEach)
- [9. Một số method khác](#9-một-số-method-khác)

## 1. Array.prototype.map()

`Array.prototype.map` là method tạo ra một array thông qua function mà ta truyền vào. Array mới này luôn có cùng length với array ban đầu.
`map()` không làm thay đổi (mutate) array ban đầu

Xét đoạn code sau:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const callbackFn = num => num * 2;
const squareNums = nums.map(callbackFn);
console.log(squareNums); // [16, 10, 4, 18, 8, 6, 2]
```

Tương đương khi ta duyệt bằng vòng lặp for:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const callbackFn = num => num * 2;
const squareNums = [];

for(let i = 0; i < nums.length; i++) {
    squareNums.push(callbackFn(nums[i]));
}

console.log(squareNums);
```



Hàm truyền vào được gọi là một callback function (hàm callback sẽ được học nhiều hơn ở phần closure và asynchronous).

Hàm callback sẽ nhận 3 tham số:
- `element`: phần tử hiện tại
- `index`: chỉ số index của phần tử hiện tại
- `array`: array gốc

Hiểu cơ bản, `nums` sẽ được duyệt qua một lần và thực hiện hàm với từng phần tử rồi trả về array kết quả.

**`map()` method được dùng trong React để render các phần tử của một array.**

## 2. Array.prototype.filter()

`Array.prototype.filter` là method lọc ra những phần tử phù hợp với điều kiện mà hàm callback được truyền vào.


Xét đoạn code sau:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const callbackFn = num => num > 4;
const numsGreaterThanFour = nums.filter(callbackFn);
console.log(numsGreaterThanFour); // [8, 5, 9]
```

Tương đương duyệt bằng vòng for:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const callbackFn = num => num > 4;
const numsGreaterThanFour = [];

for(let i = 0; i < nums.length; i++) {
    if(callbackFn(nums[i])) {
        numsGreaterThanFour.push(nums[i]);
    }
}

console.log(numsGreaterThanFour);
```

Hàm callback sẽ nhận 3 tham số:
- `element`: phần tử hiện tại
- `index`: chỉ số index của phần tử hiện tại
- `array`: array gốc

## 3. Array.prototype.find()

`Array.prototype.find` sẽ trả về phần tử tìm được **đầu tiên** trong mảng gốc phù hợp với điều kiện mà hàm callback được truyền vào.


Xét đoạn code sau:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const callbackFn = num => num > 4;
const numGreaterThanFour = nums.find(callbackFn);
console.log(numGreaterThanFour); // 8
```

Tương đương duyệt bằng vòng for:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const callbackFn = num => num > 4;
const numGreaterThanFour;

for(let i = 0; i < nums.length; i++) {
    if(callbackFn(nums[i])) {
        numGreaterThanFour = nums[i];
        break;
    }
}

console.log(numGreaterThanFour); // 8
```

Hàm callback sẽ nhận 3 tham số:
- `element`: phần tử hiện tại
- `index`: chỉ số index của phần tử hiện tại
- `array`: array gốc

## 4. Array.prototype.findIndex()

`Array.prototype.findIndex` sẽ trả về **chỉ số của phần tử tìm được đầu tiên** trong mảng gốc phù hợp với điều kiện mà hàm callback được truyền vào.


Xét đoạn code sau:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const callbackFn = num => num > 4;
const indexOfFirstElem = nums.findIndex(callbackFn);
console.log(indexOfFirstElem); // 0
```

Tương đương duyệt bằng vòng for:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const callbackFn = num => num > 4;
const indexOfFirstElem;

for(let i = 0; i < nums.length; i++) {
    if(callbackFn(nums[i])) {
        indexOfFirstElem = i;
        break;
    }
}

console.log(indexOfFirstElem); // 0
```

Hàm callback sẽ nhận 3 tham số:
- `element`: phần tử hiện tại
- `index`: chỉ số index của phần tử hiện tại
- `array`: array gốc

## 5. Array.prototype.reduce()

Đây là method có thể khó hiểu nhất trong các method của array. Method này sẽ
thực thi một hàm reducer (concept này sang phần React sẽ được tìm hiểu) trên
từng phần tử của array gốc.

Xét đoạn code tình tổng các phần tử trong array gốc:

```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const reducerFn = (accumulator, currentElem) => {
    return accumulator + currentElem;
};
const sum = nums.reduce(reducerFn, 0);
console.log(sum); // 32
```

Method `reduce` thực thi với hàm reducer là `reducerFn` với giá trị khởi tạo ban
đầu là `0`.

Tương tự vòng for:

```js
const nums = [8, 5, 2, 9, 4, 3, 1];
const reducerFn = (accumulator, currentElem) => {
    return accumulator + currentElem;
};

let sum = 0; // khởi tạo giá trị

for(let i = 0; i < nums.length; i++) {
    sum = reducerFn(sum, nums[i]); // tương đương sum = sum + nums[i]
}

console.log(sum);
```

Giá trị khởi tạo ban đầu có thể là bất cứ kiểu dữ liệu nào trong JavaScript. Tóm
lại, method này cơ bản là dùng để biến đổi một array sang một kiểu dữ liệu khác.

Với giá trị ban đầu là object (object rỗng):


```js
const nums  = [8, 5, 2, 9, 4, 3, 1];
const reducerFn = (accumulator, currentElem) => {
    return {
        ...accumulator,
        [`value${index}`]: currentElem
    };
};
const sum = nums.reduce(reducerFn, {});
console.log(sum); // {value0: 8, value1: 5, value2: 2, value3: 9, value4: 4…}
```

Hàm reducer sẽ nhận 3 tham số:
- `accumulator`: giá trị khởi tạo ban đầu
- `element`: phần tử hiện tại
- `index`: chỉ số index của phần tử hiện tại
- `array`: array gốc

## 6. Array.prototype.flat()

`Array.prototype.flat` là method **làm phẳng** mảng

Xét đoạn code sau:

```js
const nums = [0, 1, 2, [3, 4]];

console.log(nums.flat());
// expected output: [0, 1, 2, 3, 4]

const secondNums = [0, 1, 2, [[[3, 4]]]];

console.log(secondNums.flat(2));
// expected output: [0, 1, 2, [3, 4]]
```

Tham số truyền vào:
- depth - number: độ sâu level của mảng muốn flat


## 7. Array.prototype.concat()

`Array.prototype.concat` là method gộp 2 hay nhiều mảng thành một

Xét đoạn code sau:

```js
const a = [0, 1, 2];
const b = [3, 4, 5];

console.log(a.concat(b)); // [0, 1, 2, 3, 4, 5]

// hoặc

console.log(a.concat(...b)); // [0, 1, 2, 3, 4, 5]
console.log(a.concat(3, 4, 5)); // [0, 1, 2, 3, 4, 5]
```

## 8. Array.prototype.forEach()

`Array.prototype.forEach` là method tương tự vòng lặp for thường nhưng có một số khác biệt
so với for thường (sau này đến phần NodeJS sẽ thấy).

Xét đoạn code sau:

```js
const nums = [0, 1, 2, 3];
const callbackFn = num => console.log(num)
nums.forEach(callbackFn);
/*
0
1
2
3
*/
```

Nếu ta return trong vòng lặp forEach sẽ không có bất cứ điều gì xảy ra, **đừng viết return trong forEach**.

Hàm callback sẽ nhận 3 tham số:
- `element`: phần tử hiện tại
- `index`: chỉ số index của phần tử hiện tại
- `array`: array gốc

## 9. Một số method khác:

Ngoài các method kể trên, có một số method đơn giản hơn cần nắm như:

- Array.prototype.includes()
- Array.prototype.some()
- Array.prototype.every()
- Array.prototype.reverse() \
...