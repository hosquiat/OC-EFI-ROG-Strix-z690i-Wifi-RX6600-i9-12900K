# OpenCore EFI

Download OpenCore **RELEASE** from [here](https://github.com/acidanthera/OpenCorePkg/releases/latest)

## ACPI

- SSDT-AWAC.aml
- SSDT-GPRW.aml
- SSDT-RHUB.aml
- SSDT-USBW.aml
- SSDT-PLUG-ALT.aml
- SSDT-SBUS-MCHC.aml
- SSDT-BRG0.aml
- SSDT-MAPLE-RIDGE-RP05-V2.aml
- SSDT-EC-USBX.aml

## Driver

- [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/raw/master/Drivers/HfsPlus.efi)
- OpenRuntime.efi - Included in OpenCore package

## Kext - Make sure to download RELEASE version

- [Lilu.kext](https://github.com/acidanthera/Lilu/releases/latest)
- [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC/releases/latest)
- [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases/latest)
- [AppleALC.kext](https://github.com/acidanthera/AppleALC/releases/latest)
- [IntelMausi.kext](https://github.com/acidanthera/IntelMausi/releases/latest)
- USBPorts.kext - [Refer post installation](POST_INSTALL.md)
- SMCProcessor.kext - Included in VirtualSMC package
- SMCSuperIO.kext - Included in VirtualSMC package

## Tools

- TpmInfo.efi - Included in OpenCore package
- RtcRw.efi - Included in OpenCore package
- ResetSystem.efi - Included in OpenCore package
- OpenShell.efi - Included in OpenCore package
- OpenControl.efi - Included in OpenCore package
- MmapDump.efi - Included in OpenCore package
- ListPartitions.efi - Included in OpenCore package
- KeyTester.efi - Included in OpenCore package
- GopStop.efi - Included in OpenCore package
- FontTester.efi - Included in OpenCore package
- CsrUtil.efi - Included in OpenCore package
- ControlMsrE2.efi - Included in OpenCore package
- CleanNvram.efi - Included in OpenCore package
- ChipTune.efi - Included in OpenCore package
- BootKicker.efi - Included in OpenCore package

## config.plist

- Use the provided `config.plist`.

## EFI Folder Structure

```
.
├── EFI
│   ├── BOOT
│   │   └── BOOTx64.efi
│   └── OC
│       ├── ACPI
│       │   ├── SSDT-AWAC.aml
│       │   ├── SSDT-BRG0.aml
│       │   ├── SSDT-EC-USBX.aml
│       │   ├── SSDT-GPRW.aml
│       │   ├── SSDT-MAPLE-RIDGE-RP05-V2.aml
│       │   ├── SSDT-PLUG-ALT.aml
│       │   ├── SSDT-RHUB.aml
│       │   ├── SSDT-SBUS-MCHC.aml
│       │   └── SSDT-USBW.aml
│       ├── Drivers
│       │   ├── HfsPlus.efi
│       │   ├── OpenCanopy.efi
│       │   ├── OpenRuntime.efi
│       │   └── ResetNvramEntry.efi
│       ├── Kexts
│       │   ├── AMFIPass.kext
│       │   ├── AppleALCU.kext
│       │   ├── AppleIGC.kext
│       │   ├── CPUFriend.kext
│       │   ├── CPUFriendDataProvider.kext
│       │   ├── CpuTopologyRebuild.kext
│       │   ├── IO80211FamilyLegacy.kext
│       │   ├── IOSkywalkFamily.kext
│       │   ├── Lilu.kext
│       │   ├── NVMeFix.kext
│       │   ├── RestrictEvents.kext
│       │   ├── SMCProcessor.kext
│       │   ├── SMCSuperIO.kext
│       │   ├── USBPower.kext
│       │   ├── USBWakeFixup.kext
│       │   ├── VirtualSMC.kext
│       │   ├── WhateverGreen.kext
│       │   └── Z690-XHCI-unsupported.kext
│       ├── OpenCore.efi
│       └── config.plist
```
