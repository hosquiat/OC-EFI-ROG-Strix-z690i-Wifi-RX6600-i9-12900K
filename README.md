![neofetch](images/neofetch.png)

# OpenCore EFI for AMD Ryzen Hackintosh [![tests](https://github.com/mikigal/ryzen-hackintosh/actions/workflows/tests.yml/badge.svg)](https://github.com/mikigal/ryzen-hackintosh/actions/workflows/tests.yml)

## Verified Specification

| **Component**    | **Model**                                  |
| ---------------- | ------------------------------------------ |
| CPU              | Intel Core i9-12900K Alder Lake @ 3.2GHz   |
| Motherboard      | ASUS ROG STRIX Z690-I GAMING WIFI          |
| RAM              | 64GB (2 x 32GB) TeamGroup Vulcan @ 4800MHz |
| GPU              | PowerColor AMD Radeon RX 6600              |
| Audio Chipset    | ALC-4080                                   |
| Ethernet         | Intel I225                                 |
| WiFi & Bluetooth | Custom Wifi Card (BCM94360NG)              |
| OS Disk (SSD)    | Samsung 870 EVO 1TB                        |

**macOS version**: 13.3.1 (a) (22E261) \
**OpenCore version**: REL-092-2023-05-08

## Table of contents

- [Installation](#Installation)
- [BIOS Settings](#BIOS-Settings)
- [PAT Patch](#PAT-Patch)
- [MKL and Intel Fast Memset Patch](#MKL-and-Intel-Fast-Memset-Patch)
- [DRMs support](#DRMs-support)
- [Sleep](#Sleep)
- [Virtualization](#Virtualization)
- [Guides](#Guides)
- [Credits](#Credits)

## Software Compatibility

- Ventura (13.x)
- Monterey (12.x)
- Big Sur (11.x)
- Catalina (10.15.x)
- Mojave (10.14.x)
- High Sierra (10.13.x)

## Installation

### Bootable USB

1. Follow [this guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/) to create your bootable USB.

2. Clone this repository and copy "BOOT" & "OC" directories to your "EFI" directory on your bootable USB. The structure should look somewhat like this: `EFI -> BOOT, OC`.

### SMBIOS

4. Use [this tool](https://github.com/corpnewt/GenSMBIOS) to generate your unique SMBIOS info.

- SMBIOS has to be unique, you cannot use one present in this repository.

- Run the tool and select `Generate SMBIOS`.
- Select the appropriate model for your hardware using the table below.
- Go to [Apple Coverage](https://checkcoverage.apple.com/) and paste generated _Serial_. You need "Invalid Serial" or "Purchase Date not Validated" message. If you get something another you have to generate SMBIOS data and check it again.
- Open _config.plist_ and search for `PlatformInfo -> Generic` and replace these values:
  - _SystemProductName_ - Model
  - _MLB_ - Board Serial
  - _SystemSerialNumber_ - Serial
  - _SystemUUID_ - SmUUID
- _ROM_ entry should be set to your [network card's MAC address](https://www.wikihow.com/Find-the-MAC-Address-of-Your-Computer), without separators (e. g. `:`, `-`).

| **GPU Series**       | **Model**               |
| -------------------- | ----------------------- |
| AMD Navi Series      | iMacPro1,1 <sup>1</sup> |
| AMD Vega Series      | iMacPro1,1 <sup>1</sup> |
| AMD Polaris Series   | iMacPro1,1 <sup>1</sup> |
| AMD Radeon R5/R7/R9  | MacPro6,1               |
| AMD HD 8000 Series   | MacPro6,1               |
| AMD HD 7000 Series   | MacPro6,1               |
| Nvidia Kepler Series | MacPro7,1 <sup>2</sup>  |

<sup>1</sup> For Catalina and newer you can also use `MacPro7,1` if you have some issues (e. g. unfixable DRMs).

<sup>2</sup> For Catalina and older use `iMac14,2`.

### Configuration

5. You should update your BIOS to the latest version and configure it appropriately. See [BIOS Settings](#BIOS-Settings) for details.
6. That's it! Now you can boot macOS installer.

### Post-Installation

9. Copy your EFI directory onto your main drive EFI partition, you'll be able to boot the system without your bootable USB.
10. If you have `Unknown` instead of your CPU name in About this Mac go to `PlatformInfo -> Generic -> ProcessorType` in your configuration file. Set it to `3841` if your CPU has 8 or more physical cores, else set it to `1537`.
11. When everything work you can disable verbose mode - then you will see Apple's logo instead of logs while booting. To do it you have to remove `-v debug=0x100 keepsyms=1` from `boot-args` in your configuration file.

### Bootstrap

In general, enabling Bootstrap is not required, but it will protect your OpenCore from being overriden. \
Remember to do not enable Bootstrap on pendrive - do it only after copying OpenCore to your disk's EFI.

13. Go to `Misc -> Boot -> LauncherOption` in your configuration file and set it to `Full`.
14. Reboot your computer.
15. Reboot PC again and go to your BIOS settings. In boot options you will see new boot entry named `OpenCore`. Set BIOS to boot from it, instead of your drive.
16. It's done!

## BIOS Settings

| **Option**            | **Status**           |
| --------------------- | -------------------- |
| SATA Mode             | AHCI                 |
| Above 4G Decoding     | Enabled <sup>1</sup> |
| EHCI/XHCI Hand-off    | Enabled              |
| SVM                   | Enabled              |
| CSM                   | Disabled             |
| Resizable BAR Support | Disabled             |
| Secure Boot           | Disabled             |

<sup>1</sup> If you have this option in BIOS you must also remove `npci=0x2000` from `boot-args` in your configuration file.

**Some of these options may not exist in your firmware, just try to match it as closely as possible.**

**Before booting macOS remember to update BIOS to the latest version.**

![Screenshot](/screenshot.png?raw=true)
