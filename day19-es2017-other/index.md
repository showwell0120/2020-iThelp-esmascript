# [Day19] ES2017(ES8) - 其他

## 字串

### `String.prototype.padStart(targetLength:number, padString?:string)`

`padString`預設為 `' ' `(空字串)。重複填充到字串的前面，直到到達指定的長度 `targetLength`後回傳。

如果 `targetLength` 小於原來的字串長度，則回傳原字串。

```javascript
"One Punch Man".padStart(20); // "       One Punch Man"
"One Punch Man".padStart(23, "-"); // "----------One Punch Man"
```

### `String.prototype.padEnd(targetLength:number, padString?:string)`

與 `padStart` 相似，不過填充的位置為字串後方。

```javascript
"One Punch Man".padEnd(20); // "One Punch Man       "
"One Punch Man".padEnd(23, "-"); // "One Punch Man----------"
```

以上兩種實體方法，主要目的為讓字串能有特定長度時可以使用。

## 物件

在[Day7](https://ithelp.ithome.com.tw/articles/10241983)有提到物件的迭代器。除了 `Object.keys`，在 ES2017 中有再擴充可以使用的方法。

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

### `Object.getOwnPropertyDescriptors(obj)`

回傳物件中實體屬性的詳細描述物件，包含

- **set**：setter 函式
- **get**：getter 函式
- **value**：屬性值
- **writable**：屬性值是否可修改覆寫
- **enumerable**：是否為可列舉屬性
- **configurable**：如果該屬性從物件中移除，此描述物件是否可作更動

這個方法的主要目的是搭配`Object.defineProperties` ，來解決 `Object.assign()` 無法正確複製 `get` & `set` 屬性的問題。

假設有個物件 obj 想複製到 obj2，以 `Object.assign`來寫的話，會無法正確讀取到 prop 這個 setter 屬性

```javascript
const obj1 = {
  set prop(v) {
    console.log(v);
  },
};
const obj2 = {};
Object.assign(obj2, obj1);
Object.getOwnPropertyDescriptor(obj2, "prop");
// {value: undefined, writable: true, enumerable: true, configurable: true}
```

如果使用 `Object.getOwnPropertyDescriptors(obj)` 的話，則可以取到 setter 函式。

```javascript
Object.defineProperties(obj2, Object.getOwnPropertyDescriptors(obj1));
Object.getOwnPropertyDescriptor(obj2, "prop");
// {get: undefined, enumerable: true, configurable: true, set: ƒ}
```

## 尾逗號（Trailing Commas）

在參數傳遞、物件、陣列等，允許在後面多加一個逗號`,`。

```javascript
fn(p1, p2);
const arr = [1, 2, 3];
const obj = { name, id };
```

這個標準主要有兩個好處

- 排列元素項目比較簡單。如果要調整最後一個元素到前面，較不容易發生錯誤
- 協助版本控制

## 參考資源

- [Object.getOwnPropertyDescriptors()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptors)
- [JS Object.defineProperty(): (5) 相關方法](https://ithelp.ithome.com.tw/articles/10203918)
- [es6 javascript 的对象 Object.getOwnPropertyDescriptors()](https://blog.csdn.net/qq_30100043/article/details/53424963)
