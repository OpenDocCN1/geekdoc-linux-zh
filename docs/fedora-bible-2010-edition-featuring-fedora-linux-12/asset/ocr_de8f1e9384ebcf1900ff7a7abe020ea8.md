A text-based version of the bootloader should appear. You will probably have to press a key to prevent the system from booting the default boot entry. Edit the boot loader as needed (for example, you may want to add a `1` to the end of the kernel line to enter run level 1) and have the bootloader continue. After that, press `Ctrl+⌥` to close the console window and return to your regular `VNC` view of the guest.

Besides the issues just mentioned, you can use your virtual guest from within the VNC window as you would any operating system directly from the desktop. When you are done using it for the moment, just close the window. While this closes your view to the running system, it does not stop that system from running. Just double-click the guest's entry in the Virtual Machine Manager window and you can begin viewing it again.

# ## Cloning guests

Once you have a virtual guest working the way you want it, why not repeat your fun? By cloning your virtual guest you can have a copy of that guest that can run on your host system or to run on another system. Here's how you clone a virtual guest:

+   1. **Pause or shut down the guest.** If the guest you want to clone is running, select Shut Down from the running guest. Then choose Shut Down or Force Off. If you prefer, you can simply pause the guest by selecting the Pause button.

+   2. **Select Clone.** From the guest's Virtual Machine window, select `Virtual Machine → Clone`. A Clone Virtual Machine window appears, as shown in Figure 25-6.

![](bbox=[0.26, 0.51, 0.78, 0.87])

**Figure 25-6:** Create clones of useful virtual guests.