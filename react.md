# 整理 `React` 相关的面试题

`React` 中如何在父组件获取子组件的方法

<details>

<summary>在 React 中，父组件可以通过以下几种方式获取子组件的方法：</summary>

### 一、使用 refs

1. 在父组件中创建一个 ref：

```typescript
const RefSubCom = forwardRef<SubRefInstance>((_, ref) => {
  useImperativeHandle(ref, () => ({
    callChildMethod: () => console.log("Ref child method called"),
  }));
  return <p>Ref children component</p>;
});

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

</details>
