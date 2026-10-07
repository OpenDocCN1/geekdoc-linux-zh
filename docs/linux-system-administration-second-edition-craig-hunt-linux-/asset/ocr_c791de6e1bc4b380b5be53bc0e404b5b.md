that is on a separate disk, enter **linux dd**.

# ## Selecting an Installation Method

The first two screens ask you to select the language you speak and the type of keyboard you use. Assuming you booted from an IDE CD-ROM as we did, the next screen you’ll see is the Mouse Configuration screen, discussed in the next section. If you have a non-IDE CD-ROM drive, you’ll be offered an additional choice between SCSI and Other. If you choose SCSI, you’ll be prompted to select your SCSI Adapter from a list. Choose the adapter that most closely resembles the one in your system. If your adapter is not recognized, you may enter additional options for the driver. These options are the same ones that would be specified at the boot prompt to give the boot loader information about an unrecognized SCSI adapter. These options are discussed in Chapter 3.

If your CD-ROM drive is neither SCSI nor IDE, you must select the Other option. CD-ROM drives in this category are usually those run from a proprietary sound card. Such drives are extremely rare in modern computers; you’re only likely to find them in old 386 or 486 computers. You might have to specify options for the driver that supports such a card.

If you’ve forgotten to put the CD-ROM into the drive, you’ll be prompted to do so.

# ## Configure the Mouse

The install next moves on to the Mouse Configuration screen, which offers a number of style choices for PS/2, bus, and serial mice. Select the brand and style that matches your mouse. If none look right, you may select the appropriate Generic choice, and it should work. Select the correct device and port; if your system has been running Windows before, your selection should match the port used there. If you have a two-button mouse, you’ll want to select the Emulate 3 Buttons option near the bottom of the screen. This will allow you to simulate the third button by pressing both buttons at the same time. Three buttons are useful on a Linux system because X is built around a three-button mouse. The middle button is often used to paste text selections in X applications.

# ## Partition the Disk

The Install Options screen appears next. It requires that you choose the Install Type you’ve decided to use to partition your disk.

The options you’ll see on the Install Options screen are divided into Install options and the Upgrade option. The Install options are the ones we discussed before: Workstation, Server System, Laptop, and Custom System. These provide the partition schemes described earlier. There is only one Upgrade option. It keeps the existing partition scheme and just upgrades the software. For this example, we’re using the Server System installation since, as a system administrator, you are likely to be setting up server machines. You could also set up a server using a Custom installation to take advantage of the greater flexibility in partitioning and package selection. In the end, the Server System setup is easier and quicker to run through, but it is likely to produce a Linux installation that’s bloated with packages you never use. A Custom System setup can produce a trimmer system, but takes more up-front time and knowledge about what individual packages do. Because the server installation will write over any existing installation, the subsequent Automatic Partitioning screen warns you that it is about to erase any existing partitions on your hard drive and offers you the alternative of creating your partitions manually with either Disk Druid or fdisk. You are also offered the option of retracting your steps and performing a customized installation. To try out the partitioning process for yourself, select the Manually Partition with Disk Druid option and press the Next button. Figure 2.3 shows the Disk Druid Partitioning screen.

44