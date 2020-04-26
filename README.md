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
- OpenCore 0.5.7，Debug和Release版本各下一份备用: https://github.com/acidanthera/OpenCorePkg/releases
- AppleSupportPkg：https://github.com/acidanthera/AppleSupportPkg/releases ，好像没有什么用，待确认；
- ProperTree：https://github.com/corpnewt/ProperTree

### 5. 制作安装U盘
- 下载MacOS镜像：
  - 执行gibMacOS.command
  - 选1，下载最新版本<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-1.png"/>
  - 下载完毕
- 制作Catalina安装程序：
  - 执行BuildmacOSInstallApp.command命令
  - 将macOS Downloads目录拖拽到命令行窗口,目录名一定要到最底一层(gibMacOS-master/macOS\ Downloads/publicrelease/061-96006\ -\ 10.15.4\ macOS\ Catalina )，继续执行<div align=left><img  src="https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-5.jpg"/>
  - 执行完毕，生成安装程序：Install macOS Catalina.app
  - 此处有图
  - 将Install macOS Catalina.app复制到/Applications目录下
- 格式化U盘:
  - 这样会创建两个分区：MyVolume和EFI，EFI缺省未挂载，所以当前还看不见
  - 卷名修改为MyVolume，格式为Mac OS Extended(日志)，分区为GUID；<div align=left><img 此处有图  src="https://github.com/sobravo/hackintosh/blob/master/img/gibMacOS-1.png"/>
- 制作Catalina安装U盘，执行命令(目录名需要根据实际修改)：sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
  - 此次有图
- 挂载OpenCore的EFI分区，执行./MountEFI.command
  - 这时候会出现一个空的EFI分区
 
### 6. 清理EFI中不必要的文件（为了兼容老平台的驱动）
- 复制OpenCorePkg的EFI目录
- 确保目录结构完整，包括BOOT,OC,Resources这三个目录
- 删除OC\Drivers目录的以下文件：
  - OpenUsbKbDxe.efi
  - NvmExpressDxe.efi
  - XhciDxe.efi
  - HiiDatabase.efi
  - HiiDatabase.efi
- 删除Tools下的所有文件，可以保留OpenShell.efi
- 确认最终结果，此处有图

### 7. 配置OpenCore中的驱动
- 驱动的选择是高度定制化的，需要根据实际硬件配置选择，这里列出的仅仅匹配我现在的硬件配置，仅供大家参考。建议在实际配置的时候，仔细研读OpenCore Vanilla Guide中的Gathering file章节，做到心中有数。完整的过程大致分为两个阶段，本章（包括后续量章）是第一阶段，主要是确保硬件基本可用，在后处理章节还有硬件进一步的调优。
- 配置规则
  - SSDTs和custom DSDTs(.aml)放在ACPI目录
  - Kexts(.kext)放在Kexts目录
  - Firmware drivers(.efi) 放在Drivers目录
- 注意事项
- 最终的完成清单如下，此处有图

### 8. 配置SSDTs
  
### 9. 设置CONFIG.PLIST（Coffee Lake配置）

### 10. BIOS设置
- 禁止
- 真的好吗
- 打开

### 11. 安装

### 12. 后处理
- 脱离U盘启动
- 优化
