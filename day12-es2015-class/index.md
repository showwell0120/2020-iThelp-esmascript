# [Day12] ES2015(ES6) - 類別(class)

在 Javascript 中，實體的建立機制主要是 **prototype-based**為基礎的物件導向設計。在 ES5，我們需要新增建構函式，來產生所謂的**原型**，並以 `prototype` 進行原型的擴充 ，最後再以 `new` 的關鍵字建立實體。

在 ES2015 推出了`class`，在寫法上跟**class-based**為基礎的物件導向設計很相似，但是骨子裡還是 prototype-based 的機制。所以只能說是 ES5 寫法上的語法糖，在使用上需要注意。

接著就直接從關鍵字簡要說明，來看看怎麼寫類別吧。

## 建立與初始 - `class` ＆`constructor`

以 `class` 加上類別名稱進行宣告。 `class Anime { //... }`

當以 `new` 建立實體時，如果要對傳入的參數進行初始化的話，可在 `constructor` 的程式區塊中執行。

```javascript
class Comic {
  constructor(name) {
    this.name = name;
  }
  printName() {
    return `NAME:${this.name}`;
  }
}

let c = new Comic("One Punch Man");
c.printName(); // NAME: "One Punch Man"
```

## 繼承 - `super` & `extends`

`super`的關鍵字有兩個使用時機

- 在執行建構式時，將初始父類別用的參數透過 `super()` 傳入
- 在類別方法中取用父類別的屬性或方法時，呼叫 `super.XXX`取得

子類別可透過 `extends` 來繼承父類別。

```javascript
class Anime extends Comic {
  constructor(name, op) {
    super(name);
    this.op = op;
  }
  printName() {
    return `${super.printName()}(動畫)`;
  }
  printOP() {
    return `OP:${this.op}`;
  }
}
let a = new Anime("彼女、お借りします", "センチメートル");
a.printOP(); // "OP:センチメートル"
```

## 存取 - `set` & `get`

在方法前面加上前綴字 - `set` 或 `get`，可設定某個私有屬性的輸出(Getter)與輸入(Setter)。

在名稱命名上，私有屬性的名稱前面需加上 **\_**，而 Getter 和 Setter 的名稱需和屬性名稱相同。

當使用 Setter 時，直接以等號指派值進去即可。而當類別只有 Setter 時，表示此屬性僅能設值，而無法取值。

```javascript
class Anime extends Comic {
  constructor(name, op) {
    super(name);
    this.op = op;
  }
  printName() {
    return `${super.printName()}(動畫)`;
  }
  printOP() {
    return `OP:${this.op}`;
  }

  set year(value) {
    this._year = value;
  }

  get year() {
    return this._year;
  }
}

let a = new Anime("Re:0");
a.year = 2020;
console.log(a.year); // 2020
```

## `static`

如果類別中有方法是只有類別可使用，其他繼承的子類別無法使用的話，可以在方法前面加 `static` 前綴字。

```javascript
class Comic {
  constructor(name, author) {
    this.name = name;
  }
  printName() {
    return `NAME:${this.name}`;
  }
  static printInfo() {
    console.log("This is Comic Class");
  }
}
let a = new Anime("Re:0", "STYX HELIX");
a.printInfo(); // Error  a.printInfo is not a function
Comic.printInfo(); // This is Comic Class
```

## 小結

今天了解如何以類別建立實體模型，這樣的寫法雖然貼近大型架構用的語言(Java, C#等)，但底層的機制仍不大一樣。所以在開發時，需要注意在繼承或擴充類別時，是否會造成其他類別或實體的影響喔。

## 參考資源

- [ES5 to ESNext —  自 2015 以来 JavaScript 新增的所有新特性](https://zhuanlan.zhihu.com/p/59535309)
- [你懂 JavaScript 嗎？#20 行為委派（Behavior Delegation）](https://cythilya.github.io/2018/10/27/behavior-delegation/#widget-%E9%A1%9E%E5%88%A5)
- [你懂 JavaScript 嗎？#21 ES6 Class](https://cythilya.github.io/2018/10/28/es6-class/)
