[Day10] ES2015(ES6) - 函式(Function)

## 參數的預設值

在 ES5 沒有預設值，也沒有 Typescript 協助開發時檢查的情況，通常在寫有參數的函式時，我們在一開始得先寫參數的檢查，就像這樣

```javascript
function func(p1, p2) {
  if (!p1 || !p2) return;
  // ...
}
```

但是在 ES2015 中，函式允許我們為參數設定預設值。當呼叫函式時沒傳入參數時，函式會以預設值來帶入執行。

```javascript
function func(p1 = 1, p2 = 2) {
  // ...
}
```

不過需要注意的是，如果使用 Typescript 開發的話，當使用 `?:` 宣告參數型別為選擇性參數時，則不能再設定預設值。通常編輯器也會出現紅線提醒。

```javascript
function func(p1 = 1, p2?: number) {
  // ...
}
```

另外在 coding style 上，會宣告預設值的參數通常會是在後面。因為就算是這類的參數，在呼叫時也沒有辦法以空位的方式跳過忽略。所以為了減少呼叫時參數設定的錯誤，會避免把可選擇性傳入的參數放在中間。

```javascript
// not good
function func(p1, p2 = 2, p3) {
  return [p1, p2, p3];
}

func(1); // [1, 2, undefined];
func(1, , 3); // 出現錯誤 Uncaught SyntaxError: Unexpected token ','
func(1, undefined , 3);  // [1, 2, 3]
```

```javascript
// better
function func1(p1, p2, p3 = 3) {
  return [p1, p2, p3];
}
func1(1, 2); // [1, 2, 3]
```

## 參數的解構賦值 (Destructuring)

如果參數數量過多時，通常會包成物件的方式傳遞參數。因此我們可以利用解構賦值的特性，方便我們在函式中，直接取用參數。這部分如果有寫過 React 的 Function Component 應該很熟悉，因為 props 是個物件，為了方便撰寫，我們通常會以這種方式直接取得特定的 prop。

```javascript
function fun({ p1, p2 }) {
  return p1 + p2;
}
```

```javascript
interface I_CompProps {
  id: number;
  name: string;
}
const ReactComp: React.FC<I_CompProps> = ({ id, name }) => {
  // ...
};
```

另外解構賦值也可以結合參數的預設值。

```javascript
function fun({ p1, p2 = 2 }) {
  return p1 + p2;
}
fun({ p1: 1 }); // 3
fun({ p1: 1, p2: 4 }); //5
```

## 箭頭函式 (Arrow Function)

Arrow Function 是允許讓開發者在宣告函式時，可以省去寫 `function` 的關鍵字，以 `=>` 來代替，寫法上跟以往有蠻大的不同，在一些情況下的寫法方便許多。

- 當參數只有一個時，可以省去包裹參數的 `()`
- 當函式只需一行的話，可以省去 `return` 關鍵字 和 包裹執行函式作用域的`{}`。不過回傳值是 **物件** 的話，物件外面需要以 `()` 包裹

```javascript
//ES5
const f1 = function (a) {
  return a * a;
};
//Arrow function
const f2 = (a) => a * a;
const f3 = (a) => ({ name: a });
```

### 需要注意`this`

先複習一下`this`。簡單來說，是指執行函式時，看誰是呼叫的人就指向誰。

例如在瀏覽器中，以全域宣告一個函式 `funcA`後直接呼叫執行，這時的`this`預設指向 **window**；
而如果在物件 Obj 中新增一個函式`funcB`並呼叫執行，這時的`this`預設指向 **Obj**。

```javascript
function funcA() {
  console.log("this:", this);
}
funcA(); //this: Window {...}

const Obj = {
  name: "One Punch Man",
  logThis() {
    console.log("this:", this);
  },
  logName() {
    console.log(this.name);
  },
};
Obj.logThis(); // this: {name: "One Punch Man", logThis: ƒ, logName: ƒ}
Obj.logName(); // One Punch Man
```

在使用箭頭函式宣告時，因為本身並沒有自己的`this`，所以會固定指向上一層作用域的`this`。

