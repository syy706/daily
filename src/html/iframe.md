# iframe src 设置

## 设置页面地址

## 设置 get 请求

## post 请求设置

```js
import React, { useRef } from "react";

const MyComponent = () => {
  const iframeRef = useRef(null);

  const handleSubmit = () => {
    const iframe = iframeRef.current;
    const form = document.createElement("form");
    form.method = "post";
    form.action = "your-post-url";
    iframe.contentDocument.body.appendChild(form);
    form.submit();
  };

  return (
    <div>
      <button onClick={handleSubmit}>Submit</button>
      <iframe ref={iframeRef} />
    </div>
  );
};

export default MyComponent;
```
