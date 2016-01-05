---
layout: post
title: Tinking in Java 读书笔记（二） 一切都是对象
category: 读书笔记
comments: true
---

##2.一切都是对象
###2.1用引用操纵对象
```java
String s;
```
* 这只是一个引用，并没有对象与之关联。
* 比较安全的做法是创建一个引用的同时对其就初始化。

```java
String s="abc";
```
###2.2必须由你创造所有的对象
* 通过new来实现引用与一个新的对象相关联

```java
Stirng s = new String("abc")
```
* 对象的引用存放在堆栈中
* 所有的Java对象存放在堆中。
* Java中基本数据类型，创建一个直接存值得变量，并且存在堆栈中。
基本数据类型包括 boolean char byte short int long float double **void**
* 高进度数字 BigInteger BigDecimal
* Java会确保数组被初始化

###2.3永远不需要销毁对象
```java
{
	Stirng s = new String("abc")
}
```
* 仅仅s会在作用域终点消失，而new出来的对象会继续存在。
* 垃圾回收器会监视所有new出来的对象，当对象不会再被引用，即所有指向对象的引用断开的时候，对象的内存就会被释放。

###2.4创建新的数据类型：类
* 类就是一种数据类型

>类包括字段（数据成员）和方法（成员函数）

* 类的成员变量必须初始化。
* 如果成员变量没有初始化Java会自动初始化
	1.如果是引用型的，比如：String，还有类对象，他们的默认值都是：null；
	2.如果是基本数据类型，char=null , **boolean=false** ，其余为0
	3.如果基本数据类型是局部变量不会被初始化，编译也会出错。

###2.5方法、参数和返回值
>Java中的方法只能作为类的一部分来创建

* 方法只能通过对象来调用
* void修饰的方法可以没有return语句

###2.6构建一个Java程序
> 通过反转Internet的域名来构建自己的类库名

* net.mindview.utility.foibles

>当申明一个事物是static，意味着这个域或方法不会与类的任何对象实例关联在一起。

* 这样可以为特定的域分配单独的存储空间，也可以不创建对象就调用某个特定的方法。
* 修饰为static以后可以通过对象名或者类名来直接调用。

```java
class StaticTest{
	static int i=47;
}

StaticTest st1 = new staticTest();
StaticTest st2 = new staticTest();
//此时st1.i=st2.i=staticTest.i=47
staticTest.i++;
//此时st1.i=st2.i=staticTest.i=48
```
###2.7你的第一个Java程序
*   **学会查看JDK API**

```java
import java.text.SimpleDateFormat;
import java.util.Date;

public class HelloDate {
	
	public static void main(String[] args)
	{
		System.out.println("Hello,it's");
		System.out.println(new Date());
		System.out.println(new Date().toString());
		System.out.println(new SimpleDateFormat("yyyy-MM-dd E  HH:mm:ss").format(new Date()));
	}
}
```
![](http://cl.ly/2f2t2Y241i3a/download/Image%202016-01-05%20at%2010.55.41%20%E4%B8%8B%E5%8D%88.png)

###2.8注释和嵌入文档
>使用javadoc的方式有两种：嵌入HTML和“文档标签”。

* 嵌入HTML主要是html标签 **不添加html中的标题标签**
* 文档标签：@开头

###2.9编码风格
* 驼峰法
* **类名首字母大写**其余变量，方法名开头小写。


