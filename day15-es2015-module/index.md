# [Day15] ES2015(ES6) - 模組 (Module)

## 主流的模組規範

### CommonJS

### UMD

### ES Module

## `export`

### `export {fn1 as fn2}`

```javascript
const fn1 = (s) => console.log(s);
export { fn1 as fn2 };
```

### `export default`

```javascript
const fn = (s) => console.log(s);
export default fn;
// -----------------------------

export default class MyClass {
    this.name = '';
}
```

### `export * from './MyModule'`

```javascript

```

### `export { fn1, fn2 } from './MyModule'`

```javascript
export { fn1, fn2 } from "./MyModule";

//
```

## `import`

### `import fn1 from './MyModule'`

```javascript

```

### `import * as MyModule from './MyModule'`

```javascript

```

### `import { fn1, fn2 } from './MyModule'`

```javascript

```

## 小結

## 參考資源

- [[譯] 解析 Javascript 模組機制與建置函式庫觀念](https://andyyou.github.io/2017/12/13/anatomy-of-js-modules/)
- [深入 CommonJs 與 ES6 Module](https://iter01.com/77315.html)
- [Module 的语法](https://es6.ruanyifeng.com/#docs/module#import-%E5%91%BD%E4%BB%A4)
