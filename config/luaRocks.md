# luaRocks(3.7.0)

### 是什么

### 安装[^1]
  1. wget https://luarocks.org/releases/luarocks-3.7.0.tar.gz
  2. tar zxpf luarocks-3.7.0.tar.gz
  3. cd luarocks-3.7.0
  4. ./configure --lua-suffix=jit --with-lua=/usr/local/openresty/luajit --with-lua-include=/usr/local/openresty/luajit/include/luajit-2.1
  5. make build
  6. sudo make install
  注意：部分地方因安装路径的不同会去进行路径配置

[^1]:https://luarocks.org/