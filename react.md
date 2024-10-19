# 整理 `React` 相关的面试题

以下问题来自 `百安居` 1 面：

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

由于我本人对 `formily` 比较了解，所以结合 `formily` 的特性在低代码中发挥的用途，我总结的 `formily` 记录：https://github.com/cgfeel/formily

- 提供了开箱即用的开源低代码编辑器
- 采用 `MVVM` 设计模式，精确渲染，将视图模型抽象出来，然后在 DSL 模板层消费
- 提供领域模型，可以多字段联动，主动、被动受控
- 提供点对点的路径系统，能够在低代码中匹配、筛查特定字段
- 细粒度极高的生命周期，从顶层的表单，到底层的字段，从创建到更新，每一个阶段都有对应生命周期
- 协议驱动，提供 `schema`，可以完美通过 `json` 驱动视图
- 分层架构，主要分为 4 大库
  - `@formily/reactive`：数据记录，状态更新
  - `@formily/core`：模型解析、生命周期
  - `@formily/react`：桥接 `react`，使其拥有调用 `formily` 能力
  - `@formily/antd-v5`：`UI` 库之一，作为模型下的组件库，也可以自定义或适配第三方库

### 微前端

微前端是一种将前端应用拆分为多个独立小型前端应用的架构模式。

**主要特点**

1. **独立开发**：各个微前端应用可以由不同的团队独立开发，使用不同的技术栈，提高开发效率。
2. **独立部署**：每个微前端应用可以独立部署，不影响其他应用，实现快速迭代。
3. **技术栈无关**：允许在一个项目中集成不同技术栈的应用，增加了技术选型的灵活性。

**优势**

1. **提升开发效率**：团队可以专注于特定的微前端应用，减少开发过程中的冲突和协调成本。
2. **增强可维护性**：较小的代码库更容易理解和维护。
3. **灵活升级**：可以逐步升级单个微前端应用，而无需对整个系统进行大规模升级。

**实现方式**

1. **路由分发**：通过路由将不同的 `URL` 分配给不同的微前端应用，如：`qiankun`、`single-spa`。
2. **组合式应用**：将多个微前端应用组合在一个页面中，通过 `iframe` 进行管理，如：`wujie` 降级模式 `degradee`。
3. **微组件化**：将微前端应用封装成 `web-component`，在主应用中动态加载，如：`micro-app`、`wujie` 默认模式。

我总结的微前端记录：https://github.com/cgfeel/zf-micro-app

</details>

### 🔴 `useCallback` 使用过没？

<details>

<summary>答案：</summary>

`useCallback` 是 `React` 中的一个 `Hook`。它用于返回一个 `memoized` 回调函数，在依赖项不变的情况下，多次渲染之间始终返回相同的函数实例。这有助于避免在组件重新渲染时，因为回调函数的重新创建而导致子组件不必要的重新渲染。

**使用场景**

1. 当把回调函数传递给子组件时，如果这个回调函数在每次父组件渲染时都重新创建，可能会导致子组件的性能问题。使用 `useCallback` 可以避免这种情况。
2. 在优化性能时，对于一些复杂的计算或可能频繁触发重新渲染的场景，使用 `useCallback` 可以确保只有在必要的时候才重新计算回调函数。

**示例用法**

```tsx
import { FC, useCallback } from "react";

const MyComponent: FC = () => {
  const handleClick = useCallback(() => {
    console.log("Button clicked");
  }, []);

  return <button onClick={handleClick}>Click me</button>;
};

export default MyComponent;
```

在这个例子中 `handleClick` 回调函数在组件初次渲染时创建一次，因为依赖项数组为空。如果有依赖项，只有当依赖项发生变化时，才会重新创建回调函数。

</details>

### 🔴 函数组价和类组件处理重复渲染有什么区别？

<details>

<summary>答案：</summary>

**函数组件**

1. 利用 `React.memo`：将函数组件包裹在 `React.memo` 中来实现浅比较 `props` 的方式来减少重复渲染。当组件的 `props` 没有变化时，组件不会重新渲染。
2. 依赖优化：在使用 `useEffect`、`useMemo` 和 `useCallback` 等 Hook 时，可以通过精确指定依赖项数组来控制何时触发副作用和计算新的值，从而避免不必要的重复渲染。

`React.memo` 默认是浅比较，可以通过第 2 个参数进行深度检查：

