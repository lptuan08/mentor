# Object

Phần này sẽ xoay quanh kiểu dữ liệu collection Object trong JavaScript

Các mục trong phần này:
- [1. Khai báo một Object](#1-khai-báo-một-object)
- [2. Sử dụng thuộc tính/phương thức của một object](#2-sử-dụng-thuộc-tínhphương-thức-của-một-object)
- [3. Function Constructor và Prototype](#3-function-constructor-và-prototype)
    + [Function Constructor](#function-constructor)
    + [Prototype](#prototype)
    + [Kế thừa](#kế-thừa)
- [4. Một số Static Method và toán tử thường dùng của Object](#4-một-số-static-method-và-toán-tử-thường-dùng-của-object)
    + [Object.create()](#objectcreate)
    + [Object.assign()](#objectassign)
    + [Object.entries()](#objectentries)
    + [Object.keys()](#objectkeys)
    + [Object.values()](#objectvalues)
    + [Object.freeze() và Object.isFrozen](#objectfreeze-và-objectisfrozen)
    + [Object.seal() và Object.isSealed](#objectseal-và-objectissealed)
    + [Object.getOwnPropertyNames()](#objectgetownpropertynames)
- [BÀI TẬP](#bài-tập)

## 1. Khai báo một Object:

Có thể khai báo một Object trong JavaScript với cú pháp **object literal**:

```js
const person = {
    name: 'Tony Stark',
    age: 48,
    introduce: function () {
        console.log(`My name is ${this.name}`);
    }
};
```

Trong đó `name`, `age` được gọi là các thuộc tính (property), `getName` được gọi
là phương thức (method). Ngoài ra, ta có thể khai báo một method theo cách dưới
đây.

```js
const person = {
    name: 'Tony Stark',
    age: 48,
    introduce: function () {
        console.log(`My name is ${this.name}`);
    }
};
```

Chú ý rằng, **không sử dụng arrow function để khai báo method trong object
literal** (vấn đề liên quan đến context của từ khoá `this` sẽ học ở phần sau).

## 2. Sử dụng thuộc tính/phương thức của một object:

Để đọc hoặc ghi một thuộc tính của object. Ta có thể sử dụng 2 cách: `Bracket Notation` và
`Dot Notation`.

```js
const person = {
    name: 'Tony Stark',
    age: 48,
    introduce: function () {
        console.log(`My name is ${this.name}`);
    }
};

// Dot Notation
console.log(person.name); // Tony Stark
console.log(person.age); // 48
person.printName(); // My name is Tony Stark

// Bracket Notation
console.log(person['name']); // Tony Stark
console.log(person.['age']); // 48
person['printName'](); // My name is Tony Stark
```

`Bracket Notation` thường được dùng khi ta muốn đọc một thuộc tính bằng một biến JS.

```js
const person = {
    name: 'Tony Stark',
    age: 48,
    introduce: function () {
        console.log(`My name is ${this.name}`);
    }
};

const prop = 'name';
console.log(person[prop]); // Tony Stark
```

## 3. Function Constructor và Prototype:

### Mọi thứ đều là object

Trong JavaScript, mọi thứ đều là object. Với các "hàm khởi tạo" được dựng sẵn
như `Object`, `String`, `Number`, `Array`, ... ta có thể tạo ra object mới với từ khoá `new`.

```js
const name = new String('Bruce Wayne');
console.log(name); // String {"Bruce Wayne"}
console.log(typeof name); // object ?????

const nums = new Array(0, 1, 2, 3, 4);
console.log(nums); // [0, 1, 2, 3, 4]
console.log(typeof nums); // object

// JavaScript string và array đều là object có các thuộc tính: length, 0, 1, 2, 3, 4,...
// Với string mỗi index là một ký tự
// Với array mỗi index là một phần tử
```

### Function Constructor

Các "hàm khởi tạo" như trên gọi là `function constructor`. Ta có thể tạo một
custom function constructor và sử dụng từ khoá `new` để tạo mới một instance.

```js
function Person(name, age, city) {
    this.name = name;
    this.age = age;
    this.city = city;
    this.introduce = function() {
        console.log(`My name is ${this.name}`);
    };
}

const person1 = new Person('Bruce Wayne', 32, 'Gotham');
const person2 = new Person('Selena Kyle', 28, 'Gotham');

person1.introduce(); // My name is Bruce Wayne
person2.introduce(); // My name is Selena Kyle

// Kiểm tra constructor của một instance
console.log(person1.constructor); // Person
console.log(person1.constructor === Person); // true
```

Chú ý rằng, một function constructor không có câu lệnh `return` và các thuộc tính hay
phương thức được gán trực tiếp trên `this` object.

Ta có thể kiểm tra một instance có phải là instance của một Function Constructor nào đó hay không bằng cách sử dụng toán tử `instanceof`.

```js
function Person(name, age, city) {
    this.name = name;
    this.age = age;
    this.city = city;
    this.introduce = function() {
        console.log(`My name is ${this.name}`);
    };
}

const person = new Person('Damian Wayne', 16, 'Gotham');

console.log(person instanceof Person); // true
console.log(person instanceof Object); // true, vì Person kế thừa từ Object
```

### Prototype

Mỗi function đều được tạo ra với một thuộc tính `prototype`. Thuộc tính này là một object
chứa các thuộc tính và phương thức có sẵn đối với các instance. Nó sẽ chỉ được tạo ra một khi
constructor được gọi với từ khoá `new`. Lợi ích của prototype đó là những thuộc tính và
phương thức sẵn có sẽ được chia sẻ giữa các instance.

Ta có đoạn code sử dụng Prototype:

```js
function Person() {} // let Person = function() {} cũng được

Person.prototype.name = 'Harry Potter';
Person.prototype.age = 17;
Person.prototype.job = 'The Witch';

Person.prototype.sayName = function() {
    console.log(this.name);
}

const person1 = new Person();
person1.sayName(); // Harry Potter

const person2 = new Person();
person2.sayName(); // Harry Potter

console.log(person1.sayName === person2.sayName); // true
// prototype được share giữa các instance
// hay nói cách khác, các instance sử dụng chung một prototype
```

Cách mà prototype hoạt động: Khi một function được tạo, sẽ kèm theo một thuộc tính
được gọi là `prototype`.

Khi ta định nghĩa một custom constructor, `prototype` mặc định sẽ có thuộc tính
`constructor` (thuộc tính này trỏ đến chính Function Constructor chứa nó). Toàn bộ
các phương thức còn lại được kế thừa từ `Object`.

Mỗi khi constructor được gọi để tạo ra một instance mới, instance đó sẽ có một
`internal pointer` trỏ tới `prototype` của constructor. Theo ECMA-262, `internal pointer`
này được gọi là *[[Prototype]]*. Thật ra không có một cách nào gọi là "chuẩn" để truy
cập *[[Prototype]]* trong JavaScript nhưng Chrome, Firefox, Safari có hỗ trợ một thuộc
tính gọi là `__proto__`. Ở những môi trường khác thì thuộc tính này bị ẩn hoàn toàn và
không thể truy cập.

```js
function Person() {}

console.log(typeof Person.prototype); // object
console.log(Person.prototype);
/*
{
    constructor: f Person()
    __proto__: {
        constructor: f Object(),
        hasOwnProperty: f hasOwnProperty()
        isPrototypeOf: f isPrototypeOf()
        ...etc
    }
}
*/

console.log(Person.prototype.__proto__ = Object.prototype); // true
console.log(Person.prototype.__proto__.constructor === Object); // true

const person = new Person();
console.log(person.__proto__ === Person.prototype); // true
console.log(person.__proto__.constructor === Person); // true

// Kiểm tra một prototype có phải là prototype của một object hay không
console.log(Person.prototype.isPrototypeOf(person)); // true
```

Đoạn code bên dưới là một số phương thức của Object.prototype và toán tử `in`:

```js
function Person() {}

Person.prototype.name = 'Tony Stark';
Person.prototype.age = 48;
Person.prototype.job = 'Iron Man';
Person.prototype.sayName = function() {
    console.log(this.name);
};

const person = new Person();

// hasOwnProperty(): method kiểm tra xem một thuộc tính có phải là thuộc tính riêng của
// instance (trả về true) hay là một thuộc tính trong prototype (trả về false)
console.log(person.hasOwnProperty('name')); // false
person.name = 'Anthony Stark';
console.log(person.hasOwnProperty('name')); // true

// Toán tử "in": dùng để kiểm tra xem một thuộc tính có trong instance hay không, bất kể
// là từ instance hay từ prototype (true nếu có, false nếu không)
console.log('name' in person); // true - từ instance
console.log('age' in person); // true - từ prototype
console.log('city' in person); // false

// Sử dụng for in để duyệt qua các thuộc tính của object (từ instance và từ prototype)
for(const key in person) {
    console.log(key);
}
// name
// age
// job
// sayName
```

### Kế thừa

Ta có đoạn code kế thừa để tính tổng 2 số `a` và `b` mà không sử dụng toán tử `+`:

```js
Number.prototype.add = function(num) {
    return this + num;
}

let a = 5;
let b = 1;
console.log(a.add(b)); // 6
```

Để kế thừa từ một `Function Constructor` ta có thể thêm trực tiếp method vào prototype của nó.

Ví dụ với custom Function Constructor:

```js
function Person(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function() {
        console.log(this.name);
    };
}

Person.prototype.sayJob = function() {
    console.log(this.job);
};

const person1 = new Person('Harry', 17, 'Witch');
person1.sayJob(); // Witch
person1.sayAge(); // undefined, sayAge chưa được định nghĩa

Person.prototype.sayAge = function() {
    console.log(this.age);
};

const person2 = new Person('Dumbledore', 115, 'Wizard');
person2.sayJob(); // Wizard
person2.sayAge(); // 115

person1.sayAge(); // 17
```

## 4. Một số Static Method và toán tử thường dùng của Object:

### Object.create()

`Object.create()` tạo một object mới từ một object có sẵn. Object mới sẽ coi object có sẵn đó
như là prototype.

```js
const singer = {
    name: 'Ed Sheeran',
    age: 30,
    instruments: ['Guitar', 'Piano'],
    sayName: function() {
        console.log(this.name);
    }
};

const newSinger = Object.create(singer);
console.log(newSinger);
/*
{}
--__proto__: {
    age: 30,
    instruments: ['Guitar', 'Piano'],
    name: 'Ed Sheeran',
    sayName: f (),
    __proto__: Object
}
*/
```

### Object.assign()

`Object.assign()` sẽ copy tất cả các *enumerable own property* (thuộc tính từ object và có thể lặp qua với vòng lặp for ... in) từ object `source` sang object `target`. Nếu một thuộc tính đã có sẵn trong `target` nó sẽ được ghi đè với giá trị từ `source`.

`Object.assign()` làm thay đổi (mutate) luôn object `target` và trả về object đã được copy.

```js
const target = { a: 1, b: 2 };
const source = { b: 3, c: 4 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// { a: 1, b: 3, c: 4 }
console.log(returnedTarget);
// { a: 1, b: 3, c: 4 }
```

### Object.entries()

`Object.entries` sẽ trả về một mảng mà trong đó, mỗi phần tử là một mảng con `[key, value]`. Tương tự như khi dùng vòng lặp for ... in.

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
};

console.log(Object.entries(obj)); // [ ['a', 1], ['b', 2], ['c', 3] ]
```

### Object.keys()

`Object.keys()` trả về một mảng chứa các thuộc tính `key` của object.

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
};

console.log(Object.keys(obj)); // ['a', 'b', 'c']
```

### Object.values()

`Object.keys()` trả về một mảng chứa các giá trị `value` của object.

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
};

console.log(Object.values(obj)); // [1, 2, 3]
```

### Object.freeze() và Object.isFrozen()

`Object.freeze()` sẽ "đông cứng" một object. Một object sau khi bị "đông cứng" sẽ không thể
bị thay đổi thuộc tính và cũng không thể thêm thuộc tính mới vào nó. Method này trả về một
object đã được "đông cứng".

`Object.isFrozen()` dùng để kiểm tra xem một object đã bị "đông cứng" hay chưa. Nếu có trả
về true, không trả về false.

```js
const person = { name: 'Cristine' };
Object.freeze(person);

person.name = 'Anna'; // sẽ báo lỗi nếu ở strict mode ('use strict')
console.log(person.name); // Cristine

person.age = 21;
console.log(person.age); // undefined

console.log(Object.isFrozen(person)); // true
```

### Object.seal() và Object.isSealed

`Object.seal()` tương tự như `Object.freeze()`, nhưng `seal()` chỉ không cho phép thêm thuộc
tính mới nhưng vẫn có thể thay đổi thuộc tính cũ.

`Object.isSealed()` dùng để kiểm tra xem một object đã bị "seal" hay chưa. Nếu có trả
về true, không trả về false.

```js
const person = { name: 'Cristine' };
Object.seal(person);

person.name = 'Anna';
console.log(person.name); // Anna

person.age = 21;
console.log(person.age); // undefined

console.log(Object.isSealed(person)); // true
```

### Object.getOwnPropertyNames()

`Object.getOwnPropertyNames()` trả về một mảng chứa các thuộc tính (kể cả non-enumerable own property).

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
};

console.log(Object.getOwnPropertyNames(obj)); // ['a', 'b', 'c']

// Object.keys() vs Object.getOwnPropertyNames()
console.log(Object.keys('foo'));                                // [0, 1, 2]
console.log(Object.getOwnPropertyNames('foo')); // [0, 1, 2, 'length']
```

## BÀI TẬP

### Bài 1

Không chạy đoạn code bên dưới, cho biết kết quả được log ra? Giải thích vì sao từng giá trị
được log ra như vậy.

```js
function Character() {}
Character.prototype.name = 'Shinichi Kudo';
Character.prototype.age = 17;
Character.prototype.iq = '180';

const character = new Character();

console.log(character.__proto__);

character.name = 'Conan Edogawa';
character.age = 7;

console.log(character.name);
console.log(character.age);
console.log(character.iq);
```

### Bài 2

Tạo một method `String.prototype.concat` để cộng 2 chuỗi a, b sử dụng toán tử string concatenation `+`.

Ví dụ:

```js
const a = 'Hello';
const b =', World!';

console.log(a.concat(b)); // Hello, World!
```

### Bài 3

Tìm cách tạo một static method `Person.log` của Function Constructor Person được cho dưới
đây, static method này sẽ log ra một string *"I am a person, not an animal"*

```js
function Person() {}
Person.prototype.name = 'Anne';
Person.prototype.age = 38;
Person.prototype.job = 'Actress';

// kết quả mong đợi
Person.log(); // I am a person, not an animal
```

### Bài 4

Sử dụng `Object.keys()` và `Array.prototype.map()`, tạo một mảng với các phần tử là tên của các nhân vật từ object sau:

```js
const characters = {
    conan: {
        name: 'Conan Edogawa',
        age: 6
    },
    ran: {
        name: 'Ran Mori',
        age: 17
    },
    haibara: {
        name: 'Haibara Ai',
        age: 6
    },
    agasa: {
        name: 'Agasa Hiroshi',
        age: 50
    }
};

// Kết quả mong đợi
const characterNames = ['Conan Edogawa', 'Ran Mori', 'Haibara Ai', 'Agasa Hiroshi'];
```

### Bài 5

Giải thích sự giống nhau và khác nhau của `Object.freeze()` và `Object.seal()`.