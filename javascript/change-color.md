---
title: "Change Color"
date: 2020-05-10T22:21:59+08:00
draft: false
categories: ["javascript"]
tags: ["javascript"]
---

&emsp;&emsp;在代码中主要用到了javaScript中的onchange事件。onchange事件可以用于input text、textarea、select option等HTML Form元素上，当元素内容改变时就触发这 个事件来执行你所写的javaScript程序。  
* 变背景

   **html**
```javascript
     <select id="changeBackground" onchange="changeBg()">
       <option value="blue">blue</option>
       <option value="pink">pink</option>
       <option value="gray">gray</option>
     </select>
```
   **js**
```javascript
     <script>
       function changeBg(color) {
          var getSelectValue = document.getElementById("changeBackground").value;
          document.bgColor = getSelectValue;
       }
     </script>
```
* 变字体颜色

    **html**
```javascript
     <select id="changeFontColor" onchange="changeFC(value)" >
       <option value=1>selete, please</option>
       <option value="blue">blue</option>
       <option value="pink">pink</option>
       <option value="gray">gray</option>
     </select>
     <div id="text">She is my mother!</div>
```
  **js**  
    第一种方式，通过直接使用onchange事件来实现
```javascript
     <script>
       function chageFC(color) {
          document.getElementById("text").style.color = color; 
       }
     </script>
```

&emsp;&emsp;第二种方式，可以不用在select标签中添加onchange事件，使用window.onload= funcRef;当window load事件触发时，funcRed()方法会被调用。
```javascript
    <script>
       window.onload=function() {
           var colors = document.getElementById("changeFontColor");
           var content = document.getElementById("text");
           colors.onchange=setColor;
           function setColor() {
                var optionValue = colors.options[colors.selectedIndex].value;
                if(optionValue != 1) {
                      content.style.color = optionValue;
                }
            }
       } 
    </script>
```
注意有两点：  
> 使用第一种方式，html中的onchange="changeFC(value)中的value是 对应option中的value属性的，不可更改为其他的变量名；  
> 改变字体颜色中，所 指定的唯一标识符必须是id，如在html中<div class="text">…</div>, js中…document.getElementsByName(“text”). style.colot = color…就会出 现一个Uncaught TypeError:Cannot set property ‘color’ of undefined的错误

#### REFERENCE  

[1] https://www.wibibi.com/info.php?tid=208  
[2] http://www.softwhy.com/article-8054-1.html  
[3] https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalEventHandlers/onload

