# 一些不常用或者容易忘记的 api

## visibilitychange

页面的可见性发生变化（最小化、最大化、切换标签页）

```js
window.addEventListener("visibilitychange", () => {
  if (document.visibilityState === "visible") {
    // TODO
  } else {
    // TODO
  }
});
```

## Broadcast Channel API

它允许浏览器上下文互相发送和接收基本数据

```js
//a.js
const broadcast = new BroadcastChannel("new_channel");
broadcast.postMessage("text");

setTimeout(() => {
  broadcast.close();
});
```

```js
//b.js
const broadcast = new BroadcastChannel("new_channel");
broadcast.on("message", ({ data, origin, lastEventId, source, ports }) => {
  console.log(data);
  //text
});
```

### 和 window.postMessage 的区别

1、broadcast 消息通道，允许多个窗口和标签页监听同一个页面,并接收发送到该通道 的消息
2、broadcast 需要同源

## Internationalization API

处理国际化和本地化的 Web API

### API

1、Intl.Collator: 用于比较字符串的对象，可用于排序和搜索操作。

```js
const strings = ["apple", "Banana", "cherry", "date"];
const collator = new Intl.Collator("en-US", { sensitivity: "base" });

strings.sort(collator.compare);
console.log(strings); // 输出: ["apple", "Banana", "cherry", "date"]
```

2、Intl.DateTimeFormat: 用于格式化日期和时间的对象。

```js
const date = new Date("2022-05-15T09:30:00Z");
const formatter = new Intl.DateTimeFormat("fr-FR", {
  weekday: "long",
  year: "numeric",
  month: "long",
  day: "numeric",
  hour: "numeric",
  minute: "numeric",
  timeZone: "UTC",
});

console.log(formatter.format(date)); // 输出: dimanche 15 mai 2022 à 09:30
```

3、Intl.NumberFormat: 用于格式化数字的对象。

```js
const number = 1234567.89;
const formatter = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",
});

console.log(formatter.format(number)); // 输出: $1,234,567.89
```

4、Intl.PluralRules: 用于确定给定数字的复数形式的对象。

```js
const formatter = new Intl.PluralRules("en-US");
console.log(formatter.select(1)); // 输出: one
console.log(formatter.select(2)); // 输出: other
```

5、Intl.RelativeTimeFormat: 用于格式化相对时间的对象。

```js
const rtf = new Intl.RelativeTimeFormat("en", { numeric: "auto" });

console.log(rtf.format(-1, "day")); // 输出: yesterday
console.log(rtf.format(1, "day")); // 输出: tomorrow
console.log(rtf.format(-2, "month")); // 输出: 2 months ago
console.log(rtf.format(3, "quarter")); // 输出: in 3 quarters
```
