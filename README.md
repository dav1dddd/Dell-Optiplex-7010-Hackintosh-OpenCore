# Dell-Optiplex-7010-Hackintosh-OpenCore
If macOS is not working, make sure that you change iMac14,4 to iMac13,1 in config.plist. I am not sure if iMac14,4 SMBIOS works for versions of macOS older than Big Sur:
- PlatformInfo -> Generic -> SystemProductName, changing `iMac14,4` to `iMac13,1`

## What's working
- WiFi/Ethernet
- Graphics Acceleration
- USB ports (but not all)
- Audio (might have to set in macOS: System Preferences -> Sound -> Output)

## What isn't working
- Sleep (not working correctly, once woken from sleep macOS will most likely freeze.)
I would recommend that you do the following:
    - Settings -> Energy Saver -> Tick "Prevent computer from sleeping automatically when the display is off".
    - Set the "Computer sleep" slider to **Never** if you have that (Display sleep can be left alone as that just turns off the display, but the PC doesn't.)

## Usage
Follow the guide up until you have installed macOS on your USB (Make sure to use `OpenCore` in `MakeInstall.py`.) Then replace everything inside `BOOT` with everything in this repo. (this assumes that you are using the recovery installer).  
You can also use the full installer to installer macOS, and then go to [Post Install](#post-install)

## Optional (but recommended) kexts
- SMCProcessor.kext - This kext is a VirtualSMC plugin that is used to monitor CPU temps.
- SMCSuperIO.kext - This kext is a VirtualSMC plugin that is used to monitor fan speed.

## config.plist - Use [ProperTree](https://github.com/corpnewt/ProperTree)
- Language
    - `NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> prev-lang:kbd` - The value of this is HEX encoded. You will need to find the HEX for your language. This should be in the format of `lang-COUNTRY:keyboard`. For example. because I'm in the UK, I have set this to `en-GB:0`. You will need to specify your country here [HEX Encoder](https://www.convertstring.com/EncodeDecode/HexEncode), and replace the value with the HEX you are given. If the language on the macOS installer doesn't change, select the option `Reset NVRAM`, then the language should change.

## Networking
Ethernet should be working. You can’t use USB tethering on your phone, as this will not work. You must use an Ethernet cable during installation. WiFi will not work until you have installed macOS and the driver required for your wireless adapter/card. You could also create a full macOS installer on your USB by creating a macOS virtual machine, and installing it from that to your USB. This way, you will not need an internet connection during installation.

## Post Install
This should be done after installing macOS
- Booting without USB
    - First you need to find your computers EFI partition. To do this, open the terminal, and type `diskutil list` as shown in the below screenshot. ![alt text](https://i.imgur.com/ezYQPhk.png)
    - Mount your EFI partition using `sudo diskutil mount /dev/diskXsY` where `X` is the disk and `Y` is the partition. For example, I would mount `/dev/disk0s2` as that is my EFI partition ![alt text](https://cdn.discordapp.com/attachments/782341614659305482/782344498700222514/unknown.png)
    - Depending on which method you have to install macOS, you can do one of the following
        - If you have used the full macOS installer, download this repo, unzip it, and do the following: `sudo cp -r ~/Downloads/Dell-Optiplex-7010-Hackintosh-OpenCore-master/EFI/* /Volumes/NO\ NAME/EFI`
        - If you are installing from the recovery installer, do the following: `sudo cp -r /Volumes/USB/EFI/* /Volumes/NO\ NAME/EFI`.
        - If the OpenCore bootloader does not show, make sure your [BIOS settings](https://dortania.github.io/OpenCore-Install-Guide/config.plist/ivy-bridge.html#intel-bios-settings) are correct. If they are correct, and you are still having this problem, try to clean NVRAM by doing the following:
            - Boot macOS from your USB
            - Press space
            - Select "CleanNvram.efi". Unplug your USB and check boot options. You should see OpenCore.

There are also other things you can do after installing macOS. If you would like to do anything else such as fixing your USB ports, you can do so here [Post Install](https://dortania.github.io/OpenCore-Post-Install/#how-to-follow-this-guide). I have not done much here, since I am fine with how macOS is working for me.

## Sources
- [OpenCore Guide](https://dortania.github.io/OpenCore-Desktop-Guide/)
- [Hackintosh Discord](https://discord.com/invite/8aKs69x)
