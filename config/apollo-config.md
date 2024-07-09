#### apollo的安装与配置
  - version:
     1.8.0 
  
  - 安装
     * 1. 下载
        &nbsp;&nbsp; ** https://github.com/ctripcorp/apollo/releases **分别下载apollo-adminservice-1.9.0-github.zip、apollo-configservice-1.8.0-github.zip、apollo-portal-1.8.0-github.zip

     * 2. 安装
	    &nbsp;&nbsp;上传服务器，分别创建3个文件夹，并把3个压缩包分别放到相关的文件夹下，并进行解压，如unzip解压命令

	 * 3. 修改ip地址
	    &nbsp;&nbsp;分别打开文件下的config配置文件，找到里面的** application-github.properties ** 文件，如
	     - apollo-configservice	
		   ```
               spring.datasource.url = jdbc:mysql://192.168.1.16:3306/ApolloConfigDB?characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai                                                                    
               spring.datasource.username = your database username
               spring.datasource.password = your database password
		   ```
		 
		 - apollo-adminservice
		   ```
               spring.datasource.url = jdbc:mysql://192.168.1.16:3306/ApolloConfigDB?characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai                                                                    
               spring.datasource.username = your database username
               spring.datasource.password = your database password
		   ```

		 - apollo-portal
		   ```
               spring.datasource.url = jdbc:mysql://192.168.1.16:3306/ApolloPortalDB?characterEncoding=utf8&useSSL=false&serverTimezone=Asia/Shanghai                                                                    
               spring.datasource.username = your database username
               spring.datasource.password = your database password
		   ```
	
		** Tips: ** &nbsp; '''192.168.1.16'''是你的ip地址，其中apollo-portal文件中的config配置文件下，还有一个环境配置,即apollo-env.properties,如下：
		```
           local.meta=http://192.168.1.11:8080
           dev.meta=http://192.168.1.11:8080
           fat.meta=http://192.168.1.11:8080                                                                                                                                                                         
           uat.meta=http://192.168.1.11:8080
           lpt.meta=${lpt_meta}
           pro.meta=http://192.168.1.11.8080 
		```
  
  - 导数据库
    - 1. 导apolloportaldb.sql
	    https://github.com/apolloconfig/apollo-build-scripts/blob/master/sql/apolloportaldb.sql   
    - 2. 导apolloconfigdb.sql
	    https://github.com/apolloconfig/apollo-build-scripts/blob/master/sql/apolloconfigdb.sql   
    复制里面的sql语句，然后直接执行就可以了。

- 注意点
  &emsp;对于日志配置，需要修改相关的apollo-adminservice.conf里面的路径，同时在startup.sh里面的日志路径(三个服务都要修改)
  &emsp;对于高版本JDK需要在startup.sh里面进行设置，否则启动不了

#### 参考文献
	[1] https://www.apolloconfig.com/#/zh/deployment/distributed-deployment-guide?id=_21-创建数据库
