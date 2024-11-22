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
- 重要：若以上答案出现遗漏偏差，再根据实际情况复盘，修正

目前已有题目做复盘修正，尤其是 `GPT` 给出的答案可能考虑的角度并没有那么深入

> 需要说明的是，整理的文档不会标注更新日期，如有必要请参考 `commit` 记录 [[查看](https://github.com/cgfeel/frontend-interview-questions/commits/main/)]

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

### `Javascript` 篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md

### `React` 篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md

### `Webpack` 篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/webpack.md

### 开放问题篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/open.md

### 前端场景篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md

### 前端输出篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md

### 网络篇

https://github.com/cgfeel/frontend-interview-questions/blob/main/document/network.md

## 来源索引

归纳有明确出处的面试题

### 百安居 1 面

1. 项目中遇到的难点？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/open.md#-%E9%A1%B9%E7%9B%AE%E4%B8%AD%E9%81%87%E5%88%B0%E7%9A%84%E9%9A%BE%E7%82%B9)]
2. 说说自己做的比较好的项目？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/open.md#-%E8%AF%B4%E8%AF%B4%E8%87%AA%E5%B7%B1%E5%81%9A%E7%9A%84%E6%AF%94%E8%BE%83%E5%A5%BD%E7%9A%84%E9%A1%B9%E7%9B%AE)]
3. `React` 中有对状态管理有做进一步封装吗？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-react-%E4%B8%AD%E6%9C%89%E5%AF%B9%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86%E6%9C%89%E5%81%9A%E8%BF%9B%E4%B8%80%E6%AD%A5%E5%B0%81%E8%A3%85%E5%90%97)]
4. `React` 中如何在父组件获取子组件的方法？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-react-%E4%B8%AD%E5%A6%82%E4%BD%95%E5%9C%A8%E7%88%B6%E7%BB%84%E4%BB%B6%E8%8E%B7%E5%8F%96%E5%AD%90%E7%BB%84%E4%BB%B6%E7%9A%84%E6%96%B9%E6%B3%95)]
5. 低代码和微前端有了解吗？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md#-%E4%BD%8E%E4%BB%A3%E7%A0%81%E5%92%8C%E5%BE%AE%E5%89%8D%E7%AB%AF%E6%9C%89%E4%BA%86%E8%A7%A3%E5%90%97)]
6. `useCallback` 使用过没？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-usecallback-%E4%BD%BF%E7%94%A8%E8%BF%87%E6%B2%A1)]
7. 函数组件和类组件处理重复渲染有什么区别？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-%E5%87%BD%E6%95%B0%E7%BB%84%E4%BB%B6%E5%92%8C%E7%B1%BB%E7%BB%84%E4%BB%B6%E5%A4%84%E7%90%86%E9%87%8D%E5%A4%8D%E6%B8%B2%E6%9F%93%E6%9C%89%E4%BB%80%E4%B9%88%E5%8C%BA%E5%88%AB)]
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
7. 谈谈前端性能优化？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md#-%E8%B0%88%E8%B0%88%E5%89%8D%E7%AB%AF%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96)]
8. 做的最好和最有成就的项目是哪个？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/open.md#-%E5%81%9A%E7%9A%84%E6%9C%80%E5%A5%BD%E5%92%8C%E6%9C%80%E6%9C%89%E6%88%90%E5%B0%B1%E7%9A%84%E9%A1%B9%E7%9B%AE%E6%98%AF%E5%93%AA%E4%B8%AA)]
9. 性格优缺点？爱好？前同事对你的评价？未来的规划？平时怎么学习？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/open.md#-%E6%80%A7%E6%A0%BC%E4%BC%98%E7%BC%BA%E7%82%B9%E7%88%B1%E5%A5%BD%E5%89%8D%E5%90%8C%E4%BA%8B%E5%AF%B9%E4%BD%A0%E7%9A%84%E8%AF%84%E4%BB%B7%E6%9C%AA%E6%9D%A5%E7%9A%84%E8%A7%84%E5%88%92%E5%B9%B3%E6%97%B6%E6%80%8E%E4%B9%88%E5%AD%A6%E4%B9%A0)]

### Gate.io

**1 面**

