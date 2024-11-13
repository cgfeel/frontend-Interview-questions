# 整理 `javascript` 相关的面试题

### 🧑‍💻 数组合并有哪些方法？

来自：`万云科技`

<details>

<summary>答案：</summary>

**1. 在循环中 `push`：**

```js
const data1 = [1, 2, 3];
const data2 = [4, 5, 6];

for (let item of data2) {
  data1.push(item);
}

console.log(data1);
```

**2. 扩展预算符：**

```js
const data2 = [4, 5, 6];
const data1 = [1, 2, 3, ...data2];

console.log(data1);
```

**3. `concat`：**

```js
const data1 = [1, 2, 3].concat([4, 5, 6]);
console.log(data1);
```

**4. `splice`：**

```js
const data1 = [1, 2, 3];
data1.splice(3, 0, 4, 5, 6);

console.log(data1);
```

</details>

### 🔴 请求参数如何防篡改？

来自：`万云科技`

<details>

<summary>以下是一些防止请求参数被篡改的方法：</summary>

**签名验证：**

原理：在发送请求前，根据请求参数和一个密钥生成一个签名，服务器端使用相同的方法和密钥验证签名的合法性。如果参数被篡改，签名将无法通过验证。

例如：

- 客户端将请求参数按照一定规则排序，然后与密钥进行哈希运算生成签名，将签名和参数一起发送到服务器。
- 服务器端接收到请求后，按照相同规则提取参数并生成签名，对比客户端发送的签名和服务器生成的签名是否一致。

**加密传输：**

原理：对请求参数进行加密，即使被篡改也难以理解其内容。只有服务器端能够解密并验证参数的完整性。

例如：

- 使用 `HTTPS` 协议进行数据传输，确保数据在网络传输过程中的安全性，防止被窃听和篡改。
- 对敏感参数进行单独加密，如使用对称加密算法或非对称加密算法对参数进行加密后再发送。

**时间戳验证：**

原理：客户端在发送请求时添加一个时间戳，服务器端验证时间戳是否在合理范围内。如果时间戳过期或与服务器时间相差太大，则认为请求可能被篡改。

例如：

- 客户端发送请求时，将当前时间戳作为一个参数发送给服务器。
- 服务器端接收到请求后，检查时间戳是否在允许的时间范围内，比如与服务器时间相差不超过一定时长（如 5 分钟）。

**参数校验：**

原理：服务器端对接收的请求参数进行严格的校验，包括参数的类型、格式、范围等。如果参数不符合预期，拒绝该请求。

例如：

- 对于数值类型的参数，检查其是否为合法的数字；对于字符串类型的参数，检查其长度、格式是否符合要求。
- 对一些关键参数进行必填项检查，确保请求的完整性。

</details>

### 🧑‍💻 `localStorage` 如何跨域获取？

来自：`万云科技`

<details>

<summary>答案：</summary>

`localStorage` 通常不能直接跨域获取。这是出于浏览器的安全考虑，不同源的网页不能随意访问彼此的 `localStorage` 数据。

但是，可以通过一些特定的方法在一定程度上实现跨域数据共享：

**使用 `postMessage` 和 `window.addEventListener`：**

1. 在源页面（假设为 `http://example.com/page1.html`）中：

```html
<!DOCTYPE html>
<html>
  <body>
    <script>
      const targetOrigin = "http://anotherdomain.com";
      window.addEventListener("message", function (event) {
        if (event.origin === targetOrigin) {
          // 响应来自目标页面的请求
          event.source.postMessage(
            { localStorageData: localStorage.getItem("key") },
            targetOrigin
          );
        }
      });
      const iframe = document.createElement("iframe");
      iframe.src = targetOrigin + "/receiver.html";
      document.body.appendChild(iframe);
    </script>
  </body>
</html>
```

2. 在目标页面（假设为 `http://anotherdomain.com/receiver.html`）中：

```html
<!DOCTYPE html>
<html>
  <body>
    <script>
      const sourceOrigin = "http://example.com";
      window.addEventListener("message", function (event) {
        if (event.origin === sourceOrigin) {
          const data = event.data;
          console.log(data.localStorageData);
        }
      });
      const iframe = document.createElement("iframe");
      iframe.src = sourceOrigin + "/page1.html";
      document.body.appendChild(iframe);

      // 向源页面发送请求
      iframe.contentWindow.postMessage("request data", sourceOrigin);
    </script>
  </body>
</html>
```

