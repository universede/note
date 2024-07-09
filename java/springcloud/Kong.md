# Kong(2.4.1)

#### 背景和动机
   存在大量非功能性的重复开发(鉴权、限流等逻辑)
   需要知道服务间调用关系(服务更新、下线很糟心)
   统一接口，减少接入成本
   蓝绿，金丝雀
   调用链跟踪
   ![](https://camo.githubusercontent.com/335b3c6ef2bcaa9cf5f04ce2f6a96864af80e9f0f767c09bb79b3c1cedde372c/68747470733a2f2f6b6f6e6768712e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031382f30352f6b6f6e672d62656e65666974732d6769746875622d726561646d652e706e67 =1000x)
   
### 为什么选择Kong
   身份认证插件：OAuth2.0 authentication、HMAC authentication、JWT、LDAP authentication等
   安全控制插件：ACL(访问控制)、CORS(跨域资源共享)、动态SSL、IP限制、爬虫检测实现
   流量控制插件：请求限流(基于请求计数限流)、上游相应限流(根据upstream响应计数限流)、请求大小限流。限流支持本地、Redis和集群限流模式
   分析监控插件：zipkin、Prometheus
   协议转换插件：请求转换(在转发到upstream之前修改请求)、响应转换(在upstream响应返回给客户端之前修改响应)
   日志应用插件：TCP、UDP、HTTP、File、Syslog、StatsD、Loggly等

### Kong网关的安装[^1]   
#### 数据库安装
  * 准备数据库或声明式配置文件(相当于数据库，但比使用数据库时插件较少，文件类型是yaml)
        &emsp;使用数据库时，你将使用<font color=#79EDEF>kong.conf</font>配置文件在启动和数据库中将<font color=#70EDEF>kong</font>的配置属性设置为所有已配置的实体的存储，例如，Kong网关代理的路由和服务。  
        &emsp;不u使用数据库时，你可以使用<font color=#79EDDE>kong.conf</font>配置属性和<font color=#79EDFE>kong.yaml</font>文件，用于将实体指定为声明式配置  
   * 使用数据库  
        &emsp;**Kong**能够连接数据库，支持<font color=#79ERFE>PostgreSQL 9.5+</font>和<font color=#79DEFE>Cassandra 3.x.x</font>以上版本  
        基于**PostgreSQL**的使用方式：
        1. 使用二进制安装，[教程](/media/universe/_dde_data/document/note/markdown/databases/postgresql.md)
        2. 创建数据库
            `CREATE USER kong; CREATE DATABASE kong OWNER kong;`
            **Tips**:<font color=#79EDED>USER</font>表示创建用户，<font color=#79EDED>OWNER</font>表示把某一个数据库交由某人来管理  
   * 不使用数据库
        如果你使用<font color=#70EFED>DB-less model</font>来运行**Kong**，你在开始之前就需要声明*配置文件*，在当前的文件夹里使用以下命令会生成一个<font color=#70EFED>kong.yaml</font>的文件。它包含了关于如何补充的说明。  
>     kong config init
        
   &emsp;补充<font color=#70EDED>kong.yaml</font>文件之后，编辑<font color=#70EEEE>kong.yaml</font>，在**kong.yaml**文件里对分别配置<font color=#70EDED>database=off</font>和<font color=#70EDSE>declarative_config=/path/to/kong.yml</font>
>     database = off
>     declaretice_config = /path/to/kong.yaml

#### Kong安装[^2][^3][^4]
   * 安装
       1. openssl，[教程](/media/universe/_dde_data/document/note/markdown/config/openssl.md)
       2. openResty，[教程](/media/universe/_dde_data/document/note/markdown/config/openResty.md)
       3. luaRocks，[教程](/media/universe/_dde_data/document/note/markdown/config/luaRocks.md)
       4. 运行`../luarocks/bin/luarocks make`，`../`表示<font color=#70ESDE>luarocks</font>的安装路径前半部分
       5. bin/kong start -c kong.conf
       6. 第5步可能存在报错，需要<font color=#70ESDE>yaml</font>相关的东西，[教程](/media/universe/_dde_data/document/note/markdown/config/libyaml.md)
       &emsp;部分插件无法直接使用<font color=#70EDED>luarocks</font>安装，只能先到<font color=#70EDED>[依赖库](https://luarocks.org/modules/kong)</font>找到相关的插件再安装。

### Kong网关的管理与配置[^5]
   * 验证Kong网关的配置
     - Using Kong Manager 
        打开浏览器并导航到`http://<admin-hostname>:8002`
     - Using the Admin API
        - cURL
           `curl -i -X GET http://<admin-hostname>:8001`  
        - HTTPie
          `http <admin-hostname>:8001`
     - Using deck(YAML)
           `deck ping`
   * 验证控制平面和数据平面连接
      &emsp;如果你在混合模式下运行Kong网关，则需要从控制平面执行本指南中的所有任务。但是，你可以使用集群状态CLI检查从控制平面向数据平面推送所有配置。
      运行：
      - cURL
         `curl -i -X GET http://<admin-hostname>:8001/clustering/data-planes`
      - HTTPie
         `http :8001/clustering/data-planes`
      结果：
      ```json
            {
                "data": [
                    {
                        "config_hash": "a9a166c59873245db8f1a747ba9a80a7",
                        "hostname": "data-plane-2",
                        "id": "ed58ac85-dba6-4946-999d-e8b5071607d4",
                        "ip": "192.168.10.3",
                        "last_seen": 1580623199,
                        "status": "connected"
                    },
                    {
                        "config_hash": "a9a166c59873245db8f1a747ba9a80a7",
                        "hostname": "data-plane-1",
                        "id": "ed58ac85-dba6-4946-999d-e8b5071607d4",
                        "ip": "192.168.10.4",
                        "last_seen": 1580623200,
                        "status": "connected"
                    }
                ],
                "next": null
          }
      ```

### 使用Kong网关公开(暴露)服务[^6]
  * 目标
      1. 使用Routes公开服务
      2. 准备好Kong网关
      3. 安装过Kong网关

  * Service and Routes是什么？
     **服务**和**路由**对象允许你将你的服务公开(暴露)给带Kong网关的客户。配置对API的访问时，你将首先指定服务。在Kong网关中，服务是代表外部上游API或Micro Service的实体。例如，数据转换微服务，计费API等。  
     服务的主要属性是其<font color=#70DDEF>URL</font>，该服务侦听请求，你可以使用单个字符串指定URL，或通过单独指定其协议(Protocol)，主机(Host)，端口(Port)和路径(Individually)  
     在你开始对该服务的请求开始之前，你需要向其添加路由。路由决定在到达Kong网关后如何将请求发送到其服务。单个服务可以有许多的路由。  
     配置服务和路由后，你将能够通过Kong网关开始提出请求。  
     该图说明了通过服务到后端API的服务的请求和响应的流程。如图：
     ![服务的请求与响应图](https://docs.konghq.com/assets/images/docs/getting-started-guide/route-and-service.png =900x)

  * 增加服务(Add a Service)
     出于此示例的目的，你将创建一个指向Mockbin API的服务。Mockbin是一个“echo”类型的公共网站，将请求返回请求者作为响应。 这种可视化将有助于学习Kong网关代理API请求。  
     Kong网关在端口上公开RESTful Admin API`:8081`。网关的配置包括添加服务和路由，通过对Admin API的请求完成。  
     * Using Kong Manager
        ```
          1. 在Workspaces选项卡上，在Kong Manager中，滚动到“工作区”部分，然后单击默认工作区。此示例使用默认工作区，但您还可以创建一个新的工作区，或使用现有工作区。
          2. 向下滚动到服务，然后单击“添加服务”。
          3. 在“创建服务”对话框中，输入名称`example_service`和URL`http://mockbin.org`
          4. 点击创建
        ```
     * Using the Admin API
       - cURL
          ```
            curl -i -X POST http://<admin-hostname>:8001/services \
            --data name=example_service \
            --data url='http://mockbin.org'
          ```
          验证服务端点：
          `curl -i http://<admin-hostname>:8001/services/example_service`
       - HTTPie
         ```
            http POST :8001/services \
            name=example_service \
            url='http://mockbin.org'
         ```
         验证服务端点：
         `http :8001/services/example_service`
    * Using deck(YAML)
       1. 在`Kong.yaml`文件中，你准备导出到Administer Kong网关，定义一个服务名为`example_service`和URL`http://mockbin.org`：
          ```
            _format_version: "1.1"
            services:
            - host: mockbin.org
            name: example_service
            port: 80
            protocol: http
          ```
       2. 保存文件，打开终端，同步配置并更新网关
          `deck sync`
  * 增加路由
     对于通过API网关访问的服务，你需要添加一个路由  
   * Using Kong Manager
      1.  从`example_service`overiew页面，向下滚动到路由部分，然后点击`增加路由`  
         “创建路由”对话框将显示使用服务名称和ID号自动填充的服务字段。 此字段是必需的。  
           注意：如果不自动填充服务字段，请单击左侧导航窗格中的服务。 找到您的服务，单击ID字段旁边的剪贴板图标，然后返回“创建路由”页面并将其粘贴到“服务”字段中。
      2. 输入路由的名称，以及以下字段中的至少一个：主机，方法或路径。 对于此示例，请使用以下内容：
           1. name中，输入`mocking`
           2. path(s)中，点击增加路由，并输入`/mock`，然后按回车(<font color=#70FFFF>Enter</font>)
      3. 点击创建
      这个路由创建后，会自动重定向到`example_service`页面，新的路由出现在路由部分下。
   * Using the Admin API
      使用客户端需要请求的特定路径来定义服务（`example_service`）的路由（`/mock`）。 注意必须为要与服务匹配的路由设置至少一个主机，路径或方法。
      - cURL
         ```
             curl -i -X POST http://<admin-hostname>:8001/services/example_service/routes \
            --data 'paths[]=/mock' \
            --data name=mocking
         ```
      - HTTPie
        ```
        http :8001/services/example_service/routes \
        paths:='["/mock"]' \
        name=mocking
        ```
         验证路由重定向请求到服务：
         1.  Using Web Brower
              默认情况下，Kong网关处理端口上的代理请求：`8000`。
              打开浏览器：输入`http://<admin-hostname>:8000/mock`
         2. Using the Admin API
             - cURL
                   `curl -i -X GET http://<admin-hostname>:8000/mock/request`
             - HTTPie
                   `http :8000/mock/request`

### 服务保护
  * 什么是<font color=#70EWSD>限速</font>
    &emsp;限速允许你限制你的上游服务从API消费者收到的请求数量，或每一个用户可以对用API的频率  
    
  * 为什么使用限速
    &emsp;限速保护API免于意外或恶意过度使用，没有限速，每个用户可以想他们一样经常请求，这可能导致其他消费者的请求饿死。启动限速后，API回调被限制在每秒固定的请求数。

  * 设置限速
     * Using Kong Manager
        1. 访问你的Kong Manger实例和默认工作区
        2. 进入API Gateway > Plugins
        3. 点击新增Plugins
        4. 滚动到<font color=#70EDED>Traffic Control</font>，找到<font color=#78EEDD>Rata  Limiting Advanted plugins</font>, 点击<font color=#78EEDD>Enable</font>
        5. 将插件应用为<font color=#79DFFD>Global</font>，这意味着限速适用于所有请求，包括工作区中的每个服务和路由。
        6. 滚动并使用以下参数填写以下字段
            - `onfig.limit:5`
            - `config.sync_rate:-1`
            - `config.window_size:30`
         7. 点击创建
     * Using the Admin API
         - cURL
            ```
            curl -i -X POST http://<admin-hostname>:8001/plugins \
            --data name=rate-limiting \
            --data config.minute=5 \
            --data config.policy=local
            ```
         - HTTPie
            ```
            http -f post :8001/plugins \
            name=rate-limiting \
            config.minute=5 \
            config.policy=local
            ```
     * Using deck(YAML)
        1.在`kong.yaml`配置文件下新增`plugins`  
         ```json
            plugins:
              - name: rate-limiting
              config:
                 minute: 5
                 policy: local
         ```  
         &emsp;以上配置的插件作用于全局，如果想只作用于已存在的服务、路由或消费者，则把当前代码放到具体的对象下
        2. 同步配置
            `deck sync`


### Run Kong Exception
1.
```w
Error: /usr/local/lib/luarocks/rocks-5.1 does not exist and your user does not have write permissions in /usr/local/lib 
-- you may want to run as a privileged user or use your local tree with --local.
```
解决：在相关的命令尾加参数<font color=#70RFED>--local</font>

2.
```w
ERROR: ./kong/tools/utils.lua:734: module 'resty.ipmatcher' not found:No LuaRocks module found for resty.ipmatcher
        no field package.preload['resty.ipmatcher']
        no file './resty/ipmatcher.lua'
        no file './resty/ipmatcher/init.lua'
        no file '/usr/local/openresty/site/lualib/resty/ipmatcher.ljbc'
        no file '/usr/local/openresty/site/lualib/resty/ipmatcher/init.ljbc'
        no file '/usr/local/openresty/lualib/resty/ipmatcher.ljbc'
        no file '/usr/local/openresty/lualib/resty/ipmatcher/init.ljbc'
        no file '/usr/local/openresty/site/lualib/resty/ipmatcher.lua'
        no file '/usr/local/openresty/site/lualib/resty/ipmatcher/init.lua'
        no file '/usr/local/openresty/lualib/resty/ipmatcher.lua'
        no file '/usr/local/openresty/lualib/resty/ipmatcher/init.lua'
        no file './resty/ipmatcher.lua'
        no file '/usr/local/openresty/luajit/share/luajit-2.1.0-beta3/resty/ipmatcher.lua'
        no file '/usr/local/share/lua/5.1/resty/ipmatcher.lua'
        no file '/usr/local/share/lua/5.1/resty/ipmatcher/init.lua'
        no file '/usr/local/openresty/luajit/share/lua/5.1/resty/ipmatcher.lua'
        no file '/usr/local/openresty/luajit/share/lua/5.1/resty/ipmatcher/init.lua'
        no file '/home/universe/.luarocks/share/
        ....
```
解决：却模块，在luarocks模块站搜索相关的模块，然后下载

3.
```w
prefix directory /media/universe/_dde_data/application/env/kong/kongs not found, trying to create it
Error: /usr/local/openresty/luajit/lib/libluajit-5.1.so.2: undefined symbol: EVP_PKEY_base_id
  Run with --v (verbose) or --vv (debug) for more details

```
缺少库<font color=#70SDRE>[FFI](https://luajit.org/ext_ffi.html)</font>，造成在引用时找不到里面的方法等

### 参考文献
[^1]:https://docs.konghq.com/install/debian/
[^2]:http://www.manongjc.com/detail/23-twsglzmyksztwkv.html
[^3]:https://blog.csdn.net/kaikai136412162/article/details/105795621
[^4]:https://my.oschina.net/huaxian8812/blog/4282164
[^5]:https://docs.konghq.com/getting-started-guide/2.4.x/prepare/
[^6]:https://docs.konghq.com/getting-started-guide/2.4.x/expose-services/

