# [Day20] ES2018(ES9) - 非同步<未完>

## `for - await - of`

```javascript
let html = "";
const asyncItr = {
  [Symbol.asyncIterator]() {
    return {
      i: 1,
      next() {
        if (this.i < 4) {
          return Promise.resolve({ value: this.i++, done: false });
        }
      },
    };
  },
};
async function printNumbers() {
  for await (let v of asyncItr) {
    html = `${v}</br>`;
    document.write(txt);
  }
}
printNumbers();

/* output
1
2
3
*/
```

## `Promise.prototype.finally()`

```javascript
// 一秒後隨機取數，如果是偶數就會該數字，如果不是就回QQ
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    const n = Math.floor(Math.random() * 100);
    console.log(n);
    if (n % 2 == 0) resolve(n);
    else reject("QQ");
  }, 1000);
})
  .then((n) => {
    console.log("2nd then", n);
  })
  .catch((err) => {
    console.error(err);
  })
  .finally(() => {
    console.log("finally done");
  });

/* output
82
2nd then 82
finally done
*/
```

## 參考資源

- [ES2018（ES9） 带来的重大新特性 – JavaScript 完全手册（2018 版）](https://www.html.cn/archives/9990)
- [What is the importance of 'for await...of' statement in JavaScript?](https://www.tutorialspoint.com/what-is-the-importance-of-for-await-of-statement-in-javascript)
