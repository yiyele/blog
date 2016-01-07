---
layout: post
title: Tinking in Java 读书笔记（三） 操作符
category: 读书笔记
comments: true
---

##3.操作符##
* >对对象进行赋值操作仅仅是将对象的引用进行赋值，复制后两个引用都指向同一个对象。

```java 
class Letter
{
	char c ;
}

public class Test {
	
	static void f(Letter y)
	{
		y.c = 'z';
	}

	public static void main(String[] args) {
		Letter x = new Letter();
		x.c = 'a';
		System.out.println("X.c="+x.c);
		f(x);
		System.out.println("X.c="+x.c);
	}

}

```

* 方法传递的是一个引用。
* Random的使用

```java
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Random;
public class TestRandom {

	public static void main(String[] args) {
		Random random1 = new Random(47);
		//使用相同的随机数种子，将产生相同的随机数。
		System.out.println("此次程序执行的时间为"+new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date()));
		System.out.println(""+(random1.nextInt(100)+1));//产生1-100的随机数
		System.out.println(""+(random1.nextInt(100)+1));
		Random random2 = new Random();
		//如果构造函数没有参数将以当前时间作为随机数种子，进而每次产生的随机数不同
		System.out.println(""+(random2.nextInt(100)+1));
		
	}

}
```

![](http://cl.ly/2Y1g3i2d0U1R/download/Image%202016-01-06%20at%207.47.27%20%E4%B8%8B%E5%8D%88.png)
![](http://cl.ly/380J3h1x2N1i/download/Image%202016-01-06%20at%207.47.43%20%E4%B8%8B%E5%8D%88.png)

* ++a,先运算再生成值 ； a++，先生成值再运算。
* n1==n2 Or n1.equals(n2) 

```java
class Dog{
	public Dog(String name)
	{
		this.name = name;
	}
	
	String name;
	public void say() {
		System.out.println("My name is "+this.name);
	}
}
public class TestEquals {

	public static void main(String[] args) {
		Integer n1 = new Integer(47);
		Integer n2 = new Integer(47);
		System.out.println((n1==n2));//比较引用
		System.out.println(n1.equals(n2));//比较值
		Dog dog1 = new Dog("heihei");
		Dog dog2 = new Dog("heihei");
		Dog dog3 = dog1;
		dog1.say();
		dog2.say();
		System.out.println(dog1==dog2);
		System.out.println(dog1.equals(dog2));
		System.out.println(dog1==dog3);
		System.out.println(dog1.equals(dog3));

	}

}
```
![](http://cl.ly/0y3905002J1m/download/Image%202016-01-06%20at%208.10.33%20%E4%B8%8B%E5%8D%88.png)
* 16进制 0x 开头 8进制 0 开头

```java
import java.util.Random;
public class TestBase {

	public static void main(String[] args) {
		Random random = new Random();
		int i = random.nextInt(20)+1;
		System.out.println("十进制\t"+Integer.toString(i));
		System.out.println("二进制 \t"+Integer.toBinaryString(i));
		System.out.println("16进制 \t"+Integer.toHexString(i));
		System.out.println("8进制\t"+Integer.toOctalString(i));

	}

}
```
![](http://i.imgur.com/Ow17Ts9.png)

* Java中浮点值转化为整形值采用的是截尾。

```java
public class TestTranslate {
	public static void main(String[] args) {
		float number = 0.6f;
		System.out.println(""+number);
		System.out.println(""+(int)number);
		System.out.println(""+Math.round(number));
	}

}
```
![](http://i.imgur.com/gvZwcAW.png)
