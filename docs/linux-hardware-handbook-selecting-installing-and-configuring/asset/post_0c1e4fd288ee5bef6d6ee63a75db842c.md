
## Linux PC Card Support

The 2.2.x kernel series includes essentially no support for PC Card devices. Instead, a separate package of kernel modules is available from the Linux PC Card site, http://pcmcia.sourceforge.org. You can obtain these drivers and install them separately from the kernel. When installed, these drivers work as if they were normal kernel modules. In the 2.3.x kernel, drivers for some PC Card devices exist in the main kernel. PC Card Ethernet adapter support, for instance, exists in the Network device support, PCMCIA network device support kernel menu. For other uses, such as PC Card hard disk support, you must still acquire the separate PC Card support package.

PC Cards are designed to be hot-swappable—that is, you can insert or remove them when the computer is powered on. This fact presents certain challenges to Linux, which tends to assume devices won’t disappear unexpectedly. Therefore, PC Card support in Linux requires special software. This support is provided by a feature known as Card Services, which is available from the Linux PC Card site. When installed, Card Services controls PC Card access through files in the /etc/pcmcia directory. There’s a script in this directory for each type of PC Card—for instance, network and ide.

> **NOTE**
> Devices such as palmtop computers and digital cameras frequently use *Compact Flash* (CF) or SmartMedia cards for storage. These devices are *not* hard disks, but they can look like PC Card IDE hard disks when coupled with an appropriate adapter. You can therefore use Linux’s PC Card support to access these storage media. You can use this feature to read images you’ve recorded with a digital camera because these devices use the FAT filesystem.

Fortunately, most Linux distributions ship with PC Card support enabled by default. You therefore don’t normally need to be concerned with starting Card Services yourself. When you insert or remove a PC Card, Card Services runs the appropriate script in /etc/pcmcia. This script shuts down or starts up whatever functions are required for the device. For instance, when you insert a PC Card Ethernet adapter, Card Services loads the PC Card’s kernel driver and then activates the Ethernet interface, including assigning its IP address, setting a default route, and so on. When you eject that Ethernet card, Card Services shuts down the interface, removes the interface’s routing table entries, and so on.

## The Importance of Audio/Video Support

When you buy a desktop computer, you almost always have the option of replacing troublesome components. For instance, if your video card doesn’t work to your satisfaction, you can remove it and install another card. Some desktop systems support some features through chipsets built into the motherboard, but you can usually disable these features and install a separate card to handle these functions. Not so with notebooks. Because of the severe space constraints, notebook computers don’t include conventional ISA or PCI slots. To some extent you can use a PC Card or possibly an external device to work around non-functional integrated components, such as a modem. Sound and video, however, can be virtually impossible to replace. It’s critically important that any notebook computer you purchase use a video chipset that’s supported by XFree86 or a commercial Linux X server. You might or might not consider sound support to be so critical but, if you do, you must be equally sure that Linux supports your computer’s sound hardware.

### Locating Support for Your Hardware

Fortunately, most notebook manufacturers make it clear what video hardware they use. Ads for notebook computers typically include this information. Because the video support is integrated into the motherboard, the ads usually specify the video chipset that’s in use. This is precisely what you need to know to locate a Linux driver, as described in Chapter 12, “Video Cards,” and Appendix A, “Linux Device Drivers.”

Sound chipsets are not always advertised quite as clearly as are video chipsets. Many manufacturers merely report that their notebooks have “SoundBlaster-compatible” sound, or they trumpet the manufacturer of the speakers, but don’t mention who makes the sound chipset in use. In some cases the sound chipset is integrated into the motherboard chipset, and isn’t well known to consumers. Many notebook computers sold in 2000 that use VIA chipsets, for instance, incorporate sound support from the VIA 82c686a, which is incorporated into some of VIA’s recent motherboard chipsets.

In the case of both video and audio chipsets, you can usually find what the computer uses if you can access the computer when it’s running Windows. To do so, open the System item in the Windows Control Panel, as shown in Figure 23.3. Click the Device Manager tab and then click the plus signs next to the Display adapters and Sound, video and game controllers items to reveal the video and audio chipsets used by the computer. In the case of the computer used to create Figure 23.3, the display adapter is a Trident CyberBlade i7, and the audio support comes from a VIA PCI audio controller.

