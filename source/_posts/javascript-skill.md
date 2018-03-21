---
title: JavaScript 开发小技巧
date: 2018-02-22 16:04:05
tags:
- JavaScript
- tips
categories: JavaScript
---

# JavaScript 开发小技巧
## 三目运算符
下面是一个很好的例子，将一个完整的 if 语句，简写为一行代码。
``` js
const x=20;
let answer  
if (x>10){
    answer="greater than 10"
}
else{
    answer="less than 10"
}
```
可以简写为:
``` js
let answer =x>10?"greater than 10":"less than 10"
```
<!----more--->
## 循环语句
当使用纯JavaScript（不依赖外部库，如 jQuery 或lodash）时，下面的简写会非常有用。
```  js
for (let i = 0 ; i < array.length ;i++)
```
可以简写为:
``` js
for (let index of array)
```
下面是遍历数组forEach 的简写示例：
``` js
[11,22,33].forEach((element,index,array)=>{
    console.log(`array[${index}]=${element}`)
})
logs:
array[0]=11
array[1]=22
array[2]=33
```
## 声明变量
在函数开始之前，对变量进行赋值是一种很好的习惯。在申明多个变量时：
``` js
let x;
let y;
let z=3;
```
可以简写为:
``` js
let x,y,z=3;
```
## 使用 === 代替 ==
==（或者!=）做对比的时候会将进行对比的两者转换到同一类型再比较。===（或者!==）则不会，他会将进行对比的两者做类型对比和值对比，相对于 == ，=== 的对比会更加严谨。
``` js
[10] == 10 // true
[10] === 10 // false
"10" == 10 // true
"10" === 10 // false
[] == 0 // true
[] === 0 // false
"" == false // true 但是 true == "a" 是false
"" === false // false
```
## if 语句
在使用 if 进行基本判断时，可以省略赋值运算符。
``` js
if (flag===true)
```
可以简写为:
``` js
if (flag)
```
## 十进制数
可以使用科学计数法来代替较大的数据，如可以将 10000000 简写为 1e7。
``` js
let i=10000000;
```
可以简写为:
``` js
let i=1e7;
```
## 模版字符串（ES5以下不支持）
传统的JavaScript语言，输出模板通常是这样写的，字符串拼接很让人头疼，也很容易出错。
``` js
$('#result').append(
  'There are <b>' + basket.count + '</b> ' +
  'items in your basket, ' +
  '<em>' + basket.onSale +
  '</em> are on sale!'
);
```
ES6引入了模板字符串解决这个问题
``` js
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```
## 转换数值的更加的方法
``` js
let i ="1234"
i = + str; // i=1234
```
## 清空一个数组
你定义一个数组，并希望清空它的内容。通常，你会这样做：
``` js
var list = [1, 2, 3, 4];
function empty() {
    //清空数组
    list = [];
}
empty();
```
但是还有一种更高性能的方法。
你可以使用这些代码：
``` js
var list = [1, 2, 3, 4];
function empty() {
    //清空数组
    list.length = 0;
}
empty();
```
· list =[] 将一个变量指定个引用到那个数组，而其他引用都不受影响。这意味着，对于先前数组的内容的引用仍然保留在内存中，从而导致内存泄漏。
· list.length = 0 删除数组内的所有东西，这不需要引用任何其他的东西
然而，如果你有一个copy的数组（A和copy-A），如果你使用list.length = 0 删除其内容，副本也会失去它的内容。
``` js
var foo = [1,2,3];
var bar = [1,2,3];
var foo2 = foo;
var bar2 = bar;
foo = [];
bar.length = 0;
console.log(foo, bar, foo2, bar2);
//[] [] [1, 2, 3] []
```
StackOverflow上的更多详情：difference-between-array-length-0-and-array