这种方法通过 `postMessage` 在两个不同源的窗口之间传递消息，从而实现数据的间接获取。但需要注意的是，这种方式需要双方页面的配合，并且要严格验证消息的来源以确保安全性。

**使用代理服务器：**

可以设置一个服务器端的代理，源页面将 `localStorage` 中的数据发送到代理服务器，目标页面从代理服务器获取数据。但这需要服务器端进行额外的开发和配置。

例如：

1. 源页面向代理服务器发送数据：

```js
const dataToSend = localStorage.getItem("key");
fetch("/proxy", {
  method: "POST",
  body: JSON.stringify({ data: dataToSend }),
  headers: {
    "Content-Type": "application/json",
  },
});
```

2. 代理服务器接收并存储数据，当目标页面请求时返回数据：

```js
const express = require("express");
const app = express();

let storedData;
app.post("/proxy", (req, res) => {
  storedData = req.body.data;
  res.sendStatus(200);
});
app.get("/proxy", (req, res) => {
  res.json({ data: storedData });
});
app.listen(3000);
```

3. 目标页面从代理服务器获取数据：

```js
fetch("/proxy")
  .then((response) => response.json())
  .then((data) => console.log(data.data));
```

这种方法虽然可以实现跨域获取数据，但依赖于服务器的中间处理，增加了系统的复杂性。

</details>

### 🧑‍💻 如何写一个 `splice` 方法并覆盖数组的原方法？

来自：`万云科技`

> 题目写的是 `split`，但这是 `String.prototype` 上的方法，我想问题应该是问 `splice`

<details>

<summary>归纳如下：</summary>

先写一个统一的 `splite` 的方法用于覆盖使用，然后再通过不同的方式重写

```js
function defineSplice(start, deleteCount, ...items) {
  const length = this.length;
  if (start < 0) {
    start = start >= -length ? length + start : 0;
  }

  if (deleteCount === undefined) {
    deleteCount = length - start;
  }

  const removeItems = [];
  const removeLength = start + deleteCount;

  for (let i = start; i < removeLength; i++) {
    removeItems.push(this[i]);
  }

  for (let i = removeLength, j = 0; j < items.length; i++, j++) {
    this[i] = items[j];
  }

  this.length = length - deleteCount + items.length;
  return removeItems;
}
```

**1. 重写 `prototype`：**

- 优点：兼容性好
- 缺点：全局覆盖，可能造成意外问题

```js
// 重写方法，闭包运行避免污染
(function () {
  const originalSplice = Array.prototype.splice;
  Array.prototype.splice = defineSplice;

  const arr = [1, 2, 3, 4, 5];
  const removed = arr.splice(1, 2, 10, 11);

  console.log("rewrite property", arr);
  console.log("remove", removed);

  Array.prototype.splice = originalSplice;
})();
```

**2. 通过 `proxy` 代理数组方法：**

- 优点：不会造成全局污染
- 缺点：不兼容 `ie`

```js
// 通过 proxy 代理重写 splice，缺点是不兼容 ie
const arr = [1, 2, 3, 4, 5];
const proxyArr = new Proxy(arr, {
  get(target, property, args) {
    if (property === "splice") {
      return defineSplice;
    }
    return target[property];
  },
});

const removeProxy = proxyArr.splice(1, 2, 10, 11);

console.log("proxy array", arr);
console.log("remove proxy", removeProxy);
```

**3. 通过 `defineProperty` 劫持数组方法：**

- 优点：不会全局污染，兼容性比 `proxy` 要好
- 缺点：一个劫持对应一个方法，相比 `proxy` 要繁琐

```js
// 通过 Object.defineProperty 劫持 splice，兼容 ie
const arr1 = [1, 2, 3, 4, 5];
const defineArr = Object.defineProperty({}, "splice", {
  value: function (...args) {
    return defineSplice.apply(this, args);
  },
});

const defineRemove = defineArr.splice.call(arr1, 1, 2, 10, 11);

console.log("define array", arr1);
console.log("remove define", defineRemove);
```

> 注意这里劫持的是一个空对象，避免污染全局对象，通过 `call` 和 `apply` 修正指向

完整实例：https://codepen.io/levi0001/pen/mdNRgVJ

</details>

### 🧑‍💻 `forEach` 循环和 `for` 循环哪个性能高？`forEach` 循环可以中断吗？

来自：`万云科技`

<details>

