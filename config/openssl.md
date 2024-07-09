# openssl(3.0.0)

### 是什么

### 安装
   * 下载[^1]
   * 安装
      1. 解压
      2. ./config shared zlib
      3. make
      4. sudo make install
      5. sudo mv /usr/bin/openssl /usr/bin/openssl.bak
      6. find / -name openssl
      7. sudo ln -s /usr/local/bin/openssl /usr/bin/openssl
      8. sudo "/usr/local/lib64" >> sudo /etc/ld.so.conf(在我的系统后面需要增加<font color=#70EDSE>sudo</font>，不然权限不足)
      9. sudo ldconfig(动态链接)
      10. openssl version -a
      注意：部分地方因安装路径的不同会去进行路径配置

[^1]:http://openresty.org/cn/download.html