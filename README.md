# macOS on Lenovo Thinkpad X1 Carbon Gen 8 (20U9)

OpenCore-based EFI for Lenovo Thinkpad X1 Carbon 8th Generation | Model 20U9
<img align="right" src="https://avadirect-freedomusainc1.netdna-ssl.com/Pictures/500/Lenovo_ThinkPad_X1_Carbon_Gen_8_20U90030US.png" alt="Lenovo ThinkPad X1 Carbon Gen 8" width="350">
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

## Status

<details>  

<summary><strong>WORKING ✅</strong></summary>
<br>

> ### Video and Audio
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Full Graphics Accleration (QE/CI)    | ✅   | `WhateverGreen.kext` & `AAPL,ig-platform-id` = 0900A53E & `device-id` = C89B0000 | -   |
| Audio Output                      | ✅   | `AppleALC.kext` with Layout ID = 71    | -   |
| Audio Speakers                       | ✅   | `AppleALC.kext` with Layout ID = 71    | You have to manually select the right speakers (2 at the bottom rear), can't get all 4 speakers to work together   |
| Audio Input | ✅   | `AppleALC.kext` with Layout ID = 71    | Headset microphone is inconsistent and needs more testing   |
| Automatic Headphone Output Switching | ✅   | `AppleALC.kext` with Layout ID = 71    | -   |

> ### Power Management, Battery, Charge, Sleep and Hibernation
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Battery | ✅    | `ECEnabler.kext`             | - |
| CPU Power Management (SpeedShift)    |    ✅  | `CPUFriend.kext` with `CPUFriendFriend` | Idle at 800mhz
| iGPU Power Management        | ✅ | XCPM, enabled by `SSDT-PLUG.aml`                   | - |
| NVMe Drive Battery Management | ✅     | `NVMeFix.kext`  | Generally, NVMe drives will drain more power than SATA drives.           |
| S3 Sleep / Hibernation Mode 3 | ✅ | - | - |

