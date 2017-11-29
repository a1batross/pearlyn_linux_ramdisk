# A basic and very small generic ramdisk

This ramdisk should be enough for most Linux distributions, and made for Razer Forge TV. Should work on other devices too!
I don't take responsibility for any bricked devices.

Linux Installation:

0. Take any ARM Linux distribution(I tried Gentoo & Arch Linux ARM);
1. Take original Android ROM, make sure you have unlocked bootloader(fastboot oem unlock);
2. Take kernel source code for your device. Recompile it with "CONFIG_DEVTMPFS=y" support and try to run Android with this kernel(see steps 4 repacking your boot.img);
3. Compile BusyBox from source code(patched for Android: https://github.com/LineageOS/android_external_busybox). Use "busybox_config" from this repo by renaming it to ".config";
4. Place STATIC version of it in /sbin/busybox;
5. Compile mkbootimg from Android Core [source code](https://github.com/LineageOS/android_system_core). If you don't want to compile, [there](https://github.com/xiaolu/mkbootimg_tools) is precompiled versions.
I know, you may ask about abootimg from Ubuntu/Debian repository. I tried it on my device, it didn't worked.
MediaTek boot.img are known for it's special format. Google it. Maybe you want take a look for a [MediaDeb](https://github.com/MediaDeb) project;
6. Open "init" file, read all the comments and change it anyhow you need(partition names, for example). If you have an Ethernet port and cable, use FORCE_DROP=1 for telnet access;
6. Unpack boot.img and replace contents of ramdisk with this repo. Pack boot.img;
7. Flash it through fastboot;
8. Try to run. If you have "FORCE_DROP=1" set, the device should be available through Telnet. Check if everything is fine;
9. Use "simg2img" utility to convert system.img to RAW system.img;
10. Mount it and copy contents of distribution image to mounted directory. Make sure you don't lost owners and permissions;
11. Use "img2simg" utility to convert RAW system.img to sparse system.img;
12. Flash it.
13. Boot it.
14. If you have a network access to the device, check it through telnetd. If it's still available, init-script encounted an error. Fix it.
15. Repeat 12-14 for any boot.img modificaiton, until device will not be booted fully.
16. ???
17. PROFIT!



