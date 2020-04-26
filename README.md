### 0. 前言

### 1. 硬件配置
 |配件|型号|
 |---|---|
 |CPU|Intel i9-9900KF|
 |主板|华硕-ROG-STRIX Z390-I GAMING|
 |无线网卡|Intel Wireless-AC 9560, 主板集成，未更换博通免驱网卡|
 |有线网卡|Intel I219-V 千兆网卡, 主板集成|
 |显卡|华硕-ROG-STRIX-RX5700XT-O8G|
 |内存|美商海盗船 统治者白金 DDR4 3200 16G * 2|
 |存储|西数 SN750 1TB * 2|

### 2. 常用术语
- Vanilla：这里特指一种黑苹果的安装方式，也是当前唯一推荐的安装方式，其他的方式还有Unibeast，Multibeast，Distros，这三种都不推荐使用。本文就是按照Vanilla步骤组织黑苹果的安装顺序。
- Clover：
- OpenCore：

### 3. 硬件准备
- 安装环境：MacAir 13, Mac OS Catalina 10.15.3
- USB配置：SanDisk CZ430酷豆 USB3.1 128GB

### 4. 软件准备
- 获取gibMacOS：https://github.com/corpnewt/gibMacOS ，下载压缩包直接解压
- 获取MountEFI：https://github.com/corpnewt/MountEFI

### 5. 制作安装U盘
- 制作安装镜像
  - 下载MacOS镜像：执行gibMacOS.command
    - 选1，下载最新版本
  <!-- ![](https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-1.png) -- Can't align to the left, be check in the future --><div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-1.png"/>
    - 下载完毕
  - 制作Catalina安装程序：执行BuildmacOSInstallApp.command命令
    - 将macOS Downloads目录拖拽到命令行窗口,目录名一定要到最底一层(gibMacOS-master/macOS\ Downloads/publicrelease/061-96006\ -\ 10.15.4\ macOS\ Catalina )，继续执行
<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-5.jpg"/>
    - 执行完毕，生成安装程序：Install macOS Catalina.app
    - 此处有图
  - 格式化U盘:这样会创建两个分区：MyVolumn和EFI
    - 卷名修改为MyVolumn，格式为Mac OS Extended(日志)，分区为GUID；
<div align=left><img 此处有图  src="https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-1.png"/>
  - 制作Catalina安装U盘，执行命令(目录名需要根据实际修改)：sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
    - 此次有图
 - 挂载OpenCore的EFI分区，执行./MountEFI.command
   - 这时候会出现一个空的EFI分区
### 6. 设置EFI
- BOOT？
- 删除以下Drivers
- 删除Tools下的所有文件，可以保留OpenShell.efi
- 确认最终结果

### 7. 配置OpenCore
- 配置规则
  - SSDTs和custom DSDTs(.aml)放在ACPI目录
  - Kexts(.kext)放在Kexts目录
  - Firmware drivers(.efi) 放在Drivers目录
### 8. 设置CONFIG.PLIST（Coffee Lake配置）

### 9. BIOS设置
- 禁止
- 真的好吗
- 打开

### 10. 安装

### 11. 后处理
- 脱离U盘启动
- 优化
