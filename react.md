# 整理 `React` 相关的面试题

以下问题来自 `百安居`：

### 🔴 `React` 中有对状态管理有做进一步封装吗？

<details>

<summary>答案：</summary>

`React` 本身除了 `useContext` 和 `useReducer` 之外，没有内置的复杂状态管理方案，但它的生态系统中有很多流行的状态管理库，为复杂组件间的状态管理提供了进一步的封装和优化。

### 主要的解决方案和封装

1. **`Context API`：**

- `React` 提供了 `Context API`，可以不用通过每一层组件传递 `props` 的情况下，全局共享状态。
- 但当应用程序变得复杂时，单靠 `Context API` 管理状态会变得繁琐，并且可能导致性能问题，特别是组件不必要的重新渲染。

2. **`React Redux`：**

- 提供了一种可预测的方式来管理和集中应用的状态。
- 通过中间件（如 `redux-thunk` 或 `redux-saga`），`Redux` 可以处理副作用。
- 此外，`React-Redux` 可以更高效地将 `Redux` 与 `React` 组件结合起来。

> `Redux Toolkit`：`Redux` 的封装，简化了传统 `Redux` 的配置，减少了样板代码，并提供了处理异步逻辑的 `createAsyncThunk` 工具。

3. **`Recoil`：**

- `Facebook` 开发的一个状态管理库，旨在与 `React` 的并发模式无缝工作。
- 它专注于高效地管理全局和派生状态，允许更细粒度的响应式更新。
- 只有使用了特定状态的组件会在该状态变化时重新渲染。

4. **`Zustand`：**

- 一个小巧、快速、可扩展的状态管理库
- 提供了一个简单的 `API` 来管理全局和局部状态，并避免不必要的重新渲染。
- 相比 `Redux` 更简洁，适用于小到中型项目。

5. **`Jotai`：**

- 另一个轻量级的状态管理库，基于 `React` 的 `Context API` 构建
- 提供了一种更结构化的方式来管理 `atoms`（状态单元）。
- 它使不同状态之间的依赖关系更加显式化，类似 `Recoil`，可以做到细粒度的更新。

6. **`MobX`：**

- 专注于简洁和响应式编程，允许状态自动派生和更新，减少手动将状态连接到组件的需求。
- `React` 组件可以观察状态的变化，`MobX` 确保只进行必要的最少量的重新渲染。

7. **`React Query`：**

- 虽然 `React Query` 不是纯粹的状态管理库，但它是管理服务器状态（如 `API` 数据）的利器
- 简化了数据获取逻辑、缓存、同步和更新等操作，特别适合处理异步数据。

### 总结:

`React` 的核心功能可以通过不同的状态管理解决方案得到扩展，如 `Redux`、`Recoil`、`MobX` 等。这些解决方案根据项目的复杂性，为状态管理提供了不同的优化，通常在管理大规模应用时提升性能并简化代码组织。具体使用哪一个取决于项目的需求。

</details>

### 🔴 `React` 中如何在父组件获取子组件的方法？

<details>

<summary>在 React 中，父组件可以通过以下几种方式获取子组件的方法：</summary>

### 一、使用 `refs`

1. 在父组件中创建一个 `ref`：

```tsx
const RefParentCom: FC = () => {
  const comRef = useRef();
  return (
    <div>
      <p>Ref parent component</p>
      <p>
        <button onClick={() => comRef.current?.callChildMethod()}>
          click me
        </button>
      </p>
      <hr />
      <RefSubCom ref={comRef} />
    </div>
  );
};
```

2. 在子组件中暴露需要被父组件调用的方法：

```tsx
const RefSubCom = forwardRef<SubRefInstance>((_, ref) => {
  useImperativeHandle(ref, () => ({
    callChildMethod: () => console.log("Ref child method called"),
  }));
  return <p>Ref children component</p>;
});
interface SubRefInstance {
  callChildMethod: () => viod;
}
```

