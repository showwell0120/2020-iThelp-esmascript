# [Day07] ES2015(ES6) - 物件(Object)

今天介紹的是關於物件的處理，包括屬性的表示和方法的擴充。  
一起來看看吧！

## 屬性的表示

在 ES2015 中，物件屬性的擴充大大提升簡潔性以及彈性。主要提供的新特性有以下三種

- **變數名稱填入賦值**: 當填入變數名稱，其名稱會成為屬性名稱，而變數的值成為屬性值
  ```javascript
  let name = "One Punch Man";
  let lead = "Saitama";
  const data = { name, lead };
  // { name: "One Punch Man", lead: "Saitama"}
  ```
- **簡化新增方法屬性**: 除了可以像上面一樣變數賦值，也可直接在屬性名稱後加 `(){}` 新增函式
  ```javascript
  function sayHi() {
    console.log("Hello");
  }
  const data1 = { name, lead, sayHi };
  const data2 = {
    name,
    lead,
    sayBye() {
      console.log("Bye");
    },
  };
  ```
- **動態屬性名稱**: 屬性名稱以 `[variable]` 中括號包覆變數的形式，動態決定屬性名稱。我很喜歡這特性，在開發上也用上不少，算是很實用的語法!
  ```javascript
  const sns = ["fb", "ig", "line"];
  let data = {};
  sns.map((s, i) => (data[`sns_${s}`] = i));
  console.log(data);
  /*
    {
      sns_fb: 0
      sns_ig: 1
      sns_line: 2
    }
  */
  ```

## 靜態方法

### `Object.is(value1, value2)`

比較兩個值是否相等。回傳布林值。

在 ES5 中，比較兩個值相等需要靠 `==` 和 `===`(嚴格等於) 運算子來比較，可是這些運算子各自有些不合理的地方

- `==`: 會自動轉換型別 e.g. `1 == '1' //true`
- `===`:
  - `NaN`不等於自己 e.g. `NaN === NaN //false`
  - `+0` 等於 `-0` e.g. `0 === -0 //true`

因此在 ES2015 中，有在 Object 底下新增一個靜態方法 `Object.is` 為比較相等提供比較正確的方式。

以下列出在 `Object.is` 中會回 `true` 的情況

- 兩者都是 `undefined` / `null` / `NaN` / `true` / `false` / `+0` / `-0`
- 兩者為完全相等的非零數值 / 字串
- 兩者參考到同一個物件 / 陣列

```javascript
const arr = [1, 2, 3];
const _arr1 = arr,
  _arr2 = arr;
const obj = { name: "One Punch Man" };
const _obj1 = obj,
  _obj2 = obj;

Object.is(_arr1, _arr2); //true
Object.is(_obj1, _obj2); //true
Object.is([1, 2, 3], [1, 2, 3]); //false
Object.is({ name: "One Punch Man" }, { name: "One Punch Man" }); //false
```

### `Object.assign(target, obj1, obj2, ...)`

複製所有傳入物件的可列舉屬性，並合併到一個目標物件中。回傳被合併過後的目標物件。

什麼是可列舉屬性呢? 物件的屬性有分為以下兩種

- 存在於 `prototype`: 屬於不可列舉的屬性

  ```javascript
  const obj = { name: "One Punch Man" };
  obj.valueOf(); //{ name: "One Punch Man" }
  ```

  `obj` 雖然沒有宣告 `valueOf` 的方法，但是因為在 `Object` 的 `prototype` 中有這個方法。所以繼承 `Object` 的 `obj` 就能使用

- 存在於實體: 如果沒特別設定，一般屬於可列舉的屬性
  ```javascript
  const obj = { name: "One Punch Man", sayHi(){...} };
  obj.sayHi();
  ```
  我們在 `obj` 的實體上新增一個方法 `sayHi`，所以才能直接呼叫 `obj.sayHi()`

屬性能不能列舉，會影響到一些函式的結果，像是迭代(`for...in`、`Object.keys`)和 `JSON.stringify`等。

回到正題，當我們想把一些物件進行合併時，這個方法就能幫助物件進行合併。如果之間有屬性名稱相同時，會以後蓋前的方式取代掉。

要注意的地方是，目標物件同時也會被修改到。如果希望目標物件不被修改到，第一個參數改傳入 `{}`。

```javascript
const target = { a: 1, b: 2 };
const target1 = { a: 1, b: 2 };
const source = { b: 4, c: 5 };
const returnedTarget = Object.assign(target, source);
const returnedTarget1 = Object.assign({}, target, source);
console.log(target); // { a: 1, b: 4, c: 5 }
console.log(target1); // {a: 1, b: 2}
```

### Object Iterator (物件迭代器)

跟昨天提到的陣列迭代器一樣，ES2015 也為物件提供相似的方法來迭代可列舉屬性。根據回傳的內容不同有以下三個方法可使用

- `Object.keys`: 依序將每個屬性的名稱存到陣列
- `Object.values`: 依序將每個屬性的值存到陣列
- `Object.entries`: 依序將每個屬性的名稱與值存到陣列 A，再把陣列 A 存到陣列 B

```javascript
const object1 = {
  a: "somestring",
  b: 42,
};
Object.keys(object1); // ["a", "b"]
Object.values(object1); // ["somestring", 42]
Object.entries(object1); // [["a", "somestring"], ["b", 42]]
```

## 小結

我們發現在 ES2015 中，要處理物件變得輕鬆許多，也提供解讀性跟簡潔性更好的迭代方法，在物件操作上可以用更少程式來完成複雜的任務。

## 參考資源

- [JS 中的可列舉屬性與不可列舉屬性](https://www.itread01.com/content/1549409968.html)
- [Object.is()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/is)
- [[筆記] JavaScript ES6 中的物件的擴展（object literal extension）](https://pjchender.blogspot.com/2017/01/es6-object-literal-extension.html)
- [对象的新增方法](https://es6.ruanyifeng.com/#docs/object-methods)
- [对象的扩展](https://es6.ruanyifeng.com/#docs/object)
