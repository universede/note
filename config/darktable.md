# darktable

#### GLIBC[^1]
Linux/Centos下/lib64/libc.so.6: version `GLIBC_2.30' not found
解决:
wget http://mirrors.nju.edu.cn/gnu/libc/glibc-2.30.tar.xz
xz -d glibc-2.30.tar.xz
tar -xf glibc-2.30.tar
mkdir build
cd build
../configure  --prefix=$HOME/local   // --prefix安装路径
make

#### bison[^2]
These critical programs are missing or too old: bison
sudo apt install bison

#### 参考文献
[^1]:https://blog.csdn.net/wangmengmeng99/article/details/102872708
[^2]:https://www.cnblogs.com/liujiaxin2018/p/13196207.html
https://blog.csdn.net/qq_35550345/article/details/120531684