完整实例：https://codepen.io/levi0001/pen/oNKBwwa

### 二、通过 `context` 父组件调用子组件的方法

1. 创建一个 `context`，并包裹在父子组件最外层：

```tsx
const ConnContext = createContext<ConnInstance>({} as ConnInstance);
const App: FC = () => {
  return (
    <ConnContext.Provider value={{}}>
      <ParentComponent>
        <SubComponent />
      </ParentComponent>
    </ConnContext.Provider>
  );
};
interface ConnInstance {
  callChildMethod?: () => void;
}
```

2. 子组价获取 `context` 并绑定方法

```tsx
const SubComponent: FC = () => {
  const conn = useContext(ConnContext);
  useEffect(() => {
    conn.callChildMethod = () => console.log("call sub method");
  }, [conn]);
  return <p>Sub children component</p>;
};
```

3. 父组价通过 `context` 调用子组件的方法

```tsx
const ParentComponent: FC<PropsWithChildren> = ({ children }) => {
  const conn = useContext(ConnContext);
  return (
    <div>
      <p>Parent children component</p>
      <p>
        <button onClick={() => conn?.callChildMethod()}>click me</button>
      </p>
      <hr />
      {children}
    </div>
  );
};
```

完整实例：https://codepen.io/levi0001/pen/YzmNQvb

</details>

### 🔴 低代码和微前端有了解吗？

<details>

<summary>答案：</summary>

### 低代码

低代码是一种快速开发应用程序的方法，有以下几个特性：

1. **特点**：可视化开发、提高产出速度、降低开发门槛
2. **优势**：提高效率、降低人力成本、易于维护
3. **应用场景**：企业内部管理系统、移动应用开发、数据可视化
4. **数据发展**：随着技术的不断进步，低代码开发平台将越来越智能化，能够自动生成更多的代码，进一步提高开发效率。同时，低代码开发也将与人工智能、大数据等技术相结合，为企业提供更强大的解决方案。

由于我本人对 `formily` 比较了解，所以结合 `formily` 的特性在低代码中发挥的用途，我总结的 `formily` 的记录：https://github.com/cgfeel/formily

**精确渲染**

`formily` 采用 `MVVM` 设计模式。将视图模型抽象出来然后在 `DSL` 模板层消费，`DSL` 借助依赖收集机制在视图模型中统一调度，保证精确渲染。借助于 `Mobx` 从 `MVVM` 模型抽象出状态管理解决方案，设计出了 `@formily/reactive`。

> `DSL`（`Domain Specific Language`）为特定领域设计的语言片段，如 `vue` 中：
>
> - 双花括号表示用于绑定数据 `{{message}}`
> - 使用 `@click` 绑定事件
>
> `formily` 中的 `DSL`：通过内置表达式作用域，见：文档 [[查看](https://react.formilyjs.org/zh-CN/api/shared/schema#%E5%86%85%E7%BD%AE%E8%A1%A8%E8%BE%BE%E5%BC%8F%E4%BD%9C%E7%94%A8%E5%9F%9F)]

**领域模型**

`formily` 根据数据值、组件、展示状态、路径等抽象出模型，它包含了字段相关的所有状态，只要去操作这些状态就能引发联动。这样通过模型就能让表单的联动变得可枚举可预测。

**路径系统**

`formily` 的路径系统 `@formily/path` 很好的解决了这个问题，不仅仅是让字段查找变得优雅，它还能通过解构表达式去处理前后端数据结构不一致的恶心问题。

将其作为顶层模型管理着所有字段模型，让每个字段都有着自己的路径。在异步事件动作中，优雅的查找某个字段实现联动。

**生命周期**

`formily` 有着比 `React` 更细粒度的生命周期，无论对于顶层表单，还是叶子节点的字段，包括模型驱动，无论是初始化还是数据更新、亦或者状态变化都能够对应匹配。

</details>
