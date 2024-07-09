---
title: "String"
date: 2020-05-10T22:05:13+08:00
draft: false 
categories: ["java"]
tags: ["String"]
---
&emsp;&emsp;从概念上将，Java字符串就是Unicode字符序列。e.g:串"Java\u2122由5个Unicode字符J a v a和TM。Java没有内置的的字符串，而是在标准Java类库中提供了一个预定义类，很自然地叫做String。每一个用引号括起来的字符串就是String类的一个实例。    
&emsp;&emsp;在字符串中，分为不可变字符串(String)和可变字符串(StringBuffer和StringBuilder)。 

#### String  
&emsp;&emsp;String类在JDK API中使用final修饰的，意为不可修改类。以下是String类图。    
![String](https://leidu.github.io/blogs/image/java/String.png "String类图")  
```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    ...
}
```  
* String的创建  
```java
    String str = “She is my mother”;   
    String str2 = “She is my mother”;   
    String str3 = new String(“She is my mother”);
    System.out.println(str == str2);  //true
    System.out.println(str.equals(str2));  //true
    System.out.println(str == str3);  //false
    System.out.println(str.equals(str3));  //true
```   
&emsp;&emsp; 通过分析，虽然str,str2,str3都是指向一个地址，但“str == str3”的值是false，可以得到一个结果，str和
str2这两个对象是在常量池中保存，而str3是通过关键字**new**创建的一个对象，被存放在了堆内存中，而通过equals比较时，str3被重写了，重写过后变成了值比较，如"str == str2"。 
```java
    System.out.println(“She is my mother, and her name” + name);   
```
&emsp;&emsp;通过println()里的语句，‘+’是一个连接符，如果在一条语句里，存在字符串和‘+’ ，那么这条语句就还是字符串；如果是数值(2+3)，则这时‘+’就起算术运算。  
* String的方法  
    String里面有很多的方法使用,如length()、split()、comparaTo()、substring()等，具体详见源码。    
  
&emsp;&emsp;创建成功的字符串对象，其长度是固定的，内容不能被改变和编译。虽然使用“+” 可以达到附加新字符或字符串的目的，但“+”就会产生一个新的String实例，会在内存中创建心得字符串对象，如果多次对该字符串对象进行反复的修改，就会使内存的开销增加，使内存耗尽，最终导致系统运行的崩溃。  

#### StringBuffer与StringBudilder
&emsp;&emsp;StringBuffer和StringBudilder都是可以对其字符串进行追加、增加、删除等的操作。但要注意，StringBuffer允许采用多线程的方式执行添加或删除字符的操作，但效率低，而StringBuilder采用单线程来对字符进行增加和删除，效率高。  
* StringBuffer  
&emsp;&emsp;根据JDK API源码分析，可以得到StringBuffer的继承关系，如下图:  
![StringBuffer](https://leidu.github.io/blogs/image/java/StringBuffer.png "StringBuffer类图")  
&emsp;&emsp;在StringBuffer中的方法都使用了关键字**synchronized**来修饰，那么为什么要使用这个关键字呢？  
**synchronized**关键字是线程中的一个关键字，表示同步锁，为了线程安全而设计的。如果没有这个关键字，而且同时有很多的线程需要执行，这是就会形成并发，而每一个线程都会去分得内存，如果内存不足，就会造成程序的崩溃。如果加了这个关键字，会把所进入的对象进行加锁，如果该进程运行完毕，才把其他的对象加锁来访问资源，如果该进程没运行完，则其他对象则进行等待。  

* StringBuilder  
&emsp;&emsp;在StringBuilder的源码中，因为都是继承于**AbstractStringBuilder**类，实现**Serializable**和**CharSequence**，所以和StringBuffer的具体实现都差不多。有点差别的地方就是StringBuffer使用了同步锁来保证线程的安全，而StringBuilder是不是线程安全的。  
![StringBuilder](https://leidu.github.io/blogs/image/java/StringBuilder.png "StringBuilder类图") 

#### SUMMER  
相同点:1.String、StringBuffer、StringBuilder都是使用final修饰，表示不可继承，不可变。  
        
不同点:1.String没有增加删除修改的方法，而StringBuffer和StringBuilder都提供了这些方法，以此来减少对象过多而过度消耗的内存。  
      2.StringBuffer使用关键字**synchronized**来保护线程，来支持多线程的开发,效率慢，而StringBuilder先非线程安全的，用于单线程开发，效率高。  

#### REFERENCE
[1] 凯 S.霍斯特曼.java核心技术卷I.译(周立新).北京：机械出版社.2018重印   
[2] 明日科技.Java从入门到精通.北京：清华大学出版社.2016.   
[3] https://www.zhihu.com/question/31345592   
[4] https://juejin.im/post/5c7ddcd06fb9a04a06059bea   
[5] https://blog.csdn.net/qq_28632639/article/details/98724482  
