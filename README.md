# Gigabyte B550I Aorus Pro AX + Ryzen 9 5900X + RX 6900 XT

- OpenCore ver 0.8.6
- MacPro7,1
- Monterey 12.6.1

Ventura likely works too but I don’t use it yet.

## Current hardware

Powerful and near-silent even under full CPU load.

![](media/sliger-s620.jpeg)
![](media/radeon.jpeg)
![](media/cb23.png)
![](media/gb5-cpu.png)
![](media/gb5-gpu-metal.png)
![](media/unigine-heaven.png)

- [Gigabyte B550I Aorus Pro AX](https://www.gigabyte.com/Motherboard/B550I-AORUS-PRO-AX-rev-10/) motherboard (rev 1.0)
- AMD [Ryzen 9 5900X](https://www.amd.com/en/products/cpu/amd-ryzen-9-5900x) CPU
- XPG [Levante 240](https://www.xpg.com/en/feature/644/) AIO with 2 Noctua [NF-A12x25](https://noctua.at/en/products/fan/nf-a12x25-pwm) fans set as intake.
- AMD [RX 6900 XT](https://www.amd.com/en/products/graphics/amd-radeon-rx-6900-xt) graphics card, no riser card.
- Corsair [Vengeance LPX](https://www.corsair.com/us/en/Categories/Products/Memory/VENGEANCE-LPX/p/CMK32GX4M2D3600C18) 32 GB (2 x 16 GB) DDR4 3600MHz CL18
- ADATA [XPG 8200 Pro](https://www.xpg.com/us/feature/583/) 1TB NVMe SSD
- Samsung [860 EVO](https://www.samsung.com/us/computing/memory-storage/solid-state-drives/ssd-860-evo-2-5--sata-iii-500gb-mz-76e500b-am/) 500 GB 2.5in SSD
- Corsair [SF750 Platinum](https://www.corsair.com/us/en/Categories/Products/Power-Supply-Units/Power-Supply-Units-Advanced/SF-Series/p/CP-9020186-NA) SFX PSU
- Noctua [NF-A12x25](https://noctua.at/en/products/fan/nf-a12x25-pwm) case fan as the back exhaust 
- Noctua [NF-A12x15](https://noctua.at/en/products/fan/nf-a12x15-pwm) case fan as the top exhaust
- Sliger [S620](https://sliger.com/products/cases/s620/) SFF case

### WiFI / Bt

[Broadcom BCM94360NG](https://www.aliexpress.com/item/1005003324812245.html) card, direct replacement for the existing card on the board.

### BIOS

Version `F16e`

- Fast Boot: `Disabled`
- CSM: `Disabled`
- Above 4G Decoding: `Enabled`
- Resizable Bar Support: `Enabled`
- PCIe slot speed: `Auto`
- XMP Profile activated
- PBO2 set to Enabled, nothing custom set.

## Usage

1. [Update `PlatformInfo/Generic` stuff](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#generate-a-new-serial) with your own, inside `config.plist`
2. Use your Ethernet’s MAC address for `ROM` value, as explained in the Dortania guide. Don’t leave it as all 0s.
3. Update value of `brcmfx-country` argument in `NVRAM/7C436110-AB2A-4BBB-A880-FE41995C9F82/boot-args` with your country code. Should be identical or compatible with what your WiFi router is broadcasting. (Remove the parameter if you don’t know what I’m talking about here.)
4. Turn off Power Nap in Energy Saver.

### What’s working

- CPU Power Management.
- NVMe and 2.5in SATA SSD.
- WiFi, Bluetooth, Ethernet.
- All USB ports (without map, just with RHUB reset).
- Radeon GPU is natively supported.
- 4K HDMI or DisplayPort with HDR.
- Watch unlock, Handoff, iMessage, iCloud, Keychain, Xcode etc.
- System Integrity Protection (SIP) fully enabled.
- All media & DRM

### What’s not working

Sidecar most likely. Did not even try it but I suspect it does not work.

Sleep is not working post-F12 BIOS versions but might start working with proper USB mapping. Not that much of an issue for me.

## Notes

- OpenCanopy (GUI boot menu) is up and running.
- I don’t boot Windows 10/11 using OC, thus I can’t guarantee it will work. I have Windows installed on separate SSD and switch using Boot Menu.

## Usage

*Use at your own risk.* Nothing is guaranteed, even if you use exactly the same hardware as me.

You may use this EFI as example but be prepared to dive way deeper then you hoped. It’s always advisable to build your own EFI from scratch, [following the guide](https://dortania.github.io/OpenCore-Install-Guide/) —  then you’ll have an idea how things work,  how to ask for help in proper channels:
- [on Reddit](https://www.reddit.com/r/hackintosh/)
- [Discord server](https://discord.gg/Wxam8aH)
- AMD-OSX [forums](https://forum.amd-osx.com)

Most importantly — doing stuff step by step will give you knowledge how to act on given help and hints.

Good luck.

## Give back

If you found this code useful, please consider [buying me a coffee](https://www.buymeacoffee.com/radianttap) or two. ☕️😋
