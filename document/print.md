# 根据代码直接说输出

前端中有这样一个情况，根据代码片段直接说输出。输出会在 `codepen` 做演示，查看 `console`，原理尽可能的在答案中整理概述。

### 🔴 变量作用域输出问题？

来自：`群友`

```js
var a = 0;
console.log(a, window.a);

if (true) {
  console.log(a, window.a);

  a = 1;
  console.log(a, window.a);

  function a() {}
  console.log(a, window.a);

  a = 21;
  console.log(a, window.a);
  console.log("里面 ", a, window.a);
}

console.log("外面 ", a, window.a);
```

输出：https://codepen.io/levi0001/pen/BaXgKoW

> 原理目前还不清楚，只能说严格模式下产生的结果可能会符合大多数人想法

### 🔴 请说出对象的输出？

来自：`群友`、`渡一`

```js
const map = new Map();
map.set(true, 0);
map[true] = 10;

console.log(map.get(true));
console.log(map.get("true"));
console.log(map["true"]);
```

输出：https://codepen.io/levi0001/pen/XWvvayV

<details>

<summary>答案：</summary>

> 0
>
> undefined
>
> 10

先看 `Map` 对象，存在 `get` 和 `set` 方法，当 `set` 一个 `true` 为 0，获取 `true` 也一定是 0，但是获取字符 `'true'` 的时候由于 `key` 不存在拿到 `undefined`

这里简短补个内容：`Map` 和 `WeakMap` 的区别

| 分类     | `Map`                    | `WeakMap`                         |
| -------- | ------------------------ | --------------------------------- |
| `key`    | 任意类型                 | `Object`                          |
| 内存管理 | 不能自动回收             | 自动回收                          |
| 遍历     | 可遍历                   | 只能取值不可遍历                  |
| 使用场景 | 缓存数据、唯一标识的集合 | 需要自动回收，如 `Dom` 关联的方法 |

> 内存管理即引用机制，当设置 `key` 为一个 `Object` 时，除了集合对象其他地方不再使用的时候是否自动回收

然后再来看对象取值，以下内容来自 `渡一`：属性读取方式，有这么一段代码

```js
const obj = {};
const x = 'x';

obj.x;
obj.[x];
```

浏览器对 `js` 对象的读和写会转成一个内部方法，这里以 `[[Get]]` 和 `[[Set]]` 作为演示，都有 3 个参数：

```js
// 参数：操作对象、属性名称，`this` 指向
[[Get]](obj, "x", obj);

// `this` 指的向存在，是为了属性有可能是一个访问器，访问器中有可能会用到 `this`
const obj = {
  get x() {
    return this.y;
  },
};
```

在读取属性时分两种读法：

- `obj.x`：直接将属性 `x` 转换成字符串
- `obj[]`：这里会将属性做一个处理，判断是否为 `Symbol`

```js
// isSymbol 为自定义演示用，和浏览器内部判断方法不一样
const symbolTag = "[object Symbol]";
const isObject = (value) => typeof value === "object" && value !== null;
const isSymbol = (value) =>
  value === "symbol" ||
  (isObject(value) && Object.prototype.toString.call(value) === symbolTag);

obj.x; // [[Get]](obj, 'x', obj)
obj[x]; // [[Get]](obj, isSymbol(x) ? x : String(x) : obj)
```

结合上面总结，来看数组：

```js
const arr = [];
arr[0] = 1;
arr["0"] = 2;
```

这里得到长度为 1 的数组，且下标 0 的值为 2：

- 因为 `[]` 中的 `key` 都不是 `Symbol`，全部转换成字符 `'0'`

结合上面总结，将 `Object` 作为 `key`：

```js
const obj = {};
obj[{ a: 1 }] = 1;
obj[{ a: 2 }] = 2;

console.log(obj);
```

最终会将 `key` 转换成字符为 `[object Object]`，最后得到：

- `{ '[object Object]': 2 }`

</details>

### 🔴 请根据 `iframe` 说出最终输出结果？

来自：`群友`

```js
var iframe = document.createElement("iframe");
document.documentElement.appendChild(iframe);

iframe.src = "javascript: var a = [];";
var a, b;

setTimeout(() => {
  a = iframe.contentWindow.a;
  b = [];

  console.log(a instanceof Array, b instanceof Array);
  console.log(Array.isArray(a), Array.isArray(b));
}, 0);
```

输出：https://codepen.io/levi0001/pen/KwPPdPe

<details>

<summary>答案：</summary>

> false, true
>
> true, true

变量 `a` 和 `b` 都是 `array`，不同的是它们的原型链不同，`a` 的原型链指向 `iframe.contentWindow.Array`，而 `b` 的原型链是 `window.Array`（即 `Array`）。

- 在第一个判断中 `Array` 为全局对象 `window` 的属性，因此得到 `false, true`
- 而 `Array.is` 仅用于判断对象是不是 `Array`，不需要考虑原型链，因此得到 `true, true`

</details>
