#### apollo的认识

  -  整体结构图分析
     ![apollo](vx_images/4055021816421.png "apollo" =650x)
    1. 通过把config server和admin server注册到Eureka注册中心(config server读取、推送功能,Apollo客户端(应用程序)从这里读取配置; admin server修改、发布功能(开发人员在这里配置文件))
    2. configservice和adminservice是多实例服务，需要将其注册到Eureka服务中心
    3. 在Eureka注册中心上有一层封装的Meta server的服务发现接口
    4. Client和Portal通过域名访问Meta server获取configservice和adminservice的服务列表(ip:port)，然后通过套接字访问服务

  - 四个维度
    - 应用
      &nbsp;&nbsp;在springboot的application.yaml定义的appid的key-value，标识该类型的应用
    - 环境
      - DEV(开发环境)
      - FAT(功能测试)
      - UAT(验收测试)
      - PRO(生产环境)

    - 集群
      &nbsp;&nbsp;每一个模块相当于一个集群
    - 命名空间

#### 使用

#### 参考文献
[1] https://www.jianshu.com/p/2742b47389bf
