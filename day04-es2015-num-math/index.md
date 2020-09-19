# [Day04] ES2015(ES6) - 數值與數學運算

ES2015在數值的判斷與運算多了很多擴充，還包含新的型別 `BigInt`的推出。今天就整理出幾個覺得比較常用和基本的特性。想要了解更多的，可以再前往底下的參考資源查看喔！

## 擴充判斷數值的方法

### `Number.isInteger()`
判斷數值是否為整數，回傳結果為布林值。

```javascript
Number.isInteger(25) //true
Number.isInteger(-88) //true
Number.isInteger(0) //true
Number.isInteger(3.14) //false
Number.isInteger(-8.2544) //false
```

### `Number.isNaN()`
判斷數值是否為`NaN`，回傳結果為布林值。

```javascript
Number.isNaN(NaN) // true
Number.isNaN('NaN') // false
Number.isNaN(true) // false
Number.isNaN(88) // false
```

### `Math.sign()`
判斷數值是正數、負數、或為0，回傳結果分別為：
  - 正數： **1**
  - 負數： **-1**
  - 0： **0**
  - -0： **-0**
  - 其他： **NaN**

```javascript
Math.sign(28) // 1
Math.sign(-5.6974) // -1
Math.sign(0) // 0
Math.sign(-0) // -0
Math.sign(NaN) // NaN
```

如果是字串，會先轉為數值類型再回傳。如果無法轉為數值，則回傳`NaN`。

```javascript
Math.sign('25.564') // 1
Math.sign('string') // NaN
```

## 擴充處理數值的方法

### `Math.trunc()`

將數值的小數點移除，只回傳整數的結果。
若是布林值，則回傳1或0。

```javascript
Math.trunc(45.1561) // 45
Math.trunc(-36.2542) // -36
Math.trunc(true) // 1
Math.trunc(false) // 0
Math.trunc(null) // 0
```

如果是字串，會先轉為數值類型再回傳。如果無法轉為數值，則回傳`NaN`。

```javascript
Math.trunc('45.1561') // 45
Math.trunc('-36.2542') // -36
Math.trunc('true') // NaN
Math.trunc('false') // NaN
Math.trunc('null') // NaN
```

## 減少全域方法的使用

在ES2015後，鼓勵是以模組化的方式開發，其中就包含降低全域方法的使用。所以像是`parseInt()`和`parseFloat()`，在Number物件裡也有實現同樣的方法。

### `Number.parseInt(numStr:string, radix:number)`

將輸入的字串轉成整數。如果無法轉為數值，則回傳`NaN`。

```javascript
Number.parseInt('-532');  //-532
Number.parseInt('  3  ');  //3
Number.parseInt('NaN');  //NaN
Number.parseInt('true');  //NaN
```

### `Number.parseFloat(numStr:string)`

將輸入的字串轉成浮點數。如果無法轉為數值，則回傳`NaN`。

```javascript
Number.parseFloat('-532.2546');  //-532.2546
Number.parseFloat('  3.14  ');  //3.14
Number.parseFloat('NaN');  //NaN
Number.parseFloat('true');  //NaN
```

## 小結
以Javascript來說，處理數值的方法，最主要就是來自Number和Math這兩個內建物件。   
今天認識了一些還蠻實用的方法，希望也能幫助到你囉！

## 參考資源

-[数值的扩展](https://es6.ruanyifeng.com/#docs/number)

