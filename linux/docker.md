# docker

### 安装[^1]
1. [下载](https://download.docker.com/linux/static/stable/x86_64/)
2.  解压
    `tar zvxf docker.tgz`
 3. 创建配置文件
      (1). socket.service
      ```java
        [Unit]                                                                                                       
        Description=Docker Application Container Engine
        Documentation=https://docs.docker.com
        After=network-online.target firewalld.service
        Wants=network-online.target
        [Service]
        Type=notify
        ExecStart=/usr/bin/dockerd --graph /media/universe/_dde_data/application/server/docker/data
        ExecReload=/bin/kill -s HUP $MAINPID
        LimitNOFILE=infinity
        LimitNPROC=infinity
        LimitCORE=infinity
        TimeoutStartSec=0
        Delegate=yes
        KillMode=process
        Restart=on-failure
        StartLimitBurst=3
        StartLimitInterval=60s
        [Install]
        WantedBy=multi-user.target

      ```
      (2).docker.socket 
      ```java
      [Unit]                                                                                                       
        Description=Docker Socket for the API
        [Socket]
        # If /var/run is not implemented as a symlink to /run, you may need to
        # specify ListenStream=/var/run/docker.sock instead.
        # ListenStream=/run/docker.sock
        ListenStream=/media/universe/_dde_data/application/server/docker/sock/docker.sock
        SocketMode=0660
        SocketUser=root
        SocketGroup=docker        
        [Install]
        WantedBy=sockets.target
      ```
      (3). daemon.json
      ```java
      {                                                                                                            
        "registry-mirrors": ["https://hub-mirror.c.163.com", "https://bmtrgdvx.mirror.aliyuncs.com", "https://docke    rhub.azk8s.cn", "https://hub.wuxiaobai.win","https://docker.mirrors.ustc.edu.cn"],
        "hosts":["unix:///media/universe/_dde_data/application/server/docker/data", "tcp://127.0.0.1:2357"]
      }
      ```
   4. 移位置
   <font color=#7070ED>docker.service</font>和<font color=#7070ED>docket.socket</font>复制到<font coloe=#7070ED>/etc/systemd/system</font>下，<font>daemon.json</font>复制到<font color=#7070ED>/etc/docket</font>下
   5. 启动服务
     `sudo dockerd`
     **Tips:**启动docker需要使用管理员才行

[^1]:https://www.cnblogs.com/txlsz/p/13587720.html