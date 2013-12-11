---
layout: post
title: Java getClass()方法和类的继承
keywords: Java getClass 继承
description: 傲游浏览器浏览人人网主页超级拖放功能失效
categories: [编程]
tags: [编程]
group: archive
icon: globe
---
{% include codepiano/setup %}

前几天创建了一个Hibernate DAO的泛型 DAO 类和接口，其中使用到了`getClass()`方法。好嘛！我用得不明不白的，今天被小伙伴一问，瞬间就尴尬了，上网去科普了下。至于`getClass()`方法是用来做什么的，也许我也说不清楚，自己去看Java API吧，大概就是获取当前类的Class类型。主要卡在类继承时构造函数初始化上面。

代码：
    
	```java
	public class Parent {
		public Parent() {
			System.out.println(getClass().getName());
		}
	}
	public class Child extends Parent {
		public static void main(String[] args) {
			new Child();
		}	
	}
	```

猜猜看会输出什么结果？

输出：`Child`

我想不通为什么会是输出Child呢？明明是在Parent中调用的`getClass().getName()`方法嘛，应该输出`Parent`撒，主要是没搞清继承初始化的问题，我的想法：在构造Child对象的时候会使用Parent类的构造函数来构造Child类中从Parent继承的属性、方法等。所以其实当前类还是Child而不是Parent。其实我说的都是废话，因为我明明是new的Child类，当然应该是输出Child了。哈哈！
