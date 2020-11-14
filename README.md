# Dell-Optiplex-7010-Hackintosh-OpenCore

This git repo has the config.plist and kexts required for the Dell Optiplex 7010. I have SFF, but this should work on any of them.

## Usage

Follow the guide up until you have installed macOS on your USB (Make sure to use `OpenCore` in `MakeInstall.py`.) Then replace everything inside `BOOT` with everything in this repo.

## Optional (but recommended Kexts)

- SMCProcessor.kext - This kext is a VirtualSMC plugin that is used to monitor CPU temps.
- SMCSuperIO.kext - This kext is a VirtualSMC plugin that is used to monitor fan speed.

## Kexts I didn't add

- AppleALC.kext - This kext allows your audio to work. This should work by default on ALC269 (if you have that). ~~This may also require you to modify your config.plist.~~ I added `alcid=1` to the boot args. I forgot to add this, but now audio should work (System Preferences -> Sound -> Output -> Internal Speakers/Headphones)
- WiFi/Ethernet kexts - ~~Other people might have different WiFi/Ethernet. I have an Archer T4U V3, but you might not have that.~~ I have added the IntelMausi.kext, an Ethernet LAN driver for macOS (my Optiplex has 82579LM).

## config.plist - Use [ProperTree](https://github.com/corpnewt/ProperTree)

- `DeviceProperties -> Add -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id` - The value of this will need to be changed to `0x0A006601` for the iGPU to work properly. You should be able to boot your macOS USB if your Optiplex 7010 is connected to your monitor/TV via DVI/HDMI (**VGA does not work**).
- `NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> prev-lang:kbd` - The value of this is HEX encoded. You will need to find the HEX for your language. This should be in the format of `lang-COUNTRY:keyboard`. For example. because I'm in the UK, I have set this to `en-GB:0`. You will need to specify your country here [HEX Encoder](https://www.convertstring.com/EncodeDecode/HexEncode), and replace the value with the HEX you are given. If the language on the macOS installer doesn't change, select the option `Reset NVRAM`, then the language should change.

## Networking
Ethernet should be working. You can’t use USB tethering on your phone for this, as this will not work. You must use an Ethernet cable during installation. WiFi will not work until you have installed macOS and the driver required for your wireless adapter/card. You could also create a full macOS installer on your USB by creating a macOS virtual machine, and installing it from that to your USB. This way, you will not need an internet connection during installation.

## Post Install
After installing macOS, you are not done. There are issues with Ivy Bridge CPUs connecting to Apple's XCPM (Xnu CPU Power Management). I have already modified the config.plist `ACPI -> Delete` tables, but you will need to use [ssdtPRGen](https://github.com/Piker-Alpha/ssdtPRGen.sh). There may be other things you have to do after installation See here -> [Post Install](https://dortania.github.io/OpenCore-Desktop-Guide/post-install/).

### Sources

- [OpenCore Guide](https://dortania.github.io/OpenCore-Desktop-Guide/)
- [Hackintosh Discord](https://discord.com/invite/8aKs69x)
