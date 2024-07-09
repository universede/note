# go

### 学习文档
[基于视频](https://www.bilibili.com/video/BV1s341147US?p=1)
[基于文档](https://www.topgoer.com/)
[基于文档](https://golang.fasionchan.com/zh_CN/latest/about/contact.html)
[基于文档](https://golang.iswbm.com/c01/c01_01.html)

### 环境配置
* 系统环境路径  
编辑/etc/profile,导入以下文本：  
 ```shell
    export GOCACHE="/media/universe/_dde_data/application/env/go-env/go-build"
    export GOENV="/media/universe/_dde_data/application/env/go-env/env/env"
    export GOPATH="/media/universe/_dde_data/document/study/project/go"
    export GOMODCACHE="/media/universe/_dde_data/document/study/project/go/pkg/mod"
 ```
* 用户环境配置
```shell
go env -w GOPROXY="https://goproxy.cn,https://gocenter.io,https://goproxy.io,https://proxy.golang.org,direct"
go env -w GOROOT="/media/universe/_dde_data/application/language/go"
go env -w GOTOOLDIR="/media/universe/_dde_data/application/language/go/pkg/tool/linux_amd64"
```

### 命名规则  [^1]
  go语言是一门区分大小写的语言,需要**对外暴露**的名字必须**大写字母**开头;**不对外暴露**的名字应该**首字母小写**  
  当命名(常量、变量、函数名、结构字段等)以首字母大写开头,如Ant,这种形式的标识符的对象就表示**可以被外部包的代码使用**,称为**导包**(面向对象中的public)  
  当命名以首字母小写开头,如ant,这种表示**对外包不可见,在整个包的内部是可见并可使用**(面向对象中的private)   
* 包  
    小写单词开头,不要使用下划线或者混合大小写,包的名字尽量和目录保持一致,不与标准库冲突  
* 文件  
    小写单词开头,使用下划线分隔各个单词  
* 结构体  
   采用驼峰命名,首字母根据访问控制来规定  
   struct申明和初始化采用多行  
* 接口
   命名规则参照结构体  
   单个函数的结构名以"er"作为后缀,如Reader
* 变量
   命名规则参照结构体,对于特有名词需要注意:
   1. 如果变量为私有,且特有名词为单个字母,使用小写,如appService
   2. 如变量类型为bool类型,则命名为Has,Is,Can或Allow开头
* 常量
    均以大写字母,使用下划线分隔各个单词
    如果是枚举类型的常量,需要先创建相应类型

### 变量与常量
  变量使用```var```声明；常量使用```const```声明
  跨包全局常量,首字母需要**大写**
- 变量
  ```go
    // 第一种方式
    var a int
    a = 10
    // 第二种方式
    var a int = 11
    // 第三种方式
    a = 12
    // 第四中方式
    a := 13
    // 第四种方式,一次声明多个变量
    var (
       a int = 14
       a = 15
       a int
       a = 16
    )
  ```
- 常量
```go
    const B int = 90
	const C = 11
	D := 80
	const (
		E     = 20
		F int = 23
	)
```
### 基本类型


#### go导包
* 一个项目引入另一个项目
```go
require github.com/commom/common v0.0.0

replace github.com/commom/common => ../common
```
github.com/commom/common是任意命名，但为了规范需要参考go导出包的命名规范
v0.0.0 是版本号
../common 另一个项目

* 使用go work来管理空间


### 参考文献
[^1]:https://www.cnblogs.com/rickiyang/p/11074174.html