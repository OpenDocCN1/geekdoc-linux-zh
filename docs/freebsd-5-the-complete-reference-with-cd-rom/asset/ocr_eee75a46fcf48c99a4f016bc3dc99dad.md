# # Supported Audio Hardware

To learn if your sound card is supported, check the HARDWARE.TXT file that ships with FreeBSD (it's in the root directory of the installation CD-ROM). The section of this file entitled "Audio Devices" specifies which chipsets are supported. As with many hardware devices, this list appears deceptively short; many of the devices listed are chipsets that are used in many different products. For instance, Crystal Semiconductor, ESS, and OPTi chipsets are used in many sound cards; and the Intel and VIA drivers work with the audio support included on many motherboards.

> **Tip**
> 
> *If your motherboard has built-in audio support that doesn't work with FreeBSD, you can still add a regular sound card and ignore the built-in audio device. Using the BIOS to disable the built-in sound support can help avoid conflicts if you do this.*

You can find the kernel sound modules compiled on your FreeBSD 5.0 system in `/boot/kernel/`, or `/modules` for FreeBSD 4.x. These files have names that begin with snd, so typing `ls /boot/kernel/snd*` (`ls /modules/snd*` on FreeBSD 4.x) should reveal the available sound modules. If you've recompiled your kernel and included your sound support in the new kernel, though, you won't find the module in this location. If you can't seem to find an appropriate kernel module, you may need to recompile your kernel with support for the appropriate device, as described in Chapter 12.

Unfortunately, determining which driver to use isn't always easy. There are two problems you may need to overcome:

+   - **Determining your audio chipset** You may not be able to tell which chipset a specific sound card uses. You may be able to glean clues from a Windows driver or Windows device listing, if your computer dual-boots to Windows; or you may be able to find the information by inspecting the chips on the board. The FreeBSD `dmesg` output may also contain clues, if FreeBSD can auto-detect the sound card.
+   
+   - **Matching the chipset to the driver** The chipset list in the HARDWARE.TXT file specifies the driver name associated with most drivers. The names are also usually related; for instance, `snd_ess.ko` is the driver for ESS chipsets, and `snd_via82c686.ko` is the driver for VIA chipsets.

If you can't determine with certainty which driver to use, you can try loading modules randomly or deterministically, as described in the next section, "Starting Sound Support." You'll be able to load an incorrect sound module, but it won't work. Chances are it won't do harm, although in theory it might cause other devices to malfunction in some rare situations.