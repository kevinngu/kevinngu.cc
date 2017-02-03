---
title: ECMAScript6 入门（1）
categories:
- ECMAScript6
tags:
- ECMAScript6
---
> 变量与常量

<!-- more -->

从大神@(阮一峰)的ECMAScript6 入门摘抄的一点笔记，希望能系统的入门ECMAScript6，顺便附上完整原著传送门[ECMAScript6 入门](http://es6.ruanyifeng.com/#docs/let)

#### let基本用法
let可以用来声明变量(在swift中是常量)，而且只在声明的代码块内有效:
```javascript 
 {
	 let a = 10;
	 var b = 1;
 }
 a // ReferenceError: a is not defined
 b // 1
``` 
用`var`声明的变量只有一份，所以`console.log(i)` 输出的是最新的值：
```javascript 
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```
而用`let`声明的变量，由于`i`只在本轮循环内有效，所以10个变量都是不相同的，最后结果也跟`var`的不一样:
```javascript 
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```
`for`循环的特别之处，循环语句部分是一个父作用域，而循环体内部是一个单独的子作用域:
```javascript 
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
} //会输出3次abc，子作用域的i并不会影响循环
```
#### let不存在变量提升
意思是let要先声明，否则报错，var则不会（报undefined）。
#### 暂时性死区
同上，在用到let和const的地方，不先声明，就报错，
以上都是为了养成良好的编码习惯，先声明，后调用。
#### 块级作用域
块级作用域的出现，实际上使得获得广泛应用的立即执行函数表达式（IIFE）不再必要了（避免变量污染）:
```javascript 
// IIFE 写法
(function () {
  var tmp = ...;
  ...
}());

// 块级作用域写法
{
  let tmp = ...;
  ...
}
```
ES6允许在块级作用域中声明函数(一定要在大括号内)，ES5在严格模式下是不可以的。
另外，在块级作用域上加`do`将会把整个块级作用域当返回值返回。
#### const基本用法
`const`声明一个只读常量，一旦声明就不能更改，只声明不赋值，作用域和`let`一样，在声明的作用域内有效。

对于复合类型的变量，变量名不指向数据，而是指向数据所在的地址。const命令只是保证变量名指向的地址不变，并不保证该地址的数据不变，所以将一个对象声明为常量必须非常小心。
```javascript 
const foo = {};
foo.prop = 123;

foo.prop
// 123

foo = {}; // TypeError: "foo" is read-only
```

----------------------我是有底线的人------------------------