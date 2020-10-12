# [Day27] ES2021(ES12) - part 2

## `WeakRef` & `Finalizers`

```javascript
const callback = () => {
  const aBigObj = new WeakRef({
    name: "Backbencher",
  });
  console.log(aBigObj.deref().name);
};

(async function () {
  await new Promise((resolve) => {
    setTimeout(() => {
      callback(); // Guaranteed to print "Backbencher"
      resolve();
    }, 2000);
  });

  await new Promise((resolve) => {
    setTimeout(() => {
      callback(); // No Gaurantee that "Backbencher" is printed
      resolve();
    }, 5000);
  });
})();
```

```javascript
const registry = new FinalizationRegistry((value) => {
  console.log(value);
});

(function () {
  const obj = {};
  registry.register(obj, "Backbencher");
})();
```

## `Intl`

### `Intl.ListFormat`

```javascript
const list = ["Apple", "Orange", "Banana"];
new Intl.ListFormat("en-GB", { style: "long", type: "conjunction" }).format(
  list
);
// "Apple, Orange and Banana"
new Intl.ListFormat("zh-tw", { style: "short", type: "conjunction" }).format(
  list
);
// "Apple、Orange和Banana"
```

### `Intl.DateTimeFormat

```javascript
let o = new Intl.DateTimeFormat("en", {
  timeStyle: "short",
});
console.log(o.format(Date.now())); // "13:31"
let o = new Intl.DateTimeFormat("en", {
  dateStyle: "short",
});
console.log(o.format(Date.now())); // "21.03.2012"
let o = new Intl.DateTimeFormat("en", {
  timeStyle: "medium",
  dateStyle: "short",
});
console.log(o.format(Date.now())); // "21.03.2012, 13:31"
```

## 參考資源

- [Finished Proposals](https://github.com/tc39/proposals/blob/master/finished-proposals.md)
- [”扶我起来，我还能学！“ 之 ES2021 抢先尝](https://juejin.im/post/6856704516499832845)
- [ES2021 / ES12 New Features](https://backbencher.dev/javascript/es2021-new-features)
