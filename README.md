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

### 3. 硬件准备
- 安装环境：MacAir 13
- USB配置：SanDisk CZ430酷豆 USB3.1 128GB

### 4. 软件准备
- 获取gibMacOS：https://github.com/corpnewt/gibMacOS ，下载压缩包直接解压
- 获取MountEFI：https://github.com/corpnewt/MountEFI


### 5. BIOS设置
- 禁止
- 打开
### 6. 制作安装U盘
- 制作安装镜像
  - 执行gibMacOS.command，下载MacOS镜像
  - 执行1，选择最新版本
  <!-- ![](https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-1.png) -- Can't align to the left, be check in the future -->
  <div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-1.png"/>
 
  - 下载完毕
  - 执行BuildmacOSInstallApp.command命令，下载OpenCore
  - 将macOS Downloads目录拖拽到命令行窗口，继续执行
- 格式化U盘:这样会创建两个分区：MyVolumn和EFI
  - 卷名修改为MyVolumn
  - 格式为Mac OS Extended(Journaled)
  - Scheme为GUID
  - 执行命令(目录名需要根据实际修改)：sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
 - 执行./MountEFI.command，挂接OpenCore的EFI环境
### 7. 配置OpenCore
 
