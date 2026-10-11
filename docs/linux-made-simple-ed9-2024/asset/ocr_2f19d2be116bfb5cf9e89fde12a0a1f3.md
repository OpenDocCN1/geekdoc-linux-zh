# **Take a snapshot**

Your VM is now set up and ready for action. It should work in exactly the same way as any physical machine, but it has one crucial advantage: snapshots. Snapshots let you take one-click backups of your guest at a specific point in time. You can then proceed secure in the knowledge you can roll back to the snapshot and undo all the changes you've made since.

You can create snapshots while your machine is powered off, or during use – just select Machine > Take Snapshot to do so. Give your snapshot an identifiable name, and also add a description if you wish, then click 'OK'.

When you take a snapshot, VirtualBox starts recording changes to the drive in a different file. If you delete a snapshot, those changes are merged back into the main file, while if you roll back to an earlier snapshot (or the base image), the snapshot's changes are lost unless you create an additional snapshot when prompted. VMs support multiple snapshots, and you can even move between them, allowing you to create multiple setups from within a single guest.

![](bbox=[0.46, 0.07, 0.93, 0.27])

# **Terminal use**

VirtualBox's user interface may be a convenient way to get started with virtualisation, but once you've up and running you'll be pleased to learn there are a number of command-line tools you can employ if that works better for you. You can even bypass the graphical VirtualBox Manager entirely if you're willing to learn the rather lengthy list of sub-commands for the VBoxManage tool, such as: `createnv` and `startvm`, but even if you're happy with the point-and-click approach, there are a number of tools you should take a closer look at.

The first is VBoxSDL – if you'd like to launch your VM in a 'pure', distraction-free environment (so none of the controls offered by the default VM window), this is the tool for you. Its usage is pretty straightforward:

```
`VBoxSDL -startvm <vmname>`
```

Replace `<vmname>` with the name of your VM (or its UUID if you prefer). Once it's running, you'll not only have access to the menu commands offered by the main VirtualBox window, but some handy shortcuts you can employ while pressing the host key (the right [Ctrl] key by default): [F] toggles full-screen view on and off, while [k] takes a snapshot. Press [h] to press the ACPI power button, [p] to pause and resume, [q] to power off or [r] to reset. Finally, press [Del] in conjunction with the host key and you'll send a [Ctrl]+[Alt]+[Del] to the guest machine. Alternatively, shut down your VM using the VBoxManage tool – just type the following command to initiate the ACPI power button, eg: `VBoxManage controlvm "VM name" accpowerbutton`

Another handy command-line tool is VBoxHeadless, which enables you to run your virtual machine headless. To do this – and allow yourself to access it remotely from another computer (*check out our Headless setup box*).

Whether you plan to use VirtualBox from the command line or its GUI, you'll find it's packed with powerful and useful features that will convert you to the possibilities and power of virtualisation. You'll wonder how you ever coped before! **1**

# **Remove all the desktop paraphernalia and run your guest in a lean, distraction-free window using VBoxSDL.**

# ## Extend the size of your VM drive

![](bbox=[0.07, 0.63, 0.34, 0.77])

# **1 Consolidate snapshots**

If your VM contains snapshots, the resizing process will affect only the original base image. To resolve this, right-click the VM and choose Settings, then append :old to the end of its name. Click 'OK', right-click the VM again, but this time choose Clone. Click 'Expert Mode', then rename it and verify that 'Full Clone' and 'Current machine state' are selected before clicking 'Clone'.

![](bbox=[0.37, 0.63, 0.63, 0.77])

# **2 Resize virtual drive**

Close VirtualBox, open Terminal and navigate to the folder containing your VDI file. Now type the following command, replacing *drivename.vdi* with the filename of your particular VDI file: `VBoxManage modifyvdi "drivename.vdi" --resize 10000`

The resize figure is in MB, so 10,000 equals 10,000MB or 10GB.

![](bbox=[0.67, 0.63, 0.93, 0.77])

# **3 Extend partition**

The drive concerned has been resized, but you'll now need to repartition it. Boot your VM having attached an ISO of the Gparted Live CD and then use that to move partitions around to use the extra space – you may have to resize the extended partition first, then move the swap volume to the end before resizing the partition from the left to make the space available.