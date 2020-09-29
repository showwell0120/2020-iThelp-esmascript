# [Day13] ES2015(ES6) - 可迭代(Iterable)與產生器(Generator)

## 可迭代(Iterable)

在前面幾天中，我們有介紹到資料結構，像是 `Set`、`Map`，以及我們熟悉的陣列，並提起有 **迭代器(Iterator)** 可以使用，例如 `set.entries`、`set.keys`等。

這些資料結構我們可以說他們是具有 **可迭代(Iterable)** 特性的集合。也就是說這種類型的集合可以透過特定的方法，在每次遍歷集合時，透過內建的 `next` 方法指到下一個元素進行操作。而這種特定的方法就叫做 **迭代器(Iterator)** 。其實最常用的 `array.forEach`、`array.map(fn)`等，就是陣列內建的迭代器實作之一。

目前來說，原生具有 Iterable 的資料結構有：

- `String`
- `Array`
- `Map`
- `Set`
- `arguments` (Array-Like Object)
- `NodeList` (Array-Like Object)
- `TypedArray`
- **`Generator`** （後面會再提）

## `for of`

在前面介紹的[陣列](https://ithelp.ithome.com.tw/articles/10241233)、[Set 跟 Map](https://ithelp.ithome.com.tw/articles/10243277)都有提到在 ES2015 中新增了這個迭代器。

為了要提供 Iterable 有一致的迭代方法，因此產生了 `for ... of` 的寫法，所以就算在字串、Nodelist 等也是可以的。

統整一下`for of`在遍歷常用的 Iterable 下的情境吧。

```javascript
// String
const str = "12";
for (let v of str) {
  console.log(v);
}
// 1
// 2

// Array
const arr = ["a", "b"];
for (let v of arr) {
  console.log(v);
}
// a
// b

// Map
const map = new Map();
map.set(1, "a");
map.set(2, "b");
for (let v of map) {
  console.log(v);
}
// [1, "a"]
// [2, "b"]

// Set
const set = new Set([1, 1, "a", "b"]);
for (let v of set) {
  console.log(v);
}
// 1
// a
// b

// arguments
function fn(params) {
  for (let v of arguments) {
    console.log(v);
  }
}
fn("a", "b");
// a
// b

// NodeList
const nodeList = document.querySelectorAll("meta");
for (let v of nodeList) {
  console.log(v);
}
// <meta http-equiv=​"X-UA-Compatible" content=​"IE=edge,chrome=1">​
// <meta name=​"viewport" content=​"width=device-width">​
```

## 產生器(Generator)

### `function* fnName() {...}`

### `yield` & `next()`

### 使用時機與延伸

- **減少額外變數，降低記憶體使用**：由 `yield*`進行委派，在這之後的產生器或可迭代物件執行迭代的行為
- **改變執行結果**：以 `next` 傳入取代
- `redux-saga`

## 小結

今天忙交屋擠不出時間寫嗚嗚，會再趕快補上！

## 參考資源

- [Iterator 和 for...of 循环](https://es6.ruanyifeng.com/#docs/iterator)
- [Arguments 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Functions/arguments)
- [產生器（Generator）](https://cythilya.github.io/2020/01/29/generator/)
