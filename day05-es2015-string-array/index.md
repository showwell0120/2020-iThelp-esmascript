# [Day05] 字串 (String)

今天介紹的是關於字串的處理，包括實體方法的擴充，以及對於字串宣告制定新的定義方式。   
我們來看看吧！

## 實體方法

### `str.includes(searchString:string, position?:number)`

從 str 中檢查 searchString 是否存在。結果回傳布林值。
position 可以指定在 str 中開始搜尋的索引值。預設值為 0。

```javascript
const str = "One Punch Man!!";             
const result1 = str.includes('Punch');      //true
const result2 = str.includes('Punch', 3);   //true
const result3 = str.includes('Punch', 5);   //false
```

### `str.startsWith(searchString:string, position?:number)`

從 str 中檢查是否以 searchString 開頭。結果回傳布林值。   
position 可以指定在 str 中開始搜尋的索引值。預設值為 0。

```javascript
const str = "One Punch Man!!";             
const result1 = str.startsWith('One');    //true
const result2 = str.includes('One', 4);   //false
```

### `str.endsWith(searchString:string, length?:number)`

從 str 中檢查是否以 searchString 結尾。結果回傳布林值。   
length 可以指定在 str 符合的長度。預設值為 str 的長度。

```javascript
const str = "One Punch Man!!";             
const result1 = str.endsWith('Man!!');     //true
const result2 = str.endsWith('Main!!', 2); //false
```

### `str.repeat(count:number)`

將 str 以重複 count 的次數回傳新的字串。

```javascript
const result = 'Man!'.repeat(3);  //Man!Man!Man!
```

## Template Literals（模板字面值）

這是ES2015中嶄新的特性。透過` `` `包覆，就能將運算式或變數和字串結合起來。另外也能支援字串的換行，成為多行字串。不僅可以提升可讀性，在撰寫上也輕鬆許多！

### 內崁變數

使用 `${...}` 將變數、運算式、函式等包覆，並置於想放的位置上。

```javascript
// ES5
var x=1, y=2;
const resultStr = "x加y等於：" + (x + y) + "。";

// ES2015
let x=1, y=2;
const resultStr = `x加y等於：${x + y}。`;

/* output:
x加y等於：3
*/
```

### 多行字串

```javascript
// ES5
// 需要在換行處加 \n
console.log("我最愛的動畫是: \n"+"One Punch Man!!");

//ES2015
console.log(`我最愛的動畫是:
One Punch Man!!
`);

/* output:
我最愛的動畫是:
One Punch Man!!
*/
```

## 小結

字串處理的部份，其實跟昨天的數值處理一樣，在 ES2015 中還有推出其他的擴充方法跟極值處理。這部分因為相對來說比較不常使用，有興趣的一樣可以前往參考資源查看喔！

## 參考資源
- [ES6 in Action: New String Methods — String.prototype.*](https://www.sitepoint.com/es6-string-methods-string-prototype/)
- [字符串的新增方法](https://es6.ruanyifeng.com/#docs/string-methods#String-raw)
- [字符串的扩展](https://es6.ruanyifeng.com/#docs/string)
