# Express No Order

无序版

## 路由

基本代码

```javascript
const express = require('express');

let server = express();

server.listen(8080);

```

中间件：

```javascript
const express = require('express');

let server = express();

server.listen(8080);

server.get('/a', (req, res, next) => {
    console.log('a');
    next();
}); 
server.get('/a', (req, res, next) => {

    console.log('aa')
});
```

静态文件 - 中间件：

```javascript
// 静态文件 - 中间件
server.use(express.static('./static'));
```

![截图-1574162416](https://wimg.misiyu.cn/images/20191119/1574162417_3afe64bf5e27b1f.png?x-oss-process=style/common)

## 传递数据

GET:  req.query

POST: body-parser

```bash
npm install body-parser
```

body-parser:

```javascript
server.use(bodyParser.urlencoded({
    extended: false
}));
```

然后req就有body属性：`req.body`



文件: multer

```bash
npm install -D multer
```

```javascript
let obj = multer({
    dest: './upload'
});
server.use(obj.any()); // 可以指定类型，这里是any


server.post('/reg', (req, res, next) => {
    req.files;
});
```