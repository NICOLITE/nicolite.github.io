---
title: No enclosing instance of type xxx is accessible
date: 2016-07-17 07:21:47
categories:
- Java
tags: 
---
```java
public interface Edible {

	public abstract String howToEat();
}
```
TestEdible.java  
```java
public  class TestEdible {
	public static void main(String[] args) { 
		Object[] objects = {new Tiger(), new Chicken(), new Apple()};
		for (int i = 0; i &lt; objects.length; i++) {
			if(objects[i] instanceof Edible)
			System.out.println(((Edible)objects[i]).howToEat());
		}
	}
	
	class Animal { 
		
	}
	
	class Chicken extends Animal implements Edible {

		@Override
		public String howToEat() {
			// TODO Auto-generated method stub
			return "Chicken: Fry it";
		}
		
	}
	
   class Tiger extends Animal {

	}
	
	abstract class Fruit implements Edible {
		
	}
	
	class Apple extends Fruit {

		@Override
		public String howToEat() {
			// TODO Auto-generated method stub
			return "Apple: Make apple cider";
		}
		
	}
	
	class Orangle extends Fruit {

		@Override
		public String howToEat() {
			// TODO Auto-generated method stub
			return "Orangle: Make orangle juice";
		}
		
	}
}
```
运行上面所示的代码将会出现如下错误：  
No enclosing instance of type xxx is accessible. Must qualify the allocation with an enclosing instance of type xxx (e.g. x.new A() where x is an instance of TestEdible).  

出现这样的错误的原因是，使用了静态方法调用动态类实例。所以我们需要将类改为静态的  

TestEdible.java  
```java
public  class TestEdible {

	static TestEdible td = new TestEdible() ; //这里
	public static void main(String[] args) { 
		Object[] objects = {td.new Tiger(), td.new Chicken(), td.new Apple()};  //这里
		for (int i = 0; i &lt; objects.length; i++) {
			if(objects[i] instanceof Edible)
			System.out.println(((Edible)objects[i]).howToEat());
		}
	}
	
	class Animal { 
		
	}
	
	class Chicken extends Animal implements Edible {

		@Override
		public String howToEat() {
			// TODO Auto-generated method stub
			return "Chicken: Fry it";
		}
		
	}
	
   class Tiger extends Animal {

	}
	
	abstract class Fruit implements Edible {
		
	}
	
	class Apple extends Fruit {

		@Override
		public String howToEat() {
			// TODO Auto-generated method stub
			return "Apple: Make apple cider";
		}
		
	}
	
	class Orangle extends Fruit {

		@Override
		public String howToEat() {
			// TODO Auto-generated method stub
			return "Orangle: Make orangle juice";
		}
		
	}
}
```