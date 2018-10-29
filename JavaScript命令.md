#JavaScript命令
1. 输出文本
`document.write()`
2. 更改html元素(id为demo的元素)更改其内容
`document.getElementById("demo").innerHTML="段落已修改。"`
3. `JavaScript`变量为`var`类型，不分`String`、`int`等
4. `x.innerHTML="<a href='http://wwf.org'>Visit WWF</a>";`输出网址，可点击访问
###消息框
1. 警告框
`alert("你好，我是一个警告框！");`
2. 确认框
```javascript
var r=confirm("按下按钮");
if (r==true)
{
    x="你按下了\"确定\"按钮!";
}
else
{
    x="你按下了\"取消\"按钮!";
}

```
3. 提示框
```javascript
var person=prompt("请输入你的名字","Harry Potter");
if (person!=null && person!="")
{
    x="你好 " + person + "! 今天感觉如何?";
    document.getElementById("demo").innerHTML=x;
}
```
4. 换行	`\n`

###数据类型
**1、基本类型:**
字符串（String）、数字(Number)、布尔(Boolean)、对空（Null）、未定义（Undefined）、Symbol
[Symbol介绍](https://blog.csdn.net/webxiaoma/article/details/73480960?utm_source=blogxgwz0)
**2、引用数据类型**
对象(Object)、数组(Array)、函数(Function)
**3、JavaScript拥有动态类型**
例：
```javascript
var x;               // x 为 undefined
var x = 5;           // 现在 x 为数字
var x = "John";      // 现在 x 为字符串
```

**6、数字**
只有一种数字类型，可带小数点或不带
极大极小的数可用科学计数法
```javascript
var y=123e5;
var z=123e-5;
```
**JavaScript对象**
对象由花括号分隔，括号内部属性以名称和值的形式存在，类似键值对
可通过两种方式调用其属性
！！！？？？此处不明白键和值哪个可以为空
```javascript
<script>
var person=
{
	firstname : "John",
	lastname  : 'sdg',
};
document.write(person.firstname+"<br>");
document.write(person.lastname + "<br>");
document.write(person["lastname"] + "<br>");
</script>
```
**Undefined和Null**
Undefined 这个值表示变量不含有值。可以通过将变量的值设置为 null 来清空变量。
**声明变量类型**
```javascript
var carname=new String;
var x=      new Number;
var y=      new Boolean;
var cars=   new Array;
var person= new Object;
```
###JS对象
**1、**访问对象属性
```javascript
person.lastName;		或		person["lastName"];
```
**2**对象方法
```javascript
<script>
var person = {
	id:123
    fullName : function() 
	{
       return this.firstName + " " + this.lastName;
    }
};
document.innerHTML = person.fullName();
</script>
```
###JS函数
**1、带参函数**
不需要标明参数的类型
```javascript
<script>
function myFunction(name,job){
    alert("Welcome " + name + ", the " + job);
}
</script>
```
**2、带返回值的函数**
函数那里不需要写返回值的类型
```javascript
function myFunction()
{
    var x=5;
    return x;
}
```
###JS变量
###函数
**1、局部变量**
```<script>
function myFunction() {
    var a = 4;
    document.getElementById("demo").innerHTML = a * a;
} 
```
**2、全局变量属于window对象，可用于页面上所有的脚本**
```javascript
<script>
var a = 4;
function myFunction() {
    document.getElementById("demo").innerHTML = a * a;
} 
</script>
```
**3、向未声明的变量赋值？？？**
把值赋给尚未声明的变量，该变量将被自动作为 window 的一个属性。
例：`value ="a"`;
已声明的变量不能配置全局属性
###作用域
**1、若变量在函数内没有声明，即没有用var关键字，则该变量为全局变量**
```javascript
// 此处可调用 carName 变量 
function myFunction() {
    carName = "Volvo";
    // 此处可调用 carName 变量
}
```
**2、全局变量**
全局变量为window对象，所有数据变量均可通过`window.`来调用
例：
```javascript
//此处可使用 window.carName
function myFunction() {
    carName = "Volvo";
}
```
###JS事件
**1、HTML事件**
onchange	         HTML 元素改变
onclick			   用户点击 HTML 元素
onmouseover		用户在一个HTML元素上移动鼠标
onmouseout		用户从一个HTML元素上移开鼠标
onkeydown		用户按下键盘按键
onload			浏览器已完成页面的加载
[更多](http://www.runoob.com/jsref/dom-obj-event.html)
HTML元素中可以添加事件属性，使用JavaScript代码可以添加HTML元素
例1：
```javascript
<button onclick="getElementById('demo').innerHTML=Date()">现在的时间是?</button>
<p id="demo"></p>
```
例2（更改自身元素 innerHTML用来返回标签结束到开始间的内容）：
```javascript
<button onclick="this.innerHTML=Date()">现在的时间是?</button>
```
###字符串
**1、**
可以使用单引号或双引号包裹，当字符串中含有引号时，最外层引号和包含的引号相同时记得使用转义字符。
```javascript
var answer1='It\'s alright';
var answer2="He is called \"Johnny\"";
var answer3='He is called "Johnny"';
```
**2、特殊字符**
\'	单引号
\"	双引号
\\	反斜杠
\n	换行
\r	回车
\t	tab(制表符)
\b	退格符
\f	换页符
**3、字符串可以是对象**
```javascript
var x = "John";
var y = new String("John");
typeof x // 返回 String
typeof y //返回 Object
```
不要创建 String 对象。它会拖慢执行速度，并可能产生其他副作用
```javascript
var x = "John";              
var y = new String("John");
(x === y) // 结果为 false，因为 x 是字符串，y 是对象
```
===为绝对相等，表示数据类型和值都必须相等
**4、字符串属性和方法**
**属性**
constructor		返回创建字符串属性的函数
length		       返回字符串的长度
prototype	       允许您向对象添加属性和方法
[**方法**](http://www.runoob.com/jsref/jsref-obj-string.html)
###运算符
字符串加数字输出为字符串
[比较和逻辑运算符](http://www.runoob.com/js/js-comparisons.html)
===绝对等于（值和类型均相等）
！==不绝对等于
###循环
**1、for和while**
```javascript
<script>
cars=["BMW","Volvo","Saab","Ford"];
var i=0;
for (;cars[i];){
	document.write(cars[i] + "<br>");
	i++;
}
</script>
```
```javascript
cars=["BMW","Volvo","Saab","Ford"];
var i=0;
while (cars[i])
{
    document.write(cars[i] + "<br>");
    i++;
}
```
java中不允许这样写，其他的都一样
**2、Break和Continue**
break		和java中的一样
continue	 中断循环中的迭代，如果出现了指定的条件，然后继续循环中的下一个迭代
**3、JS标签**
有点类似于C语言的标签，用于goto语句。
名字加上冒号：就是标签
例：(结果只会输出前三个元素)
```javascript
cars=["BMW","Volvo","Saab","Ford"];
list: 
{
    document.write(cars[0] + "<br>"); 
    document.write(cars[1] + "<br>"); 
    document.write(cars[2] + "<br>"); 
    break list;
    document.write(cars[3] + "<br>"); 
    document.write(cars[4] + "<br>"); 
    document.write(cars[5] + "<br>"); 
}
```
###JS的typeof,null,undefined
**1、typeof**
**typeof用来检测变量的数据类型**
```javascript
typeof "John"                // 返回 string 
typeof 3.14                  // 返回 number
typeof false                 // 返回 boolean
typeof [1,2,3,4]             // 返回 object
typeof null             	 // 返回 object
typeof {name:'John', age:34} // 返回 object
```
**2、null**
**null是一个只有一个值的特殊类型。表示一个空对象引用。**
null 表示 "什么都没有"。
```javascript
var person = null;           // 值为 null(空), 但类型为对象
var person = undefined;     // 值为 undefined, 类型为 undefined
```
**3、undefined**
**undefined 是一个没有设置值的变量**
**4、undefined和null的区别**
null 和 undefined 的值相等，但类型不等：
```javascript
typeof undefined             // undefined
typeof null                  // object
null === undefined           // false
null == undefined            // true
```
###类型转换
**1、JS数据类型**
5 种不同的数据类型：
string
number
boolean
object
function
3 种对象类型：
Object
Date
Array
2 个不包含任何值的数据类型：
null
undefined
**2、typeof操作符**
```javascript
typeof "John"                 // 返回 string 
typeof 3.14                   // 返回 number
typeof NaN                    // 返回 number
typeof false                  // 返回 boolean
typeof [1,2,3,4]              // 返回 object
typeof {name:'John', age:34}  // 返回 object
typeof new Date()             // 返回 object
typeof function () {}         // 返回 function
typeof myCar                  // 返回 undefined (如果 myCar 没有声明)
typeof null                   // 返回 object
```
NaN 的数据类型是 number
数组(Array)的数据类型是 object
日期(Date)的数据类型为 object
null 的数据类型是 object
未定义变量的数据类型为 undefined
如果对象是 JavaScript Array 或 JavaScript Date ，我们就无法通过 typeof 来判断他们的类型，因为都是 返回 Object
**3、constructor属性**
* constructor 属性返回所有 JavaScript 变量的构造函数。
```javascript
"John".constructor                 // 返回函数 String()  { [native code] }
(3.14).constructor                 // 返回函数 Number()  { [native code] }
false.constructor                  // 返回函数 Boolean() { [native code] }
[1,2,3,4].constructor              // 返回函数 Array()   { [native code] }
{name:'John', age:34}.constructor  // 返回函数 Object()  { [native code] }
new Date().constructor             // 返回函数 Date()    { [native code] }
function () {}.constructor         // 返回函数 Function(){ [native code] }
```
* 可以使用 constructor 属性来查看对象是否为数组 (包含字符串 "Array"):
```javascript
function isArray(myArray) {
    return myArray.constructor.toString().indexOf("Array") > -1;
}
```
* 可以使用 constructor 属性来查看对象是否为日期 (包含字符串 "Date"):
```javascript
function isDate(myDate) {
    return myDate.constructor.toString().indexOf("Date") > -1;
}
```
**4、类型转换**
**JavaScript 变量可以转换为新变量或其他数据类型：**
* 通过使用 JavaScript 函数
* 通过 JavaScript 自身自动转换

**将数字转换为字符串**
* 通过全局方法String()	该方法可用于数字、字母、变量、表达式
```javascript
String(x)         // 将变量 x 转换为字符串并返回
String(123)       // 将数字 123 转换为字符串并返回
String(100 + 23)  // 将数字表达式转换为字符串并返回
```
* 通过Number方法的toString()
```javascript
x.toString()
(123).toString()
(100 + 23).toString()
```
**将布尔值转换为字符串**
* 全局方法 String() 可以将布尔值转换为字符串。

* Boolean 方法 toString() 也有相同的效果。
