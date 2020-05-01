### 0. 前言

### 1. 硬件配置
 |配件|型号|
 |---|---|
 |CPU|Intel i9-9900KF|
 |主板|华硕-ROG-STRIX Z390-I GAMING|
 |无线网卡|Intel Wireless-AC 9560, 主板集成，未更换博通免驱网卡|
 |有线网卡|Intel I219-V 千兆网卡, 主板集成|
 |声卡|ROG SupremeFX 8 声道 高清晰音频编码解码器Realtek S1220A，主板集成|
 |显卡|华硕-ROG-STRIX-RX5700XT-O8G|
 |内存|美商海盗船 统治者白金 DDR4 3200 16G * 2|
 |存储|西数 SN750 1TB * 2|
 |键盘|罗技 K580|
 |鼠标|罗技 Mx Master2|

### 2. 常用术语
- Vanilla：这里特指一种黑苹果的安装方式，也是当前唯一推荐的安装方式，其他的方式还有Unibeast，Multibeast，Distros，这三种都不推荐使用。本文就是按照Vanilla步骤组织黑苹果的安装顺序。
- Clover：
- OpenCore：
- SSDTs：

### 3. 硬件准备
- 安装环境：MacAir 13, Mac OS Catalina 10.15.3
- U盘：SanDisk CZ430酷豆 USB3.1 128GB

### 4. 软件准备
- 获取gibMacOS：https://github.com/corpnewt/gibMacOS ，下载压缩包直接解压
- 获取MountEFI：https://github.com/corpnewt/MountEFI
- OpenCore 0.5.7，Debug和Release版本各下一份备用: https://github.com/acidanthera/OpenCorePkg/releases
- AppleSupportPkg：https://github.com/acidanthera/AppleSupportPkg/releases 
- SSDTTime: https://github.com/corpnewt/SSDTTime
- ProperTree：https://github.com/corpnewt/ProperTree
- MaciASL : https://github.com/acidanthera/MaciASL/releases

### 5. 制作安装U盘
- 下载MacOS镜像：
  - 执行gibMacOS.command
  - 选1，下载最新版本<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/5-1.jpg"/>
  - 下载完毕
- 制作Catalina安装程序：
  - 执行BuildmacOSInstallApp.command命令
  - 将macOS Downloads目录拖拽到命令行窗口,目录名一定要到最底一层(gibMacOS-master/macOS\ Downloads/publicrelease/061-96006\ -\ 10.15.4\ macOS\ Catalina )，继续执行
  - 执行完毕，生成安装程序：Install macOS Catalina.app<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/5-3.jpg"/>
  - 将Install macOS Catalina.app复制到/Applications目录下
- 格式化U盘:
  - 这样会创建两个分区：MyVolume和EFI，EFI缺省未挂载，所以当前还看不见
  - 卷名修改为MyVolume，格式为Mac OS Extended(日志)，分区为GUID；<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/5-4.jpg"/>
- 制作Catalina安装U盘，执行命令(目录名需要根据实际修改)：sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
- 挂载OpenCore的EFI分区，执行./MountEFI.command
  - 这时候会出现一个空的EFI分区
 
### 6. 清理EFI中不必要的文件（为了兼容老平台的驱动）
- 复制OpenCorePkg的EFI目录新的目录，下文统称“OC”
- 确保目录结构完整，包括BOOT,OC,Resources这三个目录
- 删除OC\Drivers目录的以下文件：
  - OpenUsbKbDxe.efi
  - NvmExpressDxe.efi
  - XhciDxe.efi
  - HiiDatabase.efi
  - HiiDatabase.efi
- 删除Tools下的所有文件，可以保留OpenShell.efi<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/6-1.jpg"/>

