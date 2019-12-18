# Koa No Order

## 路由

### 基本

单独分离出来，

```bash
npm install -D koa
npm install -D koa-router #需要安装koa-router
```

**基本代码：**

```javascript
const koa = require('koa');
const koraRouter = require('koa-router');

let server = new koa();
server.listen(8080);

let router = new koraRouter();
```

**编写路由：**

```javascript
router.get('/b', async ctx => {
    ctx.body = 'hello world'; // 想返回什么，往什么放
});

server.use(router.routes()); // 必须使用
```

### 嵌套

```javascript

let router = new koaRouter(); // 最外层的router

let userRouter = new koaRouter();

let company = new koaRouter();
company.get('/a', ctx => {
    ctx.body = 'company 的a';
});
let admin = new koaRouter();
admin.get('/a', ctx => {
    ctx.body = 'admin 的 a';
});

userRouter.use('/company', company.routes()); // 使用company的路由
userRouter.use('/admin', admin.routes());

router.use('/user', userRouter.routes());

server.use(router.routes()); // 总体外部server要知道你该访问谁了吧？
```

![截图-1574325345](https://wimg.misiyu.cn/images/20191121/1574325346_2a17b525e8ee2fb.png?x-oss-process=style/common)

> 以上是写在同一文件中，真实项目中新建routers总目录，其下新建目录，目录下新建.js文件。

### 参数

`/`参数：`ctx.params`

```javascript
let router = new koaRouter();

router.get('/user/:id', async ctx => {
    console.log(ctx.params);
});


server.use(router.routes());
```

`?`参数：`ctx.query`

```javascript
router.get('/user/:id', async ctx => {
    console.log(ctx.query);
    console.log(ctx.params);
});


server.use(router.routes());
```

server.context：相当于ctx的prototype

### 信息

ctx.method

ctx.url

ctx.path

ctx.query (get数据)

ctx.ip 客户端ip

ctx.headers

### 方法

#### throw

ctx.throw(code,msg) 报错并退出

```javascript
router.get('/login', async ctx => {
    if (!ctx.query.user || !ctx.query.pass) {
        ctx.throw(400, 'user and pass was required');
    } else {
        ctx.body = 'success';
    }
});
```

![截图-1574410078](https://wimg.misiyu.cn/images/20191122/1574410077_2689182a7247707.png?x-oss-process=style/common)

#### assert

ctx.assert(条件,code,msg);

```javascript
router.get('/login', async ctx => {
    ctx.assert(ctx.query.user, 400, 'username is required');
    ctx.assert(ctx.query.pass, 400, 'password is required');
    ctx.body = 'success';
});

```

![截图-1574410181](https://wimg.misiyu.cn/images/20191122/1574410181_6caa535151c1b36.png?x-oss-process=style/common)

#### state

ctx.state=404

```javascript
router.get('/login', async ctx => {
    ctx.state = 404;
});
```

#### redirect

```javascript
router.get('/login', async ctx => {
    // ctx.state = 404;
    ctx.redirect('/logout');
});
```

![截图-1574410435](https://wimg.misiyu.cn/images/20191122/1574410435_dfd1e590babcf3a.png?x-oss-process=style/common)

#### attachment

ctx.attachment(); 下载文件

有问题

## 中间件

### static

```bash
npm install -D koa-static
```

最后来写：

```javascript
server.use(router.routes());


server.use(static('./static', {
    maxAge: 86400 * 1000,
    index: '1.html'
}));
```

![截图-1574411585](https://wimg.misiyu.cn/images/20191122/1574411585_6834fc3aa99cefe.png?x-oss-process=style/common)

**结合路由来玩：**

```javascript
let staticRouter = new koaRouter();

staticRouter.all(/(\.gif|\.png)$/i, static({
    maxAge: 1 * 86400,
}))
```

### koa-better-body

```bash
npm -D install koa-better-body
```

ctx.request.fields

```javascript
server.use(body({
    uploadDir: './static/upload'
}));

router.post('/test', async ctx => {
    // 文件和Post数据
    console.log(ctx.request.fields);
    ctx.body = 'ok';
});

server.use(router.routes());
server.use(static('./static'));
```

![截图-1574412581](https://wimg.misiyu.cn/images/20191122/1574412580_9db2cd3b9d59645.png?x-oss-process=style/common)

### Cookies

koa自带

```javascript
router.post('/test', async ctx => {
    ctx.cookies.set(); // 设置
    ctx.cookies.get(); // 获取
});
```

例子：

```javascript
router.get('/test', async ctx => {
    ctx.cookies.set('user', 'kuan', {
        maxAge: 14 * 86400 * 1000,
        signed: true
    });
    console.log(ctx.cookies.get('user', {
        signed: true
    }))
    ctx.body = 'ok';
});
```

> 设置的时候如果signed了，那么获取的时候也要signed，否则浏览器端还是能修改Cookies，不然起不到加密的效果

### Session

安装：

```bash
npm install -D koa-session
```



## 全局捕获异常

```javascript
server.use(async (ctx, next) => {
    try {
        await next();
    } catch (e) {
        ctx.body = 'something was wrong.';
    }
})

```

**路由层面的错误**

```javascript
server.use(async (ctx, next) => {
    try {
        await next();
    } catch (e) {
        ctx.body = 'something was wrong.';
    }
})


router.all('*', async (ctx) => {
    try {
        await next();
    } catch (e) {
        ctx.body = 'router was wrong.';
    }
})
```