> ### Connectivity
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| WiFi                                       | ✅ | `AirportIltwm.kext`  | -       |
| Bluetooth                                  | ✅ | `IntelBluetoothFirmware.kext` and `BlueToolFixup.kext` | - |
| Ethernet                                   | ✅ | `IntelMausi.kext` | -                  |
| HDMI 1.4                               | ✅ | BusID patching | Hotplug with 4K Resolution |
| USB 2.0 / USB 3.0 | ✅ | `USBMap.kext`   | Create your own USBMap.kext using [CorpNewt](https://github.com/corpnewt/USBMap) |
| USB 3.1 (Type-C)                           | ✅ | `USBMap.kext` and enable ThunderBolt 3 in `BIOS` | Hotplug |
| USB Power Properties in macOS              | ✅ | - | - |

> ### Display, TrackPad, TrackPoint, and Keyboard
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Brightness Adjustments | ✅  | `WhateverGreen.kext`, `SSDT-PNLF.aml`, `enable-backlight-smoother` property, and `BrightnessKeys.kext`| `enable-backlight-smoother` property is optional for smoother birghtness adjustments |
| TrackPoint             | ✅  | `VoodooPS2Controller.kext`                                      | -       |
| TrackPad               | ✅  | `VoodooPS2Controller.kext`, `VoodooI2C.kext`, and `VoodooI2CHID.kext` | - |
| Built-in Keyboard      | ✅  | `VoodooPS2Controller.kext` | - |

> ### macOS Continuity
| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| iCloud, iMessage, FaceTime | ✅ | Whitelisted Apple ID, Valid SMBIOS   | See [dortania /OpenCore-Install-Guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html)  |

</details>  

<details>  
<summary><strong>NOT WORKING ❌</strong></summary>
<br>

| Feature                              | Status | Dependency          | Remarks                      |
| :----------------------------------- | ------ | ------------------- | ---------------------------- |
| Fingerprint Reader   | ❌ | `DISABLED` in BIOS to save power if not used in other OSes.   | Never gonna work.    |
| Wireless WAN         | ❌ | `DISABLED` in BIOS to save power.   | Unable to investigate as I have no need and my model did not come with WWAN |
| Internal Microphone         | ❌ | `DISABLED` in BIOS to save power if not used in other OSes   | - |
| Fan Control / Multimedia Keys | ❌ | `YogaSMC.kext` | YogaSMC.kext needs to be updated in order to work with X1C8 |
| Continuty              | ❌    | Not working with Intel cards | - |
| AirDrop              | ❌    | Not working with Intel cards | - |

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
| Battery Life                      | ⚠️ | - | Need time to thoroughly test battery life and compare with Windows 11 |

</details> 

## Introduction

<details> 
<summary><strong>This is not a guide!</strong></summary>

This is not a guide. It shoud only be used as a reference. I provide some tips and tricks I learned on my journey in building a hackintosh. The best way of using this is as a supplement to the OpenCore guide. If you have questions about how to setup your specific hardware, are unclear about what to do, or would like to see the settings I've used.

I understand that some may simply add the OC and Boot folders to their EFI folder. For clarity the EFI partition needs a folder called EFI that contains the Boot and OC folder.

```EFI
EFI (drive)
	EFI
	├── BOOT
	├── OC
```

It should work and your X1C7 should boot and work fine. **You will at minimum need to generate SMBIOS values if you want Apple services to work.** Note that all error reporting/logging has been turned off in the config.plist. You will have a difficult time trouble shooting with the setup provided. You can easily turn on the error reporting and logging if you follow the Dortania guide. Best of luck.

> **NOTE** if you simply wish to copy my EFI please do the following:
>
>1. [Generate SMBIOS values](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake-plus.html#nvram) and add them in the config.plist (Use MacBookPro15,1)
>2. Ensure the value of `showpicker` is  `true` in the config.plist file to provide the opencore menu when booting. 
>3. Prepare your install [USB](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
>4. Move the entire EFI folder (with your modifications) to the proper partition on your [USB](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#setting-up-opencore-s-efi-environment) (or [hard drive](https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html) once the install is complete).
>5. [Install](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#double-checking-your-work) - You'll need to select F12 to get the boot menu options and **boot from the USB each time the computer restarts** until you've copied the EFI folder onto the hard drive. You may also need to select the correct boot option during install.

</details>  

<details> 
<summary><strong>This is a guide!</strong></summary>

- To install macOS follow the guides provided by [Dortania](https://dortania.github.io/OpenCore-Install-Guide/)
- Useful tools by [CorpNewt](https://github.com/corpnewt) and [headkaze](https://github.com/headkaze/Hackintool)

</details>  

<details> 
<summary><strong>Credits</strong></summary>

**Shout out** to [NotARobot6969](https://github.com/NotARobot6969) for the DevicesProperties patches to enable HDMI.

### Credit to all these great people whom I don't know but have made my hackintosh dreams a reality:

- [EETagent](https://github.com/EETagent) For orginal T480 OpenCore repo (I like the layout of his guide and used it to create this one)
- The guys from [Acidanthera](https://github.com/acidanthera) that make this possible
- [1Revenger1](https://github.com/1Revenger1) and [leo-labs](https://github.com/leo-labs) for [VoodooRMI](https://github.com/VoodooSMBus/VoodooRMI) and [VoodooSMBus](https://github.com/VoodooSMBus/VoodooSMBus)
- [Apple](http://apple.com) for macOS and HfsPlus.efi
- [corpnewt](https://github.com/corpnewt) for [USBMap](https://github.com/corpnewt/USBMap) and [CPUFriendDataProvider](https://github.com/corpnewt/CPUFriendFriend)
- [headkaze](https://github.com/headkaze) for [Hackintool](https://github.com/headkaze/Hackintool)
- [jwise](https://github.com/jwise) for [HoRNDIS](https://github.com/jwise/HoRNDIS)
- [Mieze](https://github.com/Mieze) for [IntelMausiEthernet](https://github.com/Mieze/IntelMausiEthernet)
- [MSzturc](https://github.com/MSzturc) for [ThinkPad Assistant](https://github.com/MSzturc/ThinkpadAssistant)
- [OpenIntelWireless](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases) for [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware), [itlwm](https://github.com/OpenIntelWireless/itlwm) and [HeliPort](hhttps://github.com/OpenIntelWireless/HeliPort)
- [zhen-zen](https://github.com/zhen-zen) for [YogaSMC](https://github.com/zhen-zen/YogaSMC)
- And every other contributor
- People at [r/hackintosh](https://www.reddit.com/r/hackintosh/) for their advice and help

</details>  

<details>
<summary><strong> OTHER REPOSITORIES </strong></summary>
<br>


- x1c7-hackintosh repositories:
  - [suhrmann/x1c7-hackintosh](https://github.com/suhrmann/x1c7-hackintosh)
  - [aidanchandra/x1c7-hackintosh](https://github.com/aidanchandra/x1c7-hackintosh)

- x1c6-hackintosh repositories:
  - [tylernguyen/x1c6-hackintosh](https://github.com/tylernguyen/x1c6-hackintosh) 
  - [benbender/x1c6-hackintosh](https://github.com/benbender/x1c6-hackintosh)
  - [zhtengw/EFI-for-X1C6-hackintosh](

</details>  

<details>
<summary><strong>Hardware</strong></summary>
<br>

I used to own two Lenovo ThinkPad X1 Gen 7 laptops, an i5 and an i7. I now only have the one outlined below:

[![UEFI](https://img.shields.io/badge/UEFI-N2HET58W-lightgrey)](https://pcsupport.lenovo.com/ca/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-carbon-7th-gen-type-20qd-20qe/downloads/ds540232-bios-update-utility-bootable-cd-for-linux-windows-10-64-bit-thinkpad-x1-carbon-7th-gen-x1-yoga-4th-gen)

### X1C7 i5

| Category  | Component                                       | Note                                                         |
| --------- | ----------------------------------------------- | ------------------------------------------------------------ |
| Type      | 20QD, 20QE                                      |                                                              |
| CPU       | Intel Core i5-8265U                             |                                                              |
| GPU       | Intel UHD 620                                   |                                                              |
| SSD       | Toshiba 512GB                                   | Replaced cursed PM 981 which still doesn't work reliably     |
| Screen    | 14" WQHD - 2560x1440                            |                                                              |
| Memory    | 16GB / 2133MHz LPDDR3                           |                                                              |
| Battery   | Integrated Li-Polymer 51Wh                      | Single battery                                               |
| Camera    | 720p Camera                                     |                                                              |
| Wifi & BT | Intel Wireless-AC 9560                          | Use AirportItlwm for your macOS version and enjoy native Wi-Fi control, or use Heliport app. |
| Input     | PS2 Keyboard & Synaptics TrackPad (touchscreen) | I'm using ThinkPad Assistant an alternative most seem to be moving to [YogaSMC](https://github.com/zhen-zen/YogaSMC) for media keys like microphone switch, etc. |

</details>  

<details>

<summary><strong>Main software</strong></summary>
<br>

| Component      | Version |
| -------------- | ------- |
| macOS Monterey | 12.1    |
| OpenCore       | v0.7.7  |

</details>

<details>
<summary><strong>ACPI Files</strong></summary>
<br>

| Component              |
| ---------------------- |
| SSDT-AWAC              |
| SSDT-BATT              |
| SSDT-EC-USBX-LAPTOP    |
| SSDT-PLUG-DRTNIA       |
| SSDT-PNLF-CFL          |
| SSDT-ThinkPad_ClickPad |
| SSDT-X1C6-KBRD         |
| SSDT-XOSI              |

</details>

<details>
<summary><strong>Kernel extensions</strong></summary>
<br>

| Kext                   | Version |
| --------------------- | ------- |
| AirportItlwm           | 2.1.0   |
| AppleALC               | 1.6.8   |
| BlueToolFixup          | 2.6.1   |
| CPUFriend              | 1.2.4   |
| CPUFriendDataProvider  | 1.00    |
| IntelBluetoothFirmware | 2.1.0   |
| IntelMausi             | 1.0.7   |
| Lilu                   | 1.5.9   |
| NVMeFix                | 1.0.9   |
| SMCBatteryManager      | 1.2.8   |
| SMCProcessor           | 1.2.8   |
| SMCSuperIO             | 1.2.8   |
| USBMap                 | 1.0.0   |
| VirtualSMC             | 1.2.8   |
| VoodooI2C              | 2.6.5   |
| VoodooI2CHID           | 2.6.5   |
| VoodooPS2Controller    | 2.2.7   |
| WhateverGreen          | 1.5.6   |

</details>

<details><summary><strong>UEFI drivers</strong></summary>
<br>

|     Driver      | Version           |
| ------------- | ----------------- |
|   HfsPlus.efi   | OcBinaryData      |
| OpenRuntime.efi | OpenCorePkg 0.7.7 |

</details>

<details><summary><strong>Neofetch screenshots</strong></summary>
    <br>
    <p float="left">
        <img src="./Other/README_Resources/Neofetch-Monterey.png" alt="Neofetch Monterey" width="600">
    </p>
</details> 



## Before installation

<details><summary><strong>UEFI settings</strong></summary>
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


- `Password` **Disabled**
- `Fingerprint` **Disabled**
- `Security Chip` **Disabled**
- `Memory Protection -> Execution Prevention` **Enabled**
- `Virtualization -> Kernel DMA Protection` **Disabled**
- `Virtualization -> Intel Virtualization Technology` **Enabled**
- `Virtualization -> Intel VT-d Feature` **Disabled**
- `Virtualization -> Enhanced Windows Biometric Security` **Disabled**
- `I/O Port Access -> FingerPrint Reader` **Disabled**
- `I/O Port Access -> Wireless WAN` **Disabled**
- `Secure Boot -> Secure Boot` **Disabled**
- `Intel SGX -> Intel SGX Control` **Disabled**
- `Device Guard` **Disabled**

**Startup**

- `UEFI/Legacy Boot` **UEFI Only**
- `CSM Support` **No**
- `Boot Mode` **Diagnostics** (This can be changed to "Quick" once you know your system is running properly)

</details>  

<details><summary><strong>Own prev-lang-kbd</strong></summary>
<br>
Either add as a string or as a data ( HEX data [(ProperTree)](https://github.com/corpnewt/ProperTree) )

Format is lang-COUNTRY:keyboard

- 🇺🇸 | [0] en_US - U.S --> en-US:0 --> (656e2d55 533a30 in HEX)

| Key           | Type   | Value   |
| ------------- | ------ | ------- |
| prev-lang:kbd | String | en-US:0 |


Pick your keyboard layout here:

[AppleKeyboardLayouts.txt](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt)

</details>

## Post-Install

<details><summary><strong>TrackPad - Disable force touch</strong></summary>
<br>

If the **Battery** management **doesn't show up** in the System Preferences after the SSDT-Batt.aml file is added to your ACPI folder and config.plist file. You will not be able to change any trackpad settings. You may experience the annoying behaviour of clicking on the touchpad and it doing a **Force Touch** where the preview of the file is shown. I found this very annoying. You can disable force touch by modifying the file in `~/Library/Preferences/com.apple.AppleMultitouchTrackpad.plist`
Opened it with Propertree and changed **ForceSuppressed** to **True**

Another trick to manage your trackpad, if you can't get the battery to work, is to connect a bluetooth trackpad. Once the bluetooth trackpad is connected you can adjust the settings. Disconnect the bluetooth trackpad and your built in one will maintain those settings.

I used these methods prior to receiving a SSDT-Batt.aml that worked from a friendly Redditor [Galactic_Dev](https://www.reddit.com/user/Galactic_Dev)
</details>  

<details><summary><strong>Generate your own SMBIOS</strong></summary>
<br>

[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

Use GenSMBIOS to create your own serial #... based off of your preferred model.

- MacBookPro15,1 -`What I used`
- MacBookPro15,4 -`Reported as used by others`

**Note:** If you use a different SMBIOS model than the MacbookPro15,1 that I've used. The provided USB mapping will not work.  You will need to edit the **USBMap.kext file**.  You can right click on the file and select **Show Package Contents**.  From there you can open the Info.plist file in ProperTree and change MacBookPro15,1 to whatever Model ID you've chosen. This should provide a working USBMap.kext.

</details>  

<details>  
<summary><strong>CPUFriend power management</strong></summary>
<br>

Generate CPUFriendDataProvider for your machine [here](https://github.com/fewtarius/CPUFriendFriend) or use those I've provided. My files are set for power conservation over performance. Highly recommended that you use power management.

</details>  

<details>  
<summary><strong>Audio Setup</strong></summary>
<br>

## Audio Setup enable both top and bottom speakers:

| Key       | Value    |
| --------- | -------- |
| boot-args | alcid=71 |

Using the above boot-arg to initially setup your config.plist file. This will enable the top and bottom speakers in the **System Preferences>Sound** allowing you to select either set of speakers. To combine the two you'll need to open **Audio MIDI Setup** (use Spotlight to find and open it) and create an **Aggregate Device** with both sets of speakers. Unfortunately you can't control the volume of an Aggregate Device with the volume keys. You'll need to install a utility as highlighted below.

Create **Multi-output device** or **Aggregate Device** in **Audio MIDI Setup** controller for all speakers - use utility like [AggregateVolumeMenu](https://github.com/adaskar/AggregateVolumeMenu) to control the volume

- See description here [Change Volume on Aggregate Sound](https://gurhanpolat.medium.com/change-volume-on-aggregate-sound-815fd575347a)

If you're happy with the setup above you can use the guide to replace alcid=71 per below:

- Add audio codec to DeviceProperties - layout-id | data | **47000000**

</details>
