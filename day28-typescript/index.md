# [Day28] Typescript (tsconfig.json)

在寫 Typescript 時，最重要的就是要有 **tsconfig.json**。因為 ts 或 tsx 檔並不能直接在環境執行，所以需要有一份設定檔告訴 compiler 要如何轉出可執行的 js 檔。另外開發時也會因設定的不同，會使用不同方式的型別檢查。

新增的方式有兩種。一是直接在根目錄下新增 tsconfig.json，檔案內容如果是空物件`{}`，表示使用預設設定。

另一種方式是打開 cmd，輸入`tsc --init`(須先安裝 Typescript)就會產生 tsconfig.json。

如果有看過有關 tsconfig.json 的官方文件，就知道選項其實還不少。其中有些設定也不是很好理解。

所以今天就挑幾個跟這系列比較相關的部分整理一下說明，讓同為 Typescript 的開發者，在設定 tsconfig.json 時可以更得心應手。

## `compilerOptions`

主要集中設定編譯時的選項。

### `target`

設定編譯的 js 檔，以特定的 ECMAScript 版本為標準輸出。預設值為`ES3`。可設定的版本有 -

- `ES5`
- `ES6/ES2015`
- `ES7/ES2016`
- `ES2017`
- `ES2018`
- `ES2019`
- `ES2020`
- `ESNext`

### `lib`

在 TypeScript 中，針對基本常用的 JS API(像是`String`)和瀏覽器環境（像是`document`）已經有內建的定義檔。不過根據這幾天的介紹，Javascript 和瀏覽器，每年都推陳出新，釋出新特性。

加上近幾年來 NodeJS 的發展，在程式編譯輸出的部分，我們會希望能有對應的定義檔，並且可以適當調整，移除不用的定義檔。

在`lib`中，可以以列表的方式選擇性加入 -

- `ES5`
- `ES6/ES2015` (選擇其中一種寫法)
- `ES7/ES2016` (選擇其中一種寫法)
- `ES2017`
- `ES2018`
- `ES2019`
- `ES2020`
- `ESNext`
- `DOM`
- `WebWorker`
- `ScriptHost`

如果只需要個別語法的定義檔，TypeScript 也提供以下的選項加入 -

- `DOM.Iterable`
- ES2015:
  1. `ES2015.Iterable`
  2. `ES2015.Generator` ...
- `ES2016.Array.Include`
- ES2017:
  1. `ES2017.String`
  2. `ES2017.SharedMemory` ...
- ES2018:
  1. `ES2018.Promise`
  2. `ES2018.RegExp` ...
- ES2019:
  1. `ES2019.Symbol`
  2. `ES2019.Object` ...
- ES2020:
  1. `ES2020.String`
  2. `ES2020.Full` ...
- ESNext:
  1. `ESNext.Symbol`
  2. `ESNext.Intl` ...

如果沒有特別設定`lib`，則預設內容會根據`target`的不同而有調整 -

- `target`為`ES5`: `[DOM,ES5,ScriptHost]`
- `target`為`ES6`: `[DOM,ES6,DOM.Iterable,ScriptHost]`

### `Module`

設定以哪種模組系統作爲編譯輸出。選項有 - `None`, `CommonJS`, `AMD`, `System`, `UMD`, `ES6/ES2015`或`ESNext`。

如果沒有特別設定`lib`，則預設內容會根據`target`的不同而有調整 -

- `target`為`ES5`或`ES3`: `commonjs`
- `target`為`ES6`以上: `ES6/ES2015`

### `esModuleInterop`

預設為`false`。

### `allowSyntheticDefaultImports`

開發時的型別檢查使用，當 `module === "system"` 或 `esModuleInterop === true`時使用。

### `experimentalDecorators`

允許使用目前在 stage-2 的 Decorator 語法。預設為`false`。

### `emitDecoratorMetadata`

允許使用[Metadata Reflection API](https://github.com/rbuckton/reflect-metadata)。預設為`false`。

## 參考資源

- [What TypeScript configuration produces output closest to Node.js 14 capabilities?](https://stackoverflow.com/questions/61305578/what-typescript-configuration-produces-output-closest-to-node-js-14-capabilities)
- [【Day 03】 TypeScript 編譯設定 - tsconfig.json](https://ithelp.ithome.com.tw/articles/10216636)
- [Intro to the TSConfig Reference](https://www.typescriptlang.org/tsconfig)
