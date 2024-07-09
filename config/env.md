#### apollo配置环境:
   - 启动命令:
      1. java -jar apollo-adminservice.jar
	  2. java -jar apollo-configservice.jar 
	  3. java -jar apollo-portal.jar
	  访问地址: 192.168.1.11:8070
	            192.168.1.11:8080
				192.168.1.11:8090
   参考文献：https://blog.csdn.net/qq_34707456/article/details/103702828

#### consul:
   1. 下载安装：https://www.consul.io/
   2. 解压文件
   3. 启动consul:单节点测试：consul agent -dev -client=0.0.0.0
   访问地址: 192.168.1.11:8500
   安装教程：https://blog.csdn.net/qq_38270106/article/details/83239921

#### rocketmq:
   1.下载: http://rocketmq.apache.org/docs/quick-start/
   2. 解压
   3. 找到bin目录下的启动文件：(需要先找到执行命令：这里是在/usr/local/rocketmq)
    
         sh mqnamesrv
         sh mqbroker -n 192.168.1.11:9876
         sh tools tools.sh org.apache.rocketmq.example.quickstart.Producer
         sh tools.sh org.apache.rocketmq.example.quickstart.Consumer
    
    
   * 启动可视化命令  
	     - java -jar rocketmq-console-ng-2.0.0.jar
	   访问地址: 192.168.1.11:15920
	   命令执行文档：http://rocketmq.apache.org/docs/quick-start/
   可视化安装教程：https://developer.aliyun.com/article/757445
   - 界面编译  
     &nbsp;&nbsp;找到rocketmq-console文件夹下，通过编译命令：
	 ``` mvn clean package -Dmaven.test.skip=true ```
   - 密码登录  
     &nbsp;&nbsp;在编译前找到rocketmq-console文件夹下子目录工程的配置文件，及applicarion.properties启用**rocketmq.config.loginRequired=true**，在users.properties中可以看到管理员的账号和密码(账号=密码)
   - 关闭服务
     关闭namesrv服务：sh bin/mqshutdown namesrv
     关闭broker服务 ：sh bin/mqshutdown broker 
   - 修改内存大小
     vi runbroker.sh 和runserver.sh两个脚本，找到JAVA_OPT="${JAVA_OPT}中的一些参数

#### rabbitMQ:
   启动命令: rabbitmq-server -detached
   停止命令：rabbitmqctl stop
   状态查看: rabbitmqctl status
   访问地址:http://192.168.1.11:15672/
   用户名和密码：admin     rabbit
   参考文献：https://www.cnblogs.com/fengyumeng/p/11133924.html