<summary>答案：</summary>

**`forEach` 循环和 `for` 循环的性能比较：**

在大多数情况下，简单的 `for` 循环性能可能会略高于 `forEach` 循环。这是因为 `forEach` 是一种函数调用的方式遍历数组，会有一些额外的函数调用开销。而 `for` 循环是一种更底层的遍历方式，在一些优化较好的 `JavaScript` 引擎中可能会有更好的性能表现。

> 但是，性能差异通常非常小，在实际应用中，除非是在处理非常大规模的数据或者对性能要求极其苛刻的场景下，一般不太容易察觉到明显的性能差异。

**中断循环**

理论上 `forEach` 设计出来就是为了遍历每一个回调方法的。但可以通过以下 2 种方式任务中断循环：

1. 通过 `throw` 中断循环：

```js
const arr = [1, 2, 3, 4, 5];
try {
  arr.forEach((num) => {
    if (num > 2) throw new Error("break forEach");
    console.log(num);
  });
} catch (e) {
  console.log(e.message);
}
```

2. 通过重写 `forEach`：

```js
// 重写 forEach
Array.prototype.forEach = function customForEach(callback) {
  for (let i = 0; i < this.length; i++) {
    const result = callback(this[i], i, this);
    if (result === false) break;
  }
};

const arr1 = [1, 2, 3, 4, 5];
arr1.forEach((item, index, array) => {
  if (item > 2) return false;
  console.log(item);
});
```

完整实例：https://codepen.io/levi0001/pen/MWNpKJV

</details>

### 🔴 说一下箭头函数和普通函数的区别？

来自：`Gate.io`

<details>

<summary>箭头函数和普通函数在多个方面存在区别，以下是详细介绍：</summary>

**语法形式**

普通函数：有着完整且相对规范的语法结构，由 `function` 关键字开头，后面跟着函数名（可省略，若省略则为匿名函数）、参数列表以及函数体。例如：

```js
// 有函数名的普通函数
function add(num1, num2) {
    return num1 + num2;
}

// 匿名普通函数，常作为回调函数使用
function (num) {
    console.log(num);
}
```

箭头函数：使用箭头（`=>`）来定义函数，语法更加简洁。箭头函数如果只有一个参数，参数外面的圆括号可以省略；如果函数体只有一条语句，且这条语句是返回值语句，花括号和 `return` 关键字都可以省略。例如：

```js
// 只有一个参数，省略参数括号（我的编辑器有 `prettier` 自动加了括号）
const square = (num) => num * num;

// 函数体有多条语句，需要花括号和 return
const sum = (num1, num2) => {
  const result = num1 + num2;
  return result;
};
```

**`this` 指向**

普通函数：`this` 的指向在函数被调用时才确定，它取决于函数的调用方式。在全局环境下调用普通函数，`this` 指向全局对象（在浏览器环境中是 `window`，在 `Node.js` 环境中是 `global`）；如果作为对象的方法调用，`this` 指向该对象；要是通过 `call`、`apply`、`bind` 等方法来调用，`this` 会被显式地设置为传入的第一个参数所指定的对象。例如：

```js
const person = {
  name: "张三",
  sayHello: function () {
    console.log(`Hello, I'm ${this.name}`);
  },
};

person.sayHello(); // this 指向 person 对象，输出 "Hello, I'm 张三"

const anotherSayHello = person.sayHello;
anotherSayHello(); // this 指向全局对象，输出 "Hello, I'm undefined"（因为全局对象中没有 name 属性）
```

> 上面这段代码来自豆包，存在一个错误，具体是什么？我在底部说明。

箭头函数：本身没有自己的 `this`，其 `this` 是继承自外层作用域的 `this`。箭头函数在定义时就确定了 `this` 的指向，并且之后不会再改变，无论它在何处被调用。例如：

```js
const person = {
  name: "张三",
  sayHello: () => {
    console.log(`Hello, I'm ${this.name}`);
  },
};

person.sayHello(); // this 指向全局对象，输出 "Hello, I'm undefined"（假设全局对象没有 name 属性）

