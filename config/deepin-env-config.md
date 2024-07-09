# deepin-env-config

* 环境配置

```shell
   paths=/media/universe/_dde_data/application

   export PATH=${paths}/bin:${PATH}

   export JAVA_HOME=${paths}/env/jdk/jdk-11.0.12
   export PATH=${JAVA_HOME}/bin:${PATH}
   export CLASSPATH=${JAVA_HOME}/lib
```

```shell
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]>>>[\033[00m\]:\[\033[01;34m\]\W\[\033[00m\]\$ '
PS1='${debian_chroot:+($debian_chroot)}>>>:\W\$ '    
PS1="\[\e]0;${debian_chroot:+($debian_chroot)}>>>: \W\a\]$PS1"

```

* 输入法
sudo apt install fcitx-libpinyin
http://wiki.deepinos.org.cn/deepin%E6%8A%98%E8%85%BE%E7%AC%94%E8%AE%B0/%E7%AC%AC%E5%85%AD%E7%AB%A0/6.4.html
如果自定义的皮肤没有生效，打开fctix configuration -> appearance -> show advanced options -> skin name， 修改skin name的值为dark，然后保存就会生效
注意：dark是皮肤文件，在/usr/share/fctix/skin里，如果没有，可以到网上查找自定义皮肤，复制到该路径