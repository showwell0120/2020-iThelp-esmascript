# [Day17] ES2017(ES8) - Await & Async

在 ES2015 中，將 Promise 標準化，解決了以往要寫非同步時容易產生的 callback hell。不過寫久了就會發現，如果有多個非同步，或是有複雜的判斷邏輯時，Promise 的寫法還是會讓程式產生巢狀，語意上也不好解讀。

因此在 ES2017 中，最重要的特性就是新增非同步寫法的方式 - 以 Promise 結合 Generator 的特性，以`await`跟`async`作為非同步函式的前綴字，來簡化 Promise 的實現。

基本用法是當要宣告非同步函式時，使用`async`作為函式的前綴字。當要執行函式時，使用`await`作為呼叫函式的前綴字。另外在函式裡有執行到非同步的地方，也可以用`await`表示這裡需要等待結果回傳。

```javascript
async function allResult() {
  const r1 = await fn1();
  const r2 = await fn2();
  return [r1, r2];
}
const result = await allResult();
```

跟原本的 Promise 寫法比較看看。先建立一些非同步函式 -

```javascript
const downloadData() = () => {
    return new Promise((resolve, reject) => {...})
}
const processData() = () => {
    return new Promise((resolve, reject) => {...})
}
const ProcessError() = () => {
    return new Promise((resolve, reject) => {...})
}
```

getData 回傳的 Promise 會導致 promise chaining，將函式分隔成多個部份。

```javascript
function getData(params) {
  return downloadData(params) // returns a promise
    .then(v => {
      return processData(params); // returns a promise
    });
    .catch(e => {
      return ProcessError(params); // returns a promise
    })
}
```

在 async function 沒有 promise 的鏈狀結構產生，並且以 try catch 處理意外錯誤

```javascript
async function getData(params) {
  let v;
  try {
    v = await downloadData(params);
  } catch (e) {
    v = await ProcessError(params);
  }
  return processData(vparams);
  //在 return 沒有使用 await，因為 async function 回傳值被包裝於 processData 的 Promise.resolve 之中
}
```

## 參考資源

- [async function](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements/async_function)
