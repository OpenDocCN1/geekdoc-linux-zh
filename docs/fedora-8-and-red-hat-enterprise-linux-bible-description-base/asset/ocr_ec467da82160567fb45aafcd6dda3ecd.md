The DVD can be used for any type of install; the CD with this book can only be used to copy the Fedora 8 desktop system running on the CD to hard disk.

+   2. Start your computer. If you see the Fedora installation screen, continue to the next step.

> TIP: If you don’t see the installation screen, your DVD or CD-ROM drive may not be bootable. Creating a bootable floppy is no longer an option because the 2.6 kernel doesn’t fit on a floppy. However, you may have the choice of making your DVD or CD-ROM drive bootable or copying a boot image to a bootable USB device (such as a pen drive). Here’s how: Restart the computer. Immediately, you should see a message telling you how to go into setup, such as by pressing the F1, F2, or Del key. Enter setup and look for an option such as “Boot Options” or “Boot from.” If the value is “A: First, Then C:” change it to “CD-ROM First, Then C:” or something similar. Save the changes and try to install again.
> 
> If installation succeeds, you may want to restore the boot settings. If your DVD or CD drive still won’t boot, you may need to use an alternative method to boot Fedora installation (described in “Alternatives for starting installation” later in this chapter).

+   3. Start the boot procedure. At the boot screen do one of the following, depending on whether you are installing from the DVD or CD:
+   
+   - Fedora 8 Install DVD — With “Install or upgrade” highlighted on the boot menu, press Enter to begin the installation.
+   - Fedora 8 Desktop Live CD — Either wait for the boot screen to time out or with “Run from image” highlighted on the boot menu, press Enter to start the live CD. When the CD boots up to a GNOME desktop, double-click the “Install to Hard Drive” icon to begin the installation.

The boot screen is menu-driven. So if you want to change any of the boot options for a menu selection, highlight that selection and press the Tab key. You can then remove or add options before pressing Enter to continue. For example, to install from a different medium (such as over the network), add the askmethod boot option. See the sidebar “Choosing Different Install Modes” for more boot options.

Although many of the steps are the same, the DVD and CD installs are different in a few key ways. In particular, the DVD install lets you select which packages to install. The CD install simply copies what is essentially an installed system from the live CD to your hard disk. So some of the steps that follow won’t apply to the live CD install.

+   4. Media check. At this point, you may be asked to check your installation media. If so, press Enter to check that the DVD is in working order. If a disk is damaged, this step saves you the trouble of getting deep into the install before failing. After the DVD is checked, select Skip to continue.

+   5. Continue. When the welcome screen appears, click Release Notes to see information about this version of Fedora. Click Next when you’re ready to continue.

+   6. Choose a language. When prompted, indicate the language that you would like to use during the installation procedure by moving the arrow keys and selecting Next. (Later, you will be able to add additional languages.) You are asked to choose a keyboard.