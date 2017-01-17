---
title: Swift - first day - 3
categories:
- IOS
tags:
- Swift
---
> 面向对象
<!-- more -->

#### 6.面向对象
##### Swift的面向对象类型
* 类
* 结构体
* 枚举
* （结构体和枚举只是包含了面向对象的特点）

##### 枚举
``` swift 
enum WeekDays {
	case Monday
	case Tuesday
	case Wednesday
	case Thursday
	case Friday
}
OR
enum WeekDays {
	case Monday, Tuesday, Wednesday, Thursday, Friday
}
```
##### Swift编译器可以根据上下文推断枚举类型，所以可以写成WeekDays.Monday 或者 .Monday 的形式
##### 枚举的raw values
``` swift 
enum WeekDays : Int {
	case Monday = 0
	case Tuesday = 1
	case Wednesday = 2
	case Thursday = 3
	case Friday = 4
}
let friday = WeekDays.Friday.rawValue //转换为原始值
```
##### 类
``` swift 
class Employee { 
	var no: Int = 0 
	var name: String = ""
}
let emp = Employee()
```
##### 结构体
``` swift 
struct Department {
	var no: Int = 0
	var name: String = ""
}
var dept = Department()
```
##### 无可选链
``` swift 
class Employee {
	var dept : Department = Department()
}
```
##### 可选链
``` swift 
class Employee {
	var dept : Department?
}
```
> Optional chaining is a process for querying and calling properties, methods, and subscripts on an optional that might currently be nil. If the optional contains a value, the property, method, or subscript call succeeds; if the optional is nil, the property, method, or subscript call returns nil. 

##### 按照苹果的说法，也就是说在可选链上调用的属性，方法，下标如果有空值，会返回nil.
如果用？声明可选类型，就要用！显示拆包
如果用！声明，可以隐式拆包
##### 修饰符
* public 
* internal, 访问自己模块的任何internal实体
* private

#### 7.属性
##### 存储属性，只适用于类和结构体，用var和let定义，也就是一般类和结构体的定义
##### 计算属性
``` swift 
class Employee {
	var name : String {
		get {
			return ""
		}
		set (newValue) {//newValue也可以不写，默认参数名就是newValue
			var a = newValue
		}
	}
}
```
##### 静态属性 static