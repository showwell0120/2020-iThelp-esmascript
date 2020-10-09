# [Day24] ES2020(ES11) - 模組

## Dynamic import

在模組化開發下，我們會以`import`的方式匯入需要的模組。但是因為`import`是屬於靜態函式，如果有些模組是在特定條件下才會用到的話，程式裡面還是會包含到這些模組，某些情況下可能只是徒增執行檔的大小。

不過有些 framework 或打包工具有針對這部分提供了解決方案。像是 React 內建的 `lazy`和 `suspense` API，或是第三方套件 `React Loadable`，讓開發者先享受到動態載入的便利性。

在 ES2020 後，`import`終於也可以動態載入。透過 Promise 的包裝，讓在特定條件下執行載入的模組，可以在回傳的 promise 中取得。

```javascript
btn.onclick = () => {
  // promise chaining 的方式
  import("./moduleA.js")
    .then((module) => {
      // Do something with the module.
    })
    .catch((err) => {
      // load error;
    });

    // 使用await的方式
    let module = await import("./moduleA.js");
};


```

動態匯入 json 檔也可以。

```javascript
const loadUserProfile = () => import("./user/profile.json");
loadUserProfile().then(
  (value) => value?.default && setUserProfile(value.default)
);
```

如果使用 Babel 轉譯的話，在外掛的列表上需要加上 `@babel/plugin-syntax-dynamic-import`

## Module Namespace Exports

當要匯入某個檔案的所有輸出函式，為了語意性和方便性，我們會為這些匯入的函式放在一個 namespace 底下。

```javascript
import * as Util from "../utils";
```

相對地 `export` 並沒有支援 namespace。所以我們很常在函式庫的入口處會這樣寫 -

```javascript
import * as Util from "../utils";
export { Utils };
```

在 ES2020 後，`export` 也能像 `import` 一樣以 namespace 輸出了。

```javascript
export * as Utils from "../utils";
```

## `import.meta`

針對匯入的 JS 模組檔案提供相關訊息的物件，像是模組的路徑等。

```javascript
<script type="module" src="my-module.js"></script>;

console.log(import.meta); // { url: "file:///home/user/my-module.js" }
```

## 參考資源

- [10 New JavaScript Features in ES2020 That You Should Know](https://www.freecodecamp.org/news/javascript-new-features-es2020/)
- [ES2020 新特性](https://juejin.im/post/6844904080955932679)
- [React 中使用 Dynamic Import](https://medium.com/itsoktomakemistakes/react-%E4%B8%AD%E4%BD%BF%E7%94%A8-dynamic-import-3bfed937669e)
- [import.meta](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import.meta)
