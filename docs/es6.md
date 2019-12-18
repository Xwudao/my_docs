# ES6

最新2019 (es10)

-----

方便 -> 工程性

需要了解的：

- 变量
- 作用域
- 函数
- 自带对象
- **异步处理**
  - Promise
  - async/await

## 变量

**以前**

`var`申明

**现在**

`let` 变量

`const`常量



**块级作用域**

> for() {}
>
> {}
>
> function () {}

看以下代码：

```html
<body>
    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button>4</button>
    <button>5</button>

    <script>
        let btns = document.getElementsByTagName('button');

        for (var i = 0; i < btns.length; i++) {
            btns[i].onclick = function () {
                alert(i);
            }
        }
    </script>
</body>
```

> 都会弹出5
>
> 只需将var 改成let 就会弹出0 1 2 3 4



**解构赋值**

{a:12,b:32}

[12,34,56]

注意两点：

- 左右两边一样
- 右边得是一个东西（对象、数组....）

```javascript
<script>

    let json = { a: 12, b: 43, c: 34 };
    let { a, b, c } = json;
	// 右边是a,b，c左边也得是a,b,c
	// 位置不一样，但会找到对应的值
    console.log(a, b, c);
    // 12 43 34


	let [aa, bb, cc] = data;

    console.log(aa, bb, cc)
</script>
```





## 函数

### 箭头函数

```javascript
(args) => {
	

}
```

**好处：this指向问题解决了**



### 剩余参数

```javascript
function gg(a, c, ...arr) {
        console.log(a);
        console.log(c);
        console.log(arr);
    }

    gg(1, 2, 3, 4, 5, 56, 6, 7);
```

**剩余参数必须是最后一个参数**

```JavaScript
let a = [12, 3, 4, 5, 5];
let b = [23, 4, 5, 6, 342, 3, 3];

let c = [...a, ...b];
console.log(c);

// [ 12, 3, 4, 5, 5, 23, 4, 5, 6, 342, 3, 3 ]
```



## 数组相关Array

### map

**映射**：n -> n

```JavaScript
let a = [12, 3, 4, 5, 6, 7, 8, 9, 10];
let res = a.map((item) => item * 2);
console.log(res);

// [ 24, 6, 8, 10, 12, 14, 16, 18, 20 ]
```

### reduce

**数组内的元素遍历后依次减少**

在函数内部进行想要的操作。

```JavaScript
let arr = [12, 3, 4, 5];
let bres = arr.reduce((tmp, item, index) => {
    return tmp+item;
    // console.log(tmp);
    // console.log(item);
    // console.log(index);
});

console.log(bres);
```

**求平均数**

```JavaScript
let arr = [12, 3, 4, 5];
let n = arr.reduce((tmp, item, index) => {
    if (index < arr.length - 1) {
        return tmp + item;
    }
    return (tmp + item) / arr.length;
});

// 6
```

### forEach

**循环一遍 类似for()**

### filter

```JavaScript
//filter
let arr = [12, 3, 4, 5];
let brr = arr.filter((item) => item % 2 === 0);
console.log(brr);

// [ 12, 4 ]
```

## 字符串String

### 字符串模板

```JavaScript
let arr = [12, 3, 4, 5];
arr.forEach((item, index) => {
    console.log(`这是第${index + 1}个变量：${item}`);
});

// 这是第1个变量：12
// ....
```

### startsWith

```JavaScript
let url = "https://www.misiyu.cn";
if (url.startsWith('https:') || url.startsWith('https:')) {
    console.log('是URL');
}
// 是URL
```

### endsWith

**同startsWith，不过是判断尾部**



## 异步处理

**同步：**多个操作必须一个一个的操作。

**异步：**多个操作可以是同时进行。



### Promise

**统一异步处理，**

```JavaScript

let resolve = function () {
    console.log('resolve');
};

let reject = function () {
    console.log('reject');
};

let does = function () {
    console.log('does');
    return false;
};

let p = new Promise(does).then(resolve).catch(reject);
```

> 上面这个例子稍微有点问题，用异步网络请求可以演示清楚



### Promise.all()

**等所有异步完成之后会执行then,有错误在执行catch**



### async/await

**在函数前面声明**

```JavaScript
async function f() {
    let a = 32;
    let b = 23;
}

f().then(r => console.log('fasdf'));
```

**如果函数内部有异步操作（如数据访问）九需要在此前加await**

```JavaScript
async function f() {
    let a = 32;
    let b = 23;
    let data = await $.get({url: 'https://www.misiyu.cn'});
}
```



## 其它

**es7**

** 幂运算

Array.includes()

**es8**

await/async

**es9(ECMA 2018)**

rest/spread

异步迭代

Promise.finally()

正则