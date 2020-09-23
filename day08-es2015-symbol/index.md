# [Day08] ES2015(ES6) - Symbol

Symbol 是在 ES2015 中新增加的內建資料型態。今天就來認識新面孔，並且了解基本應用吧!

## `Symbol(description?:string)`

我們先來複習一下在 ES5 的資料型態有: `Number`、`String`、`Object`、`Boolean`、`null`、`undefined`共 6 種。

而 `Symbol`是在 ES2015 後的第 7 種資料型態。以一句話來介紹，以這種型態宣告的值，每次都是不同的。

這種資料型態的出現，也讓物件在新增屬性上有相當的擴充。

在 ES5 以前，物件的屬性名稱只能接受字串類型；但在 ES2015 後，屬性名稱的類型除了字串以外，還可以接受`Symbol`型態的值。

這麼做的用意是，因為每次宣告的值都不一樣，所以可以保證不會因名稱重複，而被覆寫屬性值的問題。

先看看簡單的例子。

```javascript
let s = Symbol(),
  s1 = Symbol();
typeof s; // symbol
console.log(s === s1); // false
```

在宣告`Symbol`的變數時，可選擇性的傳入關於變數的描述。並且以 `smbl.description` 取得描述。

```javascript
const s = Symbol("One Punch Man");
console.log(s); // Symbol(One Punch Man)
console.log(s.description); // One Punch Man
```

在物件中如何以`Symbol`建立屬性以及取用呢？直接以例子看看

```javascript
const prop = Symbol('prop is property name');

// way 1
const obj = {...};
obj[prop] = "Hi";
obj.prop = "Bye";

console.log(obj.prop) // "Bye" 因為用點運算子連接的屬性名稱會被當作字串
console.log(obj[prop]) // "Hi"

// way 2: Object Literals
const obj = {
    [prop]:"Hi"
};

// way 3: Object.defineProperty
const obj = {...};
Object.defineProperty(obj, prop, {value: 'Hi'});
```

## `Symbol.for(key?:string)`

如果要建立全域的常數可以重複使用時，使用 `Symbol.for`來宣告。如果 `key` 已經存在，就不會再重新建立新的變數。

```javascript
let s = Symbol.for("Woman"),
  s1 = Symbol.for("Woman");

console.log(s === s1); // true
```

## `Symbol.keyFor(symbol)`

用來取得以 `Symbol.for` 宣告的全域常數的 key 值。

```javascript
let s = Symbol.for("Woman"),
console.log(Symbol.keyFor(s)); // "Woman"
```

## `Object.getOwnPropertySymbols(obj)`

在昨天，我們有提到物件的迭代中的可列舉屬性。而 `Symbol`型態的屬性名稱比較特別，這類的屬性無法使用
`Object.keys()`、`for...in`、`JSON.stringify()`等迭代可列舉屬性的方法。

如果要迭代這類屬性的話，則需使用 `Object.getOwnPropertySymbols`，回傳各 symbol 值的陣列。

```javascript
const obj = {
  name: "One Punch Man",
  lead: "Saitama",
  [Symbol("prop1")]: "prop1",
  [Symbol.for("prop2")]: "prop2",
};

for (let i in obj) {
  console.log(i);
}
// "One Punch Man"
// "Saitama"

const smblProps = Object.getOwnPropertySymbols(obj);
// [Symbol(props1), Symbol(props2)]
```

最後，我們試著以最常使用的場景，來體驗看看 Symbol 的應用吧。

假設我們要以 `switch case` 根據資料裡的 type 屬性來寫判斷的處理函式。

```javascript
function handleFile(data) {
  switch (data.type) {
    case T_PDF:
      convertPDF(data);
      break;
    case T_DOC:
      convertDOC(data);
      break;
    case T_IMAGE:
      convertImage(data);
      break;
    default:
      throw new Error("Unknown type of data");
  }
}
```

我們只在乎 type 的常數有沒有存在，而且值不重複。而不需要在意值的內容是什麼。

```javascript
// ES5
const T_PDF = "T_PDF",
  T_DOC = "T_DOC",
  T_IMAGE = "T_IMAGE";

//ES2015
const T_PDF = Symbol(),
  T_DOC = Symbol(),
  T_IMAGE = Symbol();
```

## 小結

今天介紹的 `Symbol`是一種嶄新的資料型態，雖然已經推出 5 年了，可是還是很少應用在專案上。今天了解在特定的開發情境中，其實用 `Symbol` 還蠻恰當的。希望大家也能嘗試著大膽使用看看喔!

## 參考資源

- [理解和使用 ES6 中的 Symbol](https://cloud.tencent.com/developer/article/1191039)
- [Symbol](https://es6.ruanyifeng.com/#docs/symbol)
- [JavaScript ES6 Symbol 資料型態](https://www.fooish.com/javascript/ES6/Symbol.html)
