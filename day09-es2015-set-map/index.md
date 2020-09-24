# [Day09] ES2015(ES6) - Set & Map

今天介紹的是 ES2015 中新增加的兩種資料結構 － **Set** 跟 **Map**。  
這兩種物件在擁有的屬性跟方法上，都非常相似。只是 **Set** 長的比較像陣列，而**Map**比較像物件。一起認識看看吧!

## `Set`

Set 跟陣列有點像，都是一種有順序性地儲存多筆資料的結構。不一樣的地方是，Set 裡的值都是唯一的。

概念跟名詞上就是延伸數學中的集合(Set)，當有值被存入結構裡時，Set 內部會先執行 `===(嚴格等於)` 來判斷值是否已存在，如果已經有的話就會忽略。

### `new Set(iterable?: Iterable)`

在建立 Set 類型的結構，我們要以 `new` 的方式建立，並且可選擇性地傳入初始資料，例如陣列，Node List 等。

```javascript
let set1 = new Set();
let set2 = new Set(["a", "b"]);
```

接著來實際介紹 Set 的常用屬性跟方法。

### 實體屬性

#### `set.size`

取得 set 實體中元素的個數。

```javascript
let set1 = new Set([1, 2, 3, 3, 3, 4]);
console.log(set1.size); // 4, Set內部會移除重複值再計算個數
```

### 實體方法

Set 實體可以使用新增、刪除以及查詢等語法來管理。  
不過需要注意的是，如果傳入的元素是 **物件或陣列** 的值而不是參考的話，還是會被當作兩個不同的元素處理喔。

#### `set.add(value)`

新增元素，回傳 set 實體本身。

```javascript
let set = new Set();
set
  .add(1)
  .add("One Punch Man")
  .add({ id: 001 })
  .add(NaN)
  .add(true)
  .add(NaN)
  .add({ id: 001 });
//  {1, "One Punch Man", {id: 001}, NaN, true, {id: 001}}
```

#### `set.delete(value)`

刪除元素，回傳布林值。

```javascript
let set1 = new Set([1, 2, 3, 3, 3, 4, { id: 001 }]);
set1.delete(1); // true
set1.delete(5); // false
set1.delete({ id: 001 }); // false
```

#### `set.has(value)`

確認實體中是否含有特定元素，回傳布林值。

```javascript
let set1 = new Set([1, 2, 3, { id: 001 }, NaN, [5, 6], true, null, undefined]);
set1.has(4); // false
set1.has({ id: 001 }); // false
set1.has([5, 6]); // false
set1.has(NaN); // true
set1.has(null); // true
set1.has(undefined); // true
set1.has(true); // true
```

#### `set.clear()`

清空所有元素，無回傳值。

```javascript
let set1 = new Set([1, 2, 3, { id: 001 }, NaN, [5, 6], true, null, undefined]);
set1.clear();
console.log(set1); // {}
```

#### 迭代與遍歷

set 實體可以使用以下方法取得迭代後的處理值或遍歷。

- `set.keys()` & `set.values()` : 在 Set 裡，並沒有屬性值的概念，因此這兩種都是回傳含有元素值的 Set 迭代器
- `set.entries()` :對應每個元素產生 key 跟 value 都是元素值的鍵值對，並回傳 Set 迭代器
- `set.forEach((value1, value2, set) => any)` : 遍歷 set 實體
- `for (let v of set) {...}` : 遍歷 set 實體

```javascript
let set1 = new Set([1, 2, 3]);

const keys = set1.keys(); // SetIterator {1, 2, 3}

const values = set1.values(); // SetIterator {1, 2, 3}

const entries = set1.entries(); // SetIterator {1 => 1, 2 => 2, 3 => 3}

set1.forEach((value1, value2, set) => console.log(value1, value2, set));
/*
1 1 Set(3) {1, 2, 3}
2 2 Set(3) {1, 2, 3}
3 3 Set(3) {1, 2, 3}
*/

for (let v of set1) {
  console.log(v);
}
/*
1
2
3
*/
```

#### `WeakSet`

WeakSet 基本上跟 Set 類似，只差在 WeakSet 只接受 **物件** 作為元素值。

在 WeakSet 裡的物件，不會被 **Garbage Collection** 作為參考，也就是所謂的 **Weakly Reference**。所以當物件被回收時，對應的元素就會被刪除，這樣可以避免 **Memory Leak** 的問題。

因為只能存物件的特性，所以缺少可遍歷的方法，只剩 `has`、`add`、`delete` 可使用。

## `Map`

