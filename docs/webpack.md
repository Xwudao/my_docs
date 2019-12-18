# Webpack



## output

这样是错误的：

![截图-1568689533](https://wimg.misiyu.cn/images/20190917/1568689533_20e00969d7d4b80.png?x-oss-process=style/common)

![截图-1568689548](https://wimg.misiyu.cn/images/20190917/1568689548_c0e060559dce0ad.png?x-oss-process=style/common)



需要一个对象：

![截图-1568689736](https://wimg.misiyu.cn/images/20190917/1568689735_16c260f3d1bba82.png?x-oss-process=style/common)



## 其他

### export

```javascript
export let a  = xxx;

export const a  = xxx;

export {xx, xx, xx, xxxx}; // xx xxx 是已经定义好了的东西

export function sum(a, b) {
    
    
}

export class Person {
    
    
}

// export default
// 有一个默认导出

export default


```



### import

```javascript
import * as mode from "./xxx";

import {aa,vv,cc, ...} from "./xxx";

import xxx from "./yyyy"; // 引入默认成员 即前文的export default

// 模块的代码引进来，不引入内部成员
import "./1.jpg"; // 通常需要使用webpack配合某个loader

// 异步引入
let promise = import("./mode"); // 返回的是promise，异步加载需要绝对路径
// 
```

