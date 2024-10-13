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
