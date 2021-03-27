#运行/Intel-NUC8i5BEH-Hackintos

我的博客  www.runebalot.cn

-若要引用或转载本EFI，请务必注明出处，所有内容仅供个人使用和学习参考，严禁用于商业用途（tb奸商先死ma）

<p><center>中文(当前)|<a href="https://github.com/TokiharaSay/MSI-B360M-MORTAR-Hackintosh/blob/main/README.md">English</a></center></p>

|支持macOS版本| 10.15.x-11.x|
|:-|-|
|引导加载程序| OpenCore 0.6.7|
|CPU平台| Coffee Lake（i5-8259U CPU）|

|系统配置| |注意事项|
|:-|:-:|:-:|
|CPU | i5-8259U  | XCPM工作，但不确定CPU调度是否正确|
|图形| Intel Iris Plus Graphics 655 | Type-C支持转接到DP/HDMI 以及HDMI正常|
|BIOS | 087 |请看使用说明|
|声音| Realtek ALC235 |板载音频|
|磁盘| KIOXIA RC10 500G| NVME插槽|
|显示器|3840x2160 15.6'| TYPE-C支持DP1.2 我使用HDMI |
|网卡| Intel I219V6+BCM94360CS2+板载AC9560 |CS2需要硬改读卡器/不接NVME |
### 问题
* __我是硬改读卡器不能用读卡器了__
* __Type-C的雷电不能用只能当全功能Type-C使用__

### 系统相关
- Windows 和 macOS 时间不同步

- Windows 中打开命令行，输入 Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1

- 重启到 macOS，联网同步时间，再次进入 Windows 即可正常显示时间

### 使用说明
- 默认使用AirportItlwm是Catalina版本，有需要请自行更换

- BIOS设置
  - Devices -> USB -> Port Device Charging Mode: off
  - Devices -> USB -> USB Legacy -> Disabled
  - Security -> Thunderbolt Security Level: Legacy Mode
  - Power -> Wake on LAN from S4/S5: Stay Off
  - Boot -> Boot Configuration -> Network Boot: Disable
  - Boot -> Secure Boot -> Disable

- 使用 [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)生成 MLB SystemSerialNumber

- SystemUUID请在Win获取 在命令提示符下输入wmic 再输入csproduct 或 csproduct list full

- 使用以下命令来构建EFI
```bash
git clone https://github.com/TokiharaSay/Intel-NUC8i5BEH-Hackintos
cd Intel-NUC8i5BEH-Hackintos
chmod +x **/*.sh
./build.sh
```
你可以在 `Output` 目录下找到生成的 EFI。OpenCore 配置文件路径为 `Output/EFI/OC/config_sample.plist`，你需要自行生成 SMBIOS 信息（遵循 [这篇教程](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html) 的步骤，使用 `你需要的机型`）并填入配置文件中，然后将 `config_sample.plist` 重命名为 `config.plist`。

### 感谢以下朋友的帮助

- OpenCore技术交流群 群友解决雷电（不提供文件，因为不完美）

- [SukkaW](https://github.com/SukkaW)

