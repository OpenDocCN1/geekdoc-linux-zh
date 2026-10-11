# # Checking for Linux Compatibility

After you narrow your choices down to a few computers, you should begin investigating the computers' capability to run Linux. Among x86 computers, you rarely need to be concerned with the CPU or motherboard. Your choice of CPU and motherboard are important in determining your overall system speed, but Linux seldom has problems with specific models. In terms of Linux compatibility, you should focus on other components, in particular:

+   * **Video hardware** Find out what video chipset the computer uses, and then check this against the supported video hardware in XFree86 (http://www.xfree86.org). Chapter 12, "Video Cards," covers this matter in detail.
+   * **SCSI host adapter** Most x86 computers sold today do not include SCSI adapters. If you want this feature, you should be sure that the SCSI host adapter is supported in Linux. Chapter 9, "SCSI Host Adapters," covers this matter in detail.
+   * **Modem** Most x86 computers that include modems ship with software modems, many of which are unusable in Linux. Read Chapter 18, "Modems," and ask any vendor about this matter explicitly.
+   * **Sound card** Most sound cards are supported in Linux. Find out what audio chipset a computer uses, and then research Linux support for that chipset. Chapter 10, "Sound Cards," covers this matter in detail.
+   * **USB** If the computer uses a USB keyboard or mouse, I recommend you bypass it or ask for the older AT-style keyboard and a PS/2 mouse. Although you can use USB keyboards and mice in Linux, the support is still fairly new. Chapter 15, "Keyboards and Mice," covers this matter in detail.

# **NOTE**

> The preceding advice about USB devices applies to distributions based on most 2.2.x kernels. When distributions based on 2.4.x kernels become common, USB keyboards and mice will become much less troublesome. A few distributions today include USB support sufficient to handle keyboards and mice, so if you're really tempted by a system that uses these devices, check your favorite distributions for support details.

+   * **Network cards** Make sure any network card included in the computer is Linux-compatible. Linux support for network cards is excellent, as described in Chapter 17, "Network Hardware," but a quick check into the matter is worthwhile.
+   * **Printers** Retailers often offer bundles of computers with printers. Unfortunately, these bundles often include very low-end printers for which no Linux drivers exist. You should be cautious, and read Chapter 20, "Printers," before buying such a bundle.