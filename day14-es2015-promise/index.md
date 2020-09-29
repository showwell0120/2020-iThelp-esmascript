# [Day14] ES2015(ES6) - Promise

寫 ES5 時，只要需要寫到非同步請求，我們或多或少都有接觸到 promise 的寫法。但是因為在 Javascript 中還沒有實作，所以還要額外匯入支援的函式庫或模組，像是 `jQuery`、`BlueBird`等。

ES2015 中，Promise 終於被納入標準。一直到現在，Promise 已經成為實作非同步方法中的基本方式。在 `Fetch API`、`Service Worker` 等，主要也是以 Promise 實現非同步行為。所以今天就來好好認識吧！

![Imgur](https://i.imgur.com/CL3DTzp.png)

先來看 Promise 的執行流程。

- 開始執行 Promise 物件，任務結束前的回傳，都會是 **Pending** 狀態
- 任務結束後，如果沒發生意外錯誤，則會執行到 `then()`裡的 callback。反之則會執行到`catch()`裡的 Error handler
- 在 `then` 裡有兩個參數 `resolve` 跟 `reject`。
  - 當任務結果成功，以`resolve`回傳，或在執行下個 `then`
  - 當任務結果失敗，以`reject`回傳

看個基本例子。

```javascript
// 一秒後隨機取數，如果是偶數就會該數字，如果不是就回QQ
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    const n = Math.floor(Math.random() * 100);
    console.log(n);
    if (n % 2 == 0) resolve(n);
    else reject("QQ");
  }, 1000);
}).catch((err) => {
  console.error(err);
});
```

## `Promise.all([promise array])`

同時完成多個 Promise。如果任務結束，且都無意外錯誤，就會執行`then()`；反之則執行`catch()`處理錯誤。

```javascript
const f1 = fetch("/a.json");
const f2 = fetch("/b.json");
Promise.all([f1, f2])
  .then(([r1, r2]) => {
    console.log("jsons:", r1, r2);
    // jsons: {...} {...}
  })
  .catch((err) => {
    console.error(err);
  });
```

## `Promise.race([promise array])`

如同字面上意思，同時執行多個 Promise，只要最先完成 resolve 的，就會以這個 resolve 的結果執行 `then()`。

```javascript
const p1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 200, "p1");
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 300, "p2");
});
Promise.race([p1, p2]).then((result) => {
  console.log(result); // p1
});
```

## 參考資源

- [ES5 vs ES6 Promises](https://stackoverflow.com/questions/38424517/es5-vs-es6-promises)
- [ES5 to ESNext —  自 2015 以来 JavaScript 新增的所有新特性](https://zhuanlan.zhihu.com/p/59535309)
