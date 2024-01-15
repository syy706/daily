# 取消 http 请求

## 用法

```js
let controller = new AbortController();
const { signal } = controller;

const abortBtn = document.createElement("button");
abortBtn.addEventListener("click", () => {
  controller.abort();
});
fetch(url, { signal }).then((response) => {
  console.log("Download complete", response);
});
```

## 场景

### 在 useEffect 中， 接口首次请求过程时， dependencies 变更，组件重新渲染, 接口二次请求，但第一次请求返回时，触发 setState 逻辑，数据展示异常

### 接口请求时传入 signal, 组建卸载时 controller.abort();
