# redis

cd redis安装目录
make -C redis安装目录
make install prefix=redis安装目录

vim redis.config
```shell
# ./redis-server /path/to/redis.conf                             
 ./redis-server /media/universe/_dde_data/application/database/redis/redis.conf
  # pidfile /var/run/redis_6379.pid                                      
pidfile /media/universe/_dde_data/application/database/redis/tmp/redis_6379.pid
#dir ./                                                                                                     
 dir /media/universe/_dde_data/application/database/redis/tmp
 
```