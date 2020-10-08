# [Day23] ES2020(ES11) - 運算子

今年的標準 - ES2020 在年中的時候熱騰騰地推出，不曉得有多少人已經在用了呢？

跟 ES6 以後的變更差不多，沒有到說有非常大的改革。不過今年推出的特性其實都算蠻實用的，對於開發上的效率算頗有幫助。所以這裡大致依照特性的分類分為三天來整理。分別是 -

- 運算子
- 模組
- 內建物件

今天先來看看多了哪些運算子吧！

## Optional Chaining - `?!`

在以前如果要操作層次很深的屬性值或元素之前，我們難免都要寫一段又臭又長的判斷式來看它是否存在。像這樣：

```javascript
const hasProp3 = obj && obj.prop1 && obj.prop1.prop2 && obj.prop1.prop2.prop3;
if (hasProp3) {
  // ...
  // works
}
if (obj.prop1.prop2.prop3) {
  // ...
  // 如果其中一個值不存在，就會出現意外錯誤 Uncaught TypeError: Cannot read property ...
}
```

但是在 ES2020，我們可以用 `?!` 直接省去一層層的判斷，並且在物件或陣列中都可以使用。在開發上深深覺得很方便，可讀性跟維護性都提升許多。

```javascript
//object
const hasProp3 = obj?!prop1?!prop2?!prop3;
if (hasProp3) {
  // ...
  // also works
}

//array
const has8thElem = arr?.[7];
if(has8thElem) {
    // ...
}
```

## Nullish Coalescing Operator - `??`

以前在進行變數宣告時，我們會需要先判斷有沒有特定的值或變數存在，如果有則指派，沒有的話就給定預設值。寫法有以下兩種 -

```javascript
// 1. 使用條件運算子
const varA = a1 ? a1 : a2;

// 2. 使用or運算子
const varB = b1 || b2;
```

可是上面的寫法會有個漏洞 - 當 a1 和 b1 等於 **0** 或 **false** 時，使用條件運算子或是 or 運算子，都會被當成是不成立的情況。明明有值或變數存在，但是卻被指派了預設值，造成程式上的錯誤。

在以前我們為了避免這樣的錯誤，可能會寫成這樣 -

```javascript
const hasA1 = al && al !== undefined && al !== null;
const varA = hasA1 ? a1 : a2; // 避免 0 或 false 的誤判
```

在 ES2020，推出一個很方便的運算子`??`，用法與 or 運算子相似。這個運算子相當於上面例子`hasA1`做的事情，不過可以減少額外的判斷撰寫。

```javascript
const varA = a1 ?? a2; // 只有在 al 為 undefined 或 null 時才會指派 a2
```

## 參考資源

- [10 New JavaScript Features in ES2020 That You Should Know](https://www.freecodecamp.org/news/javascript-new-features-es2020/)
- [ES2020 新特性](https://juejin.im/post/6844904080955932679)
