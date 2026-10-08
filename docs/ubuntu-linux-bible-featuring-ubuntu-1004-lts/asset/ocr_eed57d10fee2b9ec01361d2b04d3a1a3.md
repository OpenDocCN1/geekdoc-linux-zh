# Chapter 24: Using Virtual Machines and Emulators

Beyond simply summarizing the boot information for your new virtual machine, this dialog points out that you may need to use the Devices Unmount command to manually unmount your boot media during installation. It is a good thing to remember if you find that your virtual machine is booting from the installation media again after a reboot.

To proceed, click Finish. The "First Run" dialog closes, and your new virtual machine should start to boot from the specified installation media.

To interact with the virtual machine during the installation process (and beyond), you will need to click inside the VirtualBox window so that the virtual machine has the input focus for your mouse and keyboard. The first time you do that, you will see a dialog like the one shown in Figure 24-14.

# FIGURE 24-14
VirtualBox keyboard/mouse focus explanation dialog

![](bbox=[0.058, 0.388, 0.538, 0.706])

The "Auto capture keyboard" option makes it easy to interact with a virtual machine rather than sending all mouse and keyboard events directly to the host system. However, some keyboard commands, such as the Ctrl+Alt+Delete required for initiating Windows logins, might accidentally shut down your host system, so you should send this sequence by selecting the "Insert Ctrl-Alt-Delete command from a virtual machine's Machine menu." Capturing keyboard input also makes interacting with the virtual machine more precise because