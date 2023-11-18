# Gigabyte B550I Aorus Pro AX · Ryzen 5x00 · Radeon 6x00

- OpenCore ver 0.9.6
- MacPro7,1

macOS support status:

- Ventura 13.6.1 running perfectly.
- Sonoma 14.1 running, Wi-Fi requires OCLP patching (see usage below)

Note that Sonoma brings back [DSC support](https://www.cablematters.com/Blog/DisplayPort/what-is-display-stream-compression) over DisplayPort 1.4. Thus in Sonoma, for the first time since Big Sur, it’s possible to use variable refresh rate or 144Hz 10bit HDR which my LG 27GN950 monitor supports.

![](media/gpu-144Hz-10bit-hdr.png)
![](media/gpu-variable-refresh-rate.png)

## Current hardware

- [Gigabyte B550I Aorus Pro AX](https://www.gigabyte.com/Motherboard/B550I-AORUS-PRO-AX-rev-10/) motherboard (rev 1.0)
- AMD [Ryzen 9 5900X](https://www.amd.com/en/products/cpu/amd-ryzen-9-5900x) CPU
- AMD [RX 6900 XT](https://www.amd.com/en/products/graphics/amd-radeon-rx-6900-xt) graphics card, no riser card.
- Corsair [Vengeance LPX](https://www.corsair.com/us/en/Categories/Products/Memory/VENGEANCE-LPX/p/CMK32GX4M2D3600C18) 32 GB (2 x 16 GB) DDR4 3600MHz CL18
- WD [Black SN850X](https://www.westerndigital.com/en-il/products/internal-drives/wd-black-sn850x-nvme-ssd#WDS200T2X0E) 2TB NVMe SSD
- WD [Black SN770](https://www.westerndigital.com/en-il/products/internal-drives/wd-black-sn770-nvme-ssd#WDS100T3X0E) 1TB NVMe SSD
- [Broadcom BCM94360NG](https://www.aliexpress.com/item/1005003324812245.html) card, direct replacement for the existing card on the board.

Note: it’s fairly easy to switch between Ryzen 5000 CPUs, just carefully update the `Replace` value in first 4 `Kernel/Patch` entries, as [per AMD OSX Vanilla repo](https://github.com/AMD-OSX/AMD_Vanilla).

You can use any of these cards: Radeon 6600 XT, 6800, 6800 XT, 6900 XT — all are natively supported.

### BIOS

Version `F18c`

- Fast Boot: `Disabled`
- CSM: `Disabled`
- Above 4G Decoding: `Enabled`
- Resizable Bar Support: `Enabled`
- PCIe slot speed: `Auto`
- XMP Profile activated

## Usage

1. [Update `PlatformInfo/Generic` stuff](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#generate-a-new-serial) with your own, inside `config.plist`
2. Use your Ethernet’s MAC address for `ROM` value, as explained in the Dortania guide. Don’t leave it as all 0s.
3. There are two USB maps - one without any onboard USB headers connected (no chassis ports) and one with all headers connected giving additional 2 USB-A 3.0 ports and 2 USB-A 2.0 ports. The former one is enabled in _config.plist_

### Sonoma only

In Sonoma, Apple removed drivers for almost all slot-in Wi-Fi cards like the 94360NG I am using. Bluetooth is still working out of the box but Wi-Fi is not. 

Per [this guide](https://github.com/5T33Z0/OC-Little-Translated/blob/main/14_OCLP_Wintel/WIiFi_Sonoma.md#2-config-and-efi-adjustments) and this [example .plist file](https://github.com/5T33Z0/OC-Little-Translated/blob/main/14_OCLP_Wintel/plist/Sonoma_WIFI_Modern.plist) I have added required kexts and updated config.plist to prepare ground for post-install patching.

Thus SecureBootModel=`Disabled` (instead of `Default`) and `csr-active-config` is set to `03080000` which is specific value that enables:

![](media/sip-03080000.png)

Once you complete the installation with this, run [OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher/) and install _Modern Wireless_ patches from Post-Install Root Patches section. After that and install, your Wi-Fi will work again.

## Notes

- OpenCanopy (GUI boot menu) is up and running.
- I don’t boot Windows 10/11 using OC, thus I can’t guarantee it will work. I have Windows installed on separate SSD and switch using Boot Menu.

---

*Use at your own risk.* Nothing is guaranteed, even if you use exactly the same hardware as me.

You may use this EFI as example but be prepared to dive way deeper than you hoped. It’s always advisable to build your own EFI from scratch, [following the guide](https://dortania.github.io/OpenCore-Install-Guide/) —  then you’ll have an idea how things work,  how to ask for help in proper channels:
- [on Reddit](https://www.reddit.com/r/hackintosh/)
- [Discord server](https://discord.gg/Wxam8aH)
- AMD-OSX [forums](https://forum.amd-osx.com)

Most importantly — doing stuff step by step will give you knowledge how to act on given help and hints.

Good luck.

## Give back

If you found this code useful, please consider [buying me a coffee](https://www.buymeacoffee.com/radianttap) or two. ☕️😋