const outerThis = { name: "李四" };
const func = function () {
  const innerFunc = () => {
    console.log(`Hello, I'm ${this.name}`);
  };
  innerFunc();
};
func.call(outerThis); // this 指向 outerThis，输出 "Hello, I'm 李四"
```

> 这段代码和上面一样，犯了相同的 1 个错误；除此之外还有第二个错误，在末尾说明

**`arguments` 对象**

普通函数：在函数内部，有一个内置的 `arguments` 对象，它是一个类数组对象，包含了函数调用时传入的所有实际参数，无论函数定义时声明了几个参数，都可以通过 `arguments` 来获取所有参数信息。例如：

```js
function sum() {
  let result = 0;
  for (let i = 0; i < arguments.length; i++) {
    result += arguments[i];
  }
  return result;
}

console.log(sum(1, 2, 3)); // 可以获取到传入的 1、2、3 这三个参数，输出 6
```

箭头函数：不存在自己的 `arguments` 对象，如果需要获取参数，可以通过定义的形参或者使用剩余参数（`...`语法）来实现，但不能像普通函数那样直接依赖 `arguments` 对象。例如：

```js
const sum = (...nums) => {
  let result = 0;
  for (let num of nums) {
    result += num;
  }
  return result;
};

console.log(sum(1, 2, 3)); // 通过剩余参数获取传入的参数，输出 6
```

> `...` 的专业叫法应该是：扩展运算符

**构造函数使用**

普通函数：可以使用 `function` 关键字定义的普通函数作为构造函数，通过 `new` 关键字来创建对象实例，在函数内部可以使用 `this` 来初始化新对象的属性等，并且会自动执行一些构造函数相关的初始化操作（如创建对象的原型链等）。例如：

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

const person = new Person("张三", 20);
console.log(person.name); // 输出 "张三"
```

箭头函数：不能作为构造函数使用，因为它没有自己的 `this`，也不存在构建对象实例相关的内部机制，如果尝试使用 `new` 来调用箭头函数，会报错。例如：

```js
const Person = (name, age) => {
  this.name = name;
  this.age = age;
};

const person = new Person("张三", 20); // 报错，箭头函数不能作为构造函数
```

---

以上答案来自豆包，以下内容为我修正

**2 个错误**

从全局对象上下文中获取 `name` 时不一定时 `undefinde`，分两种情况：

- 浏览器环境全局对象时 `window`，存在 `name` 属性，为空字符
- `Node.js` 全局对象没有 `name` 属性，为 `undefinde`

> 知识点来自 `渡一`

箭头函数在定义时就确定了 `this` 的指向，但会随上下文改变，例如：

```js
const data = { name: "levi" };
function action() {
  (() => {
    console.log(this.name);
  })();
}

action(); // ''
action.call(data); // levi
```

**2 个遗漏**

箭头函数没有原型链 `protoType`：

- 箭头函数内部找不到的对象，会直接从作用域中获取上下文，而普通函数实例化后，则会通过原型链一层层往上找
- 普通函数可以将方法通过原型链绑定在对象上，箭头函数则不可以

不能通过 `call`、`apply`、`bind` 修正箭头函数的上下文：

- 虽然都支持调用 `call`、`apply`、`bind`，但箭头函数的 `this` 永远由上下文决定
- 而普通函数可以通过此类方法修正上下文中 `this` 对象

**适用场景**

普通函数：

- 需要使用构造函数创建对象，或继承对象等 `OOP` 场景时
- 需要通过 `call`、`apply` 绑定上下文的情况
- 需要使用原型链的情况
- 事件监听方法，有可能需要通过 `this` 获取 `target`

箭头函数：

- 函数式 `React` 组件，如果组件是访问的页面，仍旧推荐普通函数，以便和页面中的组件做区分
- 在一个复合型型函数中动态获取上下文
- 纯粹的为了返回计算结果，如图形运算等，能够保持直观、简洁
- 循环遍历，如：`map`、`filter`、`reduce`

用防抖函数演示：复合型型函数中动态获取上下文

```typescript
function debounce<T extends Function, D extends any = any>(
  func: T,
  delay: number = 500
) {
  let timer = 0;
  return function (this: ThisParameterType<T>, ...args: D[]) {
    if (timer !== 0) {
      clearTimeout(timer);
    }

    timer = setTimeout(() => {
      func.apply(this, args); // 这里的 `this` 会根据监听事件的对象而改变
      timer = 0;
    }, delay);
  };
}
```

上面注解行中的 `this` 也可以通过普通方法来实现，但这就要额外声明一个代理对象，例如：

```js
function action() {
  const that = this;
  return function () {
    console.log(that);
  };
}
```

这就是箭头函数还没有时的做法，会看到很多误导性的 `that`、`this`，无法分别具体指向

</details>
