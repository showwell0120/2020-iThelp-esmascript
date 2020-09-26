# [Day11] ES2015(ES6)＆ES2018(ES9) - 剩餘/展開運算子(Rest/Spread Operator)

在 ES2015 中推出的新的運算子 **`...`**，並且針對使用對象和情境有不同用途

- **展開(Spread)**: 將對象裡的元素展開成個別的值。常用在將對象進行 **淺拷貝(clone)**。
- **剩餘(Rest)**: 跟展開的概念有點相反，集合不確定個數或剩餘的元素，並回傳為陣列或物件。常使用在 **參數傳遞** 上。

接著分別來看看如何使用吧！

## 展開運算子

在使用對象上，只要是 **可迭代** 的內建物件，像是 `String`、`Array`、類陣列(`arguments`、NodeList)，到新的型別物件 `Set`、`Map` 都能使用。

### 字串

```javascript
const str = "One Punch Man";
const arr = [...str];
// ["O", "n", "e", " ", "P", "u", "n", "c", "h", " ", "M", "a", "n"]
```

### 陣列

```javascript
const arr1 = ["a", "b", "c"];
const arr2 = ["e", "f", ...arr1]; // ['e', 'f', 'a', 'b', 'c']
const arr1_1 = [...arr1]; // ["a", "b", "c"] 將 arr1 clone 到 arr1_1
```

在函式的參數傳遞上，可將參數陣列與展開運算子結合。

```javascript
const sumFunc = (a, b, c) => a + b + c;
const arr = [1, 2, 3];
const result = sumFunc(...arr1); // 6
```

### 物件

```javascript
const obj1 = { name: "One Punch Man", age: 28 };
const obj1_1 = { ...obj1 };
// {name: "One Punch Man", age: 28}  將 obj1 clone 到 obj1_1
```

## 剩餘運算子

最常使用的情況是將 **不確定個數的參數群** 作為一組變數來傳遞到函式；另外則是結合解構賦值使用，將剩下的元素指派到一個變數中。

### 函數參數

這裏可以跟上面的展開運算子的陣列實例比較看看。一個是固定個數的參數，另一個則是不限制參數個數。同樣是加總函式，實作內容跟擴充性都有差別。

```javascript
const sumFunc = (...args) => {
  let result = 0;
  args.forEach((n) => (result += n));
  return result;
};
const result1 = sumFunc(2); // 2
const result2 = sumFunc(3, 53, 5, 64); // 125
```

### 物件屬性

這個特性在 ES2018 中才正式推出。在物件上可以搭配解構賦值將剩餘的屬性指派到一個變數。不過要注意的地方是，
需要以實際的物件值進行指派。

```javascript
const obj = { name: "One Punch Man", age: 28, lead: "Saitama", gender: "male" };
const { name, lead, ...oherProps } = obj;
console.log(otherProps); // Uncaught ReferenceError: otherProps is not defined
```

```javascript
const { name, lead, ...oherProps } = {
  name: "One Punch Man",
  age: 28,
  lead: "Saitama",
  gender: "male",
};
console.log(otherProps); // { age: 28, gender: "male" }
```

## 小結

在[這篇](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part4/rest_spread.html)有整理出相關的 coding style 建議，雖然有些不是強制，不過可以幫助大家更理解這個運算子使用的時機。

- 以剩餘運算子`...`代替函式的隱藏屬性 `arguments`
- `...`在寫法上要緊鄰後面的對象
- 以展開運算子取代 `slice`、`concat` 跟陣列處理有關的寫法
- 以展開運算子取代 `Object.assign` 等有關物件的淺拷貝寫法
- 以展開運算子取代 `fn.apply(this, [args])` 等作為不確定參數個數的傳遞方式

## 參考資源

- [ES5 to ESNext —  自 2015 以来 JavaScript 新增的所有新特性](https://zhuanlan.zhihu.com/p/59535309)
- [展開運算符與其餘運算符](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part4/rest_spread.html)
