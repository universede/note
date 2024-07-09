---
title: "Music Player base on  MUI framework"
date: 2020-06-21T18:59:47+08:00
draft: false
categories: ["javascript"]
tags: ["mui"]
---

&emsp;&emsp;这是一个基于mui框架实现的一个网页随机音乐播放,主要功能有播放与暂停,随机切歌,静音三个。
#### 需求建模  
* 原型界面  
  * 设计软件  
    * 应用端  
	  [Axure RP](https://www.axure.com.cn/)   
    * 网页版  
	  [摹客原型](https://www.mockplus.cn/rp)  
* 数据模型  
* 业务模型

#### 框架   
* 应用架构   
描述IT系统功能和技术实现的内容  
* 分类   
  +  C结构  
  Client,最早的一种初始分类单机结构,不涉及联网的客户端,如单机游戏
  + S结构  
  Server,用于网络通信的一种服务结构,使用Socket(套接字)来传输数据,包含TCP和UDP两种协议  
  + C/S结构  
  Client/Server,一种端应用,原来的APP应用,优点:稳定,功能强大;缺点:更新不及时,跨平台弱  
  + B结构  
  + B/S结构  
  Browser/Server,一种页应用,直接在网页中进行操作.  
  + C/S+B/S混合结构  
  以C/S为主,B/S为辅的一种结构,如微信小程序,快应用,现代版QQ  
  + B/S+C/S混合结构   
  以B/S为主,C/S为辅的一种结构,如在线直播,在线电影  
* 开发模型   
主要是MVC,其中包含MVC 1.0和MVC 2.0,其中MVVP是对MVC的扩展 
* 开发框架  
  + weex  
  + quickapp  
  + weixin app  
  + uniapp  
  + mui
#### 跨域与协议  
* 跨域    
定义:网页应用中的一种安全机制,域:作用域,网页应用中的ip/主机名/域名  
跨域方式:设置头部(request:伪造);设置响应许可(运行那些ip/域名来访问,服务器就做出响应);JSON;webservice  
* 协议  
协议头://host:port/contextroot/path  

* 跨域的必要条件  
协议头不同;主机名不同;IP协议不同;域名不同;端口号不同;上下文根不同  

#### 页面布局   
布局原则:做布局只考虑布局,做内容只考虑内容  
布局方式:'H'型 'T'型 '工'型 '框'型 '口'型 '国'型    
设计模式:响应式 自适应 沉浸式   

#### 例子   
* 步骤  
    本次使用面向对象的方式把代码分离，使用mvc框架，在实现时按着mvc的样式创建三个文件夹，用于存放不同的文件。  
  + 页面布局  
    根据页面布局原则，做布局时只考虑布局，做内容时只考虑内容。把布局和页面分开实现后在具体实现操作。  
  + 具体操作  
    1.在model层下，创建一个js文件用于存放属性，如` var musicM ={}; `musicA就是一个对象,里面可以声明一些属性,也可以是一些方法，但为了实现代码的可分离性，这里只放属性，如`version:''`等属性，具体详见下面具体代码。  
	2.在conctroller层下创建一个js文件，用于具体的操作，如`var musicAc={};`  
* 思路  
  1.创建``audio``元素,如document.createElement("audio");  
  2.使用mui.getJSON()方法加载源的资源，通过源里的歌曲url可以拿到播放地址，然后把url地址给audio中的src。  
* css代码:   
```css
* {
   margin: 0;
   padding: 0;
}  
html,body {
  width: 100%;
  height: 100%;
}
.wrap_panel {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-flow: column;
}
.music_panel {
  width:400px;
  height:600px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-flow: column;
}
.music_panel>div {
   width: 80%;
   height: 40px;
   margin-bottom: 20px;
}
.music_name {
   text-align: center;
   line-height: 40px;
   font-size: 1.4rem;
   font-weight: bolder;
   margin-bottom: 0px !important;
   text-shadow: 0px 0px 2px rgb(192, 238, 219);
}
.music_actor {
   text-align: center;
   line-height: 40px;
   font-size: 0.8rem;
}
.music_song {
   width: 260px !important;
   height: 260px !important;
   border-radius: 50%;
   /*0px->垂直 0px->水平 8-20->模糊范围 3-5阴影长度*/
   box-shadow: 0px 0px 8px 0.02rem hsl(26deg 30% 5%);
}
.music_song>img {
   height:100%;
   width: 100%;
   border-radius: 50%;
   box-shadow: 0px 0px 8px 0.04rem 090504; 
}
.musicPlayed {
   animation: panRouted 5s linear 0s infinite;
}
@keyframes panRouted {
   from{
       transform: rotate(0deg);
   }
   to{
       transform: rotate(360deg);
   }
}
.musicPaused {
   animation-play-state: paused;
}
.time_bar {
   height: 2px !important;
   width: 60% !important;
   border-radius: 1px;
   box-shadow: 0px 0px 5px 0.02rem hsl(26deg 30% 5%);
}
.play_bar {
   height: 100px !important;
   display: flex;
   justify-content: space-evenly;
   align-items: center;
}
.play_bar>div {
   height: 80px;
   width: 80px;
   background-color: rgb(192, 238, 219);
   border-radius: 50%;
   box-shadow: 0px 0px 5px 0.02rem hsl(26deg 30% 5%);
   display: flex;
   justify-content: center;
   align-items: center;
}
.play_bar>div>img {
   height:60%;
   width: 60%;
   border-radius: 50%;
}
.play_bar>div:nth-of-type(1) {
   height: 50px !important;
   width: 50px !important;
}
.play_bar>div:nth-of-type(2) {
}
.play_bar>div:nth-of-type(3) {
   height: 50px !important;
   width: 50px !important;
}
.music_currentTime {
   height: 100%;
   background-color: rgb(7, 6, 6);
}
.music_pic, .music_pic_center {
   position: absolute;
   height: 160px;
   width: 160px;
   margin-top: -31px;
   border-radius: 50%;
   box-shadow: 0px 0px 1px rgb(10 6 5) inset;
   background-size: cover;
}
.music_pic_center{
   height: 40px;
   width: 40px;
   background-color: aliceblue;
}
.music_pic_bg {
   /*沉浸式背景*/
   height: 100%;
   width: 100%;
   position:absolute;
   top: 0;
   left: 0;
   z-index: -1;
   background-size: cover;
   filter: blur(12px);  /*失焦*/
}
```

* html代码:   

```html
<div class="wrap_panel">
   <div class="music_panel">
       <div class="music_name">UF-M</div>
       <div class="music_actor">universe</div>
       <div class="music_song">
           <img id="panel" class="musicPlayed musicPaused" src="../image/cycle.jpg">
       </div>
       <div class="time_bar">
           <div class="music_currentTime" style="width: 0%;"></div>
       </div>
       <div class="play_bar">
           <div>
               <img onclick="musicAc.playMuted()" src="../image/voice.png">
           </div>
           <div>
               <img onclick="musicAc.playerMusic()" src="../image/play.png" style="margin-left: 10px;">
           </div>
           <div>
                <img onclick="musicAc.runMusic()" src="../image/next.png">
            </div>
        </div>
    </div>
    <div class="music_pic musicPlayed musicPaused"></div>
    <div class="music_pic_center"></div>
    <div class="music_pic_bg"></div>
</div>

```  
* js代码:  
```javascript
var musicM = {
	version: '1.0',
	top: '音乐',
	urlapi: 'https://api.uomg.com/api/rand.music?sort=热歌榜&format=json',
	mplayer: null,
	musicInfo:{
		pic: '',
		name: '',
		sname: '',
		url: ''
	},
	playStated:false,  //播放状态
	mutedstate:false   //静音状态
}
var musicAc = {
	createPlayer:function() {
		musicM.mplayer = document.createElement("audio");
	},
	playerMusic:function() {
		var pan = mui("#panel")[0];
		var imgPan = mui(".music_pic")[0];
		if(musicM.playStated == false) {
			//暂停时，则播放
			pan.classList.remove("musicPaused");
			imgPan.classList.remove("musicPaused");
			//业务处理
			mui(".play_bar>div>img")[1].src="../image/pause.png";
			mui(".play_bar>div>img")[1].style.marginLeft="0px";
			if(musicM.mplayer != null) {
				musicM.mplayer.play();
			}else {
				musicAc.getMusicInfo("playbtn");
			}
			musicM.playStated = true;
		}else {
			//播放时，则暂停
			pan.classList.add("musicPaused");
			imgPan.classList.add("musicPaused");
			//业务处理
			mui(".play_bar>div>img")[1].src="../image/play.png";
			mui(".play_bar>div>img")[1].style.marginLeft="10px";
			musicAc.pauseMusic();
			musicM.playStated = false;
		}

	},
	pauseMusic:function() {
		if(musicM.mplayer == null) {
			musicAc.createPlayer();
		}
		musicM.mplayer.pause();
	},
	playMuted:function() {
		if(musicM.mplayer == null) {
			return;
		}
		if(musicM.mutedstate == false) {
			//变成静音
			musicM.mplayer.muted = true;
			musicM.mutedstate = true;
			mui(".play_bar>div>img")[0].src = "../image/novoice.png";
			mui.toast('静音状态', {duration:1500, type:"div"});
		}else {
			//取消静音
			musicM.mplayer.muted = false;
			musicM.mutedstate = false;
			mui(".play_bar>div>img")[0].src = "../image/voice.png";
			mui.toast('取消静音', {duration:1500, type:"div"});
		}
	},
	getMusicInfo:function(fromck) {
		mui.getJSON(musicM.urlapi, {}, function(info) {
			musicM.musicInfo.name = info.data.name;
			musicM.musicInfo.pic = info.data.picurl;
			musicM.musicInfo.sname = info.data.artistsname;
			musicM.musicInfo.url = info.data.url;
			if(fromck == "run") {
				musicAc.playerMusic();
			}

			musicAc.setMusicInfo();
			if(musicM.mplayer == null) {
				musicAc.createPlayer();
			}
			musicM.mplayer.src = musicM.musicInfo.url;
			musicM.mplayer.play();
		});
	},
	runMusic:function() {
		if(musicM.mplayer != null) {
			musicAc.playerMusic();   //用于在随机切歌后，唱片和播放按钮能处于播放状态
			musicAc.getMusicInfo("run");
		}else {
			return;
		}
		
	},
	setMusicInfo:function() {
		mui(".music_name")[0].innerHTML = musicM.musicInfo.name;
		mui(".music_actor")[0].innerHTML = musicM.musicInfo.sname;
		//这里使用到了ES6/7的语法,反引号
		mui(".music_pic")[0].style.backgroundImage = `url(${musicM.musicInfo.pic})`;
		mui(".music_pic_bg")[0].style.backgroundImage = `url(${musicM.musicInfo.pic})`;
		//处理上一首数据
		localStorage.setItem("preMusic", JSON.stringify(musicM.musicInfo));
	},
	init:function() {
		setInterval(function(){
			if(musicM.mplayer != null) {
				playTime = musicM.mplayer.currentTime / musicM.mplayer.duration * 100;
				mui(".music_currentTime")[0].style.width = playTime + "%";
				if(musicM.mplayer.ended) {
					musicAc.runMusic();
				}
			} 
		}, 3000);
	}
}
```

#### REFERENCES
[1] https://dev.dcloud.net.cn/mui/ui/  
[2] http://api.uomg.com/  
[3] https://juejin.im/post/5c23993de51d457b8c1f4ee1  
