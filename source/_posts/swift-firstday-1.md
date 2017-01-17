---
title: Swift - first day - 1
categories:
- IOS
tags:
- Swift
---
>公司ios培训第一天的swift笔记，略简陋，略随意，介绍下基本情况，以后深入学习再慢慢作补充。 终于明白为什么别人写博客总要把一个点分几次来写了，一是精力不足以一次过写完所有观点，二是写太长像流水账自己也懒得看了，这篇暂且就叫firs day - 1吧 
<!-- more -->

#### 1.编译和运行swift
##### repl(简单的交互式运行编程环境)
* terminal
* xCode -> create playground

##### 编译成可执行文件(通过xcode创建os x工程)
* xCode create new project
* 使用swiftc命令

#### 2.Swift 基础语法
##### 标识符基本和java一致，字母是Unicode编码，所以可以输入表情符号
##### 常量 -> let    变量 -> var  
##### 注释和java基本一致
##### 运算符和java基本一致
##### 控制和循环和java基本一致，可以用guard关键字判断一个条件为true的情况下执行某语句，否则终止或跳过执行某语句
##### fallthrough只能用在swtich中，达到执行多个case的情况

#### 3.数组和字典
##### 创建数组：
``` swift
var arrayList = ["a" ,"b", "c"]
```
##### 创建空数组：
``` swift
var emptyList = [String]()
```
##### 创建字典：
``` swift
var occupations = ["a":"captain",
 "b":"mechanic"，]
```
###### 允许最后一个元素有逗号，当然也可以没有
##### 空字典：
``` swift
var occupations = [String:Int]()
```
##### 用var声明的可变数组，可以对数组中的元素进行追加、插入、删除和替换等操作
插入： insert()
追加： append()  ， +， +=
删除： removeAtIndex()
字典删除： removeValueForKey(key)
字典更新： updateValue(value, key)
##### 可以用 for in 对字典和数组进行遍历

#### 4.函数
``` swift
func 函数名（参数名： 类型...） -> 返回值类型{
	语句组
	return 返回值
}
```
##### 无返回值函数
``` swift
func name(param: type){}
func name(param: type) -> (){}
func name(param: type) -> Void(){}
```
##### 函数可以嵌套，在调用函数并传参的时候，第一个参数名不可以省略