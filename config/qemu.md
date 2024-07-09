# qemu

&emsp;qemu虚拟机的安装

1. 下载[^1]
2. 安装`./configure --prefix=安装路径 --enable-debug --target-list=x86_64-softmmu --enable-kvm`
    报错[^2][^3]，`../meson.build:328:2: ERROR: Dependency "pixman-1" not found, tried pkgconfig`
    下载依赖：`sudo apt-get install libmount-dev`和`sudo apt-get install libpixman-1-dev`
 3. 编译：make -C 安装路径
 4. make install
 

[^1]:	https://www.qemu.org/download/
[^2]:https://blog.csdn.net/cclethe/article/details/103003437
[^3]:https://www.codeleading.com/article/68415748175/