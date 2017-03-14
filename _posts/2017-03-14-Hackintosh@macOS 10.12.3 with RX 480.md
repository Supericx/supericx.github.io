---
layout: post
title: Hackintosh@macOS 10.12.3 with RX 480
---

Credit: 
"conath"@ tonymacx86.com  
"Rehabman"@ tonymacx86.com  

本身黑苹果选好硬件安装大体不难，主要还是不通的硬件之间需要一些调整来解决一些小问题。目前我的配置大概如下：
主板：Gigabyte Z170XP-SLI  
CPU: i7-6700k  
显卡: XFX RX 480  

![system](/assets/img/system_info1.png)
剩下的配置因为跟前期安装联系不大，所以就先不提及。我主要是按照conath的方法安装了hackintosh并且能让RX480加速。Geekbench openCL大约130000分。
![openCL](/assets/img/openCL.png)


有两个SSD和一个HGST 4TB储存盘。两个SSD分别装了Windows 10和macOS 10.12.3。储存盘分了3个区：macOS的储存，windows 10的游戏，和time machine。
![disk](/assets/img/disk_info.png)

本文主要是记载下怎么给rx480加速（macOS里现在还没有相应的驱动，据说10.12.4也没有，不清楚今年WWDC的10.12.4会不会支持），怎么在windows和mac之间切换以及后期遇到的一些问题提怎么解决。至于安装hackintosh会稍微简略一些。
---
# 1. 安装10.12.3

A）选好硬件

B）装好PC（此时先别安装RX480，用cpu里的核显）

C）用unibeast制作安装盘+把multibeast放到USB里

D）开机，用unibeast装好macOS幷通过mutibeast安装驱动

* 这里在mutibeast里我选的是这些：
* UEFI Boot mode
* Audio - Realtek ALCXXX - ALC1150 + Option 3 Port(5.1) Audio
* Disk - AHCI
* Miassets/scgaopenCL.png.21
* Network - IntelMausiEthernet v2.2.0
* USB - All
* Customize - Graphics Configuration - HD 530
* Customize - System Definition - iMac 17,1

E) 这个时候，这台hackintosh应该能正常启动，上网。但是声音可能会有点问题，屏幕左上角会闪，以及还有很多其他的小问题。

F) 下载Clover Configurator, mount EFI, 用clover configurator 打开config.plist

G) 去SMBIOS, 点魔法棒，选择iMac 17,1 - 点shake，然后复制生成的serial number。

H) www.checkcoverage.apple.com，搜索刚生成的号码，如果显示错误，那么就可以用。

I) 打开terminal，然后输入 uuidgen ，把UUID复制到Clover Configurator SMBIOS里的SmUUID。

J) 把之前生成的serial number复制到Board Serial Number 然后加五个随机的HEX数字（0-9，A-F）

K）保存，重启，关机。（我的iMessage在这一步就已经可以用了，如果你的不行， 可以看tonymacx上的Fix iMessage）

# 2. 安装RX 480

A）进入 /System/Library/Extensions/ 把AMDRadeonX4100复制到桌面，右键open contents打开Info.plist然后找到<key>IOPCIMatch</key>这一行。把“0x67DF1002“添加到<stirng>里。保存

B）把桌面的这个修改过的AMDRadeonX00.kext放到KextUtility.app（需要下载）来安装。

C）打开Clover Configurator - Graphics 

* 点Inject EDID = on, 
* FB Name = Dayman, 
* ig-platform-id = 0x1912, 
* Load VBios = off,
* Patch Bios = on,
* Inject Intel = off,
* Inject ATI = on,
* 进入ACPI
* Fix Display = on
* 进到Devices
* Fake ID - ATI - 0x67DF1002
* 进到Boot
* Darkwake = 8,
* Timeout = 2,
* Default Boot Volume = 写你自己的macOS的硬盘的名字
* 进到Kernel and Kext Patches -ForceKextsToLoad
* 加一个 “\System\Library\Extensions\AMDRadeonX4100.kext"
* 和"\System\Library\Extensions\AMD9500COntroller.kext"
* 把这一段code加到config.plist的KextsToPatch里(credits to @Mork_vom_Ork)

