# Dell-Optiplex-7010-Hackintosh-OpenCore

This git repo specifies the config.plist and kexts required for the Dell Optiplex 7010. I have SFF, but this should work on any of them.

## Usage

Follow the guide up until you have installed macOS on your USB (Make sure to use `OpenCore` in `MakeInstall.py`.) Then replace everything inside `BOOT` with everything in this repo.

## Optional (but recommended Kexts)

- SMCProcessor.kext - This kext is a VirtualSMC plugin that is used to monitor CPU temps.
- SMCSuperIO.kext - This kext is a VirtualSMC plugin that is used to monitor fan speed.

## Kexts I didn't add

- AppleALC.kext - This kext allows your audio to work. This should work by default on ALC269 (if you have that). This may also require you to modify your config.plist.
- ~~WiFi/Ethernet kexts - Other people might have different WiFi/Ethernet. I have an Archer T4U V3, but you might not have that.~~

## config.plist

- `DeviceProperties -> Add -> PciRoot(0x0)/Pci(0x2,0x0) -> AAPL,ig-platform-id` - The value of this will need to be changed to `0A006601` for the iGPU to work properly. I only used `0x12345678` to get it booting on my PC. You shouldn't have any issues booting if your Dell is connected to your monitor/TV via DVI/HDMI. You can leave this at `0x12345678` if you'd like to, however after installation you will need to get graphics working (it probably won't work on VGA).
- `NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> prev-lang:kbd` - The value of this is HEX encoded. You will need to find the HEX for your language. This should be in the format of `lang-COUNTRY:keyboard`. For example. because I'm in the UK, I have set this to `en-GB:0`. You will need to specify your country on this [HEX Encoder](https://www.convertstring.com/EncodeDecode/HexEncode), and replace the value with the HEX you are given. If the language on the macOS installer doesn't change, select the option `Reset NVRAM`, then the language should change.

## Networking
To use ethernet, you can't use USB tethering from your phone (I couldn't and I doubt it would be any different for you), you need an ethernet cable from your PC to your router, or from PC to another PC (I did the latter), to connect from PC to PC, you need to bridge connections on windows (ctrl + click "Ethernet" and "WiFi", right click then click "Bridge Connections"). Check if internet is working by going to "Ping" in the network utility, then try pinging a website. If it is working, you shuold be able to install macOS.

## Post Install

After installing macOS, you are not done. There are issues with Ivy Bridge CPUs connecting to Apple's XCPM (Xnu CPU Power Management). I have already modified the config.plist `ACPI -> Delete` tables, but you will need to use [ssdtPRGen](https://github.com/Piker-Alpha/ssdtPRGen.sh). There may be other things you have to do after installation See here -> [Post Install](https://dortania.github.io/OpenCore-Desktop-Guide/post-install/).

### Sources

- [OpenCore Guide](https://dortania.github.io/OpenCore-Desktop-Guide/)
- [Hackintosh Discord](https://discord.com/invite/8aKs69x)
