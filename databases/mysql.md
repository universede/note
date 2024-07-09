---
title: "Mysql"
date: 2020-05-10T21:18:23+08:00
draft: false
categories: ["databases"]
tags: ["mysql"]
---
&emsp;&emsp;MySQL是一个开源的关系型数据库管理系统，由瑞典MySQL公司开发，属于Oracle旗下产品。
#### 安装[^1]

##### 下载并解压 下载
* 创建存放mysql文件夹  
    mkdir /media/universe/_dde_data/mysql
* 解压并赋予权限  
    tar -xJvf mysql.tar.xz
* 创建data文件夹和log文件夹并赋予权限  
    mkdir /media/universe/_dde_data/mysql/data
    mkdir /media/universe/_dde_data/mysql/log

* 配置  
    **创建mysql用户和组**  
    groupadd mysql  
    useradd mysql  
    **编写my.cnf配置并移到/etc目录**
```
      [mysqld]
      port=3306
      pid-file=/media/universe/_dde_data/mysql/data/mysqld.pid
      socket=/media/universe/_dde_data/mysql/data/mysql.sock
      log-error=/media/universe/_dde_data/mysql/log/mysqld.log
      basedir=/media/universe/_dde_data/mysql
      datadir=/media/universe/_dde_data/mysql/data
      [client]
      port=3306
      socket=/media/universe/_dde_data/mysql/data/mysqld.sock
```
**把配置文件移到其他文件下sudo mv /media/universe/_dde_data/my.cnf /etc**  
    **进行初始化**
    /media/universe/_dde_data/mysql/bin/mysqld -\-initialize -\-user=mysql
    -\-basedir=/media/universe/_dde_data/mysql -\-datadir=/media/universe/_dde_data/mysql/data  
    *注意*：如果在my.cnf里面配置了mysql的basedir和datadir不用在初始化里在写，如果写了在进行初始化的时候会报错。  
    **测试mysql**  
    cd mysql/bin/，执行./mysqld_safe，启动mysql初始化状态  
    cd mysql/support-files,执行mysql.server, 启动mysql服务  
    cd mysql/bin,执行./mysql -u用户名 -p密码, 进去mysql命令状态  
    注意：密码在开始的时候是随机生成的，在mysqld.log里可以找到，在进入mysql里面可以进行修改。  
    如果mysql测试能够正常使用，可以通过软连接的方式吧执行命令放到相应的文件夹下，在下次使用是直接使用相应的命令即可。    
    **创建软连接**  
    sudo ln -s /media/universe/_dde_data/mysql /usr/local/mysql  
    sudo ln -s /media/universe/_dde_data/mysql/bin/mysql /usr/bin/mysql  
    复制mysql.server并修改mysql和mysqld里的安装路径和存放数据的路径  
    sudo cp /media/universe/_dde_data/mysql/support-files/mysql.server /etc/init.d/mysql  
    sudo cp /media/universe/_dde_data/mysql/support-files/mysql.server /etc/init.d/mysqld  
    **开启服务并开始**  
    mysqld  
    server mysql start

#### 数据库操作[^2][^3]

    创建数据库
    根据数据库的要求我们可以如下创建数据库:
    create database database_name;
    删除数据库
    drop database database_name;
    选择数据库
    这个用于linux中对要操作的数据库赋予操作权限
    use databases;

##### 表的操作

* 创建表  
    create table table_name(column_name column_type);  

* 删除表  
    drop table table_name;  

* 插入数据    
    insert into table_name(field1, field2....) values (value1, value2....);  

* 删除数据  
    delete from table_name [where condition]|[order by子句]|[limit子句];  

* 更新数据  
    update table_name set column=value [where condition]|[order by子句]|[limit子句];  

* LIKE子句  
    select field... from table_name where field link condition;  
    condition: %字符->任意字符(相当于’*‘号)  
    e.g select * from role where like “%com”;  
    这个表示查询后缀为'com'的全部数据  
    LIKE子句也可以用在delete和update的命令中，可以通过where…like…来进行指定条件  

* UNION  
    数据库UNION操作符用于把两个以上的select语句的结果组合到一个结果集合中  
    select expression.... from table [where condition] uion [all|distinct] select expression.... from table [where condition]  

* 约束条件  
    mysql中有六种约束条件:主键约束(primary key)、外键约束(foreign key)、唯一约束(unique)、检查约束(check)、默认值(default)、非空约束(not null)  

* 主键约束  
    直接创建: <字段名><数据类型> primary key <默认值>  
    修改添加: alter table table_name add primary key(column_name);  

* 外键约束  
    直接创建: constraint <外键名> foreign key(字段名...) references <主表名> 主键列...;  
    修改添加: alter table table_name add constraint <外键名> foreign key(column_name) references <主表名>(主键列);  
    删除约束: alter table table_name drop foreign key <外键名>;  

* 唯一约束  
    直接创建: <字段名><数据类型> unique;  
    修改添加: alter table table_name add constraint <唯一约束名> unique(列名);  
    删除约束: alter table table_name drop index <唯一约束名>;  

* 检查约束  
    直接创建: check <expression>;  
    修改添加: alter table table_name add constraint <检查约束名> check <expression>;  
    删除约束: alert table table_name drop constraint <检查约束名>;  

* 默认值  
    直接创建: <字段名><数据类型> default <默认值>;  
    修改添加: alter table table_name change column <字段名><数据类型> default <默认值>;  
    删除约束: alter table table_name change column <字段名> <字段名> <数据类型> defualt null;  

* 非空约束  
    直接创建: <字段名><数据类型> not null;  
    修改添加: alter table table_name change column <字段名><字段名><数据类型> not null;  
    删除约束: alter table table_name change column <字段名> <字段名> <数据类型> null;  

* 查询方式  
    mysql中查询方式分为六种:内连接查询、外连接查询、子查询、制定过滤条件、正则表达式查询  

    内连接查询

* 视图  
    创建视图:create view <视图名> as <select语句>  
    查询视图:describe 视图名;  
    修改视图:alter view <视图名> as <select语句>  
    删除视图:drop view <视图_1>….  

参考文献

[1] http://c.biancheng.net/view/2376.html  
[2] https://www.runoob.com/mysql/mysql-tutorial.html  
[3] http://c.biancheng.net/mysql/  
[4] https://baike.baidu.com/item/MySQL/471251  

