# 前端面试题整理

整理渠道：

1. 自己的面试经历
2. 群友的面试过程、朋友圈、社区分享
3. 面试官、讲师主动分享

> 如果你也有题，或者答案有问题或遗漏，也同样欢迎通过 `issue` 进行补充 [[查看](https://github.com/cgfeel/frontend-interview-questions/issues)]

整理方式：

- 自己的面试：复盘整理
- 其他面试，有答案的情况下：默认作为标准答案
- 其他面试，没有标准答案下：以各大 `GPT` 答案为准
- 重要：若以上答案出现遗漏偏差，再根据实际情况复盘，修复

> 目前已有题目做复盘修复，尤其是 `GPT` 给出的答案可能考虑的角度并没有那么深入

要求：

- 基础：按照下限原则，尽可能全部都理解问题，以及问的知识点、能够概述回答问题
- 进阶：能够透过答案垂直深入，牢记原理和底层
- 高级：代入实际场景、可以演示的情况能够不借助任何参考手写完成

> 每个问题前会标识 🔴，若标识的是 🧑‍💻 建议除了口述答案之外最好能手写一遍

归纳方式，分为 3 块：

- 问题归类整理：分 `js` 基础、网络、`React` 等，存放在 `/document` [[查看](#问题整理)]
- 根据来源索引问题：直接通过 `README` 整理 [[查看](#来源索引)]
- 实例演示：目前通过 `codepen` 完成

> 没有索引来源的问题全部来自网友提供

问题整理格式大致如下：

```
- 标题
- 出处
- 答案
  - 摘要总结（选填）
  - 详细答案
  - 答案修正（选填）
```

## 问题整理

### 网络篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/network.md

### `javascript` 篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md

### `React` 篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md

### 前端场景篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md

## 来源索引

### 百安居 1 面

- `React` 中有对状态管理有做进一步封装吗？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-react-%E4%B8%AD%E6%9C%89%E5%AF%B9%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86%E6%9C%89%E5%81%9A%E8%BF%9B%E4%B8%80%E6%AD%A5%E5%B0%81%E8%A3%85%E5%90%97)]
- `React` 中如何在父组件获取子组件的方法？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-react-%E4%B8%AD%E5%A6%82%E4%BD%95%E5%9C%A8%E7%88%B6%E7%BB%84%E4%BB%B6%E8%8E%B7%E5%8F%96%E5%AD%90%E7%BB%84%E4%BB%B6%E7%9A%84%E6%96%B9%E6%B3%95)]
- 低代码和微前端有了解吗？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md#-%E4%BD%8E%E4%BB%A3%E7%A0%81%E5%92%8C%E5%BE%AE%E5%89%8D%E7%AB%AF%E6%9C%89%E4%BA%86%E8%A7%A3%E5%90%97)]
- `useCallback` 使用过没？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-usecallback-%E4%BD%BF%E7%94%A8%E8%BF%87%E6%B2%A1)]
- 函数组价和类组件处理重复渲染有什么区别？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E5%87%BD%E6%95%B0%E7%BB%84%E4%BB%B7%E5%92%8C%E7%B1%BB%E7%BB%84%E4%BB%B6%E5%A4%84%E7%90%86%E9%87%8D%E5%A4%8D%E6%B8%B2%E6%9F%93%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB)]
- 封装的按钮权限组件怎么实现？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E5%B0%81%E8%A3%85%E7%9A%84%E6%8C%89%E9%92%AE%E6%9D%83%E9%99%90%E7%BB%84%E4%BB%B6%E6%80%8E%E4%B9%88%E5%AE%9E%E7%8E%B0)]
- 数据什么时候定义在组件里面，什么时候定义在状态管理里面？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E6%95%B0%E6%8D%AE%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%AE%9A%E4%B9%89%E5%9C%A8%E7%BB%84%E4%BB%B6%E9%87%8C%E9%9D%A2%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%AE%9A%E4%B9%89%E5%9C%A8%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86%E9%87%8C%E9%9D%A2)]
- 方法什么时候写在父组件中，什么时候写在子组件中？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E6%96%B9%E6%B3%95%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%86%99%E5%9C%A8%E7%88%B6%E7%BB%84%E4%BB%B6%E4%B8%AD%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%86%99%E5%9C%A8%E5%AD%90%E7%BB%84%E4%BB%B6%E4%B8%AD)]
