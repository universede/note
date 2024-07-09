# adb的使用

andriod 手机连接桥

打开手机开发者模式，开启Usb调试，使用数据线连接电脑

lsusb
查看手机设备id
```shell
Bus 002 Device 013: ID 2717:ff88
```

错误1：
```shell
ba46404 no permissions (user universe is not in the plugdev group); see [http://developer.android.com/tools/device.html]
```
解决：
```shell
sudo vim /etc/udev/rules.d/90-android.rules
SUBSYSTEM=="usb",ATTRS{idVendor}=="2717",ATTRS{idProduct}=="ff88",MODE="0666",GROUP="plugdev",SYMLINK+="android",SYMLINK+="android_adb"

```
注意 2721 ff88信息来自lsusb查询可得

错误2：
```shell
ba46404 unauthorized
```
解决：回到手机端，手机可能会弹出一个授权的提示框，点击确定

查看是否连接手机调试
```shell
sudo service udev restart
adb kill-server
adb start-server
adb devices

```