```javascript
function f1() {
  this.name = "One Punch Man";
  setTimeout(() => {
    console.log("name:", this.name);
  }, 1);
}

// 轉換為ES5
function f1() {
  this.name = "One Punch Man";
  var _this = this;
  setTimeout(function () {
    console.log("name:", _this.name);
  }, 1);
}
```

這個特性其實很適合對事件的 callback 函數進行封裝，我們做個實驗來看看。

```javascript
const Handler = {
  _name: "One Punch Man",
  _doSomething: function (type) {
    console.log("Handling " + type + " for " + this._name);
  },

  // 正確寫法
  // callback 使用箭頭函式宣告，h1使用傳統函式宣告
  // this 指向 h1 的所屬物件(Handler)
  h1: function () {
    document.addEventListener(
      "click",
      (event) => {
        console.log("h1: ", this);
        // h1:  {_name: "One Punch Man", _doSomething: ƒ, thisIsDocument1: ƒ, thisIsDocument2: ƒ, thisIsWindow: ƒ}
        this._doSomething(event.type);
        // Handling click for One Punch Man
      },
      false
    );
  },

  // callback 使用傳統函式宣告，h2 使用傳統函式宣告
  // this 指向 callback 的所屬物件(document)
  h2: function () {
    document.addEventListener(
      "click",
      function (event) {
        console.log("h2: ", this);
        // h2:  #document
        this._doSomething(event.type);
        // Uncaught TypeError: this.doSomething is not a function
      },
      false
    );
  },

  // callback 使用傳統函式宣告，h3 使用箭頭函式宣告
  // this 指向 callback 的所屬物件(document)
  h3: () => {
    document.addEventListener(
      "click",
      function (event) {
        console.log("h3: ", this);
        // h3:  #document
        this._doSomething(event.type);
        // Uncaught TypeError: this.doSomething is not a function
      },
      false
    );
  },

  // callback使用箭頭函式宣告，h4 使用箭頭函式宣告
  // this 指向 h4 的所屬物件，可是 h4 是箭頭函式，本身無 this，所以會指向全域的 window
  h4: () => {
    document.addEventListener(
      "click",
      (event) => {
        console.log("h4: ", this);
        //h4:  Window {…}
        this._doSomething(event.type);
        // Uncaught TypeError: this.doSomething is not a function
      },
      false
    );
  },
};
```

另外還有一個特性是，箭頭函式可以讓 `this` 指向定義時所在的作用域，而不是執行時所在的作用域。

```javascript
function Timer() {
  this.s1 = 0;
  this.s2 = 0;

  setInterval(() => this.s1++, 1000);

  setInterval(function () {
    this.s2++;
  }, 1000);
}

const timer = new Timer();

setTimeout(() => console.log("s1: ", timer.s1), 5000);
setTimeout(() => console.log("s2: ", timer.s2), 5000);

// s1: 5 -> this 指向的是定義時所在的作用域 timer
// s2: 0 ->  this 指向的是執行時所在的作用域 Window
```

### 不適合以及不能用的地方

- 需要動態指向 `this`。因為箭頭函式沒有自己的 `this`，所以也不能用`call()`、`apply()`、`bind()`來改變 `this` 的指向。
- 不能當建構函式，也就是不能用 `new` 產生函式實體
- 無法使用 `arguments`的物件。在箭頭函式中並不存在
- 不可以作為 `Generator` 函式，之後會再介紹到

## 小結

今天的大重點是後面提到的箭頭函式，因為使用上真的需要先對 `this` 有一定掌握，才不會一直採雷出 bug。如果大家覺得使用上有什麼心得的話，可以留言討論喔。

## 參考資源

- [ES5 to ESNext —  自 2015 以来 JavaScript 新增的所有新特性](https://zhuanlan.zhihu.com/p/59535309)
- [鐵人賽：JavaScript 的 this 到底是誰？](https://wcc723.github.io/javascript/2017/12/12/javascript-this/)
- [函数的扩展](https://es6.ruanyifeng.com/#docs/function#%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0)