Code: 
````
<dict>
<key>Comment</key>
<string>Change_#_of_RX4x0_CUs-(C)_by_okrasit_2016</string>
<key>Disabled</key>
<false/>
<key>Find</key>
<data>SLgCAAAAAQAAAEiJQ1THQ3wIAAAA</data>
<key>Name</key>
<string>AMDRadeonX4100</string>
<key>Replace</key>
<data>SLgEAAAAAQAAAEiJQ1THQ3wSAAAA</data>
</dict>
<dict>
<key>Comment</key>
<string>Remove_CU_limit_of_RX4x0-(C)_by_okrasit_2016</string>
<key>Disabled</key>
<false/>
<key>Find</key>
<data>D0LIiYuAAAAARIizmQAAAESIcyA=</data>
<key>Name</key>
<string>AMDRadeonX4100</string>
<key>Replace</key>
<data>kJCQiYuAAAAARIizmQAAAESIcyA=</data>
</dict>
<dict>
<key>Comment</key>
<string>Change_init_from_BAFFIN_to_ELLESMERE-(C)_by_Fl0r!an_2016</string>
<key>Disabled</key>
<false/>
<key>Find</key>
<data>6EmF/v++SAEAAEyJ9w==</data>
<key>Name</key>
<string>AMDRadeonX4100</string>
<key>Replace</key>
<data>6EbkAAC+SAEAAEyJ9w==</data>
</dict>
<dict>
<key>Comment</key>
<string>PP_DisablePowerContainment=1</string>
<key>Disabled</key>
<false/>
<key>InfoPlistPatch</key>
<true/>
<key>Name</key>
<string>AMD9500Controller</string>
<key>Find</key>
<data>PGtleT5QUF9EaXNhYmxlUG93ZXJDb250YWlubWVudDwva2V5PjxpbnRlZ2VyPjA8L2ludGVnZXI+</data>
<key>Replace</key>
<data>PGtleT5QUF9EaXNhYmxlUG93ZXJDb250YWlubWVudDwva2V5PjxpbnRlZ2VyPjE8L2ludGVnZXI+</data>
</dict>
<dict>
<key>Comment</key>
<string>Change "R9xxx" to "RX 480" by CONATH</string>
<key>Disabled</key>
<false/>
<key>Find</key>
<data>
OSB4eHgAQVRZLFBhcnQjAA==
</data>
<key>Name</key>
<string>AMD9500Controller</string>
<key>Replace</key>
<data>
WCA0ODAAAAAAAAAAAAAAAA==
</data>
</dict>
````

保存，关机，开机。
进入BIOS选择核显启动（非常重要）

B）把RX480插到第一个PCIE（有反应插在第二个接口不行的），然后把显示器的线接到RX480上。开机，等很久，然后应该就可以了。

要等很久是因为启动的时候用的是核显，所以显示器连在RX480上不会输出任何信号，需要等到进入macOS后才能显示。

# 3. 优化hackintosh
上面这两步基本都是按照conath的步骤来的， 中间根据我的硬件修改了一些过程，但是似乎现在只能用这种办法来加速RX480，我写的也比较简单，大家可以看conath的原帖。
后面是我加上去的一些优化和出现的问题的解决方法。

A) 我发现的第一个问题是音响接后面版的line out没有声音。

首先可以试试更改一下mutibeast里面audio的驱动如果不能解决。按照这个帖子：

https://www.tonymacx86.com/threads/no-audio-devices-realtek-alc-applehda-guide.143752/

B）Facetime摄像头

我买了个logitech C615,可用。一些其他型号应该也可以。

C) handoff and continuity

需要买macbook或者imac上的蓝牙模块加转换头，我买的是BCM94360CD和一个adapter，亚马逊和ebay都能买到。装上去之后可以跑一下github上的一个开源软件叫Continuity Activation Tool。我的一开始不行，等了半天之后就可以了。现在唯一不行的就是Unlock with Apple Watch。这个选项可以选但是login的时候没有自动解锁。

D)Final Cut Pro

最新版用不了（不支持RX 480，等更新），但是10.2.3可以用。

E) Power Management

https://www.tonymacx86.com/threads/quick-guide-to-generate-a-ssdt-for-cpu-power-management.177456/

到这里如果你只用macOS基本小问题都能解决了。可以算是一台完美的黑苹果直到下一次系统更新。

F) 睡眠后不能用chrome和看youtube，facetime也有问题

不要手动睡眠。如果非要手动睡眠，把chrome的setting里use hardware acceleration 关了就可以用chrome了。还没找到这个问题完美的解决方案。

# 4. 双系统

为了玩overwatch，我必须要装一个windows。所以又买了块SSD然后装了windows。发现每次启动需要把HDMI线拔了换到主板上然后进入bios启动windows再换回显卡上非常麻烦。所以找到了如下解决方案：
HDMI switch
可以用遥控器控制主板还是显卡的HDMI输入，这样每次换windows的时候就方便多了。
我用的是IOGEAR的HDMI switch，很好用。

# 5. 储存盘分区

因为macOS下用的是HFS+, windows用NTFS，所以如果想Mac和windows共用一个分区需要在windows下安装HFS+的程序或者反过来在Mac下安装NTFS的程序。但是我不需要共用所以现在macOS里分区，把windows要用的分成FAT，然后再在windows下erase成NTFS就可以了。


最后说一句，hackintosh虽然比较有意思也能用更便宜的价格获取更高的性能，但是比较耗时耗力。推荐有一台或以上其他主力机。
happy hackintoshing :)