### 7. 配置OpenCore中的固件和驱动
- 驱动的选择是高度定制化的，需要根据实际硬件配置选择，这里列出的仅仅匹配我现在的硬件配置，仅供大家参考。建议在实际配置的时候，仔细研读OpenCore Vanilla Guide中的Gathering file章节，做到心中有数。完整的过程大致分为两个阶段，本章（包括后续量章）是第一阶段，主要是确保硬件基本可用，在后处理章节还有硬件进一步的调优。
- 复制固件和驱动到OC目录（含特殊说明）
  - “Gathering file”章节有完整的下载链接，大部分直接复制到本地解压即可，有一部分在OpenCore 0.5.7和AppleSupportPkg这两个包里
  - 我选择的都是Release版本，如果后续出问题，可以替换成相应的DEBUG版本调试
  - 复制规则
    - SSDTs和custom DSDTs(.aml)放在ACPI目录（下一章再处理）
    - Kexts(.kext)放在Kexts目录
    - Firmware drivers(.efi) 放在Drivers目录
  - Kext必须从“驱动名.kext”这个目录作为顶层节点开始复制，如VirtualSMC.kext，里面包括Contents子目录，info.plist，MacOS子目录下是实际的驱动文件
  - 类似“IntelMausiEthernet”（Intel以太网卡驱动）有点特殊，Github上归档的是xcode工程，我是下载后只有用xcode打开，才能看到Products目录下的IntelMausiEthernet.kext的驱动。<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/7-3.jpg"/>
- 最终的完成清单如下，<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/7-2.jpg"/>
- config.plist中需要添加相应配置，遗留到第9章处理

### 8. 配置SSDTs
- 如果是第一次接触，需要仔细阅读，搞清楚之后实际操作很简单
  - 仔细阅读https://dortania.github.io/Getting-Started-With-ACPI/
  - 有Easy Way和Long Way这两种选择，我这里用的是Easy Way
- 在目标机器（就是要装黑苹果的机器，不要弄错了）上执行SSDTTime
  - 选择4：Dump DSDT
  - 选择3：FakeEC
  - 选择2：PluginType
  - 导出的文件存放在Results子目录下
- 根据平台类型，挑选涉及的aml文件，我这里选的是Desktop-CoffeLake
- 复制aml文件到OC对应的目录
- aml文件有重复，需要单独说明
- config.plist中需要添加相应配置，遗留到第9章处理

### 9. 设置CONFIG.PLIST（Coffee Lake配置）
- 将下载的OpenCore\Docs里的Sample.plist改名config.plist，并复制到OC
- 运行ProperTree，Cmd + Shift + R选取OC 
- ProperTree会自动在config.plist里添加SDDTs，kexts，efi，对于存在依赖关系的会自动排序，对于不需要的配置项会自动删除，非常方便
- 参考这个基于Coffee Lake的描述，逐个设置配置项：https://dortania.github.io/OpenCore-Desktop-Guide/config.plist/coffee-lake.html ，这里单列了一些推荐之外的调整，大家可以根据自己的情况调整：
  - 在设置aml的时候如果发现跟上一章不一致，以本章为准，可能需要重新下载编译aml？不一定
  - MISC->DEBUG->DisplayLevel：第一次安装时发现黑屏，后续调试的时候加上的，83，打印各种级别的日志，并记录日志
  - NVRAM->Add->7C...->boot-arg: 第一次安装时发现黑屏，后续调试的时候加上的agdpmod=pikera。跟显卡相关，上网搜的,试试看。
  - UEFI->OUTPUT->Resolution: 显示器是4K分辨率，字体太小，修改为1080p
  - UEFI->OUTPUT->TextRenderer: 用文本的渲染引擎SystemText
- 做一下最后的校验，有问题修复：https://opencore.slowgeek.com/
- 在ProperTree中保存设置，并将整个OC目录复制到U盘，至此完成安装盘的初始化制作

### 10. BIOS设置
|类型|推荐设置项|说明|
|---|---|---|
|禁止|Fast Boot| |
|禁止|VT-d|DisableIoMapper设置YES后可以打开|
|禁止|CSM| |
|禁止|Thunderbolt|不涉及|
|禁止|Intel SGX||
|禁止|Intel Platform Trust|没找到？|
|禁止|CFG Lock||
|打开|VT-x||
|打开|Above 4G decoding||
|打开|Hyper-Threading||
|打开|Execute Disable Bit||
|打开|EHCI/XHCI Hand-off||
|打开|OS type: Windows 8.1/10 UEFI Mode||
|打开|DVMT Pre-Allocated(iGPU Memory): 64MB|没有集显，不涉及|