## 对数组排序进行"洗牌"(随机排序)
这段代码在这里使用Fisher Yates洗牌算法给一个指定的数组进行洗牌(随机排序)。
``` js
function shuffle(array) {
    var m = array.length, i;
    // 如果还有剩余的需要打乱的元素...
    while (m) {
        // 选择一个剩余的元素
        i = Math.floor(Math.random() * m--);
        // 和当前元素交换
        [array[i],array[m]]=[array[m],array[i]]
    }
    return array;
}
```
案例：
``` js
console.log(shuffle([1,2,3,4,5,6,7,8,9,10,11]));
//[2, 3, 5, 4, 1, 6, 11, 9, 7, 8, 10]
```
##  在数组插入一个元素
``` js
var arr = [1,2,4,5];
arr.push(6); // [1, 2, 4, 5, 6]
arr.unshift(0); // [0, 1, 2, 4, 5, 6]
arr.splice(3, 0, 3); // [0, 1, 2, 3, 4, 5, 6]
```
## 字符排序
``` js
['Shanghai', 'New York', 'Mumbai', 'Buenos Aires'].sort();
// ["Buenos Aires", "Mumbai", "New York", "Shanghai"]
```
## 冒泡排序
``` js
function bubbleSort(arr) {
    var i = arr.length, j;
    while (i > 0) {
        for (j = 0; j < i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j],arr[j + 1]]=[arr[j+1],arr[j]]
            }
        }
        i--;
    }
    return arr;
}
```
##  undefined 和 null 的不同
- undefined指的是一个变量未被声明，或者一个变量被声明但未赋值
- null是指一个特定的值，即"没有值"
- JavaScript给未赋值的变量默认定义为undefined
- JavaScript不会给未赋值的变量设置null值，它被程序员用来表示一个无价值的值
- undefined在json格式数据中是无效的，而null有效
- undefined 类型是 undefined
- null类似是object.为什么呢？
- 两者都是原始值
- 两者都被认为false(Boolean(undefined) // false, Boolean(null) // false)。
- 辨认变量是不是undefined
typeof variable === "undefined" 
- 检查变量是不是null
variable === "null" 
从值考虑他们是相等的，但是从类型和值共同考虑他们是不相等的
null == undefined // true
null === undefined // false 
##  严格模式"use strict"
严格模式的JavaScript让开发人员更加安全的编写JavaScript。  
默认情况下，JavaScript允许开发者懒惰，例如，我们在第一次声明变量的时候可以不用var，虽然这可能看起来像一个没有经验的开发人员，同时这也是很多错误的根源，变量名拼写错误或意外地将它提到了外部作用域。  
程序员喜欢让电脑为我们做些无聊的事，检查一些我们工作的错误。"use strict"指令我们做这些，将我们的错误转换成JavaScript的错误。  
我们把这个指令可以通过添加在一个js文件的顶部：
``` js
// 整个script文件都将是严格模式语法
"use strict";
var v = "Hi! I'm a strict mode script!";
或者在函数内：
function f()
{
// 函数范围内的严格模式语法
'use strict';
function nested() { return "And so am I!"; }
return "Hi! I'm a strict mode function! " + nested();
}
function f2() { return "I'm not strict."; }
```
在包含这个指令的JavaScript文件或者函数内，我们将一些较大的JavaScript项目中的不良行为直接在JavaScript引擎执行中禁止了。在其他情况中，严格模式改变以下的行为：
- 变量只有在前面 var 声明了才能用
- 试图写入只读属性产生的误差
- 必须用 new 关键字调用构造函数
- this 不会默认指向全局对象
- 非常有限的使用eval()
- 保护保留字符或未来保留字符不被作为变量名使用
严格模式在新项目中是很有好处的，但是在大多数地方没使用到它的老项目里使用它是非常具有挑战性的。当你把多个文件合并到一个文件时，它也是个问题，就像可能导致整个文件都在严格模式下执行。  
它不是一个声明，只是一个字面量，早期版本的浏览器会忽略它。严格模式支持：
- IE 10+
- FF 4+
- Chrome 13+
- Safari 5.1+
- Opera 12+
## 检查一个对象是否有属性
当你要检查一个对象是否存在某个属性时，你可能会这样做 ：
``` js
var myObject = {name: '@tips_js'};
if (myObject.name) { ... }
```
这是可以的，但你必须知道这个还有两原生的方式，in operator 和 object.hasownproperty，每个对象是对象，既可用方法。每个object都继承自Object，这两个方法都可用。  
两个方法的一些不同点：
``` js
var myObject = {name: '@tips_js'};
myObject.hasOwnProperty('name'); // true
'name' in myObject; // true
myObject.hasOwnProperty('valueOf'); // false, valueOf 是从原型链继承的
'valueOf' in myObject; // true
```
他们之间的不同在于检查的性质，换句话说，当该对象本身有查找的属性时hasOwnProperty返回yrue，然而，in operator不区分属性创建的对象和属性继承的原型链。  
这里有另外一个例子：
``` js
var myFunc = function() {
    this.name = '@tips_js';
};
myFunc.prototype.age = '10 days';
var user = new myFunc();
user.hasOwnProperty('name'); // true
user.hasOwnProperty('age'); // false, 因为age是原型链上的
```
## ES6中参数处理
在许多编程语言中，函数的参数是默认的，而开发人员必须显式定义一个参数是可选的。在JavaScript中的每个参数是可选的，但我们可以这一行为而不让一个函数利用ES6的默认值作为参数。
``` js
const _err = function( message ){
throw new Error( message );
}
const getSum = (a = _err('a is not defined'), b = _err('b is not defined')) => a + b
getSum( 10 ) // throws Error, b is not defined
getSum( undefined, 10 ) // throws Error, a is not defined
```
> _err是立即抛出一个错误的函数。如果没有一个参数作为值，默认值是会被使用，_err将被调用，将抛出错误。你可以在Mozilla开发者网络看到的更多默认参数的例子。
## 测量一个JavaScript代码块性能的技巧
快速测量一个JavaScript块的性能，我们可以使用控制台的功能像console.time(label)和console.timeEnd(label)
``` js
console.time("Array initialize");
var arr = new Array(1000),
len = arr.length,
i;
for (i = 0; i < len; i++) {
arr[i] = new Object();
};
console.timeEnd("Array initialize"); // 输出: Array initialize: 0.451904296875ms
```
更多信息Console object, JavaScript benchmarking 
demo：jsfiddle-codepen (在浏览器控制台输出)
## arrow 函数(ES6)
介绍下ES6里的新功能，arrow函数可能会是个很方便的工具，用更少行数写更多代码。他的名字来源于他的语法，=>和小箭头->比就像一个“胖胖的箭头”。可能有些人知道，这种函数类型和其他静态语言如lambda表达式的匿名函数。它被称为匿名，因为这些箭头函数没有一个描述性的函数名。  
那么这样有什么好处呢？  
语法：更少的LOC，不用一次次的键入函数关键字。  
语义：从上下文中捕捉关键字this。  
简单语法案例：  
看看下面的两段代码片段，他们做的是一样的工作。你能很快的理解arrow函数的功能。
``` js
// arrow函数的日常语法
param => expression
// 可能也会写在括号中
// 括号是多参数要求
(param1 [, param2]) => expression
 
// 使用日常函数
var arr = [5,3,2,9,1];
var arrFunc = arr.map(function(x) {
    return x * x;
});
console.log(arr)
 
// 使用arrow函数
var arr = [5,3,2,9,1];
var arrFunc = arr.map((x) => x*x);
console.log(arr)
```
正如你所看到的，这个例子中的arrow函数可以节省你输入括号内参数和返回关键字的时间。建议把圆括号内的参数输入，如 (x,y) => x+y 。在不同的使用情况下，它只是用来应对遗忘的一种方式。但是上面的代码也会这样执行：x => x*x.目前看来，这些仅仅是导致更少的LOC和更好的可读性的句法改进。  
this 绑定  
还有一个更好的理由使用arrow函数。那就是在会出现this问题的背景下。使用arrow函数，你就不用担心.bind(this)和 that=this 了。因为arrow函数会从上下文中找到this。  
看下面的例子：
``` js
// 全局定义this.i
this.i = 100;
var counterA = new CounterA();
var counterB = new CounterB();
var counterC = new CounterC();
var counterD = new CounterD();
 
// 不好的示例
function CounterA() {
    // CounterA's `this` 实例 (!! 忽略这里)
    this.i = 0;
    setInterval(function () {
        // `this` 指全局对象，而不是 CounterA's `this`
        // 因此，开始计数与100，而不是0 (本地的 this.i)
        this.i++;
        document.getElementById("counterA").innerHTML = this.i;
    }, 500);
}
// 手动绑定 that = this
function CounterB() {
    this.i = 0;
    var that = this;
    setInterval(function() {
        that.i++;
        document.getElementById("counterB").innerHTML = that.i;
    }, 500);
}
// 使用 .bind(this)
function CounterC() {
    this.i = 0;
    setInterval(function() {
        this.i++;
        document.getElementById("counterC").innerHTML = this.i;
    }.bind(this), 500);
}
// 使用 arrow函数
function CounterD() {
    this.i = 0;
    setInterval(() => {
        this.i++;
        document.getElementById("counterD").innerHTML = this.i;
    }, 500);
}
```
## 使用更简单的类似indexOf的包含判断方式
原生的JavaScript没有contains方法。对检查字符串或字符串数组项中是否存在某值，你可以这样做：
``` js
var someText = 'JavaScript rules';
if (someText.indexOf('JavaScript') !== -1) {
}
// 或者
if (someText.indexOf('JavaScript') >= 0) {
}
```
但是我们再看看这些ExpressJs代码片段。
``` js
// examples/mvc/lib/boot.js
for (var key in obj) {
// "reserved" exports
if (~['name', 'prefix', 'engine', 'before'].indexOf(key)) continue;
 
// examples/lib/utils.js
exports.normalizeType = function(type){
return ~type.indexOf('/')
? acceptParams(type)
: { value: mime.lookup(type), params: {} };
};
 
// examples/web-service/index.js
// key is invalid
if (!~apiKeys.indexOf(key)) return next(error(401, 'invalid api key'));
```
问题是~位运算符。"运算符执行操作这样的二进制表达式，但他们返回标准的JavaScript的数值."  
他们将-1转换为0，而0在JavaScript中又是false。
``` js
var someText = 'text';
!!~someText.indexOf('tex'); // someText 包含 "tex" - true
!~someText.indexOf('tex'); // someText 不包含 "tex" - false
~someText.indexOf('asd'); // someText 不包含 "asd" - false
~someText.indexOf('ext'); // someText 包含 "ext" - true
String.prototype.includes()
```
在ES6(ES 2015)中介绍了includes()方法可以用来确定是否一个字符串包含另一个字符串：  
'something'.includes('thing'); // true   
在ECMAScript 2016 (ES7)中，甚至数组都可以这样操作，如indexOf：  
!!~[1, 2, 3].indexOf(1); // true  
[1, 2, 3].includes(1); // true   
不幸的是，这只是在Chrome，Firefox，Safari 9或以上的浏览器中被支持。

## 给回调函数传递参数
在默认情况下，你无法将参数传给回调函数，如下：
``` js
function callback() {
console.log('Hi human');
}
document.getElementById('someelem').addEventListener('click', callback);
```
你可以采取JavaScript闭包的优点来给回调函数传参，案例如下：
``` js
function callback(a, b) {
return function() {
console.log('sum = ', (a+b));
}
}
var x = 1, y = 2;
document.getElementById('someelem').addEventListener('click', callback(x, y));
```
什么是闭包呢？闭包是指一个针对独立的(自由)变量的函数。换句话说，闭包中定义的函数会记住它被创建的环境。了解更多请参阅MDN所以这种方式当被调用的时候，参数X/Y存在于回调函数的作用域内。  
另一种方法是使用绑定方法。例如：
``` js
var alertText = function(text) {
alert(text);
};
document.getElementById('someelem').addEventListener('click', alertText.bind(this, 'hello'));
```
两种方法在性能上有一些略微区别，详情参阅jsperf

## Node.js:让module在没被require的时候运行
在node里，你可以根据代码是运行了require('./something.js')还是node something.js，来告诉你的程序去做两件不同的事情。如果你想与你的一个独立的模块进行交互，这是很有用的。
``` js
if (!module.parent) {
    // 运行 `node something.js`
    app.listen(8088, function() {
    console.log('app listening on port 8088');
})
} else {
    // 使用 `require('/.something.js')`
    module.exports = app;
}
```
更多信息，请看the documentation for modules
## 更快的四舍五入
今天的技巧是关于性能。见到过双波浪线"~~"操作符吗？它有时也被称为double NOT运算符。你可以更快的使用它来作为Math.floor()替代品。为什么呢？  
单位移~将32位转换输入-(输入+1)，因此双位移将输入转换为-(-(输入+1))，这是个趋于0的伟大的工具。对于输入的数字，它将模仿Math.ceil()取负值和Math.floor()取正值。如果执行失败，则返回0，这可能在用来代替Math.floor()失败时返回一个NaN的时候发挥作用。
``` js
// 单位移
console.log(~1337) // -1338
// 双位移
console.log(~~47.11) // -> 47
console.log(~~-12.88) // -> -12
console.log(~~1.9999) // -> 1
console.log(~~3) // -> 3
//失败的情况
console.log(~~[]) // -> 0 
console.log(~~NaN) // -> 0
console.log(~~null) // -> 0
//大于32位整数则失败
console.log(~~(2147483647 + 1) === (2147483647 + 1)) // -> 0
```
虽然~~可能有更好的表现，为了可读性，请使用Math.floor()。
## 字符串安全连接
假设你有一些类型未知的变量，你想将它们连接起来。可以肯定的是，算法操作不会在级联时应用：
``` js
var one = 1;
var two = 2;
var three = '3';
var result = one + two + three; //"33" 而不是 "123"
var result = ''+one + two + three; //"123"
var result = ''.concat(one, two, three); //"123"
```
## 返回对象的函数能够用于链式操作
当创建面向对象的JavaScript对象的function时，函数返回一个对象将能够让函数可链式的写在一起来执行。
``` js
function Person(name) {
    this.name = name;
    this.sayName = function() {
        console.log("Hello my name is: ", this.name);
        return this;
    };
    this.changeName = function(name) {
        this.name = name;
        return this;
    };
}
var person = new Person("John");
person.sayName().changeName("Timmy").sayName();
//Hello my name is: John
//Hello my name is: Timmy
```