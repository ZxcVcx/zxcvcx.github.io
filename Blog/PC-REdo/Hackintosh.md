---
layout: default
---



# Hackintosh 
设备 魔霸3 G531GU 买ROG都是臭打游戏的，没人改那残废BIOS也没人配置黑苹果啥的，想玩本老老实实买蓝天模具！！！

老实说不是很想搞，这东西没啥用，而且吃力不讨好，会对别的系统有影响。。。

注：此文章将大量引用英文片段。建议搞个好点儿的U盘，起码支持 USB 3.1，不然很难受。 

***

## 1 目标列表

- [x] 系统的完全重置
- [ ] OpenCore重新配置
- [ ] 待定

## 2 系统重置
格盘不解释，EFI太脏了，重搞。

## 3 OpenCore 配置

参考资料：
OpenCore 官方文档 https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.pdf

某博客
https://blog.xjn819.com/?p=543

dortania的教程
https://github.com/dortania
https://dortania.github.io
https://dortania.github.io/vanilla-laptop-guide/

现在 OpenCore 日渐完善，但是仍处在beta阶段，写文章的时间是 6/10/2020，选择的 OpenCore 版本号 0.5.9 。

然后先按[教程](https://dortania.github.io/vanilla-laptop-guide/)一步一步来：

## 1PREPARATION
### 1.1 Preparing a full macOS Installer (requires macOS)

封装镜像，写U盘里，完了

### 1.2 Adding Base OpenCore Files
Drivers 保留`AudioDxe.efi`,`CrScreenshotDxe.efi`,`OpenRuntime,efi`，其余删除；
Tools 保留`OpenShell.efi`，其余删除。

## 2 CONFIGURING OPENCORE

### 2.1 Gathering files

####  Firmware Drivers
HfsPlus.efi
OpenRuntime.efi

####  Kext
VirtualSMC.kext
Lilu.kext
SMCSuperIO.kext
SMCProcessor.kext
WhateverGreen.kext
AppleALC.kext
VoodooTSCSync.kext
NVMeFix.kext

####  SSDTs
SSDT-AWAC.aml
SSDT-EC-USBX.aml
SSDT-GPIO.aml
SSDT-PLUG.aml
SSDT-PMC.aml
SSDT-PNLFCFL.aml

aml文件需要根据自身情况自己编译

### 2.2 OpenCore Config

## 完事儿了


