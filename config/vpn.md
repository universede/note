# vpn

#### L2TP/IPsec方式的vpn连接失败
&emsp;在控制中心创建l2tp后，会在/etc/NetworkManager/system-connections/ 下生成对应名称的文件，编辑这个文件，在 [vpn] 段下添加如下2行，指定加密算法：
```
ipsec-esp=aes128-sha1,3des-md5
ipsec-ike=aes128-sha1-modp1024,3des-sha1-modp1024
```

具体参考：
下面是使用ike-scan.sh的输出，麻烦看看应该如何指定加密算法。谢谢！
```
IPSec预共享密钥: 123456
Phase1 Algorithms: aes128-sha1-modp1024,3des-sha1-modp1536
Phase2 Algorithms: aes128-sha1,3des-md5
```

#### 参考文献
[1]. https://bbs.deepin.org/post/153665