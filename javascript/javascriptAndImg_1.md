---
title: "Javascript And Image I"
date: 2020-05-10T22:36:52+08:00
draft: false
categories: ["javascript"]
tags: ["javascript"]
---


&emsp;&emsp;今天主要研究的是—javaScript图片库,通过点击一条超连接文本，不用跳转直接在 本页面显示图片。这个主要用到了占位符，通过占位符图片替换成自己想要查 看的图片。
思路：

> 获取超链接文件的路径  
> 获取占位符图片  
> 把超链接的文件放到占位符图片里  

**动态改变图片**

* 标记    
我认为这里的标记在这里是html文件里面所使用的标签。如以下部分代码:
```javascript
  ...
  <a href="your image path" title="your image description"
  onclick="showPic(this); return false;">xxx</a>
  <a href="your image path" title="your image description"
  onclick="showPic(this); return false;">xxx</a>
  ...
  <img id="placeholder" src="your default image path or null" />
  ...
```
&emsp;&emsp;在showPic(this)中的'this’，含义是“这个对象”，在这里指"这个<a>元素节点"。把获取到的节点通过点击事件把参数值传到javaScript中，以便使用。

**javaScript**
```javascript
  <script>
     function showPic(whichpic) {
         var source = whichpic.getAttribute("href");
         var placeholder = document.getElementById("placeholder");
         placeholder.setAttribute("src", source);
     }
  </script>
```

&emsp;&emsp;whichpic代表一个元素节点，接收来自html中this传过来的值，具体是指向某个图片 <a>元素。通过whichpic.getAttribute("href")可以获取到图片的路径。在 setAttribute函数中有两个参数，一个是属性值，一个是属性的值。在这里， placeholder.setAttribute(“src”,source)表示使用setAttribute对placeholder元素 的src属性进行刷新。

&emsp;&emsp;当触发这个showPic函数时，不仅showPic函数被调用，而且被点击链接的默认行为也 会被调用。这就意味着我们在查看图片时会被带到图片查看窗口，并不能满足所期待 的在当前页面就能显示图片。

&emsp;&emsp;在其中，我们使用了事件处理函数，它的作用是在特定事件发生时调用特定的 JavaScript代码。onclick事件就是用户点击某一个特定链接时所触发的一个动作。 如果要在本页面中显示图片，还需在，在一个<a>元素的点击事件中添加一个"return false;“语句，如onclick="showPic(this); return= false"，表示防止用户被带到目标链接窗口，如果为true，则表示用户认为可以被 带到目标窗口去。

&emsp;&emsp;而关于事件函数的使用语句，如下
event = "javaScript statement(s)。
扩展事件函数：
如果想鼠标指针悬停在某个元素上时触发一个动作，可以使用onmouseover事件 处理函数。
如果想鼠标指针离开某个元素时触发一个动作，则使用onmouseout事件处理函数。

* 关于非DOM的解决方案  
在这一节中也可以不使用setAttribute函数也可以改变src属性。  
setAttribute方法是DOM 1的组成部分，它可以设置任意元素节点的任意属性。  
getAttribute方法也是DOM 1的组成部分，它可以获取任意元素节点的值。 例如：改变某个input元素的value属性:  
非DOM的获取方法：element.value = "the new value"  
DOM的获取方法: ``` element.setAttribute(“value”, “the new value”);  
在使用DOM的优势，可移植性好；适用于任何一种标记语言。  

动态改变图片的深入  

**html**
```html
...
<a href="your image path" title="your image description"
onclick="showPic(this); return false;">xxx</a>
<a href="your image path" title="your image description"
onclick="showPic(this); return false;">xxx</a>
...
<img id="placeholder" src="your default image path or null" />
<p id = "description"></p>
...
```
**javaScript**
```javascript
  <script>
     function showPic(whichpic) {
         //改变图片
         var source = whichpic.getAttribute("href");
         var placeholder = document.getElementById("placeholder");
         placeholder.setAttribute("src", source);
         //改变文本
	 var text = whichpic.getAttribute("title");
         var description = document.getElementById("description");
         desctiption.firstChild.nodeValue = text;
     }
  </script>
```
由于在对文本操作比较难以控制，所有我们还要学习以下的几个属性，更精准 把握其中的操作过程。  

* childNodes属性  
&emsp;&emsp;这个属性可以用来获取任何一个元素的所有子元素，它是一个包含这个元素全部子 元素的数组：element.childNodes。  
&emsp;&emsp;现在假设要检索整个文档下body元素的全体子元素。首先，我们需要先使用getEle mentsByTagName来获取body元素。因为每一个文档只有一个body元素，所以它在getElemnts ByTagName(“body”)方法所返回的数组中的第一个元素。即：


var   |	body_el	=  | document.getElementsByTagName(“body”) | 	[0]   |
              
标识符|	变量名     | getElementsByTagName(“body”)方法      | 获取所要的求的元素位置数|

通过body_el.childNodes.length就可以知道body中的所有元素个数

* nodeType属性  
什么是节点？  
-> 文档里几乎每一样东西都是一个节点，甚至连空格和换行符都被解释为节点。  
获取节点的nodeType属性：node.nodeType  
nodeType属性共有12种可取值，实用价值有3种，即  
元素节点的nodeType属性值是1；   
属性节点的nodeType的属性值是2；  
文本节点的nodeType的属性值是3.  

* nodeValue属性  
&emsp;&emsp; 如果想改变一个文本节点的值，需要使用nodeValue属性，它用来得到一个节点的值。 如果要通过nodeValue来获取description对象的值时，这个调用会返回一个null值。由 于元素本身的nodeValue属性是一个空值，而我们真正需要的是元素所包含的文本的值。 而那个值是包含在元素里的文本是另一个节点，它是元素的第一个子节点。因此，所要 得到的值是它的第一个子节点的nodeValue属性值。即：description.childNodes[0].nodeValue 。

* firstChild和lastChild属性  
&emsp;&emsp;这两个属性值分别表示第一个元素和最后一个元素，它是来自于数组元素childNodes[0]的 直观的同义词。
&emsp;&emps;firstChild的语法，即 node.firstChild == node.childNodes[0]，完全等同。 lastChild的语法，即 node.lastChild == node.childNodes[node.childNodes.length - 1]。

#### REFERENCE  

[1] Keith,J.Sambells,J.javaScript DOM编程艺术.北京：人民邮电出版社.2017.08(重印)

