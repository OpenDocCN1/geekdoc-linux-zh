Here are a few other random tips that can help you during installation:

+   - If installation fails because the installation procedure is unable to detect your video card, try restarting installation in text mode. After Fedora is installed and running, use the `system-config-display` command to configure your video card and monitor. (For some cards, such as those from NVIDIA, you need to get and install special drivers from the manufacturer's Web site or `http://rpmfusion.org`.)

> **CAUTION:** Some video drivers from NVIDIA and ATI will overwrite important Xorg driver files. If you later change to a different video card, features of the new card (such as DRI) might fail. The solution is to entirely remove the NVIDIA or ATI drivers and reinstall your xorg and mesa packages.

+   - If installation completes successfully, but your screen is garbled when you reboot, you should try to get Fedora to boot to a text-login prompt. To do this, add the number `3` to the end of the kernel boot line in GRUB. Linux will start with the GUI temporarily disabled. Run `system-config-display` to try to fix the problem. (See Chapter 3 for other advice related to fixing your GUI.)

+   - If your mouse is not detected during installation, you can use arrow keys and the Tab key to make selections. Then use `mouse-test` to track down the problem.

+   - If installation improperly probes your hardware or turns on a feature that causes problems with your hardware, you might be able to solve the problem by disabling the offending feature at the install boot prompt. Try adding one or more of the following after the word `linux` at the installation boot prompt: `ide=nodma` (if your system hangs while downloading the image), `apm=off` or `acpi=off` (if you experience random failures during install), or `nousb`, `nopcmcia`, or `nofirewire` (if you suspect that install is hanging on devices of those types).

+   - If you are still having problems installing Fedora, try searching FedoraForum.org to see if they have an answer. Sign up for an account and you can ask a question yourself.

# ## Spinning Your Own Fedora Install or Live Media

All software included in Fedora can be redistributed. Because of that fact, you not only use the software as you please, but you can also repackage and redistribute it if you care to. Not only is the Fedora Project committed to protecting your rights to redistribute Fedora, but it has gone so far as to give you the tools to build your own brand new Fedora-based distribution to suit your needs.

Fedora has created several tools that let you build your own install or live media images. Using these tools, you can pick the packages you want from the Fedora repository, add new repositories, and combine the content into ISO images that can be burned to CDs, DVDs, USB flash drives, or other media. In short, you can make your own custom Linux distribution.

The two major tools that Fedora produces (which the project itself currently uses to produce its own install and live CDs) are Pungi and livedd-creator: