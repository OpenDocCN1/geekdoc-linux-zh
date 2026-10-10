+   • Click on the blue camera icon to "take a snapshot".
+   • Create a name and click "OK".

You can now use your virtual machine as normal. If you ever want to revert to the state of the machine that existed at the time of the snapshot, follow these instructions:
• Completely shut down the Virtual Machine.
• In the VirtualBox Menu, click on "Snapshots" and select the snapshot to apply.
• Click on the blue camera icon with arrow to "restore snapshot".
• Deny the option to save the current data, and click "Restore".

Optionally, if you ever want to remove a snapshot, simply click the icon with a red "X". This will remove data files to eliminate wasted space, but you cannot restore to that image once removed. It will not impact the current machine state. Many users remove old, redundant snapshots after creating newer clean machines.

I wish I could say that every reader will be able to easily build virtual machines on any computer. This is simply not the case. While most computers are capable of virtual machine usage, many will demand slight modifications in order to allow virtualization. Let's take a look at the most common errors presented by VirtualBox.

**VT-x is disabled:** Any version of this error is the most common reason your VMs will not start. This indicates that the processor of your computer either does not support virtualization or the feature is not enabled. The fix for this varies by brand of machine and processor. Immediately after the computer is turned on, before the operating system starts, enter the BIOS of the machine. This is usually accomplished by pressing delete, F2, F10, or another designated key right away until a BIOS menu appears. Once in the BIOS, you can navigate through the menu via keyboard. With many Intel processors, you can open the "Advanced" tab and set the "Virtualization (VT-x)" to "Enable". For AMD processors, open the "M.I.T." tab, "Advanced Frequency" Settings, "Advanced Core" settings, and then set the "SVM Mode" to "Enable". If none of these options appear, conduct an online search of the model of your computer followed by "virtualization" for instructions.

**VT-x is not available:** This is usually isolated to Windows 10 and 11 machines. Navigate to the Windows Control Panel and open "Programs and Features". Click "Turn Windows features on or off" and uncheck all "Hyper-V" features. Click "OK" and reboot. If the Hyper-V option is not enabled, enable Hyper-V, restart the computer, disable Hyper-V, and reboot again. Attempt to start your VM with these new settings. This may seem backwards, but it makes sense. Previous versions of VirtualBox cannot run if you are using "Hyper-V" in Windows. Basically, both systems try to get exclusive access to the virtualization capabilities of the processor. Hyper-V within Windows receives the access first and impedes VirtualBox from the capabilities. The latest version of VirtualBox attempts to correct this. If the previous setting did not help, try to re-enable all of the Hyper-V options within Windows, reboot, and try to boot your VM again. If you are still experiencing problems, read the troubleshooting chapter of the VirtualBox manual at virtualbox.org/manual/ch12.html. Expand any errors received and search the provided error codes to identify further solutions.

**VirtualBox Display:** Some readers of previous editions have reported the inability to resize VM windows within VirtualBox and the "Auto-resize Guest Display" menu option greyed out. The following commands within Terminal of the Linux VM should repair this issue. There is no harm running these if you are unsure.
```bash
sudo apt update
```