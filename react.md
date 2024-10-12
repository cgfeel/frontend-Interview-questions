# 整理 `React` 相关的面试题

`React` 中如何在父组件获取子组件的方法

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
