[TOC]
[标题](#1)
[段落](#2)
[换行](#3)
[强调](#4)
[引用](#5)
[列表](#6)
[代码](#7)
[分隔线](#8)
[链接](#9)
[图片](#10)
[转义字符](#11)
[内嵌HTML标签](#12)
[表格](#13)
[围栏代码](#14)
[脚注](#15)
[标题编号](#16)
[定义列表](#17)
[删除线](#18)
[任务列表](#19)
[使用Emoji表情](#20)
[自动网址链接](#21)
[颜色](#22)
# markdown

* <a id=1>标题</a>
以#开头

* <a id=2>段落</a>
不要使用空格或制表符缩进

* <a id=3>换行</a>
在行尾添加“结尾空格”或 HTML 的 "\<br>" 标签来实现换行

* <a id=4>强调</a>
粗体：在单词或短语的前后各添加两个星号或下划线，不要有空格
斜体：在单词或短语前后添加一个星号或下划线，不要有空格
混合使用：在单词或短语前后添加三个星号或下划线，不要有空格

* <a id=5>引用</a>
单个块：创建块引用，在段落前添加一个 > 符号，例如
> Dorothy followed her through many of the beautiful rooms in her castle.  

多个快：块引用可以包含多个段落。为段落之间的空白行添加一个 > 符号。例如：
> Dorothy followed her through many of 
>
>the beautiful rooms in her castle.

嵌套块：块引用可以嵌套。在要嵌套的段落前添加一个 >> 符号。
带有其他元素的块引用：如可以在块元素中使用加粗等元素，但并不是所有的都可以

* <a id=6>列表</a>
有序：数字后面跟一个英文句号
无序：-、*、+
混合：有序中嵌套无序或无序中嵌套有序
使用其他元素：在列表里面使用其他元素

* <a id=7>代码</a>
使用反引号包含内容，例如
```
   hello world
```
或
hello ``world``

* <a id=8>分隔线</a>
单独一行上使用三个或多个星号 (***)、破折号 (---) 或下划线 (___) ，并且不能包含其他内容。

* <a id=9>链接</a>
语法：\[超链接显示名](超链接地址 "超链接title")
链接增加标题：它放在圆括号中链接地址后面，跟链接地址之间以空格分隔。
可点击的链接：使用尖括号，例如：
<www.baidu.com>

* <a id=10>图片</a>
语法：\![图片alt]\(图片链接 "图片title")
链接图片：图像的Markdown 括在方括号中，然后将链接添加在圆括号中，例如：
\[\![图片alt]\(图片链接 "图片title")](www.baidu.com)
* <a id=11>转义</a>
字符前面添加反斜杠字符
有两个字符需要特殊处理： < 和 &，使用使用实体的形式，像是 \&lt; 和 \&amp;。

* <a id=12>内嵌HTML标签</a>
可是使用HTML里面的标签

* <a id=13>表格</a>
使用三个或多个连字符（---）创建每列的标题，并使用管道（|）分隔每列
左对齐： \:---
居中： \:----:
右对齐： \---:

* <a id=14>围栏代码块</a>
使用三个反引号或三个波浪号
语法高亮，在受防护的代码块之前的反引号旁边指定一种语言

* <a id=15>脚注</a>
在方括号（\[^1]）内添加插入符号和标识符，标识符可以是数字或单词，但不能包含空格或制表符
在括号内使用另一个插入符号和数字添加脚注，并用冒号和文本，例如：
hello world[^1]    
[^1]: The world of trust

* <a id=16>标题编号</a>
在与标题相同的行上用大括号括起该自定义ID
通过创建带有数字符号（#）和自定义标题ID的[标准链接]((/basic-syntax/links.html)，可以链接到文件中具有自定义ID的标题。

* <a id=17>定义列表</a>
要创建定义列表，请在第一行上键入术语。在下一行，键入一个冒号，后跟一个空格和定义。

* <a id=18>删除线</a>
请~~在单词前后使用两个波浪号

* <a id=19>任务列表</a>
任务列表使您可以创建带有复选框的项目列表，在支持任务列表的Markdown应用程序中，复选框将显示在内容旁边。要创建任务列表，请在任务列表项之前添加破折号（-）和方括号，并[ ]在其前面加上空格。要选择一个复选框，请x在方括号（[x]）之间添加in ，例如：
- [ ] hello

* <a id=20>使用Emoji表情</a>
冒号开头和结尾，并包含表情符号的名称。

* <a id=21>自动网址链接</a></a>
不希望自动链接URL，则可以通过将URL表示为带反引号的代码来删除该链接。

* <a id=22>颜色</a>
<font color=AliceBlue>	<font color=AliceBlue>Test</font>	Test	AliceBlue	#F0F8FF
<font color=AntiqueWhite>	<font color=AntiqueWhite>Test</font>	Test	AntiqueWhite	#FAEBD7
<font color=Aqua>	<font color=Aqua>Test</font>	Test	Aqua	#00FFFF
<font color=Aquamarine>	<font color=Aquamarine>Test</font>	Test	Aquamarine	#7FFFD4
<font color=Azure>	<font color=Azure>Test</font>	Test	Azure	#F0FFFF
<font color=Beige>	<font color=Beige>Test</font>	Test	Beige	#F5F5DC
<font color=Bisque>	<font color=Bisque>Test</font>	Test	Bisque	#FFE4C4
<font color=Black>	<font color=Black>Test</font>	Test	Black	#000000
<font color=BlanchedAlmond>	<font color=BlanchedAlmond>Test</font>	Test	BlanchedAlmond	#FFEBCD
<font color=Blue>	<font color=Blue>Test</font>	Test	Blue	#0000FF
<font color=BlueViolet>	<font color=BlueViolet>Test</font>	Test	BlueViolet	#8A2BE2
<font color=Brown>	<font color=Brown>Test</font>	Test	Brown	#A52A2A
<font color=BurlyWood>	<font color=BurlyWood>Test</font>	Test	BurlyWood	#DEB887
<font color=CadetBlue>	<font color=CadetBlue>Test</font>	Test	CadetBlue	#5F9EA0
<font color=Chartreuse>	<font color=Chartreuse>Test</font>	Test	Chartreuse	#7FFF00
<font color=Chocolate>	<font color=Chocolate>Test</font>	Test	Chocolate	#D2691E
<font color=Coral>	<font color=Coral>Test</font>	Test	Coral	#FF7F50
<font color=CornflowerBlue>	<font color=CornflowerBlue>Test</font>	Test	CornflowerBlue	#6495ED
<font color=Cornsilk>	<font color=Cornsilk>Test</font>	Test	Cornsilk	#FFF8DC
<font color=Crimson>	<font color=Crimson>Test</font>	Test	Crimson	#DC143C
<font color=Cyan>	<font color=Cyan>Test</font>	Test	Cyan	#00FFFF
<font color=DarkBlue>	<font color=DarkBlue>Test</font>	Test	DarkBlue	#00008B
<font color=DarkCyan>	<font color=DarkCyan>Test</font>	Test	DarkCyan	#008B8B
<font color=DarkGoldenRod>	<font color=DarkGoldenRod>Test</font>	Test	DarkGoldenRod	#B8860B
<font color=DarkGray>	<font color=DarkGray>Test</font>	Test	DarkGray	#A9A9A9
<font color=DarkGreen>	<font color=DarkGreen>Test</font>	Test	DarkGreen	#006400
<font color=DarkKhaki>	<font color=DarkKhaki>Test</font>	Test	DarkKhaki	#BDB76B
<font color=DarkMagenta>	<font color=DarkMagenta>Test</font>	Test	DarkMagenta	#8B008B
<font color=DarkOliveGreen>	<font color=DarkOliveGreen>Test</font>	Test	DarkOliveGreen	#556B2F
<font color=Darkorange>	<font color=Darkorange>Test</font>	Test	Darkorange	#FF8C00
<font color=DarkOrchid>	<font color=DarkOrchid>Test</font>	Test	DarkOrchid	#9932CC
<font color=DarkRed>	<font color=DarkRed>Test</font>	Test	DarkRed	#8B0000
<font color=DarkSalmon>	<font color=DarkSalmon>Test</font>	Test	DarkSalmon	#E9967A
<font color=DarkSeaGreen>	<font color=DarkSeaGreen>Test</font>	Test	DarkSeaGreen	#8FBC8F
<font color=DarkSlateBlue>	<font color=DarkSlateBlue>Test</font>	Test	DarkSlateBlue	#483D8B
<font color=DarkSlateGray>	<font color=DarkSlateGray>Test</font>	Test	DarkSlateGray	#2F4F4F
<font color=DarkTurquoise>	<font color=DarkTurquoise>Test</font>	Test	DarkTurquoise	#00CED1
<font color=DarkViolet>	<font color=DarkViolet>Test</font>	Test	DarkViolet	#9400D3
<font color=DeepPink>	<font color=DeepPink>Test</font>	Test	DeepPink	#FF1493
<font color=DeepSkyBlue>	<font color=DeepSkyBlue>Test</font>	Test	DeepSkyBlue	#00BFFF
<font color=DimGray>	<font color=DimGray>Test</font>	Test	DimGray	#696969
<font color=DodgerBlue>	<font color=DodgerBlue>Test</font>	Test	DodgerBlue	#1E90FF
<font color=Feldspar>	<font color=Feldspar>Test</font>	Test	Feldspar	#D19275
<font color=FireBrick>	<font color=FireBrick>Test</font>	Test	FireBrick	#B22222
<font color=FloralWhite>	<font color=FloralWhite>Test</font>	Test	FloralWhite	#FFFAF0
<font color=ForestGreen>	<font color=ForestGreen>Test</font>	Test	ForestGreen	#228B22
<font color=Fuchsia>	<font color=Fuchsia>Test</font>	Test	Fuchsia	#FF00FF
<font color=Gainsboro>	<font color=Gainsboro>Test</font>	Test	Gainsboro	#DCDCDC
<font color=GhostWhite>	<font color=GhostWhite>Test</font>	Test	GhostWhite	#F8F8FF
<font color=Gold>	<font color=Gold>Test</font>	Test	Gold	#FFD700
<font color=GoldenRod>	<font color=GoldenRod>Test</font>	Test	GoldenRod	#DAA520
<font color=Gray>	<font color=Gray>Test</font>	Test	Gray	#808080
<font color=Green>	<font color=Green>Test</font>	Test	Green	#008000
<font color=GreenYellow>	<font color=GreenYellow>Test</font>	Test	GreenYellow	#ADFF2F
<font color=HoneyDew>	<font color=HoneyDew>Test</font>	Test	HoneyDew	#F0FFF0
<font color=HotPink>	<font color=HotPink>Test</font>	Test	HotPink	#FF69B4
<font color=IndianRed>	<font color=IndianRed>Test</font>	Test	IndianRed	#CD5C5C
<font color=Indigo>	<font color=Indigo>Test</font>	Test	Indigo	#4B0082
<font color=Ivory>	<font color=Ivory>Test</font>	Test	Ivory	#FFFFF0
<font color=Khaki>	<font color=Khaki>Test</font>	Test	Khaki	#F0E68C
<font color=Lavender>	<font color=Lavender>Test</font>	Test	Lavender	#E6E6FA
<font color=LavenderBlush>	<font color=LavenderBlush>Test</font>	Test	LavenderBlush	#FFF0F5
<font color=LawnGreen>	<font color=LawnGreen>Test</font>	Test	LawnGreen	#7CFC00
<font color=LemonChiffon>	<font color=LemonChiffon>Test</font>	Test	LemonChiffon	#FFFACD
<font color=LightBlue>	<font color=LightBlue>Test</font>	Test	LightBlue	#ADD8E6
<font color=LightCoral>	<font color=LightCoral>Test</font>	Test	LightCoral	#F08080
<font color=LightCyan>	<font color=LightCyan>Test</font>	Test	LightCyan	#E0FFFF
<font color=LightGoldenRodYellow>	<font color=LightGoldenRodYellow>Test</font>	Test	LightGoldenRodYellow	#FAFAD2
<font color=LightGrey>	<font color=LightGrey>Test</font>	Test	LightGrey	#D3D3D3
<font color=LightGrey>	<font color=LightGrey>Test</font>	Test	LightGreen	#90EE90
<font color=LightPink>	<font color=LightPink>Test</font>	Test	LightPink	#FFB6C1
<font color=LightSalmon>	<font color=LightSalmon>Test</font>	Test	LightSalmon	#FFA07A
<font color=LightSeaGreen>	<font color=LightSeaGreen>Test</font>	Test	LightSeaGreen	#20B2AA
<font color=LightSkyBlue>	<font color=LightSkyBlue>Test</font>	Test	LightSkyBlue	#87CEFA
<font color=LightSlateBlue>	<font color=LightSlateBlue>Test</font>	Test	LightSlateBlue	#8470FF
<font color=LightSlateGray>	<font color=LightSlateGray>Test</font>	Test	LightSlateGray	#778899
<font color=LightSteelBlue>	<font color=LightSteelBlue>Test</font>	Test	LightSteelBlue	#B0C4DE
<font color=LightYellow>	<font color=LightYellow>Test</font>	Test	LightYellow	#FFFFE0
<font color=Lime>	<font color=Lime>Test</font>	Test	Lime	#00FF00
<font color=LimeGreen>	<font color=LimeGreen>Test</font>	Test	LimeGreen	#32CD32
<font color=Linen>	<font color=Linen>Test</font>	Test	Linen	#FAF0E6
<font color=Magenta>	<font color=Magenta>Test</font>	Test	Magenta	#FF00FF
<font color=Maroon>	<font color=Maroon>Test</font>	Test	Maroon	#800000
<font color=MediumAquaMarine>	<font color=MediumAquaMarine>Test</font>	Test	MediumAquaMarine	#66CDAA
<font color=MediumBlue>	<font color=MediumBlue>Test</font>	Test	MediumBlue	#0000CD
<font color=MediumOrchid>	<font color=MediumOrchid>Test</font>	Test	MediumOrchid	#BA55D3
<font color=MediumPurple>	<font color=MediumPurple>Test</font>	Test	MediumPurple	#9370D8
<font color=MediumSeaGreen>	<font color=MediumSeaGreen>Test</font>	Test	MediumSeaGreen	#3CB371
<font color=MediumSlateBlue>	<font color=MediumSlateBlue>Test</font>	Test	MediumSlateBlue	#7B68EE
<font color=MediumSpringGreen>	<font color=MediumSpringGreen>Test</font>	Test	MediumSpringGreen	#00FA9A
<font color=MediumTurquoise>	<font color=MediumTurquoise>Test</font>	Test	MediumTurquoise	#48D1CC
<font color=MediumVioletRed>	<font color=MediumVioletRed>Test</font>	Test	MediumVioletRed	#C71585
<font color=MidnightBlue>	<font color=MidnightBlue>Test</font>	Test	MidnightBlue	#191970
<font color=MintCream>	<font color=MintCream>Test</font>	Test	MintCream	#F5FFFA
<font color=MistyRose>	<font color=MistyRose>Test</font>	Test	MistyRose	#FFE4E1
<font color=Moccasin>	<font color=Moccasin>Test</font>	Test	Moccasin	#FFE4B5
<font color=NavajoWhite>	<font color=NavajoWhite>Test</font>	Test	NavajoWhite	#FFDEAD
<font color=Navy>	<font color=Navy>Test</font>	Test	Navy	#000080
<font color=OldLace>	<font color=OldLace>Test</font>	Test	OldLace	#FDF5E6
<font color=Olive>	<font color=Olive>Test</font>	Test	Olive	#808000
<font color=OliveDrab>	<font color=OliveDrab>Test</font>	Test	OliveDrab	#6B8E23
<font color=Orange>	<font color=Orange>Test</font>	Test	Orange	#FFA500
<font color=OrangeRed>	<font color=OrangeRed>Test</font>	Test	OrangeRed	#FF4500
<font color=Orchid>	<font color=Orchid>Test</font>	Test	Orchid	#DA70D6
<font color=PaleGoldenRod>	<font color=PaleGoldenRod>Test</font>	Test	PaleGoldenRod	#EEE8AA
<font color=PaleGreen>	<font color=PaleGreen>Test</font>	Test	PaleGreen	#98FB98
<font color=PaleTurquoise>	<font color=PaleTurquoise>Test</font>	Test	PaleTurquoise	#AFEEEE
<font color=PaleVioletRed>	<font color=PaleVioletRed>Test</font>	Test	PaleVioletRed	#D87093
<font color=PapayaWhip>	<font color=PapayaWhip>Test</font>	Test	PapayaWhip	#FFEFD5
<font color=PeachPuff>	<font color=PeachPuff>Test</font>	Test	PeachPuff	#FFDAB9
<font color=Peru>	<font color=Peru>Test</font>	Test	Peru	#CD853F
<font color=Pink>	<font color=Pink>Test</font>	Test	Pink	#FFC0CB
<font color=Plum>	<font color=Plum>Test</font>	Test	Plum	#DDA0DD
<font color=PowderBlue>	<font color=PowderBlue>Test</font>	Test	PowderBlue	#B0E0E6
<font color=Purple>	<font color=Purple>Test</font>	Test	Purple	#800080
<font color=Red>	<font color=Red>Test</font>	Test	Red	#FF0000
<font color=RosyBrown>	<font color=RosyBrown>Test</font>	Test	RosyBrown	#BC8F8F
<font color=RoyalBlue>	<font color=RoyalBlue>Test</font>	Test	RoyalBlue	#4169E1
<font color=SaddleBrown>	<font color=SaddleBrown>Test</font>	Test	SaddleBrown	#8B4513
<font color=Salmon>	<font color=Salmon>Test</font>	Test	Salmon	#FA8072
<font color=SandyBrown>	<font color=SandyBrown>Test</font>	Test	SandyBrown	#F4A460
<font color=SeaGreen>	<font color=SeaGreen>Test</font>	Test	SeaGreen	#2E8B57
<font color=SeaShell>	<font color=SeaShell>Test</font>	Test	SeaShell	#FFF5EE
<font color=Sienna>	<font color=Sienna>Test</font>	Test	Sienna	#A0522D
<font color=Silver>	<font color=Silver>Test</font>	Test	Silver	#C0C0C0
<font color=SkyBlue>	<font color=SkyBlue>Test</font>	Test	SkyBlue	#87CEEB
<font color=SlateBlue>	<font color=SlateBlue>Test</font>	Test	SlateBlue	#6A5ACD
<font color=SlateGray>	<font color=SlateGray>Test</font>	Test	SlateGray	#708090
<font color=Snow>	<font color=Snow>Test</font>	Test	Snow	#FFFAFA
<font color=SpringGreen>	<font color=SpringGreen>Test</font>	Test	SpringGreen	#00FF7F
<font color=SteelBlue>	<font color=SteelBlue>Test</font>	Test	SteelBlue	#4682B4
<font color=Tan>	<font color=Tan>Test</font>	Test	Tan	#D2B48C
<font color=Teal>	<font color=Teal>Test</font>	Test	Teal	#008080
<font color=Thistle>	<font color=Thistle>Test</font>	Test	Thistle	#D8BFD8
<font color=Tomato>	<font color=Tomato>Test</font>	Test	Tomato	#FF6347
<font color=Turquoise>	<font color=Turquoise>Test</font>	Test	Turquoise	#40E0D0
<font color=Violet>	<font color=Violet>Test</font>	Test	Violet	#EE82EE
<font color=VioletRed>	<font color=VioletRed>Test</font>	Test	VioletRed	#D02090
<font color=Wheat>	<font color=Wheat>Test</font>	Test	Wheat	#F5DEB3
<font color=White>	<font color=White>Test</font>	Test	White	#FFFFFF
<font color=WhiteSmoke>	<font color=WhiteSmoke>Test</font>	Test	WhiteSmoke	#F5F5F5
<font color=Yellow>	<font color=Yellow>Test</font>	Test	Yellow	#FFFF00
<font color=YellowGreen>	<font color=YellowGreen>Test</font>	Test	YellowGreen	#9ACD32


#### 注音  
<ruby>
注<rp>(</rp><rt>zhù</rt><rp>)</rp>
音<rp>(</rp><rt>yīn</rt><rp>)</rp>
</ruby>

  	格式 	效果
一声 	&amacr; 	&amacr;
二声 	&aacute; 	á
三声 	&ecaron; 	&ecaron;
四声 	&agrave; 	à
u音 	&ouml; 	ö

[1].https://www.imooc.com/wiki/markdownlesson/markdowntoc.html
[2].https://zemdalk.github.io/2022/03/22/HTML%E7%9A%84Ruby%E6%A0%87%E7%AD%BE.html