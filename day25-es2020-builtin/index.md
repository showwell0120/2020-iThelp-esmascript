# [Day25] ES2020(ES11) - 內建物件

## `Promise.allSettled`

在[Day14](https://ithelp.ithome.com.tw/articles/10246288)的時候，介紹了 Promise 針對一次執行多個 promise 時，兩種靜態方法的提供 -

1. `Promise.all`: 全部的 promise 執行結果為 `resolved` 時，才會執行 `then` 裡的 callback 函式，否則會跳到 `catch` 進行意外處理
2. `Promise.race`: 只要有其中一個 promise 執行完成且 `resolved` 的狀態，就執行 `then` 裡的 callback 函式，如果都回傳 `rejected` 的話，會跳到 `catch` 進行意外處理

而新增的靜態方法 - `Promise.allSettled`的情境是，只要所有的 promise 執行結束，並回傳 `resolved` 或 `rejected`的話，就執行 `then` 裡的 callback 函式。

```javascript
const promiseArr = [Promise.resolve(1), Promise.reject(new Error("ooh!"))];
Promise.allSettled(promiseArr).then((results) => console.log(results));

/*
(2) [{…}, {…}]
0: {status: "fulfilled", value: 1}
1: {reason: Error: ooh! , status: "rejected"}
*/
```

## `String.prototype.matchAll(regexp)`

字串物件的`matchAll`，可以傳入正規表達式`regexp`，並且以**迭代器**的資料結構，回傳所有適配`regexp`的子字串。

```javascript
const allMatched = "One Punch Man!".matchAll(/[a-h]/g);
for (let v of allMatched) {
  console.log(v);
}

/*
["e", index: 2, input: "One Punch Man!", groups: undefined]
["c", index: 7, input: "One Punch Man!", groups: undefined]
["h", index: 8, input: "One Punch Man!", groups: undefined]
["a", index: 11, input: "One Punch Man!", groups: undefined]
*/
```

## `BigInt(number)`

Javascript 在數值範圍上一直以來都有大小限制。以 `Number.MIN_SAFE_INTEGER`(-(2^53-1))和 `Number.MAX_SAFE_INTEGER`(2^53-1)來表示安全範圍內的整數。如果超過這範圍的計算，就會失去準確性。

```javascript
let n = Number.MAX_SAFE_INTEGER; // 9007199254740991

n = n + 1; // 9007199254740992

n = n + 1; // 再加一就超過安全範圍，數值還是會回傳9007199254740992

9007199254740992 === 9007199254740993; // 這時候就會造成失準，回傳true
```

因此在 ES2020，有訂定新的內建物件 - `BigInt`。跟`Number`一樣可以使用運算符，並且可以進行龐大整數的運算。

建立`BigInt`有兩種方式 -

1. 在數字後面加上`n`
   ```javascript
   const n = 123n;
   console.log(typeof n); // BigInt;
   ```
2. 使用 `BigInt(number)`宣告變數
   ```javascript
   const n = BigInt(123);
   console.log(typeof n); // BigInt;
   ```

## `globalThis`

在 Javascript 中，不同的執行環境，都有對應的全域`this`對象。像是 -

- `window`：瀏覽器特定
- `self`：Web Workers 和瀏覽器特定，NodeJS 無法使用
- `global`：NodeJS 特定

如果需要開發一個程式是需要運行在多種執行環境的話，並且要判斷全域`this`是誰的話，通常會再寫以下像`getGlobalThis`的函式 -

```javascript
const getGlobalThis = () => {
  if (typeof self !== "undefined") return self;
  if (typeof window !== "undefined") return window;
  if (typeof global !== "undefined") return global;
  throw new Error("No Global This");
};
```

在 ES2020 後，在 Javascript 中只要用`globalThis`就可以取得當前執行環境的全域`this`。

```javascript
// in web worker
globalThis === self; // true
globalThis === window; // true

// in node.js
globalThis === global; // true

// in browser
globalThis === window; // true
```

## 參考資源

- [10 New JavaScript Features in ES2020 That You Should Know](https://www.freecodecamp.org/news/javascript-new-features-es2020/)
- [ES2020 新特性](https://juejin.im/post/6844904080955932679)
