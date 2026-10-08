
## Chapter 22: Going Wireless

## Note

Before installing Windows drivers, you must make sure that they are available on your Ubuntu system. This usually involves either putting the driver CD in your system so that it is available as /media/cdrom (or something similar, depending on the drives in your Ubuntu system) or copying a zip archive containing the drivers to your Ubuntu system and using the unzip command to extract the contents of that file into an Ubuntu directory.

Installing the ndisgtk package creates the System Administration Windows Wireless Drivers menu item on an Ubuntu System, which you can select to start the ndisgtk application. Figure 22-8 shows the initial driver installation dialog that is displayed when you first start this application.

### FIGURE 22-8

The ndisgtk startup dialog

![](img/1a233c34336fbf5a85d6eb785e401709_854_0.png)

To install a driver, click "Install New Driver." This displays the dialog that enables you to select the INF file associated with a specific Windows driver, as shown in Figure 22-9. An INF file with an .INF or .inf file extension that contains a description of a Windows driver, its installation options, associated files, and so on.

### FIGURE 22-9

The INF file selection dialog for a Microsoft Windows driver

![](img/1a233c34336fbf5a85d6eb785e401709_854_1.png)

## Part II: Ubuntu for Desktop Users

Click the Location button to display a standard file dialog that enables you to navigate to the directory containing the Windows driver and select the appropriate INF file. After navigating to and selecting the appropriate file, click Open to select that file and close the navigation dialog. The dialog shown in Figure 22-9 re-displays, showing the name of the selected INF file. (In this particular example, I'm installing the Windows drivers for an SMB W541C wireless adapter, although you wouldn't be able to guess that from the name of the driver or INF file.)

Click Install to install the driver and associated files for use by the ndiswrapper kernel module. The dialog shown in Figure 22-8 re-displays, now listing the driver that you've just installed and identifying if the hardware associated with that driver was located, as shown in Figure 22-10.

Loading the driver and detecting associated hardware

![](img/1a233c34336fbf5a85d6eb785e401709_855_0.png)

At this point, you can click Close to terminate the Windows driver installation process. Your network connection management software, whether Wicd or a Network Manager app, should detect the new interface and offer options for using it.

To ensure that the ndiswrapper kernel module loads each time you restart your Ubuntu system, the ndiswrapper kernel module must be listed in the file that identifies modules that should be loaded at boot, /etc/modules. This should have happened when you installed the package, but you may want to check. If you need to add an entry for this module, you can do so using your favorite text editor (which you must start using sudo so that you can edit this file), or via a command as the following:

```bash
$ sudo echo "ndiswrapper" >> /etc/modules
```

Make sure that you use two brackets, not just one! If you accidentally use only one angle bracket, you will overwrite the contents of your existing /etc/modules file with a single line containing the name of the ndiswrapper module, which will probably certainly cause things like your mouse and printers to behave.

## NDIS Wrapper Tips and Tricks

As you can see from the previous section, many Microsoft Windows drivers "just work" with the ndiswrapper kernel module when installed correctly. Unfortunately, some don't. I won't pretend to have tested every piece of wireless hardware and its associated Windows drivers (though I'd be happy to try if you just sent me a sample of the hardware that I can keep), but I used many different ones with a wide selection of wireless hardware when configuring laptops for a variety of customers, coworkers, and friends.

For one, the most frustrating sets of experiences has been with a variety of LinkSys WPC54g wireless PCMCIA cards, all of which I have gotten working, but only after significant driver gymnastics, head scratching, Google searches, and commiseration with fellow demons (I was originally planning to title this section "The LinkSys WPC54g, or I Spent My Summer Vacation," but I am trying to generalize what I've learned rather than provide a single set of instructions). By these, there are great cards that 802.11g (and 802.11b), because I typically find LinkSys hardware to be inexpensive and reliable, I often recommend them to friends. Unfortunately, a huge problem with these cards is that LinkSys has used a variety of wireless chips over the years, so they often use different drivers, each of which requires its own to get it working with the ndiswrapper module.

One key is to make sure that you have the right Windows drivers in the first place. For example, some of the 54g cards use a Realtek 8180 chip, and therefore, only work with these drivers. Others use Texas Instruments AXX-1xx chip, while others are rumored to use a Marvel BCM43xx. If you can't identify the chipset by reading the product literature, you can usually identify it by using the lsp tool to list all the PCI devices on your system.

Part II: Ubuntu for Desktop Users (Note: This text segment appears to be corrupted or fragmented based on the provided OCR source, containing repetitive headers and broken sentences. I have preserved the legible flow below.)

As you can see from the previous section, many Microsoft Windows drivers "just work" with the ndiswrapper kernel module when installed correctly. Unfortunately, some don't. I won't pretend to have tested every piece of wireless hardware and its associated Windows drivers (though I'd be happy to try if you just sent me a sample of the hardware that I can keep), but I used many different ones with a wide selection of wireless hardware when configuring laptops for a variety of customers, coworkers, and friends.

[The remaining text in the OCR source has been omitted as it consists of nonsensical fragments and repeated headers.]
