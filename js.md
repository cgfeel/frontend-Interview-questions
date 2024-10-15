# 整理 `javascript` 相关的面试题

以下问题来自 `万云科技`：

### 🔴 数组合并有哪些方法？

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

### 🔴 `localStorage` 如何跨域获取？

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

### 🔴 如何写一个 `splice` 方法并覆盖数组的原方法？

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

### 🔴 `forEach` 循环和 `for` 循环哪个性能高？`forEach` 循环可以中断吗？

<details>

<summary>答案：</summary>

**`forEach` 循环和 `for` 循环的性能比较：**

在大多数情况下，简单的 `for` 循环性能可能会略高于 `forEach` 循环。这是因为 `forEach` 是一种函数调用的方式遍历数组，会有一些额外的函数调用开销。而 `for` 循环是一种更底层的遍历方式，在一些优化较好的 `JavaScript` 引擎中可能会有更好的性能表现。

> 但是，性能差异通常非常小，在实际应用中，除非是在处理非常大规模的数据或者对性能要求极其苛刻的场景下，一般不太容易察觉到明显的性能差异。

**中断循环**

理论上 `forEach` 设计出来就是为了遍历每一个回调方法的。但可以通过以下 2 种方式任务中断循环：

通过 `throw` 中断循环：

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

在这个例子中 `handleClick` 回调函数在组件初次渲染时创建一次，因为依赖项数组为空。如果有依赖项，只有当依赖项发生变化时，才会重新创建回调函数。

</details>
