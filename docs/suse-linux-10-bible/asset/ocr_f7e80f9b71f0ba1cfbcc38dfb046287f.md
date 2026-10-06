# ndiswrapper

If you do not use one of the popular wireless cards supported out of the box in SUSE, you can potentially use ndiswrapper. ndiswrapper is a great system that will enable you to wrap a Linux kernel driver around a Windows network card driver to be able to provide you with support for pretty any network card out.

> Before you start with the configuration of your networking with ndiswrapper, you must make sure you download the Correct Drivers. If you are using a 64-bit laptop (for an AMD 64), you must download the 64-bit version of the driver. Similarly for a 32-bit laptop, you must use the 32-bit Windows drivers.

To get ndiswrapper working:

+   1. You need to install the ndiswrapper package by YaST. For more information about how to install new applications in SUSE, refer to Chapter 1.
2. In the YaST package search screen, search for ndiswrapper and select it for installation.
3. After ndiswrapper has been installed, you will need to download or copy the Windows driver package to your SUSE installation. We use the A-Link WL54H chipset as an example.
4. When downloaded, unarchive the package (Windows drivers usually come as a zip file, in this case use the unzip command — see Listing 15-17).

# Listing 15-17: Using unzip to Unarchive a Windows Network Driver

```
linux:- unzip WL54driver2.2.6.0.zip
Archive: WL54driver2.2.6.0.zip
inflating: RaLink2/rt2560.exe
creating: Win2K/
inflating: Win2K/rt2500.cat
inflating: Win2K/rt2500.INF
inflating: Win2K/rt2500.sys
creating: Win9me/
inflating: Win9me/rt2500.INF
inflating: Win9me/rt2509x.sys
creating: WinXP/
inflating: WinXP/rt2500.cat
inflating: WinXP/rt2500.INF
inflating: WinXP/rt2500.sys
```