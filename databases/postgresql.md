# postgresql


### 安装
   * 下载[^1]
   * 安装[^2][^3]
      1. 解压**postgresql.xx.tar.gz
      2. 下载依赖，`sudo apt install libreadline6-dev`
      3. 创建一个数据文件：
          在postgresql的安装目录下，创建`/db/psql/data`
      4. 编译
          ```
             ./configure  --prefix=安装路径
             make -C 安装路径
             make install DESTDIR=安装路径
         ```
         注意：<font color=#70EDED>-C</font>编译时已经指定了路径，在<font color=#70EDED>DESTDIR</font>就可以不需要再次指定路径
     5. 修改配置文件
     6. 软连接命令
     &emsp;初始化数据库：`sudo ln -s /media/universe/_dde_data/application/database/postgresql/bin/initdb initdb`
     &emsp;启动服务：`sudo ln -s /media/universe/_dde_data/application/database/postgresql/bin/pg_ctl pg_ctl`
     &emsp;打开数据库：`	sudo ln -s /media/universe/_dde_data/application/database/postgresql/bin/psql psql`
     7. 初始化：
          `initdb --encoding=utf8 -D /media/universe/_dde_data/application/database/postgresql/db/pgsql/data/`
     8. 启动：
          `pg_ctl -D /media/universe/_dde_data/application/database/postgresql/db/pgsql/data/ -l /media/universe/_dde_data/application/database/postgresql/log/logfile start`
          **Tips:** “<font color=#70EFED>-l</font>”后面是日志文件
     9. 进入：
         `psql -h 127.0.0.1 -p 5432 -U kong -d kong`
        **Tips:**"<font color=#70EFEF>-U</font>"是用户名，没有用户名时不用写此参数，"<font color=#70EFED>-d</font>"后面是数据库名称
  * Error
      1. `FATAL: data directory "/opt/pg/data" has group or world access DETAIL: Permissions should be u=rwx (0700).`
      解决[^4]： chmod 700 -R 数据库文件目录
      2. `psql: error: connection to server at "127.0.0.1", port 5432 failed: FATAL:  role "postgres" does not exist`
      解决：指定一个初始化的数据库，如**postgres**，然后就可以登录了

[^1]:https://www.postgresql.org/ftp/source/v14beta2/
[^2]:http://www.postgres.cn/docs/12/installation.html
[^3]:https://blog.csdn.net/cuia1717324/article/details/103920072
[^4]:https://blog.csdn.net/vah101/article/details/83309018