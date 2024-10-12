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
```

2. 在子组件中暴露需要被父组件调用的方法：

```typescript
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

</details>
