---
title: "Git"
date: 2020-07-06T18:40:52+08:00
draft: false 
tags: ["git"]
categories: ["git"]
---

&emsp;&emsp;由于在git容器中删除了一个文件，在做提交时始终不能把内容提交到github容器中,以下是错误:  
```
位于分支master
您的分支与上游分支 'origin/master' 一致。
尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
    （使用 "git checkout -- <文件>..." 丢弃工作区的改动）
	  （提交或丢弃子模组中未跟踪或修改的内容）
	  
		修改：     themes/cupper-hugo-theme (修改的内容)
	
修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
``` 
原因:修改的地方并未进入到暂缓去，这里是因为删除了一个文件。  

解决：  
1.git diff  
2.git rm --cached themes/cupper-hugo-theme   
3.git commit -m "日志内容"   
4.重新git add .提交  

#### REFERENCE  
[1] https://blog.csdn.net/ningyanggege/article/details/98878660  
