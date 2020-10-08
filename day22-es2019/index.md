# [Day22] ES2019(ES10)

ES2019 在內建物件中多了一些擴充語法，還有擴增語法彈性等，一起來看看吧！

## Optional catch binding

在寫 `try catch` 時，我們很習慣在 `catch` 的程式區塊綁定一個參數`error`來捕捉瀏覽器提供的錯誤物件。

```javascript
try {
  // normal task
} catch (e) {
  console.log(e);
  // error handler
}
```

可是有時候並不會那這個物件做事情。在 ES2019 後，`catch` 可以選擇忽略綁定 `error`的參數。

```javascript
try {
  // normal task
} catch {
  // error handler
}
```

## 物件

### `Object.fromEntries(arr:Array<[key, value]>)`

在 [Day19](https://ithelp.ithome.com.tw/articles/10249038)有介紹跟這個很像的 `Object.entries` 是產生鍵值對的列表。而 `fromEntries` 則是他的反向方法，把鍵值對的列表轉換成物件。

```javascript
const object1 = {
  a: "somestring",
  b: 42,
};
const r1 = Object.entries(object1); // [["a", "somestring"], ["b", 42]]
const r2 = Object.fromEntries(r1); // { a: "somestring", b: 42 }
```

## 字串

在 ES5 中的 `trim()` ，對字串的頭尾都會把多餘的空白移除。在 ES2019 後，有擴充新語法，可選擇某一方向的空白移除。

### `String.prototype.trimStart()`

移除字串前面的空白。

```javascript
let str = "   One Punch Man   ";
str.trimStart(); // "One Punch Man   "
```

### `String.prototype.trimEnd()`

移除字串後面的空白。

```javascript
let str = "   One Punch Man   ";
str.trimEnd(); // "   One Punch Man"
```

## 陣列

### `Array.prototype.flat(depth?:number)`

對多維陣列（存有數層子陣列的陣列），依照參數傳入的數字，往外攤平對應層數的子陣列。

預設的深度設定為 1，也就是只攤平一層。

```javascript
[0, 1, [2, 3, [4, 5]]].flat(); // [0, 1, [2, 3, 4, 5]]
[0, 1, [2, 3, [4, 5]]].flat(2); // [0, 1, 2, 3, 4, 5]
```

### `Array.prototype.flatMap(callback)`

認識 `flatMap` 之前，先認識 `Array.prototype.reduce(callback)`

> reduce() 方法將一個累加器及陣列中每項元素（由左至右）傳入 callback 函式，將陣列化為單一值。(MDN)

callback 函式會依序接收以下四個參數 -

1. accumulator：在上次 callback 執行完後的結果
2. currentValue：目前執行元素的值
3. currentIndex：選擇性，目前執行元素的索引
4. array：選擇性，原陣列

```javascript
[0, 1, 2, 3].reduce(function (accumulator, currentValue, currentIndex, array) {
  console.log("accumulator, currentValue", accumulator, currentValue);
  return accumulator + currentValue;
});
/*
accumulator, currentValue 0 1
accumulator, currentValue 1 2
accumulator, currentValue 3 3
6
*/
```

`flatMap(callback)` 會先以 map 為每個元素 callback 函式，然後把執行結果以往外攤平一層的深度，壓縮為一個陣列並回傳。

callback 函式會依序接收以下四個參數 -

1. currentValue： callback 執行完後的結果
2. currentIndex：選擇性，目前執行元素的索引
3. array：選擇性，原陣列
4. thisArg：選擇性，`this`的對象

與 map 的比較：

```javascript
let arr1 = [1, 2, 3;

arr1.map(x => [x * 2]);  // [[2], [4], [6]]

arr1.flatMap(x => [x * 2]);  // [2, 4, 6]

// 只往外攤平一層
arr1.flatMap(x => [[x * 2]]);  // [[2], [4], [6]]
```

## 參考資源

- [ES2019 #29](https://github.com/axuebin/articles/issues/29)
