[TOC]
#### 架设HTTP服务
    const Koa = require('koa');
    const app = new Koa();
    app.listen(3000);
#### context对象
Koa 提供一个 Context 对象，表示一次对话的上下文（包括 HTTP 请求和 HTTP 回复）
- context.request
    - context.request.body:用户发送的内容
- context.reponse
    - context.response.body:发送给用户的内容
    - context.response.accepts():客户端希望接受的数据类型
    ```
    const main = ctx => {
        if (ctx.request.accepts('xml')) {
          ctx.response.type = 'xml';
          ctx.response.body = '<data>Hello World</data>';
        } else if (ctx.request.accepts('json')) {
          ctx.response.type = 'json';
          ctx.response.body = { data: 'Hello World' };
        } else if (ctx.request.accepts('html')) {
          ctx.response.type = 'html';
          ctx.response.body = '<p>Hello World</p>';
        } else {
          ctx.response.type = 'text';
          ctx.response.body = 'Hello World';
        }
    };
    ```
    - context.response.type:指定返回类型
> Koa默认返回类型为text/plain
#### 
