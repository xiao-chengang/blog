---
title: ES6 
date: 2018-03-03 16:55:24
tags: javascript
categories: javascript 
---

# ES6
ES6 就是ECMAScript 6是新版本JavaScript语言的标准。
## let 和 const
ES6 新增了 let 和 const 来声明变量和常量，它们的用法类似var, 但只在代码块中有效。
###  let 的基本使用
```js
{
    var a = 'hello';
    let b = 'world';
}

a // hello
b // Uncaught ReferenceError: a is not defined
```
<!-------more-------->
上述代码表明，let只在他所在的代码块中有效。
### 不能重复定义
let不允许在相同作用域内，重复声明同一个变量。
```js
let a = 'hello';
let a = 'world'; // Uncaught SyntaxError: Identifier 'a' has already been declared

function s1(arg){
    let arg;  // Uncaught SyntaxError: Identifier 'arg' has already been declared
}
```
### 不存在变量提升
var 命令会存在变量提升的问题，在定义之前使用，值为 undefined。 
let 命令改变了这个行为，必须要在声明后使用，否则报错。
``` js
console.log(a); // Uncaught ReferenceError: a is not defined
let a = 'hello world'; 

console.log(b); // 值为 undefined
var b = 'hello kitty' 
```
### 临时锁区（Temporal Distonrtion Zone）
保证了let 命令不会受到外部影响。
``` js
var a = 123;
function s1(){
    a = 'hello world';  // Uncaught ReferenceError: a is not defined
    let a = 'hello kitty';
}
```
### const 基本使用
const声明一个只读的常量。一旦声明，常量的值就不能改变。
``` js
const a = 'hello world!';
console.log(a) // hello world!

a = 'hello kitty'; // Uncaught SyntaxError: Identifier 'a' has already been declared
```
const实际上并不是保证变量的值不能变，而是变量指向的那个内存地址不得改动。
``` js
const arr = [];
arr[0] = 'hello';
arr[1] = 'world';
console.log(arr); // ["hello", "world"]

arr = []; // Uncaught SyntaxError: Identifier 'arr' has already been declared

const json = {};
json.name = 'LiMing';
console.log(json.name)  // LiMing

json = {} Uncaught SyntaxError: Identifier 'json' has already been declared
```
常量 arr, json 储存的是一个地址，只是保证了地址不可变，但数组和对象本身是可变的，所以依然可以为其添加新属性。
## 解构
### 数组解构赋值
``` js
var name = 'LiMing';
var age = 12;
// ES5 变量赋值

let [name, age] = ['LiMing', 12];
// 解构赋值
```
以前为变量赋值，只能直接指定值。ES6中可以按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构。
```js
let a = ['LiMing', 12];
let [name, age] = a;
console.log(name, age) // LiMing 12

let [,,b] = ['hello', 'world', 'hello kitty'];
console.log(b) // hello kitty

let [one, , two] = [1, 2, 3];
console.log(one, two) // 1 3

let [s1, ...s2] = [1, 2, 3, 4, 5];
console.log(s1, s2)  // 1  [2, 3, 4, 5]

let b = [];
console.log(b) // undefined

let [a1, a2 ,a3] = [1];
console.log(a1, a2)  // 1 undefined
```
如果解构不成功，变量的值就等于undefined。 
如果右边的数据不是数组将会报错。
``` js
let [a] = true; // TypeError: true is not iterable

let [a] = NaN; // TypeError: NaN is not iterable

let [a] = 1; // TypeError: 1 is not iterable

let [a] = null; // TypeError: null is not iterable

let [a] = undefined; // TypeError: undefined is not iterable

let [a] = {}; // TypeError: {} is not iterable
```
### 默认值
解构允许指定默认值
``` js
let [a = 'hello'] = [];
console.log(a) // hello 
```
ES6内部严格使用 === 来判断是否有值，所以只有当一个数组成员严格等于undefined，默认值才会生效。
```js
let [a = 'hello world'] = [undefined];
console.log(a) // hello world

let [a = 'hello world'] = [null];
let [b = 'hello kitty'] = [''];
console.log(a, b)  // null '' 
```
### 对象解构
解构当然也可以用于对象
```js
let {name, age} = {name: 'LiMing', age: 12}
console.log(name, age)  // LiMing 12
```
对象解构与数组解构不同。 数组是有顺序的，变量值有位置决定，而对象是无序的，所以变量名必须为对象的属性名
```js
let json = {name: 'zero'}
let {name} = json
let {a} = json
console.log(name, a) // zero undefined
```
如果变量名与属性名不一致，则需要：
``` js
let {a: name} = {name: 'zero'}
console.log(a)  // zero
```
### 函数参数解构
函数的参数当然也可以解构
``` js
function s1([a, b]){
    return a + b
}
console.log(s1([1, 5])) // 6


function add({a = 0, b = 0} = {}) {
    return a + b;
}
add({a: 3, b: 8}); // 11
add({a: 3}); // 3
add({}); // 0
add(); // 0
```