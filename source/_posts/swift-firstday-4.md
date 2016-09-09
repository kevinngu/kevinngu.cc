---
title: Swift - first day - 4
---
> 构造， 继承， 扩展
<!-- more -->

#### 8.构造与析构
##### 构造函数，就是java的构造方法，不过函数名是init
##### 为了可读性，可以用外部参数名...（这个真的增加了可读性吗）
``` swift 
class A {
	var width : Double
	var height : Double
	init(w width : Double, h height : Double) {
		//self相当于this关键字
		self.width = width
		self.height = height
	}
}
var a = A(w: 100.0, h:100.0)
```
函数调用第一个参数可以不指定参数名，构造函数不可以额省略
##### 在结构体中可以用默认构造函数，不适用于类
``` swift 
struct A {
	var a : Double
	var b : Double
}
//结构体中不用显式的写init函数了
var c = A(a: 10.0, b: 20.0)
```
##### 重载
* 参数列表不同 
* 外部参数名不同

也就是说，这样也算重载
``` swift
init(width : Double){}
init(W width : Double){}
```
##### 构造函数代理
横向代理，也叫便利构造函数
而且，便利构造函数必须最终以调用一个指定构造函数结束
``` swift
init(width : Double){}
//便利构造函数
convenience init(){
	self.init(width: 10.0)
}
```
向上代理,也叫指定构造函数，就是在继承的情况下调用父类的构造函数咯，用super关键字
##### 析构函数
* 与构造过程相反，实例最后释放的时候需要清除一些资源，这个过程就是析构过程。
* 析构过程中也会调用一种特殊的方法deinit，称为析构函数。
* 析构函数deinit没有返回值，也没有参数，也不需要参数的小括号，所以不能重载。
* 因为Swift有自动的内存管理机制，deinit用的也就不多，通常用在关闭文件等。 
#### 9.类继承
类似于java的单继承，但可以实现多个协议（接口）
``` swift
class Parent : Child {}
```
##### 构造过程
* 先初始化子类存储属性
* 再初始化父类存储属性
* 跟java相反

##### 安全检查
指定构造函数必须保证其所在类的所有存储属性都初始化完成之后才能调用父类构造函数代理
``` swift
init(a : String){
	self.a = a
	super.init()
}
```
为子类设置新值必须在父类构造函数调用完成之后，否则值会被父类初始化值的时候覆盖。
子类调用函数也是，否则会有编译错误。

##### 构造函数继承
* 子类没有定义任何构造函数，将自动继承父类所有指定构造函数
* 子类将自动继承父类所有便利构造函数

#### 10.扩展
> Extensions add new functionality to an existing class, structure, enumeration, or protocol type. This includes the ability to extend types for which you do not have access to the original source code (known as retroactive modeling).

逆向建模？没看明白的时候先抄一段苹果语录总是对的。

##### 声明
``` swift
extension SomeType {
        // new functionality to add to SomeType goes here
}
```

##### 可以在原始类型上扩展
``` swift
extension Int {
	var errorMessage : String {
		var errorStr = ""
		switch (self) {
			case -1:
			errorStr = "ERROR"
			default:
			errorStr = ""
		}
		return errorStr
	}
}
let message = (-1).errorMessage
}
```
##### 指定构造函数和析构函数只能由原始类型提供