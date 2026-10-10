name is the same as the machine name. Set the size. I suggest 65 GB to have enough to comfortably build the Yocto project. When you click the **Create** button, the machine is created.

There are some settings you'll want to change in the guest machine itself.

+   In `General > Advanced`, set `Shared Clipboard` and `Drag 'n Drop` to `Bidirectional`.

+   In `Network`, change `Attached to:` to `Bridged Adapter`. Make sure the correct adapter is selected. If your workstation has both wired and wireless connections, you might want to enable the second adapter. Then you can connect the target board directly to the workstation through the Ethernet port, and use the wireless port for Internet access. Note that VirtualBox makes all network adapters appear to the guest as an Intel PRO/1000.

+   If you are using a USB-to-Serial converter, plug it in. Then in `USB`, click the `Add a USB filter` icon on the right, and select your converter. This allows it to be automatically connected to the guest machine whenever it is plugged in.

+   In `Shared Folders` you'll probably want to set up a shared folder so that you can easily move files between the host and the guest. Click the `Add a new shared folder` icon on the right. Browse to the folder you want to share and give it a name. The name becomes the device you mount in the Linux guest.

+   When you're ready to boot the new guest and install Linux, go to `Storage` and click the optical disk icon under `Controller: IDE`. Then click the optical disk icon on the far right and select the ISO file for your distro, or the physical drive if you're using a real DVD.

After you get Linux installed and booted, you'll find there are some limitations to the display and mouse in basic VirtualBox. The display size is limited, and the mouse works either in the host or the guest, but not in both. These limitations are overcome by installing the VirtualBox Guest Additions.

If you're new to Linux, the instructions in this section may not make much sense until you've read Chapter 3, Introducing linux. You'll need the GCC compiler package installed (you'll need that anyway as we go along) and the kernel headers package for the kernel version you're running. The kernel headers package should be installed as part of the initial installation.

Click the VirtualBox `Devices` menu and select `Insert Guest Additions CD Image`. As root user, mount the CD image. In a shell window, cd to the just-mounted image and execute:

```
sh ./VBoxLinuxAdditions.run
```

This script builds several kernel modules. Restart the guest machine when the script finishes. You can now set the guest display to full screen if desired, and the mouse works seamlessly between the host and guest.