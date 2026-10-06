
# Chapter 12 ♦ Running Yellow Dog Linux

◆ Anaconda installer — Yellow Dog takes advantage of the well-tested Anaconda installer for easy installation.

◆ Kudzu hardware detection — Starting with the Fedora Core kudzu facility for detecting and configuring hardware, Yellow Dog has a stable foundation for probing equipment that has been extended to Mac hardware.

Refer to Chapter 8 for more information on the Fedora Core project and some of the specifics regarding its implementation.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_398_0.png)

# Installing Yellow Dog Linux

Before you can install Yellow Dog Linux, you need to get a copy of it from some of the many resources available. The first and most recommended avenue is to purchase it from the vendor. This has the dual effect of acquiring it from the source as well as supporting the company that creates Yellow Dog Linux so it can continue development for the PowerPC platform.

To purchase Yellow Dog Linux from Terra Soft Solutions, visit the Terra Soft Web store at http://terrasoftolutions.com/store/. When purchasing from Terra Soft Solutions, you receive the following in a box set:

- Four CDs and source CDs.

- Getting Started with Yellow Dog Linux, a book that covers all the information a beginning Yellow Dog user would need to know to get a fully operational Yellow Dog system running.

- Optional 60 days of installation support (you can purchase the box with or without support, depending on your needs and skill level with Linux).

- Other goodies (sticker, flexible flier depending on package purchased).

- The knowledge that you are supporting the company that created the product, allowing for further development.

Alternatives to purchasing the Yellow Dog Linux box include:

- Purchasing a subscription to YDL.net — This is Terra Soft Solutions' online resource for Yellow Dog users. You can get e-mail accounts and Web space as well as prerelease access to the latest version of Yellow Dog Linux before it is available for general release. The costs vary depending on version you choose. More information is available at www.ydl.net.

- Downloading and creating your ISO — You can download the distribution from one of the many Linux mirrors as identified at http://yellowdoglinux.com/resources/ftp_mirrors.shtml and burn your ISO.

# 368 Part III ♦ Choosing and Installing a Linux Distribution

## Hardware Support

Hardware support with the Linux operating system was a major issue in the past, but as Linux's popularity has grown, many device makers have provided access to their hardware drivers or in some cases have created hardware drivers for Linux. While this is still an issue with hardware that is brand new in the X86 community, the effects are lessened with the PowerPC platform because hardware is generally created to Apple's exacting standards. Terra Soft Solutions' focus on Apple hardware generally fewer variations in hardware add to support being faster for the PowerPC platform.

One of the great things about Yellow Dog Linux is that as you dig into it, you discover that some of the hardware issues faced by the X86 Linux (such as with Winmods, the plethora of hardware configurations and so forth) are minimized or eliminated. With Terra Soft Solutions, a fully authorized Apple Value Reseller, you are assured that the hardware you are using will be supported. There are some native hardware support differences with the release of YDL 4.0 and 4.1, but the fully capable 3.0.1 version covers any gaps of the 4.0.x series.

In addition to being able to install Yellow Dog Linux on your own Apple hardware, you can purchase Apple hardware from Terra Soft Solutions with Yellow Dog Linux preinstalled.

Terra Soft Solutions has developed official lists of hardware configurations that have been specifically tested with Yellow Dog Linux (http://yellowdoglinux.com/support/hardware/breakdown/index.php). The Yellow Dog 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

# Chapter 12 ♦ Running Yellow Dog Linux

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs.
- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs.
- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

## Planning Your Installation

Before starting, back up any data you want to retain. The next step is to determine whether you are going to multiboot or install.

## Installing OS X and Yellow Dog Linux on One Hard Drive

If you want to install OS 9 or below in addition to Yellow Dog Linux on one hard drive, you can perform the following for a dual-booted machine:

1. Boot the Mac OS CD by holding down the C with the Mac OS CD inserted.
2. Double-click the Utilities or Disk Tools.

In addition to being able to install Yellow Dog Linux on your own Apple hardware, you can purchase Apple hardware from Terra Soft Solutions with Yellow Dog Linux preinstalled.

Terra Soft Solutions has developed official lists of hardware configurations that have been specifically tested with Yellow Dog Linux (http://yellowdoglinux.com/support/hardware/breakdown/index.php). The Yellow Dog 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)

Most notably missing from Yellow Dog Linux 4.0 and 4.0.1 supported hardware is Old World ROM or beige G3 and below hardware such as 8500s, 7200s, and Performa PowerWCs. YDL 3.0.1 supports this hardware and most of the hardware currently supported by Yellow Dog Linux 4.0.1. The hardware supported and tested for Yellow Dog Linux 4.0.1 includes:

- Power Mac G3 (Yosemite Blue and White 300–400 MHz G3)
- Power Mac G4 (Power Mac G4 PCI 350–400 MHz G4 and above)
- Power Mac G5 (1.6 GHz G5 and above)
- Mac Mini
- iMac (Rev A,B 233 MHz G3, eMac G4, and iMac G5)
- PowerBook (Lombard 300–400 MHz G3, Pismo 400–500 MHz FW G3, Titanium 400–1 MHz G4, Powerbook 12" 867 MHz–1.33 GHz, and Powerbook 15–17 1.0–1.5 GHz G4)
- iBook (300–366 MHz G3—800 MHz 1.2 GHz G4)
- HPC (Xserver Cluster Node 1 1.33 MHz G4, Single/Dual 1.33 MHz G4, Cluster Node 2 2.0 GHz G5, and Single/Dual 2.0 GHz G5)
