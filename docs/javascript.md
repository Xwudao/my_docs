# JavaScript

## 变量

es5及之前用`var`申明，es6后建议`let` 和 `const`。

使用`typeof`查看变量类型。

### 1.1 变量类型

> number  小数与整数
> string  字符串(无字符类型)
> boolean  布尔数据类型
> undefined  未定义

```javascript
typeof 10  //number
typeof 3.14  //number
typeof 's'  //string
typeof "sunshine"  //string
typeof true  //boolean
typeof sun  //undefined
```

![截图-1564569518](https://wimg.misiyu.cn/images/20190731/1564569519_f25079a350e7e64.png?x-oss-process=style/first)


### 1.2 变量类型转换

**parseInt()** 转换为数字

```JavaScript
parseInt("123abc123") //123 含非数字字符,将前面的数字字符转换成数字
parseInt("a123") //NaN
parseInt("012") //12 去首部0
parseInt("0x10") //16 以十六进制计算
```

**parseFloat()**  整数字符串仍转换为整数
IsNaN  (is not a muber)不是数字返回true，是数字返回false



## 运算符

```JavaScript
var a = 1;
1+true  //2
"hello"+1  //hello1
10/3  //3.3333333333333335
"sunshine">"sun"  true
10 > "9"  true string-->number
age>18?"成年人":"未成年人" // 三目运算符
```

![截图-1564569868](https://wimg.misiyu.cn/images/20190731/1564569868_396be37972432b0.png?x-oss-process=style/first)

## 控制语句

```JavaScript
if语句
	number  非0为true,0为false
	string  内容非空为true,内容空为false。
	undefined  false
	NaN  false
switch语句
	在javascript中case后可跟常量、变量、表达式
```



## 循环语句

**for-in语句**

(1)遍历数组元素,遍历出的是数组下标

```JavaScript
var arr = [12,13,19,15,16];
for(var index in arr){
	document.write(arr[index]+",");		
}
// 普通for循环遍历数组元素
for(var index = 0 ; index<arr.length ; index++){
	document.write(arr[index]+",");	
}
```

(2)遍历对象的所有属性,遍历出的是对象的属性名

```JavaScript
function Person(id , name){
	this.id = id;
	this.name = name;	
}
var  p = new Person(110,"sunshine");
for(var property in p){
	document.write(p[property]+",");	
}
```

## With语句

使用with语句,在存取对象属性和调用方法时不用重复指定对象。

```JavaScript
with(document){
	write("&nbsp;");
}
function Person(id , name){
	this.id = id;
	this.name = name;
}
var p = new Person(110,"sunshine");
with(p){
	document.write("编号："+ p.id);
	document.write("姓名："+ name);
}
```

![截图-1564570079](https://wimg.misiyu.cn/images/20190731/1564570079_f304ce65dc844d0.png?x-oss-process=style/first)

## 函数

> 注意细节:
> (1)定义形参时是不能使用var关键字声明变量
> (2)函数没有返回值类型，如有需要直接返回即可
> (3)没有函数重载，后定义的同名函数直接覆盖前面定义的同名函数
> (4)任何函数内部都隐式维护了一个arguments数组对象，给函数传递数据的时候，会先传递到arguments对象中，然后再由arguments对象分配数据给形参

```JavaScript
function add(a,b){
	var sum = a+b;	
	//return sum;
}
function add(){
	for(var index = 0 ; index<arguments.length ; index++){
		document.write(arguments[index]+",");	
	}
}
//调用函数
add(11,21,13,14);
```

![截图-1564570165](https://wimg.misiyu.cn/images/20190731/1564570165_6e4621cc8cd0332.png?x-oss-process=style/first)

## Array数组

**创建方式**

```JavaScript
方式1:var 变量名 = new Array(); //创建一个长度为0的数组
方式2:var 变量名 = new Array(长度) //创建一个指定长度的数组对象
方式3:var 变量名 = new Array("元素1","元素2"...) //创建指定元素的数组对象
方式4:var 变量名 = ["元素1","元素2"...];
```

**在javascript中数组长度可变**

```JavaScript
var arr = new Array(3); //创建了一个长度为0的数组对象。
arr[100] = 10;
document.write("arr长度："+arr.length+"<br/>");//101	
var arr2 = new Array("sun1","sun2","sun3");
arr2 = ["sun4","sun5","sun6","sun7"];
document.write("arr2长度："+arr2.length+"<br/>");//4
```

**常见方法/属性**

- **length**：返回数组长度

- sort：排序，传入排序的方法。

  ```javascript
  function sortNumber(num1,num2){
  	return num1-num2;//升序
  }
  ```

- **slice**：指定数组的开始索引值与结束索引值截取数组的元素，**并且返回子数组**
  var subArr = arr1.slice(1,2);

- **reverse**：翻转数组元素。arr1.reverse();

- **join**：使用指定的分隔符把数组中的元素拼装成一个字符串返回。`var string = arr1.join(",");`

- **concat**：把arr1与arr2的数组元素组成一个新的数组返回
  `arr1 = arr1.concat(arr2);`

- **push**：将新元素添加到一个数组中，并返回数组的新长度值`var length = arr1.push("sunshine"); `

- **pop**：移除数组中的最后一个元素并返回该元素
  `var data = arr1.pop();`

- **shift**：移除数组中第一个元素，**并且返回**
  `var data = arr1.shift();`

- **unshift**：在数组的开头增加一个或多个元素，并返回数组的新长度。

- **splice**：第一个参数是开始删除元素的索引值，第二参数是删除元素的个数，往后的数据是插入的元素。

  > 此方法 很重要要理解到位，此方法可删除元素，可添加元素，可替换元素。原理就在于其三个（或更多）的参数的写法。

- Array.from()：从类数组对象或者可迭代对象中创建一个新的数组实例。

- Array.of()：根据一组参数来创建新的数组实例，支持任意的参数数量和类型。

- fill：将数组中指定区间的所有元素的值，都替换成某个固定的值。

  ```javascript
  var array1 = [1, 2, 3, 4];
  
  // fill with 0 from position 2 until position 4
  console.log(array1.fill(0, 2, 4));
  // expected output: [1, 2, 0, 0]
  
  // fill with 5 from position 1
  console.log(array1.fill(5, 1));
  // expected output: [1, 5, 5, 5]
  
  console.log(array1.fill(6));
  // expected output: [6, 6, 6, 6]
  ```

- indexOf()：返回数组中第一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1。

- lastIndexOf()：返回数组中最后一个（从右边数第一个）与指定值相等的元素的索引，如果找不到这样的元素，则返回 -1。

**迭代方法**

- forEach()：为数组中的每个元素执行一次回调函数。

  ```JavaScript
  let arr = [1,3,4,5,6,7,8];
  
  arr.forEach(item => {
      console.log(item);
  })
  ```

  ![截图-1564571123](https://wimg.misiyu.cn/images/20190731/1564571123_d267dd5489997c7.png?x-oss-process=style/first)

- every()：如果数组中的每个元素都满足测试函数，则返回 `true`，否则返回 `false。`

  ```JavaScript
  let arr = [1,3,4,5,6,7,8];
  
  let brr = arr.every(item => {
      if(item >2) return true;
      return false;
  });
  
  console.log(brr)
  ```

  ![截图-1564571215](https://wimg.misiyu.cn/images/20190731/1564571215_1e1bb6824975cce.png?x-oss-process=style/first)

- some()：如果数组中至少有一个元素满足测试函数，则返回 true，否则返回 false。

  ```JavaScript
  let arr = [1,3,4,5,6,7,8];
  
  let brr = arr.some(item => {
      if(item >2) return true;
      return false;
  });
  
  console.log(brr)
  ```

  ![截图-1564571273](https://wimg.misiyu.cn/images/20190731/1564571273_827b4e144356e0e.png?x-oss-process=style/first)

- filter()：将所有在过滤函数中返回 `true` 的数组元素放进一个新数组中并返回。

  ```JavaScript
  let arr = [1,3,4,5,6,7,8];
  
  let brr = arr.filter(item => {
      if(item > 5) return true;
      return false;
  });
  
  console.log(brr)
  ```

  ![截图-1564571333](https://wimg.misiyu.cn/images/20190731/1564571333_cae9a6575ee44bf.png?x-oss-process=style/first)

- map()：返回一个由回调函数的返回值组成的新数组。

  ```JavaScript
  let arr = [1,3,4,5,6,7,8];
  
  let brr = arr.map(item => {
      return 1;
  });
  
  console.log(brr)
  ```

  ![截图-1564571403](https://wimg.misiyu.cn/images/20190731/1564571404_6c90f148cd2e402.png?x-oss-process=style/first)

- reduce()：从左到右为每个数组元素执行一次回调函数，并把上次回调函数的返回值放在一个暂存器中传给下次回调函数，并返回最后一次回调函数的返回值。

## String对象

```JavaScript
var str1 = new String("hello");
var str2 = new String("hello");
document.write("两个字符串的对象一样吗？"+(str1.toString()==str2.toString()));//true
```

创建一个字符串的方式

> 方式1：new String("字符串的内容");
> 方式2：var str = "字符串的内容";

**长字符串**

有时，你的代码可能含有很长的字符串。你可能想将这样的字符串写成多行，而不是让这一行无限延长或着被编辑器折叠。有两种方法可以做到这一点。

其一，可以使用 + 运算符将多个字符串连接起来，如下所示：

```JavaScript
let longString = "This is a very long string which needs " +
                 "to wrap across multiple lines because " +
                 "otherwise my code is unreadable.";
```

其二，可以在每行末尾使用反斜杠字符（“\”），以指示字符串将在下一行继续。确保反斜杠后面没有空格或任何除换行符之外的字符或缩进; 否则反斜杠将不会工作。 如下所示：

```JavaScript
let longString = "This is a very long string which needs \
to wrap across multiple lines because \
otherwise my code is unreadable.";
```

**字符串比较**

熟练使用 C 语言的开发者经常使用 `strcmp` 函数来比较字符串，但在 JavaScript 中，你只需要

```JavaScript
var a = "a";
var b = "b";
if (a < b) // true
  print(a + " is less than " + b);
else if (a > b)
  print(a + " is greater than " + b);
else
  print(a + " and " + b + " are equal.");
```

**属性**

- length：返回字符串长度

**方法**

- String.prototype.charAt()
  返回特定位置的字符。
- String.prototype.charCodeAt()
  返回表示给定索引的字符的Unicode的值。
- String.prototype.codePointAt()
  返回使用UTF-16编码的给定位置的值的非负整数。
- String.prototype.concat()
  连接两个字符串文本，并返回一个新的字符串。
- String.prototype.includes()
  判断一个字符串里是否包含其他字符串。
- String.prototype.endsWith()
  判断一个字符串的是否以给定字符串结尾，结果返回布尔值。
- String.prototype.indexOf()
  从字符串对象中返回首个被发现的给定值的索引值，如果没有找到则返回-1。
- String.prototype.lastIndexOf()
  从字符串对象中返回最后一个被发现的给定值的索引值，如果没有找到则返回-1。
- String.prototype.localeCompare()
  返回一个数字表示是否引用字符串在排序中位于比较字符串的前面，后面，或者二者相同。
- String.prototype.match()
  使用正则表达式与字符串相比较。
- String.prototype.normalize()
  返回调用字符串值的Unicode标准化形式。
- String.prototype.padEnd()
  在当前字符串尾部填充指定的字符串， 直到达到指定的长度。 返回一个新的字符串。
- String.prototype.padStart()
  在当前字符串头部填充指定的字符串， 直到达到指定的长度。 返回一个新的字符串。
- String.prototype.repeat()
  返回指定重复次数的由元素组成的字符串对象。
- String.prototype.replace()
  被用来在正则表达式和字符串直接比较，然后用新的子串来替换被匹配的子串。
- String.prototype.search()
  对正则表达式和指定字符串进行匹配搜索，返回第一个出现的匹配项的下标。
- String.prototype.slice()
  摘取一个字符串区域，返回一个新的字符串。
- String.prototype.split()
  通过分离字符串成字串，将字符串对象分割成字符串数组。
- String.prototype.startsWith()
  判断字符串的起始位置是否匹配其他字符串中的字符。
- String.prototype.substr()
  通过指定字符数返回在指定位置开始的字符串中的字符。
- String.prototype.substring()
  返回在字符串中指定两个下标之间的字符。
- String.prototype.trim()
  从字符串的开始和结尾去除空格。参照部分 ECMAScript 5 标准。
- String.prototype.trimStart()
  String.prototype.trimLeft() 
  从字符串的左侧去除空格。
- String.prototype.trimEnd()
  String.prototype.trimRight() 
  从字符串的右侧去除空格。

## Number对象

创建Number对象的方式	

> 方式1:var 变量 = new Number(数字)	
> 方式2:var 变量 = 数字; // 十进制	

常用方法	

> toString()  把数字转换成指定进制形式的字符串，默认十进制
> toFixed()   指定保留小数位(四舍五入)

```JavaScript
var num = 10; // 十进制	
num.toString(2); // 二进制
var num2 = 3.455;
num2.toFixed(2); // 保留两位小数
```

![截图-1564572100](https://wimg.misiyu.cn/images/20190731/1564572100_a9d649382572c8d.png?x-oss-process=style/first)

## Date日期对象

**创建**

创建一个新Date对象的唯一方法是通过new 操作符：

```JavaScript
let now = new Date();
// 2019-07-31T11:23:49.162Z
```

**语法**

```JavaScript
new Date();
new Date(value);
new Date(dateString);
new Date(year, monthIndex [, day [, hours [, minutes [, seconds [, milliseconds]]]]]);
```

> **注意 参数**`monthIndex` 是从“0”开始计算的，这就意味着一月份为“0”，十二月份为“11”。

> **注意：**当Date作为构造函数调用并传入多个参数时，如果数值大于合理范围时（如月份为 13 或者分钟数为 70），相邻的数值会被调整。比如 new Date(2013, 13, 1)等于new Date(2014, 1, 1)，它们都表示日期2014-02-01（注意月份是从0开始的）。其他数值也是类似，new Date(2013, 2, 1, 0, 70)等于new Date(2013, 2, 1, 1, 10)，都表示同一个时间：`2013-03-01T01:10:00`。

> **注意：**当Date作为构造函数调用并传入多个参数时，所定义参数代表的是当地时间。如果需要使用世界协调时 UTC，使用 `new Date(Date.UTC(...))` 和相同参数。

```
year
```

表示年份的整数值。 0到99会被映射至1900年至1999年，其它值代表实际年份。参见 [示例](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date#Two_digit_years_map_to_1900_-_1999)。

```
monthIndex
```

**分别提供日期与时间的每一个成员**

> 当至少提供了年份与月份时，这一形式的 `Date() `返回的 `Date `对象中的每一个成员都来自下列参数。没有提供的成员将使用最小可能值（对日期为`1`，其他为`0`）。

表示月份的整数值，从 0（1月）到 11（12月）。

`day` 可选

表示一个月中的第几天的整数值，从1开始。默认值为1。

`hours` 可选

表示一天中的小时数的整数值 (24小时制)。默认值为0（午夜）。

`minutes` 可选

表示一个完整时间（如 01:10:00）中的分钟部分的整数值。默认值为0。

`seconds` 可选

表示一个完整时间（如 01:10:00）中的秒部分的整数值。默认值为0。

`milliseconds` 可选

表示一个完整时间的毫秒部分的整数值。默认值为0。



**方法**

- Date.now()
  返回自 1970-1-1 00:00:00  UTC（世界标准时间）至今所经过的毫秒数。

- Date.parse()

  由于浏览器解析的不一致性，该方法不建议使用。

- Date.UTC()
  接受和构造函数最长形式的参数相同的参数（从2到7），并返回从 1970-01-01 00:00:00 UTC 开始所经过的毫秒数。

**Getter**

- **Date.prototype.getDate()**
  根据本地时间返回指定日期对象的月份中的第几天（1-31）。
- **Date.prototype.getDay()**
  根据本地时间返回指定日期对象的星期中的第几天（0-6）。
- **Date.prototype.getFullYear()**
  根据本地时间返回指定日期对象的年份（四位数年份时返回四位数字）。
- **Date.prototype.getHours()**
  根据本地时间返回指定日期对象的小时（0-23）。
- **Date.prototype.getMilliseconds()**
  根据本地时间返回指定日期对象的毫秒（0-999）。
- **Date.prototype.getMinutes()**
  根据本地时间返回指定日期对象的分钟（0-59）。
- **Date.prototype.getMonth()**
  根据本地时间返回指定日期对象的月份（0-11）。
- **Date.prototype.getSeconds()**
  根据本地时间返回指定日期对象的秒数（0-59）。
- **Date.prototype.getTime()**
  返回从1970-1-1 00:00:00 UTC（协调世界时）到该日期经过的毫秒数，对于1970-1-1 00:00:00 UTC之前的时间返回负值。
- Date.prototype.getTimezoneOffset()
  返回当前时区的时区偏移。
- Date.prototype.getUTCDate()
  根据世界时返回特定日期对象一个月的第几天（1-31）.
- Date.prototype.getUTCDay()
  根据世界时返回特定日期对象一个星期的第几天（0-6）.
- Date.prototype.getUTCFullYear()
  根据世界时返回特定日期对象所在的年份（4位数）.
- Date.prototype.getUTCHours()
  根据世界时返回特定日期对象当前的小时（0-23）.
- Date.prototype.getUTCMilliseconds()
  根据世界时返回特定日期对象的毫秒数（0-999）.
- Date.prototype.getUTCMinutes()
  根据世界时返回特定日期对象的分钟数（0-59）.
- Date.prototype.getUTCMonth()
  根据世界时返回特定日期对象的月份（0-11）.
- Date.prototype.getUTCSeconds()
  根据世界时返回特定日期对象的秒数（0-59）.
- Date.prototype.getYear()【不再建议使用此方法】
  根据特定日期返回年份 (通常 2-3 位数). 使用 getFullYear() .

```JavaScript
let now = new Date();
console.log('getFullYear : '+now.getFullYear())
console.log('getMonth : '+now.getMonth())
console.log('getDate : '+now.getDate())
console.log('getDay : '+now.getDay())
console.log('getHours : '+now.getHours())
console.log('getMinutes : '+now.getMinutes())
console.log('getSeconds : '+now.getSeconds())
console.log('getTime : '+now.getTime()) // 毫秒数 
```

![截图-1564572931](https://wimg.misiyu.cn/images/20190731/1564572931_0bd71995c967df3.png?x-oss-process=style/first)

## Math对象

**常用方法**

- ceil 	  向上取整
- floor()   向下取整
- random()  随机数方法，产生的伪随机数介于0和1之间(含0不含1)
- round     四舍五入

```JavaScript
Math.ceil(3.14) //4
Math.floor(3.14) //3
Math.random()
Math.round(3.75) //4
```

## 自定义对象

> 在ES6之前，js没有类的概念。只要有函数即可创建对象

方式1:使用无参函数创建对象

```JavaScript
function Person(){}
var p = new Person(); //创建了一个Person对象
p.id = 110;
p.name = "sunshine";
```

方式2:使用带参的函数创建对象	

```JavaScript
function Person(id,name){
	this.id = id;
	this.name = name;
	this.say = function(){
		alert(name+"，你好");
	}
}
var p = new Person(110,"sunshine");
```

方式3:使用Object函数创建对象	

```JavaScript
var p = new Object();
p.id = 110;
p.name = "sunshine";
```

方式4:使用字面量的方式创建.

```JavaScript
var p = {
	id:110,
	name:"sunshine",
	say:function(){
		alert(this.name+"，你好");
	}
}
document.write("编号："+ p.id+" 姓名："+ p.name);
p.say();
```

## Prototype

需求:把getMax方法添加到数组对象中

```JavaScript
functoin Array(){
	this.prototype = new Object();
	this.getMax = function(){
	
	}
}
```

注意细节：

> 1.prototype是函数(function)的一个保留属性，任何function都有
> 2.prototype的值是一个对象
> 3.可以任意修改函数的prototype属性的值。
> 4.一个对象会自动拥有prototype的所有成员属性和方法。

```JavaScript
String.prototype.toCharArray = function(){
	var arr = new Array();
	for(var index = 0; index<this.length ;index++){
		arr[index] = this.charAt(index);	
	}
	return arr;
}	
String.prototype.reverse = function(){
	//字符串-->字符数组
	var arr = this.toCharArray();
	arr.reverse();
	return arr.join("");
}
var str = "wudao, I love you";
str = str.reverse();
console.log("翻转后的字符串："+str);
```

![截图-1564573460](https://wimg.misiyu.cn/images/20190731/1564573460_9a4e58c152fed06.png?x-oss-process=style/first)

## 事件

**注册事件方式**

1、在元素内注册：

```html
<body onload="ready()">
    <script>
       function ready(){
           alert('onload');
       }
    </script>
</body>
```

![截图-1564573562](https://wimg.misiyu.cn/images/20190731/1564573562_c1a6b361ef127e6.png?x-oss-process=style/first)

2、先获取DOM，再注册：

```html
<body>

</body>
<script>
    let body = document.querySelector('body');
    body.onload = function () {
        alert('I am load');
    }
</script>
```

![截图-1564573695](https://wimg.misiyu.cn/images/20190731/1564573696_6c4f7a353c1f78a.png?x-oss-process=style/first)

**常用事件**

**鼠标点击相关**

- onclick 单击
- ondblclick 双击
- onmousedown 按下按钮 
- onmouseup 释放按钮

**鼠标移动相关**

 - onmouseout 鼠标指针移出对象边界

 - onmousemove 鼠标划过对象

**焦点相关**

 - onblur 对象失去输入焦点
 - onfocus 对象获得焦点

**其他**

- onchange 对象或选中区的内容改变 
- onload 浏览器完成对象的装载 
- onsubmit 表单将被提交

## BOM浏览器对象模型

javascript组成部分

> EMCAScript ( 基本语法 )
> BOM( Browser Object MOdel) 浏览器对象模型.

浏览器对象模型中把浏览器的各个部分用一个对象进行描述，如果我们要操作浏览器的一些属性，可以通过浏览器对象模型的对象进行操作

> window  代表了一个新开的窗口
> location  代表了地址栏对象
> screen  代表了整个屏幕的对象



### 1.windows窗口对象

window对象常用方法	

- open()   打开一个新的窗口。
- resizeTo() 将窗口的大小更改为指定的宽度和高度值。
- moveBy()  相对于原来的窗口移动指定的x、y值。 
- moveTo() 将窗口左上角的屏幕位置移动到指定的 x 和 y 位置。 
- setInterval() 每经过指定毫秒值后就会执行指定的代码。
- clearInterval() 根据一个任务的ID取消的定时任务。
- setTimeout() 经过指定毫秒值后执行指定的代码一次。

> 注意:使用window对象的任何属性与方法都可以省略window对象不写的。

### 2.Location地址栏对象

- href:设置及获取地址栏对象
- reload():刷新当前页面

具体还有哪些内容，可在浏览器控制台输入`location`查看：

![截图-1564574128](https://wimg.misiyu.cn/images/20190731/1564574128_7be5da970e41077.png?x-oss-process=style/first)

### 3.Screen屏幕对象

**基本被支持的方法/属性**

- Screen.availHeight
  Specifies the height of the screen, in pixels, minus permanent or semipermanent user interface features displayed by the operating system, such as the Taskbar on Windows.

  （指定屏幕高度（以像素为单位）减去操作系统显示的界面，如任务栏）

- Screen.availWidth
  Returns the amount of horizontal space in pixels available to the window.

  （返回窗口可用的水平空间量（以像素为单位）。）

- Screen.colorDepth
  Returns the color depth of the screen.

  （返回屏幕的颜色深度。）

- Screen.height
  Returns the height of the screen in pixels.

  （返回屏幕的高度（以像素为单位）。）

- Screen.width
  Returns the width of the screen.

  （（返回屏幕的高度（以像素为单位）。））

![截图-1564574371](https://wimg.misiyu.cn/images/20190731/1564574371_70f39a0d958dd0b.png?x-oss-process=style/first)

## DOM文档对象模型	

html页面被浏览器加载时，浏览器会对整个html页面上所有标签创建对应的对象进行描述，用户看到的信息是这些html对象的属性信息。只要能找到对应的对象操作对象的属性，则可以改变浏览器当前显示的内容。

```html
var allNodes = document.all; //获取html文件中的所有标签节点
for(var i = 0; i < allNodes.length ; i++){
	alert(allNodes[i].nodeName); //标签的名字 nodeName
}
function writeUrl(){
	var links = document.links; //获取文档中含有href的属性的标签
	for(var i = 0; i<links.length ; i++){
		links[i].href = "http://www.misiyu.cn";
	}
}
```

## 节点查找

通过html元素的标签属性找节点

```JavaScript
document.getElementById("html元素的id") 
document.getElementsByTagName("标签名") 
document.getElementsByName("html元素的name")
```

通过关系(父子关系、兄弟关系)找标签

```JavaScript
parentNode	    获取当前元素的父节点
childNodes	    获取当前元素的所有下一级子元素
firstChild	    获取当前节点的第一个子节点
lastChild	    获取当前节点的最后一个子节点
nextSibling		获取当前节点的下一个节点（兄节点）
previousSibling	获取当前节点的上一个节点（弟节点）
```

## 节点创建、插入、删除

创建字节入插入节点、设置节点的属性。

> document.createElement("标签名")		创建新元素节点
> elt.setAttribute("属性名", "属性值")	设置属性
> elt.appendChild(e)						添加元素到elt中最后的位置

```JavaScript
//创建指定标签名的节点
var inputNode = document.createElement("input"); 	
//设置节点的属性
inputNode.setAttribute("type","button");
inputNode.setAttribute("value","按钮");
//定义新节点的父节点
var bodyNode = document.getElementsByTagName("body")[0];
//appendChild添加子节点到父结点末尾
bodyNode.appendChild(inputNode);
```

插入目标元素的位置	 

> elt.insertBefore(newNode, oldNode);	添加到elt中，child之前，elt必须是oldNode的直接父节点
> elt.removeChild(child)			    删除指定的子节点，elt必须是child的直接父节点

```JavaScript
var newNode = document.createElement("span");
var bodyNode = document.getElementsByTagName("body")[0];
var oldNode = document.getElementsByTagName("script")[1];
bodyNode.insertBefore(newNode,oldNode);
bodyNode.removeChild(oldNode);
```

## 操作CSS样式

```JavaScript
var spanNode = document.getElementById("code");
spanNode.innerHTML = code;
spanNode.style.fontSize ="24px";
spanNode.style.color = "red";
spanNode.style.backgroundColor="gray";
spanNode.style.textDecoration = "line-through";
```

现在还有dom.classList.*

比如dom.classList.add()，dom.classList.remove()

## 正则表达式

正则表达式的创建方式

> 方式1: /正则表达式/模式
> 方式2: new RegExp("正则表达式",模式);

正则表达式对象常用方法

> test()  使用正则对象去匹配字符串，如果匹配成功返回ture，否则返回false
> exec()  根据正则表达式去查找字符串符合规则的内容

模式

> g （全文查找出现的所有pattern） 	
> i （忽略大小写）

```JavaScript
var str = "hello123";
var reg = /^[A-Z0-9]+$/i;
alert(reg.test(str));	
```

```JavaScript
var str = "hello123";
var reg = /^[A-Z0-9]+$/i;
alert(reg.test(str));	
//查找出三到四个字符组成的单词。
var str  ="sun jian feng sunshine studio";
var reg = /\b[a-z]{3,4}\b/gi;
var line ="";
while((line = reg.exec(str))!=null){
	document.write(line+"<br/>")
}
```



## 面向对象

```JavaScript
class Person{
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    show() {
        console.log(this.name);
        console.log(this.age);
    }


}

let p = new Person('wudao', 20);

//继承
class Worker extends Person{
    constructor(name, age,job) {
        super(name, age);
        this.job = job;

    }

    showJob() {
        console.log(this.job);
    }
}

let w = new Worker('h', 12, 'women');
w.showJob();
```

## 闭包

**闭包可以访问创建函数时所在作用域内的全部变量**

1.底层：栈

2.高层：函数当做对象处理

### 作用

#### 封装私有变量

许多编程语言使用私有变量，这些私有变量是对外部隐藏的对象属性。这是非常有用的一种特性，因为当通过其他代码访问这些变量时，我们不希望对象的实现细节对用户造成过度负荷。遗憾的是，原生JavaScript不支持私有变量。但是，通过使用闭包，我们可以实现很接近的、可接受的私有变量。

#### 回调函数

处理回调函数是另一种常见的使用闭包的情景。回调函数指的是需要在将来不确定的某一时刻异步调用的函数。通常，在这种回调函数中，我们经常需要频繁地访问外部数据。

## 生成器函数

生成器函数几乎是一个完全崭新的函数类型，它和标准的普通函数完全不同。生成器（generator）函数能生成一组值的序列，但每个值的生成是基于每次请求，并不同于标准函数那样立即生成。我们必须显式地向生成器请求一个新的值，随后生成器要么响应一个新生成的值，要么就告诉我们它之后都不会再生成新值。更让人好奇的是，每当生成器函数生成了一个值，它都不会像普通函数一样停止执行。相反，生成器几乎从不挂起。随后，当对另一个值的请求到来后，生成器就会从上次离开的位置恢复执行。

```javascript
function * WeaponGenerator() {
    yield "Ak";
    yield "M416";
    yield "RSS";
}
for (let weapon of WeaponGenerator()) {
    console.log(weapon);
}
```

> 上面是一个简单的生成器函数，定义方法就是在函数名前面加一个*，然后，使用关键字yield生成独立的值

但其实，除了利用for-of循环之外，我们还可以使用一个迭代器来循环：

```javascript
const weaponsIterator = WeaponGenerator();
const result01 = weaponsIterator.next();
console.log(result01)
```

![截图-1572869040](https://wimg.misiyu.cn/images/20191104/1572869041_2dbc37d66090ddd.png?x-oss-process=style/common)

如上图，这里返回的是一个对象，里面有个`done`对象，这个代表什么呢？**代表迭代还未完成，也即还可以继续循环：**

```javascript
const weaponsIterator = WeaponGenerator();
let result01 = null;
while (!(result01 = weaponsIterator.next()).done) {
    console.log(result01);
}
```

所以，我们就可以利用while来循环

![截图-1572869192](https://wimg.misiyu.cn/images/20191104/1572869194_de66bbfae14e041.png?x-oss-process=style/common)

### 用处

#### 生成ID序列

> 在创建某些对象时，我们经常需要为每个对象赋一个唯一的ID值。
> 最简单的方式是通过一个全局的计数器变量，但这是一种丑陋的写法，因为这个计数器变量很容易就会不慎淹没在混乱的代码中。另外一种方式则是使用生成器

```javascript
function* IdGenerator() {
    let id = 0;
    while (true) {
        yield ++id;
    }
}

const idIterator = IdGenerator();
const misiai = { id: idIterator.next().value };
const misiai2 = { id: idIterator.next().value };
const misiai3 = { id: idIterator.next().value };
console.log(misiai)
console.log(misiai2)
console.log(misiai3)
```

![截图-1572869500](https://wimg.misiyu.cn/images/20191104/1572869501_98a34602063cc25.png?x-oss-process=style/common)

> 本例开始的迭代器中包含一个局部变量id，其代表了ID计数器。局部变量id仅能在该生成器中被访问，故而完全不必担心有人会不小心在代码的其他地方修改id值。随后是一个无限的while循环，其每次迭代都能生成一个新id值**并挂起执行**
>
> 标准函数中一般不应该书写无限循环的代码。但在生成器中没问题！当生成器遇到了一个yield语句，它就会一直挂起执行直到下次调用next方法，所以只有每次调用一次next方法，while循环才会迭代一次并返回下一个ID值。

#### 遍历DOM树

```html
<body>
    <div class="" id="tree">
        <form action="">
            <input type="text">
        </form>
        <p>
            <span class="hello">无道</span>
        </p>
    </div>
</body>
```

```JavaScript
function* DomTraversal(element) {
    yield element;
    element = element.firstElementChild;
    while (element) {
        yield* DomTraversal(element);
        element = element.nextElementSibling;
    }
}
const dom = document.getElementById('tree');
for (let el of DomTraversal(dom)) {
    if (el !== null) {
        console.log(el.nodeName);
    }
}
```

![截图-1572870094](https://wimg.misiyu.cn/images/20191104/1572870095_0b20beb9fec03d7.png?x-oss-process=style/common)

## promise

promise对象是对我们现在尚未得到但将来会得到值的占位符；它是对我们最终能够得知异步计算结果的一种保证。如果我们兑现了我们的承诺，那结果会得到一个值。如果发生了问题，结果则是一个错误，一个为什么不能交付的借口。使用promise的一个最佳例子是从服务器获取数据：我们要承诺最终会拿到数据，但其实总有可能发生错误。

```JavaScript
const myPromise = new Promise((resolve, reject) => {
    // 如果内部正确
    let msg = 'the result is ok';
    let v = true;
    if (v) {

        resolve(msg);
    } else {
        msg = 'the result is not ok';
        reject(msg);
    }

});
myPromise.then(res => {
    console.log(res)
}, err => {
    console.log(err);
})
```

> 上面是一个简单的promise

![截图-1572918446](https://wimg.misiyu.cn/images/20191105/1572918446_92f2985c4d9e9a8.png?x-oss-process=style/common)

### 链式调用

```JavaScript
getJSON("data/Kuans.json")
    .then(Kuans => getJSON(Kuans[0].missionsUrl))
    .then(missions => getJSON(missions[0].detailsUrl))
    .then(mission => assert(mission !== null, "Kuan mission obtained!"))
    .catch(error => fail("An error has occurred")); 
```

### 错误捕捉

```JavaScript
...catch(error => fail("An error has occurred:" + err));
```

### 等待多个

```JavaScript
Promise.all([
    getJson("data/hello.json"),
    getJson("data/hello.json"),
    getJson("data/hello.json"),
    getJson("data/hello.json"),
    getJson("data/hello.json"),
]).then(results => {
    console.log(results);
}).catch(error => {
    fail("A problem in carrying out our plan!");
});
```

我们不必关心任务执行的顺序，以及它们是不是都已经进入完成态。通过使用内置方法Promise.all 可以等待多个promise。这个方法将一个**promise数组**作为参数，然后创建一个新的promise对象，一旦数组中的promise**全部**被解决，这个返回的promise就会被解决，而一旦其中**有一个**promise失败了，那么整个新promise对象也会被拒绝。后续的回调函数接收成功值组成的数组，数组中的每一项都对应promise数组中的对应项。花一分钟欣赏一下处理多个并行的异步任务的代码是多么优雅。

### 竞赛

```JavaScript
Promise.race([
    getJSON("data/yoshi.json"),
    getJSON("data/hattori.json"),
    getJSON("data/hanzo.json")
]).then(Kuan => {
    console.log(Kuan);
}).catch(error => fail("Failure!"));
```

使用Promise.race方法并传入一个promise数组会返回一个全新的promise对象，一旦数组中某一个promise被处理或被拒绝，这个返回的promise就同样会被处理或被拒绝。

## 面向对象

### 原型链

#### Object.setPrototypeOf

置的方法Object.setPrototypeOf需要传入两个对象作为参数，**并将第二个对象设置为第一个对象的原型。**

```JavaScript
let wu = { hello: 123 };
let kuan = { wudao: 456 };

Object.setPrototypeOf(wu, kuan);
console.log(wu)
```

![截图-1572920345](https://wimg.misiyu.cn/images/20191105/1572920344_4c34edbdcfe8482.png?x-oss-process=style/common)

> 貌似没有改变？其实不然，
>
> ![截图-1572920364](https://wimg.misiyu.cn/images/20191105/1572920364_34f5eec790c1b11.png?x-oss-process=style/common)

#### prototype

```JavaScript
function Kuan() { };
Kuan.prototype.hello = function () {
    console.log('hello');
}

let kuan = new Kuan();
kuan.hello();
```

![截图-1572920655](https://wimg.misiyu.cn/images/20191105/1572920655_0c80c7348576b04.png?x-oss-process=style/common)

上面这段代码我们是作为 **构造器** 方法来使用的（也即new），所以其实可以正常输出hello的，但如果用以下的代码呢？

```JavaScript
function Kuan() { };
Kuan.prototype.hello = function () {
    console.log('hello');
}

let kuan = Kuan();
kuan.hello();
```

![截图-1572920843](https://wimg.misiyu.cn/images/20191105/1572920842_8cab3fc4e4f1b87.png?x-oss-process=style/common)

作为普通函数来调用，是否并不是想象中的那么美好。

#### 实例属性

**优先级问题**

```JavaScript
function Kuan() {
    this.ok = false;
    this.hello = function () {
        return !this.ok;
    }

};
Kuan.prototype.hello = function () {
    return this.ok;
}

let kuan = new Kuan();
console.log(kuan.hello());
```

当同时在内部this和原型链定义同一个名称的函数时，会使用哪个？

> 调用顺序是会首先寻找本身的属性，找不到时才会到原型链中寻找！

![截图-1572921077](https://wimg.misiyu.cn/images/20191105/1572921076_6181705a22d8ecb.png?x-oss-process=style/common)

### 实现继承

#### 原型链继承



## 控制对象访问

### Getter和Setter

```JavaScript
const Kuan = {
    xia: [1, 23, 45, 6, 7],

    get first() {
        console.log('something was getted');
        return this.xia[0];
    },

    set first(value) {
        console.log('be setted');
        this.xia[0] = value;
    }

};
Kuan.first = 10;
```

![截图-1572922224](https://wimg.misiyu.cn/images/20191105/1572922224_2beefc7e4744f30.png?x-oss-process=style/common)

### Object.defineProperty

```JavaScript
function Kuan() {
    let _skill = 'play games';

    Object.defineProperty(this, 'skill', {
        set: value => {
            console.log('be setted');
            _skill = value;
        },
        get: () => {
            console.log('something was getted');
            return _skill;
        }
    });
}

let kuan = new Kuan();
kuan.skill === 'paly games';
kuan.skill = 'watching tv';
```

![截图-1572922659](https://wimg.misiyu.cn/images/20191105/1572922659_5a763a1c732feb6.png?x-oss-process=style/common)

## 集合相关

### 数组

**1、创建**

创建数组有两种方式：

- 内置的Array构造函数
- 使用字面量[]

```JavaScript
let arr1 = ['wudao', 12, 'faf'];
let arr2 = new Array("hello", "Js");
console.log(arr1);
console.log(arr2);
```

![截图-1572950682](https://wimg.misiyu.cn/images/20191105/1572950682_0699464371c1433.png?x-oss-process=style/common)

每个数组都会有一个length属性，该属性代表该数组内有几个元素。

假如访问不存在的对象，会返回undefined。访问不存在的数组索引，也会返回undefined。

**2、添加**

- push：在数组末尾添加元素。

  ```JavaScript
  let arr1 = [1, 2, 3];
  arr1.push(4);
  console.log(arr1);
  ```

  所以，哪边是末尾？3后面呗。

  ![截图-1572951107](https://wimg.misiyu.cn/images/20191105/1572951106_e7a71c4177edf2a.png?x-oss-process=style/common)

- unshift: 在数组开头添加元素。

  ```
  let arr1 = [1, 2, 3];
  arr1.unshift(0);
  console.log(arr1);
  ```

  ![截图-1572951147](https://wimg.misiyu.cn/images/20191105/1572951147_fa48b6d31c9fa4b.png?x-oss-process=style/common)

- pop: 从数组末尾删除元素。

  ```JavaScript
  let arr1 = [1, 2, 3];
  arr1.push(4);
  arr1.unshift(0);
  console.log(arr1);
  let r = arr1.pop(); // 删除末尾元素，并将末尾元素返回
  
  console.log(r);
  console.log(arr1);
  ```

  ![截图-1572951200](https://wimg.misiyu.cn/images/20191105/1572951199_b73e90f9e2e0807.png?x-oss-process=style/common)

- shift: 从数组开头删除元素。

  ```JavaScript
  let arr1 = [1, 2, 3];
  arr1.push(4);
  arr1.unshift(0);
  console.log(arr1);
  let r = arr1.shift(); // 删除开头，并将开头元素返回
  console.log(r);
  console.log(arr1);
  ```

  ![截图-1572954288](https://wimg.misiyu.cn/images/20191105/1572954288_107f4f334a34edd.png?x-oss-process=style/common)

**3、删除指定位置元素**

可以用一个稍微粗略点的方法：delete 

  ```JavaScript
  let arr1 = [1, 2, 3];
  arr1.push(4);
  arr1.unshift(0);
  console.log(arr1);
  
  delete arr1[0];
  console.log(arr1);
  
  delete arr1[4];
  console.log(arr1);
  ```

![截图-1572954482](https://wimg.misiyu.cn/images/20191105/1572954481_396da3a5099b19b.png?x-oss-process=style/common)

但该方法不能更改数组的长度。所以我们需要用数组splice方法：

**4、splice方法**

```javascript
arrayObject.splice(index,howmany,item1,.....,itemX)
```

| 参数              | 描述                                                         |
| :---------------- | :----------------------------------------------------------- |
| index             | 必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。 |
| howmany           | 必需。要删除的项目数量。如果设置为 0，则不会删除项目。       |
| item1, ..., itemX | 可选。向数组添加的新项目。                                   |

返回：包含被删除项目的新数组，如果有的话。



> 该splice方法可以实现数组的：删除、替换、增加，怎样实现就看怎样灵活利用这三个参数
>
> howmany=0,items=待替换（1个）或增加（多个）的元素

**5、循环数组**

A. for循环

```JavaScript
let arr1 = [1, 2, 3, 4, 5, 6];
for (let i = 0; i < arr1.length; i++) {
    console.log(i + ':', arr1[i]);
}
```

![截图-1572954941](https://wimg.misiyu.cn/images/20191105/1572954940_ccc03951b7e230c.png?x-oss-process=style/common)

A. forEach

```JavaScript
array.forEach(function(currentValue, index, arr), thisValue)
```

```JavaScript
let arr1 = [1, 2, 3, 4, 5, 6];
// for (let i = 0; i < arr1.length; i++) {
//     console.log(i + ':', arr1[i]);
// }

arr1.forEach((item, index) => {
    console.log('索引', index + ':', item);
})
```

![截图-1572955028](https://wimg.misiyu.cn/images/20191105/1572955027_5adaf71571351ec.png?x-oss-process=style/common)

> 但得注意的是forEach是es6的方法



C. map

```JavaScript
array.map(function(currentValue,index,arr), thisValue)
```

但是对于如下的代码，我想取到hello的值，该如何循环？

```JavaScript
const arr = [
    { hello: '123', world: '456' },
    { hello: '344', world: '1355' },
    { hello: '6537', world: '4544766' },
];
```

其实也简单，我们需要用到map方法，**这也是es6的语法**

```JavaScript
const arr = [
    { hello: '123', world: '456' },
    { hello: '344', world: '1355' },
    { hello: '6537', world: '4544766' },
];

arr.map(item => {
    console.log(item);
    console.log(item.hello);
})
```



![截图-1572955329](https://wimg.misiyu.cn/images/20191105/1572955329_4b5df060a891521.png?x-oss-process=style/common)



D. 测试数组是否满足条件：every 和 some，当然，这也是es6的语法

every: 检测数值元素的**每个元素是否都**符合条件。

```JavaScript
array.every(function(currentValue,index,arr), thisValue)
```

例如我想知道下面arr数组里面的num是否每个都大于100：

```JavaScript
const arr = [
    { num: 123, world: '456' },
    { num: 344, world: '1355' },
    { num: 6537, world: '4544766' },
];

let res = arr.every(item => {
    return item.num >= 100;
})
console.log(res)
```

![截图-1572955653](https://wimg.misiyu.cn/images/20191105/1572955653_4e872f477f6a932.png?x-oss-process=style/common)

some: 检测数组元素中**是否有元素符合**指定条件。

例如更改以上代码，判断是否大于6000：

```JavaScript
const arr = [
    { num: 123, world: '456' },
    { num: 344, world: '1355' },
    { num: 6537, world: '4544766' },
];

let res1 = arr.every(item => {
    return item.num >= 6000;
})

let res2 = arr.some(item => {
    return item.num >= 6000;
})
console.log('every:', res1)
console.log('some:', res2)
```

![截图-1572955778](https://wimg.misiyu.cn/images/20191105/1572955777_5483248e05e5b98.png?x-oss-process=style/common)

> 对于some来说，有元素大于6000，多以返回true，
>
> 但是对于every来说，不是每一个都大于6000，所以false



**6、查找元素** 

A. find

```JavaScript
array.find(function(currentValue, index, arr),thisValue)
```

```JavaScript
const arr = [
    { num: 123, world: '456' },
    { num: 344, world: '1355' },
    { num: 6537, world: '4544766' },
];
let res = arr.find(item => {
    return item.num == 123;
});

console.log(res)
```

![截图-1572955982](https://wimg.misiyu.cn/images/20191105/1572955981_9ffe7ce00121e91.png?x-oss-process=style/common)

> 但是需要注意的是，该方法返回的是 **满足条件的元素**，而不是索引，需要索引可以使用findIndex

B.findIndex 返回满足条件的索引

```JavaScript
const arr = [
    { num: 123, world: '456' },
    { num: 344, world: '1355' },
    { num: 6537, world: '4544766' },
];
let res1 = arr.find(item => {
    return item.num == 344;
});
let res2 = arr.findIndex(item => {
    return item.num == 344;
});

console.log(res1)
console.log(res2)
```

![截图-1572956064](https://wimg.misiyu.cn/images/20191105/1572956064_cb2b160e71f12db.png?x-oss-process=style/common)



C. filter 返回满足条件的多个**元素**

```JavaScript
array.filter(function(currentValue,index,arr), thisValue)
```

```JavaScript
const arr = [
    { num: 123, world: '456' },
    { num: 344, world: '1355' },
    { num: 6537, world: '4544766' },
];

let res = arr.filter(item => {
    return item.num > 200;
});

console.log(res)

```

![截图-1572956184](https://wimg.misiyu.cn/images/20191105/1572956184_38cd277f6a337c2.png?x-oss-process=style/common)

**7、数组排序**

sort

```JavaScript
array.sort((a, b) => a – b);
```

- 如果回调函数的返回值小于0，元素a应该出现在元素b之前。
- 如果回调函数的返回值等于0，元素a和元素b出现在相同位置。
- 如果回调函数的返回值大于0，元素a应该出现在元素b之后。



**8、合计(减少)元素**

reduce：将数组元素计算为一个值（从左到右）。

reduceRight：将数组元素计算为一个值（从右到左）。

```JavaScript
array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
```

其实该方法很典型的一个例子就是计算数组之和：

```JavaScript
const arr = [
    123, 456, 789
];

let res = arr.reduce((total, item, itemIndex) => {
    return total + item;
});

console.log(res)

```

![截图-1572956781](https://wimg.misiyu.cn/images/20191105/1572956781_5629e0c653d2256.png?x-oss-process=style/common)

### Map

**1、创建map**

```JavaScript
const map1 = new Map();

map1.set("hello", "world");
map1.set("hello", "world"); // 试图两次创建hello，但只会存在一次
map1.set("hello2", "world");
console.log(map1)
console.log(map1.size)

for (let key of map1.keys()) {
    console.log(key)
}
```

![截图-1572957678](https://wimg.misiyu.cn/images/20191105/1572957678_6dbc1560d1e8482.png?x-oss-process=style/common)

**2、所拥有的方法**

A. map.size 拥有的元素个数

B. map.delete() 删除

C. map.set(key, value) 设置(添加)一个元素

D. map.get(key) 获得一个元素

E. map.has(key) 是否拥有某个元素

F. map.clear() 清空所有



**3、遍历**

A. let of

B. let key of map.keys()

C. let value of map.values()

> .keys() 和 .values() 是否只要有map的语言都支持的获取所有keys和所有values的方法



### Set

在许多实际问题中，我们必须处理一种集合，集合中的每个元素都是唯一的（每个元素只能出现一次），这种集合称为Set。

**1、创建set**

```JavaScript
let set1 = new Set();
set1.add('123');
set1.add('123'); // 两次添加123，但实际只会存在1次
set1.add('123243');
set1.add('12324qewrqr');
console.log(set1);
```

![截图-1572957593](https://wimg.misiyu.cn/images/20191105/1572957592_44dbb4d7a8a6933.png?x-oss-process=style/common)

**2、属性或方法**

A. set.size 拥有的元素个数

B. set.add(value)  添加值

C. set.delete(value) 删除某个值

D. set.has(value) 是否存在某个值

E. set.clear() 清空所有值



**3、并集**

两个集合的并集指的是创建一个新的集合，同时包含A和B中的所有成员。当然，在新的集合中的元素也不允许出现两次。

```JavaScript
const arr1 = [123, 456];
const arr2 = [789, 199, 213];
let set1 = new Set([...arr1, ...arr2]);
console.log(set1);
```

![截图-1572958193](https://wimg.misiyu.cn/images/20191105/1572958192_5143ff03b0ebae2.png?x-oss-process=style/common)

> 这里使用了es6新出来的剩余参数（三个点），而`[...arr1, ...arr2]`的意思就是说把数组arr1和arr2的值提出来组成新的一个数组。



**4、交集**

```
[...arr1].filter(item=> !arr2.has(item));
```



## 正则表达式

正则表达式是现代开发中的必需品。虽然许多开发者不用正则表达式也可以顺利完成工作，但是，如果不使用正则表达式，就无法使用JavaScript优雅地解决许多问题。



### 创建

```JavaScript
let m = 10000;
let regex = /\d+/ig;
let regex2 = new RegExp("\\d+", "g");
console.log(regex.test(m));
console.log(regex2.test(m));
```

![截图-1573007696](https://wimg.misiyu.cn/images/20191106/1573007696_a08179e3db50bf5.png?x-oss-process=style/common)

Javascript中创建正则表达式有两种创建方式

- 字面量方式
- 构造函数方法

优先是推荐使用 **字面量**方式，方便快捷。

若是需要**动态更改**正则表达式本身的话，使用构造函数方式更换（貌似也只能使用构造函数方式）

> 其次，构造函数方式涉及到字符转义的问题，如上代码使用了两个反斜杠`\\`
>
> 上图中reg.test(m)方法是测试该字符串m是否满足正则表达式



## 代码模块化

JavaScript ES6之前，只有两种作用域：全局作用域和函数作用域。

没有介于两者之间的作用域，没有命名空间或模块可以将功能进行分组。为了编写模块化代码，JavaScript开发者们不得不创造性地使用JavaScript现有的语法特性。



### ADM和CommonJS

AMD和CommonJS是两个相互竞争的标准，均可以定义JavaScript模块。除了语法和原理的区别之外，主要的区别是**AMD的设计理念是明确基于浏览器**，而**CommonJS的设计是面向通用JavaScript环境**（如Node.js服务端），而不局限于浏览器。

### AMD

AMD源于Dojo toolkit（https://dojotoolkit.org/），它是构建客户端Web应用程序的JavaScript流行工具之一。AMD可以很容易指定模块及依赖关系。同时，它支持浏览器。

目前，AMD最流行的实现是RequireJS（http://requirejs.org/）。

**定义一个依赖JQuery的模块：**

```JavaScript
define('MouseCounterModule', ['jQuery'], $ => {
    // 使用define函数指定模块及其依赖，模块工厂函数会创建对应的模块
    let numClicks = 0;
    const handleClick = () => {
        alert(++numClicks);
    };
    return { //模块的公共接口
        countClicks: () => {
            $(document).on("click", handleClick);
        }
    };
});
```

AMD提供名为define的函数，它接收以下参数：

- 新创建模块的ID。使用该ID，可以在系统的其他部分引用该模块。
- 当前模块依赖的模块ID列表。
- 初始化模块的工厂函数，该工厂函数接收依赖的模块列表作为参数。



以上代码中，我们使用AMD的define函数定义ID为MouseCounterModule的模块。该模块依赖于jQuery。因为依赖于jQuery，**因此AMD首先请求jQuery模块**，如果需要从服务端请求，那么这个过程将会花费一些时间。这个过程是异步执行的，以避免阻塞。所有依赖的模块下载并解析完成之后，调用模块的工厂函数，并传入所依赖的模块。在本例中，只依赖一个模块，因此传入一个参数jQuery。在工厂函数内部，是与标准模块模式类似的创建模块的过程：创建暴露模块公共接口的对象。



**可以看出，AMD有以下几项优点：**

- 自动处理依赖，我们无需考虑模块引入的顺序。
- 异步加载模块，避免阻塞。
- 在同一个文件中可以定义多个模块。





### CommonJS

CommonJS目前在Node.js社区具有最多的用户。

CommonJS 使用基于文件的模块，所以每个文件中只能定义一个模块。

CommonJS提供变量module，该变量具有属性exports，通过exports可以很容易地扩展额外属性。最后，module.exports作为模块的公共接口。



> 如果希望在应用的其他部分使用模块，那么可以引用模块。文件同步加载，可以访问模块公共接口。这是CommonJS在服务端更流行的原因，模块加载相对更快，只需要读取文件系统，而在客户端则必须从远程服务器下载文件，同步加载通常意味着阻塞。

**File: MouseCounterModule.js**

```JavaScript
const $ = require("jQuery"); // 同步引入jQuery模块
let numClicks = 0;
const handleClick = () => {
    alert(++numClicks);
};
module.exports = { // 使用module.exports定义模块公共接口
    countClicks: () => {
        $(document).on("click", handleClick);
    }
};
```

**在另一个模块（通常为另一个文件）这样引入：**

```JavaScript
const MouseCounterModule = require("MouseCounterModule.js");
MouseCounterModule.countClicks();
```

由于CommonJS要求一个文件是一个模块，文件中的代码就是模块的一部分。因此，不需要使用立即执行函数来包装变量。在模块中定义的变量都是安全地包含在当前模块中，不会泄露到全局作用域。例如，模块变量（$、numClicks和handleClick）虽然是在模块代码顶部（在函数或代码块外部）定义的，但是仍然在模块作用域中；如果在标准JavaScript文件中这样的写法将会生成全局变量。

再次强调，只有通过module.exports对象暴露的对象或函数才可以在模块外部访问。这个过程与模块模式的类似，唯一的区别是无需返回一个全新的对象，模块已经提供了扩展接口和属性的方法。



CommonJS最大的缺点是不显式地支持浏览器。浏览器端的JavaScript不支持module变量及export属性，我们不得不采用浏览器支持注意的格式打包代码，可以通过Browserify（http://browserify.org/）或RequireJS（http://requirejs.org/docs/commonjs.html）来实现。



### ES6模块

ES6模块结合了CommonJS与AMD的优点，具体如下。

- 与CommonJS类似，ES6模块语法相对简单，并且基于文件（每个文件就是一个模块）。
- 与AMD类似，ES6模块支持异步模块加载。

ES6引入了两个关键字：

- export
- import

一个导入，一个导出。

**导出：**

```JavaScript
const Kuan = "Yoshi"; // 在模块中定义一个顶级变量
export const message = "Hello";
export function sayHiToKuan() { // 使用关键字export分别导出定义的变量和函数
    return message + " " + Kuan; // 通过模块公共API访问模块内部变量
}
```

或在最后一行导出：

```JavaScript
const Kuan = "Yoshi";
const message = "Hello"; // 定义所有的模块标识符
function sayHiToKuan() {
    return message + " " + Kuan;
}
export { message, sayHiToKuan }; // 将所有的模块标识符全部导出
```

**默认导出**

```JavaScript
export default function () {
    return 'Kuan';
}
```

在关键字export后面增加关键字default，指定模块的默认导出。在本例中，模块默认导出一个函数。虽然指定了模块的默认导出，但是仍然可以导出其他标识符，如导出函数sayHiToKuan。

**那么如何引入？**

**引入：**

A. 分别引入

```JavaScript
import { message, sayHiToKuan } from "Kuan.js"; 
```

一行代码就可以导入。

B. 一次引入

```JavaScript
import * as myModule from "Kuan.js";
```

以上代码一次性导入了所有，并且重命名为myModule，以后就可以

C. 导入默认导出的

```JavaScript
import My from './kuan.js';
```

导入模块默认导出的内容，不需要使用花括号{}，可以任意指定名称



**在同一个文件编写两个import语句。ES6提供了简写语法：**

```JavaScript
import ImportedNinja, {compareNinjas} from "Kuan.js";
```



**导入、导出重命名**

```JavaScript
//************* Greetings.js ************/
function sayHi() {
    return "Hello";
}
assert(typeof sayHi === "function"
    && typeof sayHello === "undefined",
    "Within the module we can access only sayHi");
export { sayHi as sayHello } // 通过关键字as设置别名
//************* main.js *****************/
import { sayHello } from "Greetings.js"; // 只能导入sayHello
```



```JavaScript
/************* Hello.js *************/
export function greet() {
    return "Hello";
} //  在Hello.js文件中导出名为greet的函数
/************* Salute.js *************/
export function greet() {
    return "Salute";
} // 在Salute.js文件中导出名为greet的函数
/************* main.js *************/
import { greet as sayHello } from "Hello.js";
import { greet as salute } from "Salute.js"; //  使用as关键字重命名import的内容，避免命名冲突
```



**回顾**

导出：

```JavaScript
export const someValue = 1234
export const someValue0 = '1234'
export const someValue1 = {}
export let someValue2 = 1234
export let someValue3 = '1234'
export function someFunc = a => a+1

const someValue = 1234
function someFunc = a => a+1
let someObj = {}

export { someValue, someFunc, someObj}

// 重命名
const someValue = 1234
function someFunc = a => a+1
let someObj = {}

export {
	someValue as exportNum,
    someFunc as exportFunc,
    someObj as exportObj
}

// 默认导出，一个文件只能使用一次
export defalut someValue = 1234
```

导入：

```JavaScript
import { someValue } from './exportFile'  // 导入一个

import { someFunc, someObj } from './exportFile'   // 导入多个

import { someValue as importValue } from './exportFile'  // 重命名一个

import { someFunc as importFunc , someObj as importObj } from './exportFile' // 重命名多个

import {
    someValue,
    someFunc as importFunc 
}  // 导入多个，且部分重命名

import * as importModule from './exportFile'  // 导入全部且挂载在 importModule 对象上

console.log(importModule.someValue)  // 1234

import 'animate.css' //从其它模块整体导出

// 就是使用 default 导出的变量，导入的时候我们要为它命名
import value from './exportFile' //从其它模块部分重命名导出
```



组合使用：

```JavaScript
export * from './exportFile';// 从其它模块整体导出

export { exportValue } from './exportFile'; //其它模块部分导出

export { funcName as exportFunc } from './exportFile';//从其它模块部分重命名导出
```



## DOM操作

### 特性值

dom.setAttribute()

```JavaScript
let h = document.querySelector('.h');
h.setAttribute('id', '123');
```

![截图-1573086982](https://wimg.misiyu.cn/images/20191107/1573086982_e271fdbbdd1d5ed.png?x-oss-process=style/common)

dom.getAttribute()

```JavaScript
let h = document.querySelector('.h');
h.setAttribute('id', '123');
console.log(h.getAttribute('class'));
```

![截图-1573087043](https://wimg.misiyu.cn/images/20191107/1573087043_19eae7838ef5404.png?x-oss-process=style/common)

### 隐藏元素的属性

需要当心的是，在高度交互的网站中，元素的隐藏（display值设置为none时），可能会花一些时间，而且一个元素如果不显示的话，它就没有尺寸。在非显示元素上，尝试获取offsetWidth或offsetHeight属性值，结果都是0。

对于这样的隐藏元素，如果需要获取它在非隐藏状态时的尺寸，我们可以使用一个技巧，暂时取消元素的隐藏，然后获取值，然后再将其隐藏。当然，我们希望这种做法不要在视觉上漏出破绽，而是在幕后操作。那如何才能将一个隐藏元素，在不可见的情况下编程不隐藏呢？

