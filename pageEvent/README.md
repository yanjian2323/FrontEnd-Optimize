页面的生命周期中，dcoument.readyState会经历3个阶段,loading->interactive->complete，complete在window.onload事件后, onload要等到页面上所有的资源都加载执行完才触发，包括js、图片、css，DomContentLoaded在页面DOM就绪后就会触发(不管图片有没有下载完)

#### defer异步加载js

1. defer不会阻塞页面的渲染
2. 用defer加载的js会阻塞DOMContentLoaded事件
3. 如果同时用defer加载多个js，defer可以保证是按照加载顺序执行

#### async异步加载js

1. async也不会阻塞页面的渲染
2. 用async加载的js不会阻塞DOMCotentLoaded事件
3. 如果同时用async加载多个js，async不能保证是按照加载顺序执行

#### 使用preload加载资源

用preload加载资源使用link，如下代码：

```javascript

<link rel="preload" href="/pageEvent/js/preload.js" as="script" onload="handle()" />

function handle() {
  let sc = document.createElement('script');
  sc.src = '/pageEvent/js/preload.js';
  document.head.appendChild(sc);
}
```

1. preload加载完资源后会触发onload事件
2. preload可以使资源预先加载,但是加载完并不会执行，如果要执行，需要写上面代码中handle函数的代码
3. preload不会阻塞window的onload事件，script defer和script async会阻止window的onload