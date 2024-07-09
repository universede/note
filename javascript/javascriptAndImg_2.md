---
title: "Javascript And Image II"
date: 2020-05-10T22:53:33+08:00
draft: false
categories: ["javascript"]
tags: ["javascript"]
---

&emsp;&emsp;根据上一次的“基于javaScript"的改变图片，有一定的缺陷，如果浏览器不支持 javaScript会怎么样。而为了更高效的执行代码，现在都采用一个模式——代码分 离，这种模式使代码更高效的执行，也更好的让人阅读。接下来，就是讲解HTML 和javaScript的分离。

**html**
```html
  ...
  <div id="imgs">
     <a href="your image path" title="your description" />
     <a href="your image path" title="your description" />
     ...
  <div>
  <img id="placeholder" src="your image path" />
  <p id="description">description</p>
  ...
```
javaScript 其中的判断语句用于判断浏览器是否支持javaScript。
```javascript
function grally() {
    if(!document.getElementsByTagName) return false;
    if(!document.getElementById) return false;
    if(!document.getElementById("imgs")) return false;
    var gallery = document.getElementById("imgs");
    var links = gallery.getElementsByTagName("a");
    for(var i = 0; i < links.length; i++) {
        links[i].onclick = function() {
           return showPic(this) ? false : true;
        }
    }
}
function showPic(whichpic) {
    if(!document.getElementById("placeholder")) return false;
    var source = whichpic.getAttribute("href");
    var placeholder = document.getElementById("placeholder");
    if(placeholder.nodeName != "IMG") return false;
    placeholder.setAttribute("src", source);
    
    if(document.getElementById("description")) {
    	var text = whichpic.getAttribute("title") ? whichpic.getAttribute("title") : "";
    	var description = document.getElementById("description");
    	if(description.firstChild.nodeType == 3) {
    	    description.firstChild.nodeValue = text;
    	}
    }
    return true;
}
//window.onload = grally;
addLoadEvent(grally);
function addLoadEvent(func) {
    var oldonload = window.onload;
    if(typeof window.onload != 'function'){
        window.onload = func;
    }else {
        window.onload = function() {
            oldonload();
 	    func();
	}
    }
}
```
#### 知识点布局

添加事件处理函数 再通过HTML和javaScript的分离，在写javaScript的时候，我们需要注意这个函数所要完成的共作：  
> 检查当前浏览器是否理解getElementsByTagName  
> 检查当前浏览器是否理解getElementById  
> 检查当前网页是否存在一个id为imgs的元素  
> 遍历imags元素中的所有链接，即<a>  
> 设置onclick时间，让它在有关链接被点击时完成以下操作：  
>> 把这个链接作为参数传递给showPic函数
>> 取消链接被点击时的默认行为(打开图片显示窗口)，不让浏览器打开这个链接

* a. 检查点  
&emsp;&emsp;检查点，是通过检查浏览器是否支持getElemetsByTagName等的DOM方法的执行。即：`if(!document.getElementsByTagName) return false;`就是先检查浏览器是否支持，虽说现在的浏览器都支持，但不能的浏览器的运行机制有差异，通 过检查，更好的适应在代码、数据的变动而造成的错误，起到预防性的作用。  
&emsp;&emsp;把HTML的文档的内容和JavaScript代码所实现的行为分离要遵循一条原则，如果想把JavaScript 给某个网页添加一些行为，就不应该让JavaScript代码对这个网易的结构有任何的依赖。
* b. 变量的使用  
&emsp;&emsp;如果在一个一句代码中，调用的过程导致代码太长，可以定义一个变量，通过逐层调用的方式美化代码让代码让人阅读。如`document.getElementById(“imgs”).getElementsByTagName(“a”);`可以简写成:
```javascript 
  var imgs = document.getElementById(“imgs”);  
  var links = imgs.getElementsByTagName(“a”);
```     
* c. 遍历  
&emsp;&emsp;在以上例子中，通过获取id=imgs把所有的getAttribute(“a”)属性给找到，并放到数组中，当执行所要 的时候先指向下标的数组。即：
` var links = imgs.getElementsByTagName(“a”); //获取a元素
  var linksLength = links.length; //获取a元素的长度
`  
* d. 改变行为  
&emsp;&emsp;通过点击链接就执行一次点击事件，值得注意的是在这里使用了一个匿名函数，这是代码执行时创建的 一种函数方式。在links中我们每一次点击时，所要执行的是对数组进行操作，其实在这里把links说成数 组，还不如说它是一个节点列表，它是由DOM节点构成的集合，这个集合里的每一个节点都有自己的属性和 方法。最后，还要禁用有关链接的默认操作，如果showPic函数执行成功，就不让浏览器执行某个链接被点 击时的默认操作。
```javascript
    for(var i = 0; i < linksLength; i++) {
        links[i].onclick = function() { 
             //your code 
        } 
    } 
```
* e. 完成javaScript函数  
    这里不做详细书写。

#### 共享onload事件  
&emsp;&emsp;一种直接使用window.onload=funRef方式，而这种方式只适用于需要绑定的函数不是很多 的场合，而如果有多个要执行的函数，可以先创建一个匿名函数来容纳这些所要执行的函数，然 后把那个匿名函数绑定到onclick事件上，如下所示:
```javascript
   window.onload = function() {
      fistFunction();
      secondFunction();
   }
```
&emsp;&emsp;如在本例子中，则可以使用window.onload=grally这种方式;然而，还有一种弹性更加的解决方案， 则使用addLoadEvent函数。代码如下：
```javascript
  function addLoadEvent(func) {
      var oldonload = window.onload;
      if(typeof window.onload != 'function') {
          window.onload = func;
      }else {
         window.onload = function() {
	     oldonload();
	     func();
	 }
      }
  }
```
&emsp;&emsp;这将把那些在页面加载完毕时执行的函数创建为一个队列。如果想把刚才要加载的函数执行则直接 使用addLoadEvent(garry)即可。

&emsp;&emsp;键盘访问方式 曾听同学说过，”学会运用键盘会比鼠标更快“，而我也对计算机的更深入的了解，过去的计算机没有 图形界面和鼠标，全是通过键盘的输入和命令行操作，现在自己也学了一点指令，通过使用点击的方式的 确没有命令来的方便。以下就是通过键盘的方式实现访问。
&emsp;&emsp;在JavaScript中有一个叫onkeypress的处理事件。即：
```javascript
       links[i].onclick = function() {
           return showPic(this) ? false : true;
       }
       link[i].onkeypress = function() {
           return showPic(this) ? false : true;
       }
```

或   
 
```javascript
       links[i].onclick = function() {
           return showPic(this) ? false : true;
       }
       links[i].onkeypress = links[i].onclick;
```
&emsp;&emsp;但要值得注意的是，这个onkeypress事件，只要触动键盘上的任意键都会被执行这个函数。而且这个 事件并不是通过tab键移到某个链接就会如自己想的要有执行，它还是会依赖onclick事件来通过点击执行。

#### REFERENCE

[1] Keith,J.Sambells,J.JavaScript DOM编程艺术.北京：人民邮电出版社.2017.




