#Run/Intel-NUC8i5BEH-Hackintos

My blog www.runebalot.cn

- If you want to quote or reprint this EFI, please be sure to indicate the source, all content is for personal use and learning reference only, and it is strictly prohibited for commercial use (tb profiteer first die ma)

<p><center>English(当前)|<a href="https://github.com/TokiharaSay/Intel-NUC8i5BEH-Hackintos/edit/main/README_CN.md">中文</a></center></p>

|Support macOS version| 10.15.x-11.x|
|:-|-|
|Bootloader| OpenCore 0.6.7|
|CPU Platform| Coffee Lake (i5-8259U CPU)|

|System Configuration| |Notes|
|:-|:-:|:-:|
|CPU | i5-8259U | XCPM works, but not sure if the CPU scheduling is correct |
|Graphics| Intel Iris Plus Graphics 655 | Type-C supports transfer to DP/HDMI and HDMI is normal|
|BIOS | 087 |Please see the operating instructions|
|Sound| Realtek ALC235 |Onboard Audio|
|Disk| KIOXIA RC10 500G| NVME Slot|
|Display|3840x2160 15.6'| TYPE-C supports DP1.2 I use HDMI |
|Network Card| Intel I219V6+BCM94360CS2+ onboard AC9560 |CS2 needs to change the card reader/NVME is not connected |
### Question
* __I am hard to change the card reader and cannot use the card reader__
* __Type-C's lightning cannot be used, but can only be used as a full-featured Type-C__

### System related
- Windows and macOS time are not synchronized

-Open the command line in Windows and enter Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1

-Restart to macOS, synchronize the time on the Internet, and enter Windows again to display the time normally

### Instructions for use
-The default AirportItlwm is the Catalina version, please replace it if necessary

- BIOS settings
  - Devices -> USB -> Port Device Charging Mode: off
  - Devices -> USB -> USB Legacy -> Disabled
  - Security -> Thunderbolt Security Level: Legacy Mode
  - Power -> Wake on LAN from S4/S5: Stay Off
  - Boot -> Boot Configuration -> Network Boot: Disable
  - Boot -> Secure Boot -> Disable

- Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate MLB SystemSerialNumber

- Obtain SystemUUID in Win. Enter wmic at the command prompt and then enter csproduct or csproduct list full

- Use following command to build the EFI.

```bash
git clone https://github.com/TokiharaSay/Intel-NUC8i5BEH-Hackintos
cd Intel-NUC8i5BEH-Hackintos
chmod +x **/*.sh
./build.sh
```

Find generated EFI under `Output` folder. Find OpenCore config at `Output/EFI/OC/config_sample.plist` and fill in your own SMBIOS (Follow [the guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html), use  `model you need`) then rename `config_sample.plist` to `config.plist`.


### Thanks for the help of the following friends

- OpenCore technology exchange group, group friends solve thunder and lightning (no files are provided because they are not perfect)

- [SukkaW](https://github.com/SukkaW)
