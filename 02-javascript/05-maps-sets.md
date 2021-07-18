# Maps & Sets

## Maps

### Map là gì?

`Map` trong JS là một object lưu trữ các giá trị theo từng cặp `key - value` theo thứ tự mà ta
định nghĩa. `key` và `value` trong Map có thể là `object` hoặc `primitive types`. Điểm này
chính là một điểm khác của Map so với Object. Object chỉ có thể lưu các `key` như là một
`string` hay một `Symbol`.

Có thể xem so sánh giữa `Map` với `Object` tại [đây](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map?retiredLocale=vi#objects_vs._maps)

### Khai báo Map và các phương thức của Map

Để khai báo một Map, ta có thể sử dụng `Map` constructor với từ khoá `new`.

```js
const myEmptyMap = new Map();
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]); // từ một iterable array
```

#### Map.prototype.size

`Map.prototype.size` trả về số cặp `key - value` có trong Map đó.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
console.log(myMap.size); // 3
```

#### Map.prototype.get(key)

`Map.prototype.get(key)` trả về giá trị value tương ứng với `key` có trong Map.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
console.log(myMap.get(1)); // one
```
#### Map.prototype.set(key, value)

`Map.prototype.set(key, value)` thêm một cặp `key - value` vào Map.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
myMap.set(4, 'four');
console.log(myMap.get(4)); // four
```

#### Map.prototype.has(key)

`Map.prototype.has(key)` để kiểm tra xem có `key` trong Map hay không. Có trả về
`true`, không trả về `false`.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
console.log(myMap.has(4)); // true
console.log(myMap.has(5)); // false
```

#### Map.prototype.delete(key)

`Map.prototype.delete(key)` để xoá một cặp `key - value` trong Map.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
myMap.delete(3);
console.log(myMap.has(3)); // false
```

#### Map.prototype.clear()

`Map.prototype.clear()` sẽ xoá toàn bộ các cặp `key-value` trong Map.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
myMap.clear();
console.log(myMap); // Map (0) {}
```

#### Map.prototype.entries(), Map.prototype.keys() và Map.prototype.values()

`Map.entries()` trả về một Map Iterator bao gồm các cặp `key - value` như là mảng con

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
console.log(myMap.entries())); // Map Iterator {1 => 'one', 2 => 'two', 3 => 'three'}
```

`Map.keys()` trả về một Map Iterator bao gồm các `key` có trong Map.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
console.log(myMap.keys())); // Map Iterator {1, 2, 3}
```

`Map.values()` trả về một Map Iterator bao gồm các `value` có trong Map.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
console.log(myMap.keys())); // Map Iterator {'one', 'two', 'three'}
```

#### Map.prototype.forEach()

Ta có thể sử dụng `Map.prototype.forEach()` để lặp qua các `key - value` tương tự đối với mảng.

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);
myMap.forEach((value, key, map) => {
    console.log(key, '-', value);
    console.log(map);
});

// 1 - one
// Map(3) {}
// 2 - two
// Map(3) {}
// 3 - three
// Map(3) {}
```

Ngoài ra có thể dùng for ... of để duyệt Map:

```js
const myMap = new Map([[1, 'one'], [2, 'two'], [3, 'three']]);

for(let [key, value] of myMap) {
    console.log(key, '-', value);
}
// 1 - one
// 2 - two
// 3 - three
```

### Weak Map

`Weak Map` là một `Map` nhưng các `key` **chỉ có thể là `object`

```js
const myWeakMap = new WeakMap();
myWeakMap.set({a: 1}, 'this is object 1');
console.log(myWeakMap);
myWeakMap.set(1, 'one'); // TypeError: Invalid value used as weak map key
```

Weak Map có tất cả những phương thức mà Map có và cách sử dụng tương đương với Map.




## Sets

Một `Set` trong JavaScript là một object chứa các giá trị **duy nhất** (tức là không có 2 giá trị giống nhau trong cùng một `Set`).

### Khai báo Set và các phương thức của Set

Tương tự với `Map`, có thể khai báo `Set` như sau:

```js
const myEmptySet = new Set();
const mySet = new Set([1, 2, 3, 4, 3, 2, 1]); // từ một iterable array
console.log(mySet); // Set(4) {1, 2, 3, 4}
console.log(typeof mySet); // object
```

#### Set.prototype.size

`Set.prototype.size)` sẽ trả về số `value` có trong Set.

```js
const mySet = new Set([1, 2, 3]);
console.log(mySet.size); // 3
```

#### Set.prototype.add(value)

`Set.prototype.add(value)` sẽ thêm một giá trị `value` mới vào Set, trả về Set mới.

```js
const mySet = new Set([1, 2, 3]);
mySet.add(4);
mySet.add(1);
console.log(mySet); // Set (4) {1, 2, 3, 4}
```

#### Set.prototype.has(value)

`Set.prototype.has(value)` kiểm tra một `value` đã có trong Set hay chưa.

```js
const mySet = new Set([1, 2, 3]);
console.log(mySet.has(1)); // true
console.log(mySet.has(4)); // false
```

#### Set.prototype.delete(value)

`Set.prototype.delete(value)` sẽ xoá một `value` có trong Set.

```js
const mySet = new Set([1, 2, 3]);
mySet.delete(3);
console.log(mySet.size); // 2
```

#### Set.prototype.clear()

`Set.prototype.clear()` sẽ xoá toàn bộ các `value` trong Set.

```js
const mySet = new Set([1, 2, 3]);
mySet.clear();
console.log(mySet.size); // 0
```

#### Set.prototype.entries() và Set.prototype.values()

`Set.prototype.entries()` sẽ trả về một Set Iterator chứa các cặp `value - value`.

```js
const mySet = new Set([1, 2, 3]);
console.log(mySet.entries());
// SetIterator {1 => 1, 2 => 2, 3 => 3}
```

`Set.prototype.values()` sẽ trả về một Set Iterator chứa các `value`

```js
const mySet = new Set([1, 2, 3]);
console.log(mySet.values());
// SetIterator {1, 2, 3}
```

#### Set.prototype.forEach()

`Set.prototype.forEach()` sẽ duyệt qua từng giá trị có trong Set

```js
const mySet = new Set([1, 2, 3]);
mySet.forEach((value) => console.log(value));
// 1
// 2
// 3
```

#### Vòng lặp for ... of

Có thể duyệt Set với vòng lặp for ... of

```js
const mySet = new Set([1, 2, 3]);
for(let value of mySet) {
    console.log(value);
}
// 1
// 2
// 3
```

## Weak Set

Như mối quan hệ giữa Map với Weak Map, `Weak Set` là một `object` giống như Set nhưng
chỉ có thể chứa các giá trị có kiểu dữ liệu là `object`.

```js
const myWeakSet = new Set();
myWeakSet.add({a: 1});
myWeakSet.add(1); // TypeError
```

Weak Set có đầy đủ các phương thức của Set.