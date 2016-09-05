---
title: Swift - first day - 2
---
>离上一篇学习笔记已经10多天了，50%因为在忙公司的项目，50%是懒癌，这病得治
<!-- more -->

#### 5.闭包
##### 前提
* 支持函数类型，能够将函数作为参数或返回值传递
* 支持函数嵌套
##### Swift对闭包的定义
* 闭包是自包含的匿名函数代码块，可以作为表达式、函数参数和函数返回值。
* 闭包表达式的运算结果是一种函数类型。
* Swift中的闭包类似于Objective-C 中的代码块、C++和C#中的Lambda表达式、Java中的匿名内部类。

##### 嵌套函数一步步变闭包 
``` swift 
func calculate(operator: String) -> (Int, Int) -> Int {
	func add(a: Int, b: Int) -> Int {
		return a + b
	}
	func sub(a: Int, b: Int) -> Int {
		return a - b
	}
	var result : (Int, Int) -> Int
	switch(operator) {
		case "+" : result = add
		case "-" : result = sub
		default: result = add
	}
	return result
}
let f1: (Int, Int) -> Int = calculate("+")
print("10 + 5 = \(f1(10, 5))")
```

##### 用匿名函数代替， 也就是标准形式的闭包：
``` swift 
func calculate(operator: String) -> (Int, Int) -> Int {
	var result : (Int, Int) -> Int
	switch(operator) {
		case "+" : result = {(a: Int, b: Int) -> Int in
					return a + b
				}
		default : result = {(a: Int, b: Int) -> Int in
					return a - b
				}
	}
	return result
}
//...函数调用
```
##### 用类型推断简化（省略参数类型）的闭包代替
##### 如果返回值只有一句，return也可以省了
``` swift 
func calculate(operator: String) -> (Int, Int) -> Int {
	var result : (Int, Int) -> Int
	switch(operator) {
		case "+" : result = {a, b in return a + b}
		default : result = {a, b in a - b}
	}
	return result
}
//...函数调用
```
##### 省略参数名的写法：
``` swift 
//可以用 $0, $1, $2 ... 代替闭包中的参数，0指第一个参数，以此类推

func calculate(operator: String) -> (Int, Int) -> Int {
	var result : (Int, Int) -> Int
	switch(operator) {
		case "+" : result = {$0 + $1}
		default : result = {$0 - $1}
	}
	return result
}
//...函数调用
```
##### 直接用闭包返回值，有空深入一下js闭包：
``` swift 
let c1: Int = { (a: Int, b: Int) -> Int in
	return a + b
}(10, 5)
print("10 + 5 = \(c1)")
```

##### 尾随闭包
* 闭包表达式可以作为【函数的参数】传递
* 尾随闭包是【写在函数括号之后】的闭包表达式
* 函数支持将其作为最后一个参数调用

``` swift 
func calculate(operator: String, funN: (Int, Int) -> Int) {
	switch (operator) {
		case "+" : print("10 + 5 = \(funN(10, 5))")
		default : print("10 - 5 = \(funN(10, 5))")
	}
}
/**
*函数调用：
*把闭包表达式当参数传进去
*/
calculate("+", funN: { (a: Int, b: Int) -> Int in return a + b })

/**
*参数是函数可以提到调用的函数括号之外，喵喵喵？还提取公因式呢。。
*/
calculate("+") {
	(a: Int, b: Int) -> Int in return a + b
}

/**
*简写，看起来就像函数了。。。 如果看到大括号里面有in关键字或者$0这种就可以看成是闭包了
*/

calculate("-"){$0 - $1}
```
##### Capturing value : 捕获值
嵌套函数或闭包可以访问它所在上下文的变量和常量，这个过程称为捕获值。即便是定义这些常量和变量的原始作用域已经不存在，嵌套函数或闭包仍然可以在函数体内或闭包体内引用和修改这些值。