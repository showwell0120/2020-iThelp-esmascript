# [Day05] ES2015(ES6) - 陣列(Array)

今天介紹的是關於陣列的處理，包括實體方法和靜態方法的擴充。  
我們來看看吧！

## 靜態方法

### `Array.from(obj, mapFn?:Function, thisArg?:any)`

將 **類陣列(array-like)** 或 **可迭代(iterable)** 的物件，轉換成陣列，並回傳新的實體。

類陣列顧名思義就是很像陣列，像是會有 `length` 的屬性及索引化的元素，但卻不是陣列的物件。例如:字串、NodeList 等

而可迭代(iterable)的物件像是下一篇會提到的 `Map` 和 `Set` 這種物件，可以透過迭代的方式取到元素。

將這些物件轉換成陣列的目的，通常是要對這些物件使用 Array 提供的 API 進行操作，像較常見的是使用 `map`。因此在第二個選擇性的參數 `mapFn`，可以帶入 map 函式來遍歷元素；第三個選擇性的參數 `thisArg` 則是指定 `mapFn` 的 `this` 對象。

舉例練習看看。

```javascript
const str = "ABCDE";

const arr1 = Array.from(str, (chara) => chara.repeat(3));
// 等同於以下寫法
const arr2 = Array.from(str).map((chara) => chara.repeat(3));

// output:  ["AAA", "BBB", "CCC", "DDD", "EEE"]
```

### `Array.of(element1:any, element2?:any, ...)`

為參數裡的元素們建立陣列，並回傳新的實體。通常至少為一個以上。

```javascript
Array.of(1, 2, 3); // [1, 2, 3]
Array.of("man"); // ['man']
Array.of(true, null, undefined, 1); // [true, null, undefined, 1]
```

### 實體方法

### `ary.find(Fn:(element:any) => boolean)`

使用測試函式 `Fn` 依序遍歷 `ary`，如果有第一個符合測試函式的元素，則回傳元素本身。如果都沒有符合的，則回傳 `undefined`。

### `ary.findIndex(Fn:(element:any) => boolean)`

跟上面的 `find()`類似，不過不一樣的是，回傳的是第一個符合元素的索引值。

舉個例子練習看看。

```javascript
const inventory = [
  { name: "apples", quantity: 2 },
  { name: "bananas", quantity: 0 },
  { name: "cherries", quantity: 5 },
  { name: "tomatoes", quantity: 3 },
];

function isMidQuantity(fruit) {
  return fruit.quantity === 3;
}

const elem = inventory.find(isMidQuantity);
const elemIndex = inventory.findIndex(isMidQuantity);

console.log(elem);
console.log(elemIndex);

// { name: 'tomatoes', quantity: 3 }
// 3
```

### `ary.includes(element:any, fromIndex?: number)`

判斷陣列是否包含特定的元素。是 `indexOf(element) > 0` 的語法糖，回傳布林值。  
`fromIndex`是選擇性參數，可決定從哪個位置的元素開始找起。

```javascript
const pets = ["cat", "dog", "bird"];
const hasCat = pets.includes("cat"); // true
const hasRabbit = pets.includes("rabbit"); // false
```

### `ary.fill(value:any, startIndex?:number, endIndex?:number)`

將陣列中的第一個到最後一個元素，以 `value` 填入。後面兩個選擇性參數可決定起始索引跟結束索引。這個方法並不會回傳新的陣列，而是修改原來的陣列，使用上要小心。

```javascript
let arr = [1, 2, 3];
arr.fill(4); // [4, 4, 4]
arr.fill(5, 1); // [1, 5, 5]
arr.fill(6, 2, 3); // [1, 6, 5]
```

### Array Iterator (陣列迭代器物件)

在遍歷實體的每個元素後，產生新的陣列迭代器物件。對這個物件就能使用 `next()` `for ... of` 等特性可以使用。根據回傳的內容不同有以下三個方法可使用

- `ary.entries()`: 回傳元素的 key/value pair
- `ary.keys()`: 回傳元素的 key 值
- `ary.values()`: 回傳元素的 value 值

```javascript
const arr = ["a", "b", "c"];

const entIterator = arr.entries();
const keyIterator = arr.keys();
const valIterator = arr.values();

for (let e of entIterator) {
  console.log(`use arr.entries(): ${e}`);
}
// use arr.entries(): 0,a
// use arr.entries(): 1,b
// use arr.entries(): 2,c

for (let e of keyIterator) {
  console.log(`use arr.keys(): ${e}`);
}
// use arr.keys(): 0
// use arr.keys(): 1
// use arr.keys(): 2

for (let e of valIterator) {
  console.log(`use arr.values(): ${e}`);
}
// use arr.values(): a
// use arr.values(): b
// use arr.values(): c
```

## 小結

陣列在 Javascript 中是個很常使用的資料儲存類型。當操作複雜性提高，或資料本身結構也很複雜時，就能使用相關的語法來方便資料處理，所以可以愈熟悉，在開發上也能愈駕輕就熟喔!

### 參考資源

- [MDN-Array](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [数组的扩展](https://es6.ruanyifeng.com/#docs/number)
