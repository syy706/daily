# 为了更迅速的定位到 ts 报错的原因

## ts2783

多次指定了 "name"，因此将重写此用法。

```js
const allStates = Object.entries(stateDSL ?? {}).map(
  ([stateName, stateInfo]) => {
    return { name: stateName, ...stateInfo };
  }
);
```

stateInfo 内也包含了 name 属性
