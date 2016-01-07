---
layout: post
title: Tinking in Java 读书笔记（四） 控制执行流程
category: 读书笔记
comments: true
---

##4.控制执行流程
* Foreach语法
> 基本格式 for(类型 x : f)

```java
public class TestForeach {
	public static void main(String[] args) {
		for (char c  : "Hello,World".toCharArray()) {
			System.out.print(c+"   ");
		}

	}
}
```

![](http://i.imgur.com/jijDfJp.png)

* Java中没有goto，通过标签来实现。

```java
public class TestLabel {

	public static void main(String[] args) {
		int i =0;
		outer:
			for(;true;){
				inner:
					for(;i<10;i++){
						System.out.println("i="+i);
						if (i==2) {
							System.out.println("continue");
							continue;
						}
						if (i==3) {
							System.out.println("break");
							i++;
							break;
						}
						if (i==7) {
							System.out.println("continue outer");
							i++;
							continue outer;
						}
						if (i==8) {
							System.out.println("break outer");
							break outer;
						}
						for (int j = 0; j<5; j++) {
							if (j==3) {
								System.out.println("continue inner");
								continue inner;
							}
							
						}
					}
			}

	}

}

```
![](http://i.imgur.com/H3zVmTN.png)
1.break,中断内部迭代，回到外部迭代。
2.continue,使执行点回到内部迭代的起始处。
3.continue label 同时中断所有迭代，再从外部中断开始。
4.break label 同时中断所有迭代，不再进入中断。