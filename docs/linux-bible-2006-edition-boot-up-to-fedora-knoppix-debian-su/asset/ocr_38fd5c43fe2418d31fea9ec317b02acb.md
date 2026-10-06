# Installing Mac OS 9 or Below, Mac OS X, and Yellow Dog Linux on Multiple Drives

Because of the way system boots, you should have the drive to which you plan to install Yellow Dog Linux as the first hard drive in the IDE chain, set as Master. Mac OS or Mac OS X should be placed as the second drive in the chain and have the jumper set to Slave.

Then install the other versions of Mac OS (9 or below or X) onto the other hard drives. You only need to select a drive other than the first one during the install procedure. You must install Yellow Dog Linux as the last operating system and on the first drive.

# Yellow Dog Linux 3.0.1 Special Considerations

All the planning previously applies to Yellow Dog Linux 3.0.1, but there is one special consideration to take into account. Yellow Dog Linux 4.0.1 supports only New World systems, which are the blue-and-white G3 and above systems.

> Note There are two versions of the G3, one has a beige case and that other has the blue-and-white case.

If you are installing Yellow Dog on a New World system, go to the next section, "Beginning the Installation."

If you are using an Old World system, which are beige G3 systems and below, refer to the Yellow Dog Linux Web site (http://www.yellowdoglinux.com) for information.

# Beginning the Installation

After you have determined how you will boot your system (multiboot or single Yellow Dog Linux boot) and have loaded Mac OS X or Mac OS 9 or below appropriate, you can begin installing Yellow Dog Linux. This procedure focuses on Yellow Dog 4.0.1, but special notes on 3.0.1 are included where appropriate.

+   1. Insert Yellow Dog CD 1 into your CD-ROM drive, reboot your system, and press C to boot off the CD-ROM.
2. If you downloaded Yellow Dog or have a burned CD-R, you may want to check your media by appending `mediacheck` to the end of any of the install types (see Step 3 for install types). For example:

```
install-safe mediacheck
```

This goes through all your media to determine if it is suitable for the operating system. This can save you a lot of time by determining that all of your CDs are good before you invest your time in the installation procedure.