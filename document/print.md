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

先看 `map` 对象，存在 `get` 和 `set` 方法，当 `set` 一个 `true` 为 0，获取 `true` 也一定是 0，但是获取字符 `'true'` 的时候由于 `key` 不存在拿到 `undefined`

</details>
