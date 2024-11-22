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
