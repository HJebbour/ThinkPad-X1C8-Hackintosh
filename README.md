# macOS on Lenovo Thinkpad X1 Carbon Gen 8 (20U9)

OpenCore-based EFI for Lenovo Thinkpad X1 Carbon 8th Generation | Model 20U9
<img align="right" src="https://avadirect-freedomusainc1.netdna-ssl.com/Pictures/500/Lenovo_ThinkPad_X1_Carbon_Gen_8_20U90030US.png" alt="Lenovo ThinkPad X1 Carbon Gen 8" width="394">

**Status: Work In Progress | Stable | Daily driver**

[![macOS](https://img.shields.io/badge/macOS-Monterey-blueviolet.svg)](https://www.apple.com/macos/monterey/)
[![Version](https://img.shields.io/badge/12.2-blueviolet.svg)](https://support.apple.com/en-us/HT212585#macos122)
[![OpenCore](https://img.shields.io/badge/OpenCore-0.7.7-blue.svg)](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.7.7)
[![Model](https://img.shields.io/badge/Model-20U9-red)](https://www.lenovo.com/us/en/p/laptops/thinkpad/thinkpadx1/x1-carbon-gen-8-/20u9005mus)

This template is forked from seven-of-eleven's repo Lenovo-ThinkPad-X1C7-OC-Hackintosh

**DISCLAIMER:**
As you embark on your Hackintosh journey you are encouraged to **READ** the entire README and [Dortania](https://dortania.github.io/getting-started/) guides before you start.

You can find a wealth of knowledge on [Reddit](https://www.reddit.com/r/hackintosh/), [TonyMacX86](https://www.tonymacx86.com) or [Google](https://www.google.com).

Should you find an error, or improve anything, be it in the config itself or in the my documentation, please consider opening an issue or a pull request to contribute.

### I am not responsible for any damages you may cause.

## Summary

<details>  

<summary><strong>WORKING ✅</strong></summary>
<br>

> ### Video and Audio
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Full Graphics Accleration (QE/CI)    | ✅   | `WhateverGreen.kext` & `AAPL,ig-platform-id` = 0900A53E & `device-id` = C89B0000 | -   |
| Audio Output                      | ✅   | `AppleALC.kext` with Layout ID = 71    | -   |
| Audio Speakers                       | ✅   | `AppleALC.kext` with Layout ID = 71    | You have to manually select the proper speakers (2 at the bottom rear). I can't get all 4 speakers to work together for now |
| Audio Input | ✅   | `AppleALC.kext` with Layout ID = 71    | Headset microphone is inconsistent and needs more testing   |
| Automatic Headphone Output Switching | ✅   | `AppleALC.kext` with Layout ID = 71    | -   |

> ### Power Management
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Battery | ✅    | `ECEnabler.kext`             | - |
| CPU Power Management (SpeedShift)    |    ✅  | `CPUFriend.kext` with `CPUFriendDataProvider.kext` | Idle at 800mhz
| iGPU Power Management        | ✅ | `SSDT-PLUG.aml` | - |
| NVMe Drive Battery Management | ✅     | `NVMeFix.kext`  | Generally, NVMe drives will drain more power than SATA drives.           |
| S3 Sleep / Hibernation Mode 3 | ✅ | - | - |

> ### Connectivity
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| WiFi                                       | ✅ | `AirportIltwm.kext`  | -       |
| Bluetooth                                  | ✅ | `IntelBluetoothFirmware.kext`, `BlueToolFixup.kext`, and `USBMap.kext` | - |
| Ethernet                                   | ✅ | `IntelMausi.kext` | -                  |
| HDMI 1.4                               | ✅ | BusID patching | Hotplug with 4K Resolution |
| USB 2.0 / USB 3.0 | ✅ | `USBMap.kext`   | Create your own USBMap.kext using [CorpNewt](https://github.com/corpnewt/USBMap) |
| USB 3.1 (Type-C)                           | ✅ | `USBMap.kext` and enable Thunderbolt 3 in `BIOS` | Hotplug |
| USB Power Properties in macOS              | ✅ | - | - |

> ### Display, TrackPad, TrackPoint, Keyboard, and Webcam
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Brightness Adjustments | ✅  | `WhateverGreen.kext`, `SSDT-PNLF.aml`, `enable-backlight-smoother` property, and `BrightnessKeys.kext`| `enable-backlight-smoother` property is optional for smoother birghtness adjustments |
| TrackPoint             | ✅  | `VoodooPS2Controller.kext`                                      | -       |
| TrackPad               | ✅  | `VoodooI2C.kext`, and `VoodooI2CHID.kext` | - |
| Built-in Keyboard      | ✅  | `VoodooPS2Controller.kext` | - |
| Webcam      | ✅  | `USBMap.kext` | - |

> ### macOS Continuity
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| iCloud, iMessage, FaceTime | ✅ | Whitelisted Apple ID, Valid SMBIOS   | See [Dortania / OpenCore-Install-Guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html)  |
| Handoff | ✅ | `AirportIltwm.kext` | - |

</details>  

<details>  
<summary><strong>NOT WORKING ❌</strong></summary>
<br>

| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Fingerprint Reader   | ❌ | - | Never gonna work.    |
| Wireless WAN         | ❌ | `DISABLED` in BIOS to save power.   | Unable to investigate as I have no need and my model did not come with WWAN |
| Internal Microphone         | ❌ | - | - |
| Fan Control / Multimedia Keys | ❌ | `YogaSMC.kext` | YogaSMC.kext needs to be updated in order to work with X1C8 |
| Continuty              | ❌    | - | Not working with Intel cards |
| AirDrop              | ❌    | - | Not working with Intel cards |

</details>  

<details>  
<summary><strong>UNTESTED ⚠️</strong></summary>
<br>

| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Thunderbolt 3                      | ⚠️ | - | No device to test |
| Boot chime                      | ⚠️ | - | Not yet tested |
| FireVault 2                      | ⚠️ | - | Not yet tested |
| Sidecar                      | ⚠️ | - | No device to test |
| ThinkPad USB-C Docking Station | ⚠️ | - | Will be tested soon |

</details> 

<details>  
<summary><strong>TO-DO ⏳</strong></summary>
<br>

| Feature                              | Status | Remarks                      |
| :----------------------------------- | ------ | ---------------------------- |
| Battery Life | ⏳ | Need time to thoroughly test battery life and compare with Windows 11 |
| Four Speakers | ⏳ | I need to find a proper way to combine the two outputs or wait for a new `AppleALC.kext` update |

</details>

## Introduction

<details> 
<summary><strong>THIS IS NOT A GUIDE!</strong></summary>
</br>

This is not a guide. It shoud only be used as a reference. I provide some tips and tricks I learned on my journey in building a hackintosh. The best way of using this is as a supplement to the OpenCore guide. If you have questions about how to setup your specific hardware, are unclear about what to do, or would like to see the settings I've used.

I understand that some may simply add the OC and Boot folders to their EFI folder. For clarity the EFI partition needs a folder called EFI that contains the Boot and OC folder.

```EFI
EFI (drive)
	EFI
	├── BOOT
	├── OC
```

It should work and your X1C8 should boot and work fine. **You will at minimum need to generate SMBIOS values if you want Apple services to work.** Note that all error reporting/logging has been turned off in the config.plist. You will have a difficult time trouble shooting with the setup provided. You can easily turn on the error reporting and logging if you follow the Dortania guide. Best of luck.

> **NOTE** if you simply wish to copy my EFI please do the following:
>
>1. [Generate SMBIOS values](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake-plus.html#nvram) and add them in the config.plist (Use MacBookPro16,3)
>2. Ensure the value of `showpicker` is  `true` in the config.plist file to provide the opencore menu when booting. 
>3. Prepare your install [USB](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
>4. Move the entire EFI folder (with your modifications) to the proper partition on your [USB](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#setting-up-opencore-s-efi-environment) (or [SSD](https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html) once the install is complete).
>5. [Install](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#double-checking-your-work) - You'll need to select F12 to get the boot menu options and **boot from the USB each time the computer restarts** until you've copied the EFI folder onto the hard drive. You may also need to select the correct boot option during install.

</details>  

<details> 
<summary><strong>THIS IS A GUIDE!</strong></summary>
</br>

- To install macOS follow the guides provided by [Dortania](https://dortania.github.io/OpenCore-Install-Guide/)
- Useful tools by [CorpNewt](https://github.com/corpnewt) and [headkaze](https://github.com/headkaze/Hackintool)

</details>  

<details>
<summary><strong>HARDWARE</strong></summary>

### Lenovo ThinkPad X1 Carbon Gen 8 (Core i7)

These are relevant components on my machine which may differ from yours, keep these in mind as you will need to adjust accordingly, depending on your machine's configuration.

| Category  | Component                                       | Note                                                         |
| --------- | ----------------------------------------------- | ------------------------------------------------------------ |
| Type | 20U9 | - |
| CPU | Intel Core i7-10510U | - |
| GPU | Intel UHD Graphics | - |
| SSD | WDC PC SN720 SDAQNTW-512G-1001 | - |
| Screen | 14" FHD - 1920 x 1080 | - |
| Memory | 8GB / 2133MHz LPDDR3 | - |
| Battery | Integrated Li-Polymer 51Wh | - |
| Camera | 720p Camera | - |
| Wi-Fi & BT | Intel Wireless-AC 9560                          | - |
| Input | PS2 Keyboard & Synaptics TrackPad | - |
| Ports | 2x USB 3.1 Gen 1 (Right USB Always On)</br> 2x USB 3.1 Type-C Gen 2 / Thunderbolt 3 (Power Delivery and DisplayPort) [Max 5120x2880 @60Hz]</br> HDMI 1.4 (Max 4096x2160 @24Hz) | - |

Refer to [ThinkPad X1 Carbon Gen 8 Specs](https://psref.lenovo.com/syspool/Sys/PDF/ThinkPad/ThinkPad_X1_Carbon_Gen_8/ThinkPad_X1_Carbon_Gen_8_Spec.PDF) for possible stock configurations.

</details>  

<details>

<summary><strong>SOFTWARE</strong></summary>
<br>

| Component      | Version |
| -------------- | ------- |
| OpenCore | 0.7.7 |
| macOS Monterey | 12.2 |
| Windows 11 | 21H2 |

</details>

<details>
<summary><strong>ACPI</strong></summary>
<br>

| Component              |
| ---------------------- |
| SSDT-AWAC |
| SSDT-PLUG |
| SSDT-PNLF |
| SSDT-USBX |
| SSDT-XOSI |

</details>

<details>
<summary><strong>KEXT</strong></summary>
<br>

| Kext                   | Version |
| ---------------------- | ------- |
| AirportItlwm | 2.1.0 |
| AppleALC | 1.6.8 |
| BlueToolFixup | 2.6.1 |
| CPUFriend | 1.2.4 |
| CPUFriendDataProvider | 1.0.0 |
| ECEnabler | 1.0.2 |
| IntelBluetoothFirmware | 2.1.0 |
| IntelMausi | 1.0.7 |
| Lilu | 1.5.9 |
| NVMeFix | 1.0.9 |
| SMCBatteryManager | 1.2.8 |
| SMCProcessor | 1.2.8 |
| SMCSuperIO | 1.2.8 |
| USBMap | 1.0.0 |
| VirtualSMC | 1.2.8 |
| VoodooI2C | 2.6.5 |
| VoodooI2CHID | 2.6.5 |
| VoodooPS2Controller | 2.2.7 |
| WhateverGreen | 1.5.6 |

</details>

<details><summary><strong>UEFI DRIVERS</strong></summary>
<br>

|     Driver      | Version           |
| --------------- | ----------------- |
| OpenCanopy.efi | OpenCorePkg 0.7.7 |
| OpenHfsPlus.efi | OpenCorePkg 0.7.7 |
| OpenRuntime.efi | OpenCorePkg 0.7.7 |

</details>

<details>
<summary><strong>OTHER REPOSITORIES</strong></summary>
<br>

- X1C7-Hackintosh repositories:
  - [suhrmann/x1c7-hackintosh](https://github.com/suhrmann/x1c7-hackintosh)
  - [aidanchandra/x1c7-hackintosh](https://github.com/aidanchandra/x1c7-hackintosh)
  - [seven-of-eleven/Lenovo-ThinkPad-X1C7-OC-Hackintosh](https://github.com/seven-of-eleven/Lenovo-ThinkPad-X1C7-OC-Hackintosh)
  - [huyhoang8398/x1c7-hackintosh-20R1](https://github.com/huyhoang8398/x1c7-hackintosh-20R1)

</details>  

<details> 
<summary><strong>CREDITS</strong></summary>

### Credit to all these great people whom I don't know but have made my hackintosh dreams a reality:

- The guys from [Acidanthera](https://github.com/acidanthera) that make this possible
- [ben9923](https://github.com/ben9923) for [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C)
- [Apple](http://apple.com) for macOS
- [CorpNewt](https://github.com/corpnewt) for [USBMap](https://github.com/corpnewt/USBMap) and [CPUFriendDataProvider](https://github.com/corpnewt/CPUFriendFriend)
- [headkaze](https://github.com/headkaze) for [Hackintool](https://github.com/headkaze/Hackintool)
- [Mieze](https://github.com/Mieze) for [IntelMausiEthernet](https://github.com/Mieze/IntelMausiEthernet)
- [OpenIntelWireless](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases) for [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware), [itlwm](https://github.com/OpenIntelWireless/itlwm) and [HeliPort](hhttps://github.com/OpenIntelWireless/HeliPort)
- And every other contributor
- People at [r/hackintosh](https://www.reddit.com/r/hackintosh/) for their advice and help

</details>  

<details><summary><strong>NEOFETCH</strong></summary>
    <br>
    <p float="left">
        <img src="./Other/README_Resources/Neofetch-Monterey.png" alt="Neofetch Monterey" width="600">
    </p>
</details> 

## Before Installation

<details><summary><strong>UEFI SETTINGS</strong></summary>
<br>
	
**Config**

- **Keyboard/Mouse**
  - `Trackpoint` **Enabled**
  - `Trackpad` **Enabled**
- **Display**
  - `Boot Display Device` **ThinkPad LCD**
  - `Total Graphics Memory` **256MB**
  - `Boot Time Extension` **Disabled**
- **CPU**
  - `Intel Hyper-Threading Technology` **Enabled**
- **Thunderbolt**
  - `Thunderbolt BIOS Assist Mode` **Disabled**
  - `Security Level` **No Security**
  - `Support in Pre Boot Environment -> Thunderbolt(TM) device` **Disabled**

**Security**

- **Memory Protection**
  - `Execution Prevention` **Enabled**
- **Virtualization**
  - `Kernel DMA Protection` **Disabled**
  - `Intel Virtualization Technology` **Enabled**
  - `Intel VT-d Feature` **Disabled**
  - `Enhanced Windows Biometric Security` **Disabled**
- **I/O Port Access**
  - `Wireless WAN` **Disabled**
- **Secure Boot**
  - `Secure Boot` **Disabled**
- **Intel SGX**
  - `Intel SGX Control` **Disabled**
- **Device Guard**
  - `Device Guard` **Disabled**

**Startup**

- `UEFI/Legacy Boot` **UEFI Only**
- `CSM Support` **No**
- `Boot Mode` **Quick**

</details>  

<details><summary><strong>KEYBOARD LAYOUT</strong></summary>
<br>

Either add as a `String` or as a `Data` (HEX Data [ProperTree](https://github.com/corpnewt/ProperTree))

Format is lang-COUNTRY:keyboard

🇺🇸 | [0] en_US - U.S --> en-US:0 --> (656e2d55 533a30 in HEX)

| Key           | Type   | Value   |
| ------------- | ------ | ------- |
| prev-lang:kbd | String | en-US:0 |


Pick your keyboard layout here:

[AppleKeyboardLayouts.txt](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt)

</details>

## Post-Install

<details><summary><strong>TRACKPAD</strong></summary>
<br>

To improve the Trackpad in macOS, you have to disable `Force Click and haptic feedback` in `System Preferences -> Trackpad`

</details>  

<details><summary><strong>SMBIOS</strong></summary>
<br>

Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to create your own serial # based off of your preferred model.

- MacBookPro16,3 -`What I used`
- MacBookPro16,2 -`Used by others`

**Note:** If you use a different SMBIOS model than the MacbookPro16,3 that I've used. The provided USB mapping will not work.  You will need to edit the `USBMap.kext` file.  You can right click on the file and select **Show Package Contents**.  From there you can open the Info.plist file in ProperTree and change MacBookPro16,3 to whatever Model ID you've chosen. This should provide a working USBMap.kext.

</details>  

<details>  
<summary><strong>POWER MANAGEMENT</strong></summary>
<br>

Generate CPUFriendDataProvider for your machine [here](https://github.com/fewtarius/CPUFriendFriend) or use those I've provided. Highly recommended that you use power management.

</details>
