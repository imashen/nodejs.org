---
title: Node.js 简介
layout: learn
authors: flaviocopes, potch, MylesBorins, RomainLanz, virkt25, Trott, onel0p3z, ollelauribostrom, MarkPieszak, fhemberger, LaRuaNa, FrozenPandaz, mcollina, amiller-gh, ahmadawais, saqibameen, dangen-effy, aymen94, benhalverson, imashen
---

# Node.js 简介

Node.js 是一个开源、跨平台的 JavaScript 运行环境。它几乎是所有类型项目的常用工具！

Node.js 在浏览器之外运行 V8 JavaScript 引擎，即 Google Chrome 的核心。这使 Node.js 的性能非常出色。

Node.js 应用在单个进程中运行，不会为每个请求创建新线程。Node.js 在其标准库中提供了一组异步 I/O 基元，可防止 JavaScript 代码阻塞，并且通常 Node.js 中的库是使用非阻塞范例编写的，这使得阻塞行为不会轻易发生。

当 Node.js 执行 I/O 操作（如从网络读取、访问数据库或文件系统）时，Node.js 不会阻塞线程并浪费 CPU 周期等待，而是会在响应返回时恢复操作。

这使 Node.js 能够使用单个服务器处理数千个并发连接，而​​不会带来高并发造成的负担，进而能够避免较大的错误和BUG。

Node.js 具有独特的优势，方便数百万为浏览器编写 JavaScript 的前端开发者编写服务器端代码以及客户端代码，无需额外的学习成本。

在 Node.js 中可以顺利使用新的 ECMAScript 标准，因为您不必等待所有用户更新他们的浏览器，您可以通过更改 Node.js 版本来决定使用哪个 ECMAScript 版本，还可以通过使用特殊标记运行 Node.js 来启用特定的实验功能。

## Node.js 应用程序示例

Node.js 最常见的例子是将 Hello World 作为Web服务器：

```cjs
const { createServer } = require('node:http');

const hostname = '127.0.0.1';
const port = 3000;

const server = createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

```mjs
import { createServer } from 'node:http';

const hostname = '127.0.0.1';
const port = 3000;

const server = createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

要运行此代码段，请将其保存为 `server.js` 文件并在终端中运行 `node server.js`。

此代码首先包含 [`http` 模块](https://nodejs.org/api/http.html).

Node.js 有一个很棒的 [标准库](https://nodejs.org/api/), 包括对网络的一流支持。

`http`的 `createServer()` 方法创建一个新的 HTTP 服务器并返回它

服务器设置为监听指定的端口和主机名。当服务器准备就绪时，将调用回调函数，在这种情况下会在终端通知我们服务器正在运行。

每当收到新请求时，就会调用 [`request` 事件](https://nodejs.org/api/http.html#http_event_request) 提供两个对象: 请求 (an [`http.IncomingMessage`](https://nodejs.org/api/http.html#http_class_http_incomingmessage) object) 和响应 (an [`http.ServerResponse`](https://nodejs.org/api/http.html#http_class_http_serverresponse) object).

这两个对象对于处理 HTTP 调用至关重要。

第一个提供请求详细信息。在此简单示例中，未使用此功能，但你可以访问请求标头和请求数据。

第二个用于将数据返回给调用者。

在这种情况下：

```js
res.statusCode = 200;
```

我们将 statusCode 属性设置为 200，以指示成功响应。

我们设置了 Content-Type 标头：

```js
res.setHeader('Content-Type', 'text/plain');
```

关闭响应，将内容作为参数添加到 `end()`:

```js
res.end('Hello World\n');
```