### 11. 安装
- 由于第一次安装时出现黑屏，为了调试方便，XXX和XXX文件替换成对应的DEBUG版本
- BIOS中选择从U盘启动，此处有图
- 第一次执行时，选择情况NV，此处有图
- 选择安装External
- 重启
- 看到安装界面
- 运行DiskD，进行分区，如果已经分区可以略过，此处有图
- 按照常规步骤安装Catalina直到完成
- 特别说明：
  - 推荐准备一个支持Mac OS的键盘
  - 安装过程中，如果鼠标无法使用（我就遇到了），可以cmd+F5打开语音，根据提示用键盘执行安装步骤
  - 安装的最后步骤需要访问网络，由于我没有替换成黑苹果免驱的无线网卡，只能使用有线网络，如果不具备这个条件，一个规避的方法是使用无线中继路由器，无线网络转有线。这里推荐一个产品，中兴的H570A中继路由器，2014年出品，早就停产了，不过竟然还能在京东上扎到。它最大的特点是支持USB供电，这样直接用电脑后部的USB口供电，路由器的网口接电脑的网口，这样就不依赖市电和网络布线使用有线网络了，而且这个路由器非常小巧，长宽高=5.2CM*3.1CM*2.3CM，可以直接挂在机箱后部非常简洁，对我来说简直是神器。支持双频，5G带宽433M，勉勉强强也够用了。

### 12. 后处理
- 设置帧缓冲深度：安装好之后默认是30位的，显示器只支持24位，所以颜色偏紫
- 脱离U盘启动
- 优化
  - EFI Version在win下gpu-z可以查看
  - 电源管理的参数没有注入，看他另外的一个帖子
- Enable TRIM for Solid State Drives
  - Open Terminal and enter the following command:
  - sudo trimforce enable
  - Verify TRIM was enabled in System Report:
  - Hide Windows Drive in macOS
    - Follow these instructions to prevent the Windows drive from automatically mounting in macOS:
    - Open Terminal and enter the following command to get the Volume UUID:
    - diskutil info /Volumes/{YOUR_WINDOWS_DRIVE_NAME}
    - Enter sudo vifs to add the following line to /etc/fstab:
    - UUID={YOUR_UUID} none ntfs rw,noauto
    - Restart your system and the Windows partition will no longer automatically mount.
- Use slide=0 as as a boot flag to avoid any random freezes when using macOS on the Z390 platform.
- Enabling USB3 Speeds & Detection on Z390 Ports: To get USB3 speeds working on a motherboard the USB ports must be mapped correctly with an SSDT-USB.aml file placed in/Volumes/EFI/EFI/CLOVER/APCI/patched/

### 待研究文章
- http://www.memacx.com/thread-7571-1-1.html
- https://insanelymac.gitbook.io/opencore-guide/
- https://www.reddit.com/r/hackintosh/comments/dsvg95/really_want_to_use_this_5700xt/
- https://www.tonymacx86.com/threads/amd-radeon-rx5700-or-5700xt.285976/
- https://www.insanelymac.com/forum/topic/343461-kext-tired-of-low-geekbench-scores-use-radeonboost/
- https://heipg.cn/drivers/whatevergreen-137.html
- https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.Radeon.en.md
- https://github.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI
- https://github.com/shiruken/hackintosh
### Hint
- Make sure to have kexts like Lilu and VoodooPS2Controller are to be injected first before kexts that require them like WhateverGreen, VirtualSMC, keyboard/Mouse/Trackpad and etc.

- 2.3.2.2 没核心显卡的用户，带f的cpu (e.g. 9100f 9900kf), Xeon等不带核心显卡的用户不需要管这项，直接把AAPL,ig-platform-id选项卡删了。https://blog.xjn819.com/?p=543

- 目前已经解决问题，有色带问题的显示器是因为被mac默认设置成了10位色深，而显示器仅支持8位，所以出现了色带，解决办法下载ResXtreme，修改显示器色深为8位，修改完可以删除软件，重启不影响。我的经验是，在clove里填入edid的参数重启后没有任何改变，必须注入显示器edid驱动才可以。

- https://blog.daliansky.net/Intel-FB-Patcher-tutorial-and-insertion-pose.html
