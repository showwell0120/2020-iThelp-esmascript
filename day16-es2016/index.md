# [Day16] ES2016(ES7)

從 ES2016 開始的改版，規模並不像 ES2015 般那麼的龐大。以目前來看大部分是些內建型別或與語法的擴充。以 ES2016 來說，主要只有推出兩個標準：

## `includes(element)`

在 ES2015 以前，如果要查詢在陣列或字串中，某個元素是否存在。最常用的方法就是 `indexOf`。像這樣：

```javascript
const arr = [1, 2, 3];
const hasOne = arr.indexOf(1) > -1;
```

不過這樣子以陳述式表達的寫法，撰寫上不是那麼方便，也缺乏語意性。因此在 ES2016 擴充了查詢語法 `includes`。直接將想查詢的元素放入參數，並以布林值回傳是否存在。

```javascript
[1, 2, 3].includes(4); // false
"One Punch Man".includes("M"); // true
```

## 次冪運算子 `base ** exponent`

`**`這個運算子相當於 `Math.pow(base:number, exponent:number)`。意思是求 base 數值的 exponent 次方。這個運算子在許多語言，像是 Python、Ruby、MATLAB 等都已經被標準化，因此在這版推出，主要與其他語言有一致性，並在寫法上更簡潔。

```javascript
const n = 3 ** 4; // 81
// 等於
const n = Math.pow(3, 4); // 81
```

## 參考資源

- [ES2016（ES7） 的改进 – JavaScript 完全手册（2018 版）](https://www.html.cn/archives/9965)
