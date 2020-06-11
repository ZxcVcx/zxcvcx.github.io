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

下面来一段更新日志：

#### [OpenCore 0.5.9](https://github.com/acidanthera/OpenCorePkg/releases)

* Added full HiDPI support in OpenCanopy
* Improved OpenCanopy font rendering by using CoreText
* Fixed light and custom background font rendering
* Added `Boot####` options support in boot entry listing
* Removed `HideSelf` by pattern recognising `BOOTx64.efi`
* Added `BlacklistAppleUpdate` to avoid Apple FW updates
* Fixed accidental tool and NVRAM reset booting by default
* Fixed unrecognised select `com.apple.recovery.boot` entries
* Changed NVRAM reset not to erase `BootProtect` boot options
* Improved boot performance when picker UI is disabled
* Enforced the use of builtin picker when external fails
* Fixed warnings for empty NVRAM variables (e.g. rtc-blacklist)
* Added `ApplePanic` to store panic logs on ESP root
* Fixed `ReconnectOnResChange` reconnecting even without res change
* Fixed OpenCanopy showing internal icons for external drives
* Fixed OpenCanopy launching Shell with text over it
* Added partial hotkey support to OpenCanopy (e.g. Ctrl+Enter)
* Added builtin text renderer compatibility with Shell page mode
* Fixed `FadtEnableReset` with too small FACP tables and some laptops
* Fixed CPU detection crash with QEMU 5.0 and KVM accelerator
* Removed `RequestBootVarFallback` due to numerous bugs
* Added `DeduplicateBootOrder` UEFI quirk
* Removed `DirectGopCacheMode` due to being ineffective
* Fixed assertions on log exhaustion causing boot failures
* Fixed builtin text renderer failing to provide ConsoleControl
* Fixed compatibility with blit-only GOP (e.g. OVMF Bochs)
* Fixed ignoring `#` in DeviceProperty and NVRAM `Delete`
* Renamed `Block` to `Delete` in `ACPI`,`DeviceProperties`, and `NVRAM`
* Added MacBookPro16,2 and MacBookPro16,3 model codes
* Added PCI device scanning policy support (e.g. VIRTIO)
* Improved playback performance in AudioDxe
* Updated builtin firmware versions for SMBIOS and the rest
* Added improved CPU type detection for newer CPU types
* Added ConfigValidity utility and improved config validation
* Added serial port initialisation for serial debug logging
* Disabled empty debug log file creation to avoid ESP cluttering
* Added `TscSyncTimeout` quirk to workaround debug kernel assertions
* Added first-class Windows support to bless model
* Fixed `LapicKernelPanic` kernel quirk on 10.9
* Added prebuilt version of `CrScreenshotDxe` driver
* Fixed Hyper-V frequency detection compatibility
* Added `SysReport` option for DEBUG builds to dump system info
* Fixed crashes on some AMD firmwares when performing keyboard input

#### [AppleALC 1.5.0](https://github.com/acidanthera/AppleALC/releases)

* Update ALC283 layout-id 88 by xiaoleGun
* Fixed accidental reading of `alc-layout-id` on non-Apple firmwares
* Add patch to fix internal mic gain adjustment Conexant CX8050
* Move ALC255 layout-id 7 to layout-id 86
* Added ALC257 layout-id 86 for Lenovo T480 by armenio
* Fixed can't activate mute problem Conexant CX8070 layout-id 15 by lietxia
* Added ALC255 layout-id 20 for DELL 7447 by was3912734. Add Subwoofer drive.
* Added ALC662 layout-id 18 for MP67-DI/ESPRIMO Q900 by ryahpalma
* Added ALC256 layout-id 19 for Matebook X Pro 2019 by Durian-Life
* Added ALC256 layout-id 76 (4CH) for Matebook X Pro 2019 by Durian-Life

#### [VirtualSMC 1.1.4](https://github.com/acidanthera/VirtualSMC/releases)

 * Fixed incorrect revision reporting on T2 models (e.g. Macmini8,1)

#### [RTCMemoryFixup 1.0.6](https://github.com/acidanthera/RTCMemoryFixup/releases)

* Fix reading of key rtc-blacklist from NVRAM (only 4 bytes could be read)
* rtcfx_exclude can be combined with rtc-blacklist

#### [IntelMausi 1.0.3](https://github.com/acidanthera/IntelMausi/releases)

* Merged changes from 2.5.1d1

#### [dmidecode 3.2c](https://github.com/acidanthera/dmidecode/releases)

* Update to 5b3c8e99 with SMBIOS 3.2 improvements

#### [WhateverGreen 1.4.0](https://github.com/acidanthera/WhateverGreen/releases)

* Added 0x3EA6, 0x8A53, 0x9BC4, 0x9BC5, 0x9BC8 IGPU device-id
* Fixed `framebuffer-conX-alldata` patching regression
* Added `disable-hdmi-patches` device property alias to `-igfxnohdmi`

#### [Lilu 1.4.5](https://github.com/acidanthera/Lilu/releases)

* Fixed newer CPU generation detection
* Added failsafe versions of CML framebuffers

#### [VoodooInput 1.0.6](https://github.com/acidanthera/VoodooInput/releases)

* Reduced memory consumption and CPU usage
* Fixed dragging issues on some touchpads

#### [VoodooPS2 2.1.5](https://github.com/acidanthera/VoodooPS2/releases)

* Upgraded to VoodooInput 1.0.6
* Added logo + print scr hotkey to disable trackpad

然后先按[教程](https://dortania.github.io/vanilla-laptop-guide/)一步一步来：

## 1 Preparing a full macOS Installer (requires macOS)

封装镜像，写U盘里，完了

## 2 Adding Base OpenCore Files

