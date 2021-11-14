# Dell-Optiplex-7010-Hackintosh-OpenCore
Works from Mountain Lion - Big Sur

For macOS Monterey click [here](https://github.com/dav1dnix/Dell-Optiplex-7010-Hackintosh-OpenCore/tree/monterey), I have made it a separate branch for now.

## What's working
- WiFi/Ethernet
- Graphics Acceleration
- USB ports (but not all)
- Audio (might have to set in macOS: System Preferences -> Sound -> Output).

## What isn't working
- Sleep (not working correctly, once woken from sleep macOS will most likely freeze.).
I would recommend that you do the following in macOS:
    - System Preferences -> Energy Saver -> Tick "Prevent computer from sleeping automatically when the display is off".
    - Set the "Computer sleep" slider to **Never** if you have that option ("Display sleep" can be left alone as that just turns off the display).
    - UPDATE: it might work sometimes if you got lucky. I would try out Sleep before you disable it and see if it works and doesn't crash macOS.

## Supported graphics
The fastest processor for this PC is the i7-3770 because the motherboard has a Q77 chipset. All of these processors should be supported on this PC https://www.cpu-upgrade.com/mb-Intel_(chipsets)/Q77_Express.html, it is best to use a processor that has HD 4000 graphics, because HD 4000 is supported on Big Sur. I wouldn't recommend anything lower than HD 4000 for a Hackintosh.

## Usage
Follow the guide up until you have installed macOS on your USB (Make sure to use `OpenCore` in `MakeInstall.py`.) Then replace everything inside `BOOT` with everything in this repo. (this assumes that you are using the recovery installer).  
You can also use the full installer to installer macOS, and then go to [Post Install](#post-install).

## Optional (but recommended) kexts
- SMCProcessor.kext - This kext is a VirtualSMC plugin that is used to monitor CPU temps.
- SMCSuperIO.kext - This kext is a VirtualSMC plugin that is used to monitor fan speed.

## config.plist - Use [ProperTree](https://github.com/corpnewt/ProperTree)
- Language
    - `NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> prev-lang:kbd` - The value of this is HEX encoded. You will need to find the HEX for your language. This should be in the format of `lang-COUNTRY:keyboard`. For example. because I'm in the UK, I have set this to `en-GB:0`. You will need to specify your country here [HEX Encoder](https://www.convertstring.com/EncodeDecode/HexEncode), and replace the value with the HEX you are given. If the language on the macOS installer doesn't change, boot to your USB (which has OpenCore), press space and select "CleanNvram.efi", then the language should change.

## Networking
Ethernet should be working. You can’t use USB tethering on your phone, as this will not work. You must use an Ethernet cable during installation. WiFi will not work until you have installed macOS and the driver required for your wireless adapter/card. You could also create a full macOS installer on your USB by creating a macOS virtual machine, and installing it from that to your USB. This way, you will not need an internet connection during installation.

## Post Install
This should be done after installing macOS
- Booting without USB
    - First you need to find your computers EFI partition. To do this, open the terminal, and type `diskutil list` as shown below. ![alt text](https://i.imgur.com/ezYQPhk.png)
    - Mount your EFI partition using `sudo diskutil mount /dev/diskXsY` where `X` is the disk and `Y` is the partition. For example, I would mount `/dev/disk0s2` as that is my EFI partition. ![alt text](https://cdn.discordapp.com/attachments/782341614659305482/782344498700222514/unknown.png)
    - Depending on which method you have used to install macOS, you can do one of the following:
        - If you have used the full macOS installer, download this repo, unzip it, and do the following: `sudo cp -r ~/Downloads/Dell-Optiplex-7010-Hackintosh-OpenCore-master/EFI/* /Volumes/NO\ NAME/EFI`.
        - If you are installing from the recovery installer, do the following: `sudo cp -r /Volumes/USB/EFI/* /Volumes/NO\ NAME/EFI`.
        - If the OpenCore bootloader does not show, make sure your [BIOS settings](https://dortania.github.io/OpenCore-Install-Guide/config.plist/ivy-bridge.html#intel-bios-settings) are correct. If they are correct, and you are still having this problem, try to clean NVRAM by doing the following:
            - boot to your USB (which has OpenCore)
            - Press space
            - Select "CleanNvram.efi". Unplug your USB and check boot options. You should now have OpenCore bootloader from your EFI!

There are also other things you can do after installing macOS. If you would like to do anything else such as fixing your USB ports, you can do so here [Post Install](https://dortania.github.io/OpenCore-Post-Install/#how-to-follow-this-guide). I have not done much here, since I am fine with how macOS is working for me.

## Sources
- [OpenCore Guide](https://dortania.github.io/OpenCore-Desktop-Guide/)
- [Hackintosh Discord](https://discord.com/invite/8aKs69x)