```tsx
import { FC, memo } from "react";

const MyComponent: FC<MyComProps> = ({ value }) => <>component: {value}</>;

interface MyComProps {
  value: string;
}

export default memo(MyComponent, (prev, next) => prev.value !== next.value);
```

**类组件**

1. `shouldComponentUpdate`：重写类组件的 `shouldComponentUpdate` 方法来进行更细粒度的控制，决定是否进行重新渲染。该方法接收新的 `props` 和 `state` 作为参数，通过比较它们与当前的 `props` 和 `state`，返回一个布尔值来决定是否重新渲染组件。
2. `PureComponent`：类组件可以继承 `React.PureComponent`，它会对 `props` 和 `state` 进行浅比较来决定是否重新渲染组件。但只进行浅比较，不够灵活。

总的来说，函数组件在处理重复渲染时更加简洁和灵活，可以通过 `hook` 和 `React.memo` 等方式进行优化。而类组件则需要通过重写特定方法或继承特定类来实现类似的效果，相对来说较为复杂。

</details>

### 🔴 封装的按钮权限组件怎么实现？

<details>

<summary>答案：</summary>

根据传递的 `props` 检查对应的状态，给出对应的视图

1. 创建按钮组件通过 `props` 判断权限

```tsx
const CustomButton: FC<PropsWithChildren<CustomButtonProps>> = ({
  children,
  permissionKey,
}) => {
  const group = ["add", "edit"];
  return group.includes(permissionKey) ? (
    <button>{children}</button>
  ) : (
    <button disabled>{children}</button>
  );
};
```

2. 提供不同的 `key` 使用组件

```tsx
const App: FC = () => (
  <>
    <CustomButton permissionKey="add">Add</CustomButton>{" "}
    <CustomButton permissionKey="disable">Del</CustomButton>
  </>
);
```

完整演示：https://codepen.io/levi0001/pen/abepYKK

**总结**

在实际应用中，可以根据具体的权限管理方案来获取用户权限信息，比如从后端获取用户角色信息后进行判断，或者使用状态管理库来存储和管理权限状态。同时，可以根据需要扩展组件的功能，如添加不同的按钮样式、处理点击事件等。

</details>

### 🔴 数据什么时候定义在组件里面，什么时候定义在状态管理里面？

<details>

<summary>一般来说，可以从以下几个方面考虑数据定义的位置：</summary>

**定义在组件里面：**

- 当数据仅在特定组件内部使用，并且不会被其他组件共享或影响多个组件状态时，可以定义在组件内部。
- 如果数据的生命周期与组件的生命周期紧密相关，随着组件的创建而创建，销毁而销毁，适合放在组件里。
- 对于一些临时的、局部的、快速变化且不需要在多个地方同步的数据，可以放在组件内。

**定义在状态管理里面：**

- 当数据需要在多个组件之间共享和同步时，应该放在状态管理中。比如用户的登录状态、购物车中的商品信息等，这些数据可能会被多个不同的组件访问和修改。
- 如果数据的变化会引起多个组件的状态更新，为了更好地管理这种复杂的状态变化，将数据放在状态管理中可以集中处理状态的更新逻辑。
- 对于一些全局的、持久化的数据，如应用的配置信息等，适合放在状态管理中，以便在整个应用中随时访问和修改。

</details>

### 🔴 方法什么时候写在父组件中，什么时候写在子组件中？

<details>

<summary>以下是关于方法写在父组件和子组件中的考虑因素：</summary>

**写在父组件中：**

- 当方法的逻辑主要涉及多个子组件的协调或者对多个子组件的状态进行统一管理时，适合写在父组件中。例如，一个页面有多个子组件，父组件需要根据某个条件同时控制这些子组件的显示或隐藏，此时控制显示隐藏的方法就可以写在父组件中。
- 如果方法是与整个应用的全局状态或业务逻辑相关，而不是特定于某个子组件的功能，通常放在父组件中。比如，在一个电商应用中，父组件可能有一个方法用于处理购物车的总价计算，这个计算可能涉及多个子组件中的商品信息。

**写在子组件中：**

