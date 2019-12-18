## 系统包

- assert - 断言
- querystring - 请求的数据处理
  - querystring.parse('a=b&c=d')
  - querystring.stringify({ "a": 12, "b": "d" })
- path - 路径
  - path.extname(p);
  - path.dirname(p);
  - path.basename(p); // 文件名
  - path.resolve('/root/abc/ac', '../bb'); // 解析路径
- url - 
- net - 网络通信

### 其他包

- multiparty - 处理表单数据



### socket.io

1、简单方便

2、兼容IE5

3、自动解析数据



### 数据库

**1、分类**

- 文件型：access、sqlite
- 关系型：Mysql、Oracle
- 分布式：MongoDB
- NoSql：memcache、redis

**2、模块**

`mysql`

**安装**

```bash
npm i mysql -S
```

**简单使用**

```javascript
const mysql = require('mysql');

let db = mysql.createConnection({host: 'localhost', user: 'root', password: 'root', database: 'my_blog'});

db.query('select * from blog_articles limit  0,1000', (err, res) => {
    console.log(res);
});

```

**3、连接池**

**4、异步**

`co-mysql`【mysql封装 不能独立使用】

```javascript
const co_mysql = require('co-mysql');

let conn = mysql.createConnection({ host: 'localhost', user: 'root', password: 'root', database: 'my_blog' });
let db = co_mysql(conn);
```



### 流操作

```javascript
const fs = require('fs');

let rs = fs.createReadStream('1.txt');
let ws = fs.createWriteStream('2.txt');

rs.pipe(ws);
rs.on('error', err => {
    console.log(err);
});

ws.on('finish', () => {
    console.log('finish');

});


```





### 附代码

#### multiparty

```javascript
const multiparty = require('multiparty');
const http = require('http');


let server = http.createServer((req, res) => {

    let form = new multiparty.Form({
        uploadDir: './upload'
    });

    form.parse(req);

    form.on('field', (name, value) => {
        console.log('字段', name, value);
    });

    form.on('file', (name, file) => {
        console.log('文件', name, file);
    });

    form.on('close', ()=>{
        console.log('表单处理完成');
    })

});

server.listen(3000);
```

#### 原生ajax

```javascript
const http = require('http');
let allowOrigin = {
    'http://localhost:63342': true,
    'http://localhost': true

};
http.createServer(((req, res) => {
    let {origin} = req.headers;
    if (allowOrigin[origin]) {
        res.setHeader('Access-control-allow-origin', 'http://localhost:63342');
    }
    res.write('{"a":12,"b":"ccd"}');
    res.end();

})).listen(3000);
```

```javascript
window.onload = function () {
    let oBtn = document.getElementById('btn');
    oBtn.onclick = function () {
        let ajax = new XMLHttpRequest();
        ajax.open('GET', 'http://localhost:3000', true);
        ajax.send();
        ajax.onreadystatechange = function () {
            if (ajax.readyState === 4 && ajax.status >= 200 && ajax.status < 300) {
                console.log(JSON.parse(ajax.response));

            }
        }


    };

};
```



#### 原生封装ajax

```javascript
(function (w) {
    var responseType = function (type, content) {
        switch (type) {
            case 'TEXT':
                return content;
            case 'JSON':
                return JSON.parse(content);
            default:
                return content;
        }
    };

    var param = function (a) {
        var s = [],
            rbracket = /\[\]$/,
            isArray = function (obj) {
                return Object.prototype.toString.call(obj) === '[object Array]';
            },
            add = function (k, v) {
                v = typeof v === 'function' ? v() : v === null ? '' : v === undefined ? '' : v;
                s[s.length] = encodeURIComponent(k) + '=' + encodeURIComponent(v);
            },
            buildParams = function (prefix, obj) {
                var i, len, key;

                if (prefix) {
                    if (isArray(obj)) {
                        for (i = 0, len = obj.length; i < len; i++) {
                            if (rbracket.test(prefix)) {
                                add(prefix, obj[i]);
                            } else {
                                buildParams(prefix + '[' + (typeof obj[i] === 'object' ? i : '') + ']', obj[i]);
                            }
                        }
                    } else if (obj && String(obj) === '[object Object]') {
                        for (key in obj) {
                            buildParams(prefix + '[' + key + ']', obj[key]);
                        }
                    } else {
                        add(prefix, obj);
                    }
                } else if (isArray(obj)) {
                    for (i = 0, len = obj.length; i < len; i++) {
                        add(obj[i].name, obj[i].value);
                    }
                } else {
                    for (key in obj) {
                        buildParams(key, obj[key]);
                    }
                }
                return s;
            };

        return buildParams('', a).join('&').replace(/%20/g, '+');
    };

    async function ajax(options) {
        options.method = options.method ? options.method.toUpperCase() : 'GET';
        options.dataType = options.dataType ? options.dataType.toUpperCase() : 'TEXT';
        options.data = options.data ? options.data : '';

        options.success = options.success ? options.success : function () {
        };
        options.fail = options.fail ? options.fail : function () {
        };
        if (!options.url) {
            throw new Error("there are no url.");
        }

        var ajax = new XMLHttpRequest();
        ajax.open(options.method, options.url, true);
        if (options.method === 'POST') {
            ajax.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
            ajax.send(typeof options.data === 'object' ? param(options.data) : options.data);
        } else {
            ajax.send();
        }
        ajax.onreadystatechange = function () {
            if (ajax.readyState === 4) {
                if (ajax.status === 200 || ajax.status === 301) {
                    options.success(responseType(options.dataType, ajax.responseText));
                } else {
                    throw new Error("the status of this request is't done.");
                }
            }

        };
    }

    w.ajax = ajax;

})(window);
```

