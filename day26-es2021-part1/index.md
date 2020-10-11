# [Day26] ES2021(ES12) - part 1

## `String.prototype.replaceAll`

```javascript
const str = "I like frontend. I like JavaScript.";
const newStr = str.replaceAll("like", "love");
newStr;
// "I love frontend. I love JavaScript."
```

## `Promise.any`

```javascript
Promise.any(promises).then(
  (first) => {},
  (error) => {}
);
```

## 邏輯運算子

## 數字分隔 `_`

```javascript
let x = 2_3333_3333;
```

## 類別的私有方法 `#`

```javascript
class Person {
  // Private method
  #setType() {
    console.log("I am Private");
  }

  // Public method
  show() {
    this.#setType();
  }
}

const personObj = new Person();
personObj.show(); // "I am Private";
personObj.setType(); // TypeError: personObj.setType is not a function
```

```javascript
class Person {
  // Public accessor
  get name() {
    return "Backbencher";
  }
  set name(value) {}

  // Private accessor
  get #age() {
    return 42;
  }
  set #age(value) {}
}

const obj = new Person();
console.log(obj.name); // "Backbencher"
console.log(obj.age); // undefined
```

## 參考資源

- [”扶我起来，我还能学！“ 之 ES2021 抢先尝](https://juejin.im/post/6856704516499832845)
- [ES2021 / ES12 New Features](https://backbencher.dev/javascript/es2021-new-features)
