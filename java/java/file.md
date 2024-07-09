---
title: "File"
date: 2020-05-10T22:13:51+08:00
draft: false
categories: ["java"]
tags: ["I/O", "File", "Files", "Path", "Paths"]
---


&emsp;&emsp;在JDK中，File是从1.0开始就有的，而Files和Path是JDK 1.7才出现的。　　　  
**File**

&emsp;&emsp;来自于java.io包中，其中就有一个File类，这个类可以对文件进行读取，可以对其文件 进行创建删除和修改。　　
* 构造函数  
    File(String path); 如果path是实际路径，则表示文件目录；如果path是实际文件名，则就是该对象是文件。  
    File(String path, String name); path表示目录，name表示文件。   
    File(File dir, String name); dir表示对象的路径，name表示文件名。　　　
  

**Files**

&emsp;&emsp;来自于java.nio包中，其中就有一个Files类，这个类可以用来移除或重命名文件，或者 查询拍文件下最后被修改的时间，主要关心文件的内容。　
　　　　　
**Path**

&emsp;&emsp;来自于java.nio包中，其中就有一个Path类，表示一个目录名序列，其后可以跟着一个文 件名，主要关心磁盘上如何存储文件。
Path类实际一个接口类，不能被实例化，在NIO中也是通过流的方式在工作。在Paths中有一个 静态的Paths.get(String first, String...more)方法接受一个或多个字符串，并将他们默认的文件系统的路径分隔符连接起 来。然后解析连接起来的结果。如果其表示的不是给定文件系统中的合法路径，就会抛出 InvaildPathException异常。而连接起来的对象就是Path。如:Path pa = Paths.get("/temp”, “my.config”);

**Paths方法**  
    根据jdk1.8的源码来看，有两个方法，如下：

* 方法  
static Path get(String first, String… more  
static Path get(URI uri)

**Path方法**

 * Path resolve(Path other)   
   Path resolve(String other)   
   如果other是绝对路径，则返回oher；否则返回通过连接this和other连接得到的路径   
 * Path resolveSibling(Path other)   
   Path resolveSibling(String other)   
   如果other是绝对路径，则返回other；否则返回通过连接this的父路径和other获得的路径    
 * Path relativize(Path other)   
   返回用this进行解析，相对于other的相对路径   
 * Path normalize()     
   移除诸如.和..等冗余的路径元素    
 * Path toAbsolutePath()     
   返回与该路径等价的绝对路径   
 * Path getParent()    
   返回父路径，如果没有父路径，放回null　　　
 * Path getFileName()   
   放回该路径党的最后一个部件，如果没有任何部件，返回null　　　
 * Path getRoot()   
   返回该路径的跟部件，如果没有，则返回null　　　
 * toFile()   
   从该路径中创建一个文件  

#### IO和NIO

* 区别  
    1.IO流是面向字节流和字符流进行操作的，而NIO流是对缓冲区(Buffers)和管道(Channals)进 行操作的，数据总是从管道读取到缓冲区的，从缓冲区写到管道的。  
    2.NIO相比IO，NIO是异步(Asynchronous)的，也就是说可以当前线程在做这件事，而不需要 等待当前线程做完后再做其他的事情，它可以同使做去其它的事情。  
    3.在NIO中引入了选择器(Selector)的概念，主要用于监听多个管道的事件。  
    4.IO是阻塞的，NIO是非阻塞的。  

#### REFERENCE

[1] Cay S.Horstmann.java 核心技术　卷II(第10版).北京：机械工程出版社.2018.4(重印)  
[2] Eckel,B.java编程思想.北京：机械工程出版社.2002.9  
[3] http://c.biancheng.net/view/1133.html  
[4] https://blog.csdn.net/u010889616/article/details/52694061  
[5] https://www.jianshu.com/p/a6b7410a6fbe  
[6] https://zhuanlan.zhihu.com/p/59413274  
[7] https://juejin.im/post/5af79bcc51882542ad771546  