Of course, if you want to find hardware a notebook computer uses before you buy it, this method requires that you have access to the computer. Most local computer stores run display samples of notebook computers, so you can usually check the hardware before you buy. This might not be possible for mail-order hardware, however. In this case, you might need to rely on the sales staff or some other resource. The Linux on Laptops Web page (http://www.cs.utexas.edu//kharker//linux-laptop/) is particularly useful in this respect. This Web page includes links to a large number of descriptions of Linux systems run on a wide variety of notebook computers. Many of these individual pages include links to the XF86Config files that the maintainers use. You can then download these files and use them yourself if you buy the same or a similar computer, thus saving you some time and effort configuring XFree86.

![](img/860d0c38bd76c9ded976e9d1e179ef25_619_0.png)

**Figure 23.3**
*The Device Manager tab in the Windows System Properties dialog box can reveal the chipsets used by a notebook's audio and video hardware.*

If you buy a new notebook that's not listed on one of these pages, you can do others a great favor by putting together a Web page describing your experiences and submitting it for inclusion on the Linux on Laptops page. Even a brief description stating that the computer works, and specifying your distribution, can be helpful.

When you know what chipsets a notebook computer uses for audio and video features, you can go looking for support for those chipsets. Chapters 10, "Sound Cards" and 12 can help you in this respect, as can Appendix A. In brief, though, you should check several Web sites and other resources for information:

- **The Linux on Laptops Web page** If the computer you're considering is listed on this page, you can generally find the information you need there.
- **The Linux kernel configuration options** Check the Linux kernel sound configuration options for standard support for your sound hardware.
- **The Shareware OSS site** Check http://www.4front-tech.com for information on commercial Linux sound drivers.
- **The ALSA site** Check http://www.alsa-project.org for information on the Advanced Linux Sound Architecture (ALSA) drivers.
- **The XFree86 site** Check http://www.xfree86.org for information on video support in XFree86. You might need to dig a bit on this site to find the information you require.
- **The SuSE site** SuSE (http://www.suse.com) contributes a lot to the XFree86 project, and often makes early versions of its XFree86 drivers available from its own site.
- **The Accelerated-X site** Accelerated-X, from Xi Graphics (http://www.xig.com), is a commercial alternative to XFree86.
- **The Metro-X site** Metro-X, from MetroLink (http://www.metrolink.com), is another commercial alternative to XFree86.

If you think it’s likely that you can make a notebook’s hardware work under Linux, but you’re not positive you’ll succeed, you might still consider buying the computer. I recommend doing so only from a store with a good return policy, however. If you think you might need to use software with which you’re not familiar, you might want to try that software on a desktop system, if possible, before buying the notebook. For instance, if your target notebook’s sound chipset is supported by ALSA but not by the standard kernel drivers, you might want to try ALSA on another system, simply to familiarize yourself with it.

## Replacement Hardware

If your video chipset doesn’t work under XFree86, you might still be able to use the computer in text mode. To use X programs, you’ll need to link the computer to a network and use an X server running on another computer. That’s not very convenient for a notebook, but it might be acceptable in a pinch.

If your audio chipset doesn’t work under Linux, your options are somewhat broader, although still not good. Two possibilities are:

- **USB speakers** These devices don’t work through a standard sound card; instead, the sound card functions are included in the speakers themselves. You’ll need to lug the speakers around with you wherever you go, or at least wherever you want sound support. You’ll also need to use a 2.3.x or later kernel, or apply a back-port of the 2.3.x USB support to a 2.2.x kernel.
- **PC Card sound card** There are a small number of PC Card sound cards on the market. Most of these aren’t well supported in Linux, however. For the latest information, check http://pcmcia.sourceforge.org/ttp/SUPPORTED_CARDS, which has links to information on supported PC Cards and projects to add new support. As with USB speakers, you’ll need to carry around a set of conventional external speakers.

**CHAPTER 23**
**NOTEBOOKS**