- 说一下箭头函数和普通函数的区别？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/js.md#-%E8%AF%B4%E4%B8%80%E4%B8%8B%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0%E5%92%8C%E6%99%AE%E9%80%9A%E5%87%BD%E6%95%B0%E7%9A%84%E5%8C%BA%E5%88%AB)]
- `React` 为什么用 `function` 组件代替 `class` 组件？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/react.md#-react-%E4%B8%BA%E4%BB%80%E4%B9%88%E7%94%A8-function-%E7%BB%84%E4%BB%B6%E4%BB%A3%E6%9B%BF-class-%E7%BB%84%E4%BB%B6)]
- 前端如何优化 `FCP`？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md#-%E5%A6%82%E4%BD%95%E4%BC%98%E5%8C%96%E5%89%8D%E7%AB%AF-fcp)]
- 说下 XSS 攻击，以及前端如何预防？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/scene.md#-%E8%AF%B4%E4%B8%8B-xss-%E6%94%BB%E5%87%BB%E4%BB%A5%E5%8F%8A%E5%89%8D%E7%AB%AF%E5%A6%82%E4%BD%95%E9%A2%84%E9%98%B2)]
- 浏览器中的 `options` 请求说一下？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/network.md#-%E8%AF%B4%E4%B8%80%E4%B8%8B%E6%B5%8F%E8%A7%88%E5%99%A8%E7%9A%84-cors-%E5%90%8C%E6%BA%90%E7%AD%96%E7%95%A5)]
- `http/2` 相对于 `http/1.1` 更新了什么？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/network.md#-http2-%E7%9B%B8%E5%AF%B9%E4%BA%8E-http11-%E6%9B%B4%E6%96%B0%E4%BA%86%E4%BB%80%E4%B9%88)]
- 请聊一下 `http3`？ [[查看](https://github.com/cgfeel/frontend-interview-questions/blob/main/document/network.md#-%E8%AF%B7%E8%81%8A%E4%B8%80%E4%B8%8B-http3)]

### 字节

来自外包 `hr` 整理提供

**笔试题**

包含如下，整理在 `codepen` [[查看](https://codepen.io/collection/EPjerE)]

- 手写实现 `EventBus`，观察者模式
- `LocalStorage` 实现 `60s` 后自动删除（我通过 `Proxy` 实现）
- 手撕防抖、节流函数
- 根据一个对象替换模板中的模板变量
- 实现数组翻转
- `EventLoop` 打印顺序，有 3 道
- 给定一个字符串如 `abc` 打印出所有的可能出现的顺序
- `var` 变量在 `for` 循环中的问题
- 手写 `hooks` 实现一个 `input` 组件
- 用 `react` 实现一个倒计时器组件，使用用户传入的格式比如 `hh/mm/ss` 进行显示
- 写一个计时器实现开始暂停记录清除
- `React 16` 合成事件和原生事件冒泡顺序
- 判断是不是回文数字
- 作用域和原型链输出、修改作用域后的输出
- 数组去重
- 实现垂直居中
- 实现一个 `Promise.all`
- 手写 `Promise` 请求队列
- 算法题：将数组按照层级变成对象

## 写在最后：为什么要背题

很多人会有个疑问，为什么要背题？难道不是应该去理解吗，去实践得出来吗？

首先对此我不排斥背题，其次回想一下是否也有过如下经历：

1. 面试的问题似乎都理解，但不知道从什么地方说起或无法组织话术？
2. 能够说出一两个关键答案，但不够全面也不够深入？
3. 面试官到底在问什么？
4. 我似乎在哪里看到过，很久没做或看的太少淡忘了？
5. 这个我做过但说不出来，或者你让我写没有参考也不知道从什么地方下手？
6. 回答的七七八八，似乎也都说了，面试结束后复盘发现漏了关键点？

除此之外：

- 大前端是一个很广的范围，你可能涉猎的也非常广、非常深，但总归有知识盲区

通过背题也是一种高效理解知识的方式：

- 回顾和复盘能够增进记忆，增加对知识的深度和广度
- 能够从容应对面试问题，弥补知识遗漏的盲区
- 每个领域都有特定的关注点，不一定每个都要垂直深入
