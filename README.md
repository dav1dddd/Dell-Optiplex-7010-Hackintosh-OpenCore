# Monterey
Monterey working on Dell Optiplex 7010
![alt text](https://i.imgur.com/zbBTSXW.png)

# How?
So here's what I did. I tried to upgrade from Big Sur, but it didn't go well. So it is a clean install method:
- Download macOS Monterey [here](https://drive.google.com/drive/folders/13kKd0waycFfW6y3H0IVP5wS27EYtbfxO?usp=sharing) it will say "com.apple.recovery.boot". Extract the zip and place the "com.apple.recovery.boot" on your FAT32 USB.
- Format USB as FAT32
- Add the "com.apple.recovery.boot" folder to USB
- Update the files in your EFI/OC with the ones in this branch. It is important that you do this, as otherwise sound will not work as the updated Lilu.kext and AppleALC.kext have macOS 12 support.
- Press space bar and you should be able to boot to your USB. Format and install macOS as normal.

## Post Install
- Reboot to OC bootloader and press space bar. You should have macOS 12 Recovery. Select it.
- Go to Utilities -> Terminal
- Type these commands, which will disable SIP (System Integrity Protection) and disable SSV (Sealed System Volume) checks at boot for the root volume, allowing the root file system to be modified:
    - `csrutil disable`
    - `csrutil authenticated-root disable`
- Download [OCLP](https://github.com/dortania/OpenCore-Legacy-Patcher/releases/download/0.3.1/OpenCore-Patcher-GUI.app.zip)
- Open OCLP and click "Patch System Volume". This will install kexts for Intel HD 4000 in `/System/Library/Extensions`
- Reboot. :)

If something isn't working, let me know in the [Issues](https://github.com/dav1dnix/Dell-Optiplex-7010-Hackintosh-OpenCore/issues) tab and I will try and help you with your problem.
