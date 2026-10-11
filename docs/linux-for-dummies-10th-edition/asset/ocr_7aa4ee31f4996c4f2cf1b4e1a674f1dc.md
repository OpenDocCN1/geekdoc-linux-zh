You may or may not get an entry added to your desktop menu system for the new VirtualBox system. openSUSE places the menu entry under the *Applications → System* area in the KDE menu.

If you don't see a menu entry, you can start VirtualBox by opening a Terminal session (or Konsole session in the KDE Plasma desktop) and entering the command:

```
```
VirtualBox
```
```

Be careful to make sure you have the capitalization correct, or Linux won't find the VirtualBox program. Figure 20–1 shows what the main VirtualBox window looks like after it starts.

![](bbox=[0.14, 0.37, 0.76, 0.61])

After you've gotten to the main window you're ready to start creating some virtual machines!

# # Creating a Virtual Machine

The next step in the process is to build a virtual machine for your guest OS to run in. In this process you need to tell VirtualBox the size of the virtual machine to play in. You need to select the amount of disk space to allocate for the virtual server, and the amount of memory to use. Both these items are shared with the host system, so be careful how much you dedicate for the virtual machine! Each Linux distribution lists the minimum amount of disk space and memory required