- 当方法的逻辑完全是为了实现子组件自身的特定功能，并且与其他组件没有直接关系时，应该写在子组件中。例如，一个子组件是一个输入框，它有一个方法用于验证输入内容的格式是否正确，这个方法就适合写在子组件中。
- 如果方法只影响子组件自身的状态变化和行为，不涉及到父组件或其他子组件的状态管理，那么可以放在子组件内。比如，一个子组件是一个下拉菜单，它有一个方法用于展开或收起菜单的功能，这个方法就可以放在子组件中。

</details>

---

以下问题来自 `万云科技`：

### 🔴 `react` 用过哪些 `hooks`？

<details>

<summary>答案：</summary>

**基础状态管理：**

1. `useState`：用于在函数组件中添加状态，可以接收并管理各种数据类型的状态。
2. `useReducer`：用于处理复杂的状态逻辑，它接收一个 `reducer` 函数和初始状态作为参数。

> 此类 `hooks` 都返回当前状态和一个 `dispatch` 函数来触发状态更新。

**副作用处理：**

1. `useEffect`：用于处理组件挂载、更新和卸载时的副作用操作，比如发送网络请求、订阅事件、手动修改 DOM 等。
2. `useLayoutEffect`：与 `useEffect` 类似，但它会在浏览器渲染之前同步执行副作用操作，适合处理涉及布局的副作用。

此类 `hooks` 都接受 2 个参数：

- 参数 1：函数用于执行回调
- 参数 2：依赖项数组，只有当依赖项发生变更才触发更新

关于依赖项：

- 不提供：随每次渲染执行回调
- 空数组：仅首次渲染执行回调
- 带有状态的依赖项数组：只有状态变更才执行回调

回调返回函数：

- 执行前都会先执行返回的函数，`React` 中此类 `hooks` 采用先出后进的原则

**上下文和引用类：**

1. `useContext`：用于在函数组件中访问 `React` 的上下文（`Context`），可以方便地在组件树中传递和共享数据，避免通过层层传递 `props`。
2. `useRef`：用于创建一个可变的引用，可以在组件的整个生命周期中保持对某个值的引用，而不会引起组件的重新渲染。

**性能优化类：**

1. `useMemo`：用于缓存计算结果，只有当依赖项发生变化时才重新计算。可以避免不必要的计算，提高性能。
2. `useCallback`：与 `useMemo` 类似，用于缓存函数，只有当依赖项发生变化时才重新创建函数。可以避免不必要的函数重新创建，特别是在将函数作为 `props` 传递给子组件时。
3. `useTransition`：用于处理 “并发模式”（`Concurrent Mode`）的 `hook`，主要用于管理并发更新，使用户界面保持响应。

</details>

### 🔴 其他

见 `javascript` 篇：https://github.com/cgfeel/frontend-interview-questions/blob/main/js.md#-%E6%95%B0%E7%BB%84%E5%90%88%E5%B9%B6%E6%9C%89%E5%93%AA%E4%BA%9B%E6%96%B9%E6%B3%95

---

以下问题来自 `gate.io` 1 面：

### 🔴 `React` 为什么用 `function` 组件代替 `class` 组件？

<details>

<summary>在 React 中，越来越倾向于使用函数组件代替类组件，主要有以下几个原因：：</summary>

#### 一、简洁性

**1. 代码更简洁**

函数组件通常比类组件更简洁明了。它们以函数的形式定义组件，没有类的复杂语法和结构，减少了代码的行数和复杂度。

例如，一个简单的展示用户信息的组件，用函数组件可以这样写：

```tsx
const UserInfo: FC = ({ user }) => {
  return <div>Hello, {user.name}!</div>;
};
```

2. 提供不同的 `key` 使用组件

```tsx
const App: FC = () => (
  <>
    <CustomButton permissionKey="add">Add</CustomButton>{" "}
    <CustomButton permissionKey="disable">Del</CustomButton>
  </>
);
```

完整演示：https://codepen.io/levi0001/pen/abepYKK

**总结**

在实际应用中，可以根据具体的权限管理方案来获取用户权限信息，比如从后端获取用户角色信息后进行判断，或者使用状态管理库来存储和管理权限状态。同时，可以根据需要扩展组件的功能，如添加不同的按钮样式、处理点击事件等。

</details>

### 🔴 其他

见网络篇：https://github.com/cgfeel/frontend-interview-questions/blob/main/network.md#-http2-%E7%9B%B8%E5%AF%B9%E4%BA%8E-http11-%E6%9B%B4%E6%96%B0%E4%BA%86%E4%BB%80%E4%B9%88
