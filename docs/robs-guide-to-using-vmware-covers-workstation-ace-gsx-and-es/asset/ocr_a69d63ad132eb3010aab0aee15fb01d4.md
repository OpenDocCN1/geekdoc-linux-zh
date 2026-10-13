# 10 Transferring Data To and From a Virtual Machine

Your virtual environment will not be a static environment. You will probably have to install applications in your virtual machines or you may have created data inside of your virtual machine that you need to store on another computer. This chapter describes several ways in which you can do that with the VMware built-in functionality and by using other methods.

To install software inside a virtual machine, you can do it the same way you would normally do on a physical computer. You can attach a CD-ROM drive, floppy drive, or USB storage device to your machine to install the software from a removable device. But if the installation source resides on your host computer, you can also directly access it. There are many ways to transfer not only software but also data to and from a virtual machine. Let’s see how.

There is also an advanced method available with the VMware DiskMount utility. Section 7.4: “Using the DiskMount Utility” explains how to use this utility in detail.

# 10.1 Using the Clipboard (Windows only)

Windows contains a clipboard which can hold all sorts of data, such as text files, images, and so on.

VMware Workstation supports transferring text fragments (no images) between the host and the guest or between two guests.

The contents of the clipboard is accessible via the default keys (Ctrl-C Ctrl-X Ctrl-V) and viewable with the ClipBook viewer (CLIPBRD.EXE)

This feature is turned on by default and can be turned off via Edit → Preferences → Input tab (see Figure 10.1). Disable the checkbox to disable this feature if needed.

![](bbox=[0.48, 0.78, 0.92, 0.95])