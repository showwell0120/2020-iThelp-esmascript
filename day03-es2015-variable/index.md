# [Day03] ES2015(ES6) - 變數(Variable)

接下來到這系列結束，將會介紹每一版重要語法的部分。不過因為篇幅有限，我會把性質比較相近的語法統整在同一天的內文裡。

以今天來說，主題為「變數」，其中包括宣告方式的改變，以及 ES2015 帶來的新特性—解構賦值。

## 變數的宣告 (Declaration)

### 作用域(Scope) & 區塊(Block)

每個程式語言在設計上都會有作用域(Scope)的概念，簡單來說就是指**變數可以活動及作用的範圍**，在有些語言的術語中則是稱為 Context。

那麼要如何定義出這個範圍呢？

就像是寫文章，段落之間會彼此有空行一樣，比較嚴謹的語言會透過特殊符號，像是角括號`{...}`，將某段程式包覆起來形成**區塊(Block)**，裡面的變數的作用域不要漫無邊際。而這樣的變數也稱為**區域變數(local variable)**。

相反地，如果變數沒有被任何區塊包覆，那麼它的作用域就是整個程式本身，這樣的變數就被稱為**全域變數(global variable)**。

![Imgur](https://i.imgur.com/blaCzsR.png)

舉 Java 來說，這個範例總共有 3 個區塊(MyClass, main, main 底下的{})。

對變數 y 來說，它的作用域是橙色框框的範圍；  
而對變數 x,z 來說，則是黃色框框的範圍。這三個變數都是區域變數。

而 Javascipt 在一開始是個比較鬆散的語言，所以它的作用域只有兩個—

- **global scope**: 作用域在全域
- **function scope**: 作用域在函式內

另外我大推看[這篇](https://dev.to/lydiahallie/javascript-visualized-scope-chain-13pd)，以視覺化的動畫演示 Javascript 在瀏覽器的編譯階段，如何實現出作用域。

### 提升(Hoisting)

Javascript 特有的機制，也就是在瀏覽器的編譯階段，不管變數會在哪裡執行，只要在某處有對變數進行宣告，都會先被放入記憶體中。在執行階段時，就不會因為參考不到變數就出現錯誤。

```javascript
num = 6; ..............// step1. 執行階段，將num的值設為6
console.log(num); .....// step2. 執行階段，output為6
num = num + 7; ........// step3. 執行階段，將num的值再加7
console.log(num); .....// step4. 執行階段，output為13
var num = 1; ..........// step0. 編譯階段，以var宣告的num會放入記憶體，並且設值為1
             ..........// step5. 執行階段，將num的值設為1
console.log(num); .....// step6. 執行階段，output為1
```

這個機制一樣也有美美動畫看[(參考)](https://dev.to/lydiahallie/javascript-visualized-hoisting-478h)，可以更加了解 Hoisting 的運作。

### let & const

因為網頁開發的需求愈趨複雜且大型化，以往的`var`已經無法讓開發上有更好的維護性跟解讀性。
因此在 ES2015 的規範中，除了以上提到的兩個 scope 外，新增了**block scope**來引入區域變數的機制，並根據變數的用途建立了兩個新的關鍵字—

- **`let`**: 宣告區域變數，作用域包含`for ...`區塊、`if ...`區塊，和不帶任何控制目的純區塊中。再同一區塊不得重複宣告，增加嚴謹性
- **`const`**: 宣告區域常數，僅能在宣告時設定好初始值，並且不得再變動

以下範例僅演示用，在變數上的名稱還是盡量以不重複為主，增加可讀性為佳喔！

```javascript
const MAIN_TITLE = "Re:從零開始";

let sampleAr = ["a", "b"];

function func(ar) {
  const FUNC_TITLE = "One Punch Man";

  for (let i = 0; i < ar.length; ++i) {
    for (let i = 1; i < 3; ++i) {
      //這裡的變數i的作用域僅在這個for區塊
      console.log(`${FUNC_TITLE}_${i}`);
    }

    console.log(`${MAIN_TITLE}_${ar[i]}`);
  }
}

func(sampleAr);

/*  --- output ---
One Punch Man_1
One Punch Man_2
Re:從零開始_a
One Punch Man_1
One Punch Man_2
Re:從零開始_b
*/
```

## 變數的解構賦值 (Destructuring)

這個特性可以對陣列或物件中的資料，進行解開，各自擷取為獨立的變數。目的是讓開發上對於某些特定資料可以更方便存取。

接著就直接透過一些範例來演示囉。

### 陣列

宣告時以 **`[]`** 包覆變數。

```javascript
const sampleArr = [1, 2, 3];

//ES 2015
let [x, y, z] = sampleArr;
console.log(x, y, z); // 1 2 3

//ES5
var x1 = sampleArr[0],
  y1 = sampleArr[1],
  z1 = sampleArr[2];
console.log(x1, y1, z1); // 1 2 3
```

另外等號兩邊的數量不一定要相等，可以透過給預設值或空位來宣告，相當彈性。

```javascript
const sampleArr = ["a", "b", "c"];

// 左邊少於右邊
let [x, y] = sampleArr;
console.log(x, y); // a b

// 左邊多於右邊
// 變數 q 沒被分配到值，預設為 undefined
// 變數 r 雖然也沒被分配到值，但是可以設定預設值，因此不會變成 undefined
let [x, y, z, q, r = "d"] = sampleArr;
console.log(x, y, z, q); // a b c undefined d

//特定位置可以給空位
let [x, , y] = sampleArr;
console.log(x, y); // a c
```

陣列的解構賦值還可以運用在巢狀結構，在之後會再提到喔。

### 物件

與陣列的規則類似，不過宣告時改以 **`{}`** 包覆變數。

```javascript
const obj = { id: 1, name: "yuri", age: "20", gender: "female" };

const { name, age, hobby, country = "Taiwan" } = obj;
console.log(name, age, hobby, country); //yuri 20 undefined Taiwan
```

## 小結

今天的內容，由於五年前就推出，而且是最基本的概念，算是比較適合給初學者看的。
不過也希望老手透過今天的整理，更加熟悉應用方式喔！

## 參考資源

- [Javascript scope and hoisting: Understanding block scope](https://dev.to/aparna_joshi_/javascript-scope-and-hoisting-understanding-block-scope-503g)
- [學習 ECMAScript 6 - var, let 和 const](http://rocksaying.tw/archives/2015/ES6_var,let,const.html)
- [學習 ECMAScript 6 - Destructuring](http://rocksaying.tw/archives/2015/ES6_Destructuring.html)
- [MDN - 解構賦值](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
