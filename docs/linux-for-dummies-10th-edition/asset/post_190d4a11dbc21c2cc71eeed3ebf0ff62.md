
You may or may not get an entry added to your desktop menu system for the new VirtualBox system. openSUSE places the menu entry under the *Applications → System* area in the KDE menu.

If you don't see a menu entry, you can start VirtualBox by opening a Terminal session (or Konsole session in the KDE Plasma desktop) and entering the command:

```
VirtualBox
```

Be careful to make sure you have the capitalization correct, or Linux won't find the VirtualBox program. Figure 20–1 shows what the main VirtualBox window looks like after it starts.

![](img/577d3bff979ee86b07f9836e0df274ce_399_0.png)

After you've gotten to the main window you're ready to start creating some virtual machines!

## Creating a Virtual Machine

The next step in the process is to build a virtual machine for your guest OS to run in. In this process you need to tell VirtualBox the size of the virtual machine to play in. You need to select the amount of disk space to allocate for the virtual server, and the amount of memory to use. Both these items are shared with the host system, so be careful how much you dedicate for the virtual machine! Each Linux distribution lists the minimum amount of disk space and memory required to run, plus it's a good idea to add extra disk space so you have room to save your own programs and data. I like to give the virtual machines at least 20GB of disk space and 4GB of memory, more if it's available.

Follow along with these steps to create your first virtual server sandbox:

1. If you closed the VirtualBox main window, open it.
2. Click the New icon in the VirtualBox toolbar area.
   - A wizard starts to walk you through creating the virtual machine.
3. Assign a name to the virtual machine, select the operating system you plan on installing, and click the Next button.
   - The drop-down menu gives you lots of choices for the types of operating systems you can install in the virtual machine. Select the operating system you want to install, as shown in Figure 20-2.

![](img/577d3bff979ee86b07f9836e0df274ce_400_0.png)

The VirtualBox software package provides a way to run multiple operating systems from inside a host system, but it doesn't provide any licenses for those operating systems. It's your responsibility to obtain a proper license for any operating system software you install in VirtualBox.

![](img/577d3bff979ee86b07f9836e0df274ce_400_1.png)

4. Select the amount of memory to dedicate for the virtual machine and click the Next button.
   - VirtualBox provides a recommended amount of memory to select based on the operating system you selected, and the amount of memory installed on the host system. You can increase or decrease that amount using either the slider, or typing the amount into the text box. Remember, from the amount of memory you dedicate for the virtual machine is taken from the amount of memory available to the host server while the virtual machine is running!
5. Select hard disk emulation for the virtual machine and click the Next button.
   - VirtualBox emulates a hard drive by creating a large file on the host system. The amount of disk space you select for the hard drive is created inside the file, so it can't be larger than the disk space available on the host system.
   - Select the Create a Virtual Hard Disk Now radio button to create a new hard drive file. If you happen to have an existing hard drive file, select the Use an Existing Virtual Hard Disk File radio button and browse to its location using the file browser.
6. If you selected to create a new hard disk file, the next dialog box asks you to select a storage type. Select the type and click the Next button.
   - The VirtualBox Disk Image (VDI) is a proprietary format that can't be read by other virtualization software systems. However, it provides the best performance within VirtualBox. Select that if you just plan to run your virtual machine in VirtualBox.
7. Select the method of creating the storage file and click Next.
   - VirtualBox can either create the entire hard drive file at once (fixed size), or can create a base file and expand it as the virtual machine's operating system uses more disk space (dynamically allocated). By creating the disk space all at once you make disk access in the virtual machine faster, but eat up more disk space on the host system that may not get used by the virtual machine.
8. Select a name and location for the new hard disk file, along with the size of the file, and click the Create button.
   - You can place the hard disk file anywhere on the host system you have access to. Use the slider or the textbox to set the size of the hard disk file, as shown in Figure 20-3.

When you finish the wizard, your new virtual machine entry appears on the main VirtualBox window, shown in Figure 20-4.

Now that you have a virtual machine created, you're ready to start playing!

![](img/577d3bff979ee86b07f9836e0df274ce_402_0.png)

**FIGURE 20-3:**
Setting the virtual server hard disk file location and size.

![](img/577d3bff979ee86b07f9836e0df274ce_402_1.png)

**FIGURE 20-4:**
The virtual server entry in the VirtualBox window.

## Customizing a Virtual Machine

Before you can start entering your virtual world, you need to do a little more setup of your virtual machine. The New Virtual Machine Wizard sets up a generic environment, so you want to spruce things up a bit first. This section walks through how to customize the virtual machine and how to load your operating system in the virtual machine.

### Changing settings

Each virtual machine you create in VirtualBox has its own set of configuration settings. These configuration settings determine just what VirtualBox emulates in the virtual machine.

To get to the configuration settings, select the virtual machine entry on the left-hand side (refer to Figure 20-4) and click the Settings icon in the toolbar. The Settings dialog box, shown in Figure 20-5, appears.

![](img/577d3bff979ee86b07f9836e0df274ce_403_0.png)

The Settings dialog box has ten setting categories, shown as icons with text on the left-hand side:

- **General**: Sets the virtual machine name and OS type. The Advanced tab allows you to enable the clipboard so you can copy and paste text, files, and folders between the host and the guest systems.
- **System**: Sets the CPU and memory allocated for the virtual machine.
- **Display**: Manages the video memory and virtual displays allocated to the virtual machine.
- **Storage**: Defines the virtual hard drives and DVD drive emulation access. You should see the virtual hard drive you created listed here, but you can add additional drives if needed. Here’s where you can also allow the virtual machine access to the DVD drive on the host system. Another cool feature of VirtualBox is that you can directly mount an ISO image file directly on the virtual machine guest system. This way you can install Linux distributions directly from the ISO image file without having to burn them onto DVD! Figure 20-6 shows what this section looks like.

If you're going to install the virtual machine operating system from a DVD, make sure you mount the drive in the DVD section. Unfortunately, that's not selected by default.

![](img/577d3bff979ee86b07f9836e0df274ce_404_0.png)

![](img/577d3bff979ee86b07f9836e0df274ce_404_1.png)

- **Audio**: Manages access to the sound card on the host system. For Linux hosts, you can select the ALSA driver to allow the virtual server to send sound to the host Linux sound system.
- **Network**: The virtual machine can tap into the network connection of the host system, and here's where you can configure that feature. The default NAT option creates an internal network between the virtual machine and the host system. This places a buffer between the virtual machine and your local network so that other devices on your network can't access the virtual machine. This is beneficial if you're testing an OS and want to keep it isolated from your network. If you really want the virtual machine to have full access to your local network, select the Bridged network option instead. You can then access the host server's network using the network interface on the virtual server. Figure 20-7 shows the standard settings for this section.
- **Serial Ports**: Manage access to the serial communication ports on the host system if available.
