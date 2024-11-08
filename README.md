# 前端面试题整理

## 概述

整理渠道：

1. 自己的面试经历
2. 群友的面试过程、朋友圈、社区分享
3. 面试官、讲师主动分享

> 如果你也有题，或者答案有问题或遗漏，也同样欢迎通过 `issue` 进行补充 [[查看](https://github.com/cgfeel/frontend-interview-questions/issues)]

整理方式：

- 自己的面试：复盘整理
- 其他面试，有答案的情况下：默认作为标准答案
- 其他面试，没有答案情况下：以各大 `GPT` 答案为准
- 重要：若以上答案出现遗漏偏差，再根据实际情况复盘，修复

> 目前已有题目做复盘修复，尤其是 `GPT` 给出的答案可能考虑的角度并没有那么深入

要求：

- 基础：按照下限原则，尽可能全部都理解问题，以及问的知识点、能够概述回答问题
- 进阶：能够透过答案垂直深入，牢记原理和底层
- 高级：代入实际场景、需要演示的情况能够不借助任何参考手写完成

> 每个问题前会标识 🔴，若标识的是 🧑‍💻 建议除了口述答案之外最好能手写一遍

归纳方式，分为 3 块：

- 问题归类整理：分 `js` 基础、网络、`React` 等，存放在 `/document` [[查看](#问题整理)]
- 根据来源索引问题：直接通过 `README` 整理 [[查看](#来源索引)]
- 示例演示：目前通过 `codepen` 完成

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

所有面试题分类整理

### 网络篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/network.md

### `javascript` 篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md

### `React` 篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md

### 前端场景篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md

### 开放问题篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/open.md

## 来源索引

归纳有明确出处的面试题

### 百安居 1 面

1. 项目中遇到的难点？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/open.md#-%E9%A1%B9%E7%9B%AE%E4%B8%AD%E9%81%87%E5%88%B0%E7%9A%84%E9%9A%BE%E7%82%B9)]
2. 说说自己做的比较好的项目？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/open.md#-%E8%AF%B4%E8%AF%B4%E8%87%AA%E5%B7%B1%E5%81%9A%E7%9A%84%E6%AF%94%E8%BE%83%E5%A5%BD%E7%9A%84%E9%A1%B9%E7%9B%AE)]
3. `React` 中有对状态管理有做进一步封装吗？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-react-%E4%B8%AD%E6%9C%89%E5%AF%B9%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86%E6%9C%89%E5%81%9A%E8%BF%9B%E4%B8%80%E6%AD%A5%E5%B0%81%E8%A3%85%E5%90%97)]
4. `React` 中如何在父组件获取子组件的方法？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-react-%E4%B8%AD%E5%A6%82%E4%BD%95%E5%9C%A8%E7%88%B6%E7%BB%84%E4%BB%B6%E8%8E%B7%E5%8F%96%E5%AD%90%E7%BB%84%E4%BB%B6%E7%9A%84%E6%96%B9%E6%B3%95)]
5. 低代码和微前端有了解吗？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md#-%E4%BD%8E%E4%BB%A3%E7%A0%81%E5%92%8C%E5%BE%AE%E5%89%8D%E7%AB%AF%E6%9C%89%E4%BA%86%E8%A7%A3%E5%90%97)]
6. `useCallback` 使用过没？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-usecallback-%E4%BD%BF%E7%94%A8%E8%BF%87%E6%B2%A1)]
7. 函数组价和类组件处理重复渲染有什么区别？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E5%87%BD%E6%95%B0%E7%BB%84%E4%BB%B7%E5%92%8C%E7%B1%BB%E7%BB%84%E4%BB%B6%E5%A4%84%E7%90%86%E9%87%8D%E5%A4%8D%E6%B8%B2%E6%9F%93%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB)]
8. 封装的按钮权限组件怎么实现？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E5%B0%81%E8%A3%85%E7%9A%84%E6%8C%89%E9%92%AE%E6%9D%83%E9%99%90%E7%BB%84%E4%BB%B6%E6%80%8E%E4%B9%88%E5%AE%9E%E7%8E%B0)]
9. 数据什么时候定义在组件里面，什么时候定义在状态管理里面？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E6%95%B0%E6%8D%AE%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%AE%9A%E4%B9%89%E5%9C%A8%E7%BB%84%E4%BB%B6%E9%87%8C%E9%9D%A2%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%AE%9A%E4%B9%89%E5%9C%A8%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86%E9%87%8C%E9%9D%A2)]
10. 方法什么时候写在父组件中，什么时候写在子组件中？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E6%96%B9%E6%B3%95%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%86%99%E5%9C%A8%E7%88%B6%E7%BB%84%E4%BB%B6%E4%B8%AD%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E5%86%99%E5%9C%A8%E5%AD%90%E7%BB%84%E4%BB%B6%E4%B8%AD)]

### 万云科技

1. `react` 用过哪些 `hooks`？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-react-%E7%94%A8%E8%BF%87%E5%93%AA%E4%BA%9B-hooks)]
2. 数组合并有哪些方法？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md#-%E6%95%B0%E7%BB%84%E5%90%88%E5%B9%B6%E6%9C%89%E5%93%AA%E4%BA%9B%E6%96%B9%E6%B3%95)]
3. 请求参数如何防篡改？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md#-%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0%E5%A6%82%E4%BD%95%E9%98%B2%E7%AF%A1%E6%94%B9)]
4. `localStorage` 如何跨域获取？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md#-localstorage-%E5%A6%82%E4%BD%95%E8%B7%A8%E5%9F%9F%E8%8E%B7%E5%8F%96)]
5. 如何写一个 `splice` 方法并覆盖数组的原方法？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md#-%E5%A6%82%E4%BD%95%E5%86%99%E4%B8%80%E4%B8%AA-splice-%E6%96%B9%E6%B3%95%E5%B9%B6%E8%A6%86%E7%9B%96%E6%95%B0%E7%BB%84%E7%9A%84%E5%8E%9F%E6%96%B9%E6%B3%95)]
6. `forEach` 循环和 `for` 循环哪个性能高？`forEach` 循环可以中断吗？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md#-foreach-%E5%BE%AA%E7%8E%AF%E5%92%8C-for-%E5%BE%AA%E7%8E%AF%E5%93%AA%E4%B8%AA%E6%80%A7%E8%83%BD%E9%AB%98foreach-%E5%BE%AA%E7%8E%AF%E5%8F%AF%E4%BB%A5%E4%B8%AD%E6%96%AD%E5%90%97)]
