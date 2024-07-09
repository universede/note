# openResty(1.19.3.2)

### 是什么

### 安装
  * 下载[^1]
  * 安装
      1. 打开安装目录
      2. ./configure  --with-pcre-jit  --with-ipv6 --with-http_realip_module  --with-http_ssl_module  --with-http_stub_status_module  --with-http_v2_module  --with-openssl=/usr/bin/openssl(openssl安装目录)
      3. make
      4. sudo make install

[^1]:http://openresty.org/cn/download.html