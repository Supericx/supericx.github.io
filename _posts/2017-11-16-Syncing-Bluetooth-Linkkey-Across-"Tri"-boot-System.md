---
layout: post
title: Syncing Bluetooth Linkkey Across "Tri" boot System
---

Credit:
insanelymac.com

上周把Ubuntu装进了第三块SSD，然后目前是macOS 10.13.1 + windows 10 + Ubuntu 16.04，在解决了grub2会自动写进disk0的问题之后（重新安装一下clover就好了）三个系统就都可以用了。

下一个问题就是我的蓝牙键盘每次切换系统的时候需要重新配对。之前只有windows + macOS的时候问题不大，minila air可以同时配对，但是不知道为什么配对到linux后就不行了。所以想换一个解决方法。

#方法如下：
1. Unpair to all three OS.
2. Pair the keyboard in the following order: ubuntu(linux), windows, macOS.
3. Boot into macOS, open terminal and run:
````
sudo defaults read /var/root/Library/Preferences/com.apple.bluetoothd.plist
````
enter password
4. 找到有一行：
````
LinkKeys =     {
````
下一行就是硬件的mac地址，长得类似于“##-##-##-##-##-##"
然后是设备的mac地址，可能有多个，找到想要同步的那个，然后复制下后面的Linkkeys。也可以拍个照片。
5. Linkkeys是hex numbers，并且macOS用的是反过来的，所以我们需要处理一下：
比方说我的macOS里复制的Linkkeys是：
````
<6280b639 f6fe62c8 5f639b9f 23e6e0c3>
````
那么在windows和linux下，Linkkeys就是
````
C3 E0 E6 23 9F 9B 63 5F C8 62 FE F6 39 B6 80 62
````
6. boot into windows
7. download PStools to Desktop, extract to a folder. Run Command Prompt as Administrator. 
````
cd C:/Users/xxxx/desktop
psexec -s -i regedit
````
Goes to HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\BTHPORT\Parameters\Keys
edit the desired Linkkey to the one we just edited from mac.
8. reboot into linux.
open terminal and run:
````
gksu nautilus
````
enter password and goes to /var/lib/Bluetooth/
找到硬件mac地址，然后设备地址，有个叫info的文件，打开，拷贝修改过的linkkey进去。
9. Test and DONE.

需要注意的是，如果用的不是这几个系统版本，可能会有些区别，我就是浪费了不少时间在找high sierra下的蓝牙linkkey。
glhf