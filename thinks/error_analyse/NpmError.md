---
title: "npm error in nodejs"
date: 2020-05-30T22:36:50+08:00
draft: false
categories: ["nodeJs"]
tags: ["npm"]
---

### Install  
* [英文官网](https://nodejs.org/en/)    
* [中文官网](http://nodejs.cn/download/)  

### NPM Error  
```
   internal/modules/cjs/loader.js:1032
     throw err;
	   ^

   Error: Cannot find module '/usr/bin/node_modules/npm/bin/npm-cli.js'
       at Function.Module._resolveFilename (internal/modules/cjs/loader.js:1029:15)
	    at Function.Module._load (internal/modules/cjs/loader.js:898:27)
	    at Function.executeUserEntryPoint [as runMain] (internal/modules/run_main.js:71:12)
	    at internal/main/run_main_module.js:17:47 {
			  code: 'MODULE_NOT_FOUND',
						  requireStack: []
   }
```  

&emsp;&emsp;原因:因为不是安装在/usr/bin/这个目录下的，引起找不到所要使用的文件。  
&emsp;&emsp;解决:找到npm执行文件，使用编辑器去修改npm中的basedir路径，使用自己的安装的路径，如/media/un/_dde_data/node/lib/node_modules/npm/bin，但这样还是会报上面的错，只不过错误的路径变成了这个路径，通过报的错误，可以定位到npm-cli.js文件的路径，在npm文件中找到NPM_CLI_JS路径，可以发现npm-cli.js中的$basedir/node_modules/npm/bin/npm-cli.js路径，再看报的错误，可以确定把basedir中多了/node_modules/npm/bin的文件层级，因为在NPM_CLI_JS中已经存在这几个目录，所以basedir="/media/un/_dde_data/node/lin"即可。  

### Attachment   
&emsp;&emsp;我使用的是NodeJs 14.3.0 Current Latest Features  