Map 跟物件很像，都是鍵值對的結構。不過區別的地方在於，物件的屬性名稱只能接受字串或是 symbol 的類型；而 Map 的屬性名稱則是可以允許任何的資料形態。

另外存在 Map 裡的資料是有順序性的。當遍歷或迭代的時候，為依照寫入順序進行處理。所以當如果要建立一個 Dictionary 的資料結構時，Map 會是一個比物件好的選擇。

### `new Map(iterable?: Iterable)`

在建立 Map 類型的結構，我們要以 `new` 的方式建立，並且可選擇性地傳入初始資料，例如陣列，Node List 等。

```javascript
let map = new Map();
```

### 實體屬性

#### `map.size`

取得 map 實體中元素的個數。

```javascript
let map1 = new Map();
console.log(map1.size); // 0
```

### 實體方法

#### `map.set(key, value)`

新增新的鍵值對。如果屬性名稱存在，則會被新的值覆蓋。回傳 map 實體本身。

```javascript
let map1 = new Map();
map1.set(123, ["a", "b", "c", ""]);
map1.set("Hi String!", 12345);
map1.set({ id: 001 }, null);
map1.set("Hi String!", 111111);
/*
Map(3) {123 => Array(4), "Hi String!" => 111111, { id: 001 } => null}
*/
```

#### `map.get(key)`

以屬性名稱 key 取得值，如果沒有，則回 `undefined`。

```javascript
let map1 = new Map();
map1.set("Hi String!", 12345);
map1.get("Hi String!"); // 12345
map1.get(123); // undefined
```

#### `map.delete(key)`

以屬性名稱 key 刪除鍵值對，回傳布林值。

```javascript
let map1 = new Map();
map1.set("Hi String!", 12345);
map1.delete("Hi String!"); // true
map1.delete(123); // false
```

#### `map.has(key)`

以屬性名稱 key 查詢鍵值對，回傳布林值。

```javascript
let map1 = new Map();
map1.set("Hi String!", 12345);
map1.has("Hi String!"); // true
map1.has(123); // false
```

#### `map.clear()`

清空所有鍵值對，無回傳值。

```javascript
let map1 = new Map();
map1.set("Hi String!", 12345);
map1.clear();
console.log(map1); // {}
```

#### 迭代與遍歷

map 實體可以使用以下方法取得迭代後的處理值或遍歷。

- `map.keys()` : 回傳 map 實體裡的所有屬性名稱
- `map.values()` : 回傳 map 實體裡的所有屬性值
- `map.entries()` :對應每個元素產生 `[key,value]` 的陣列，並回傳 Map 迭代器
- `map.forEach((value, key, map) => any)` : 遍歷 map 實體
- `for (let v of map) {...}` : 遍歷 map 實體

```javascript
const map = new Map([
  ["a", 1],
  ["b", 2],
  ["c", 3],
]);

const keys = map.keys(); // MapIterator {"a", "b", "c"}

const values = map.values(); // MapIterator {1, 2, 3}

const entries = map.entries(); // MapIterator {"a" => 1, "b" => 2, "c" => 3}

map.forEach((value, key, map) => console.log(value, key, map));
/*
1 "a" Map(3) {"a" => 1, "b" => 2, "c" => 3}
2 "b" Map(3) {"a" => 1, "b" => 2, "c" => 3}
3 "c" Map(3) {"a" => 1, "b" => 2, "c" => 3}
*/

for (let v of map) {
  console.log(v);
}
/*
["a", 1]
["b", 2]
["c", 3]
*/
```

#### `WeakMap`

跟 WeakSet 類似，WeakMap 只接受**物件**作為屬性名稱的值。機制上跟 WeakSet 一樣，都是防止 **Memory Leak**的問題。最典型的應用是產生 DOM 的 Dictionary。

```javascript
let btn = document.getElementById("btn");

let wm = new WeakMap();
wm.set(btn, { click: 0 });

btn.addEventListener(
  "click",
  () => {
    let btnData = wm.get(btn);
    btnData.click++; // 當點擊btn時，累加次數
  },
  false
);
```

## 小結

今天學到的都是很實用的資料結構。對於處理資料上可以有更好的擴充性。  
希望可以幫助到你。

## 參考資源

- [JavaScript ES6 Set and WeakSet Object 物件](https://www.fooish.com/javascript/ES6/Set-and-WeakSet.html)
- [JavaScript ES6 Map and WeakMap Object 物件](https://www.fooish.com/javascript/ES6/Map-and-WeakMap.html)
