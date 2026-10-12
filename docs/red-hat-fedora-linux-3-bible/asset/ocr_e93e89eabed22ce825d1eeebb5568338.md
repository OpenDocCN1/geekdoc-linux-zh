• **Monitoring system performance** — You may have a run-away process on your system or you may just be experiencing slow performance. Tools that come with Fedora can help you determine how much of your CPU and memory are being consumed.

• **Keeping software up-to-date** — Corrections to Fedora software, especially those related to security issues, should be incorporated into your system as time goes on. The Red Hat Network offers the up-2-date service for Red Hat Enterprise Linux systems and yum and apt repositories for Fedora systems to ensure that you get critical fixes.

The aforementioned administrative tasks are described in the rest of this chapter. Later chapters cover other administrative topics, such as managing user accounts (Chapter 11), automating system tasks (Chapter 12), system backups and restores (Chapter 13), and securing your system (Chapter 14). Tasks related to network administration are covered in Chapters 15 through 26.

# ## Configuring Hardware

The following section describes how to add and reconfigure hardware using kudzu. The section after that describes how to manage loadable modules when hardware isn't being detected and configured properly.

# ### Reconfiguring hardware with kudzu

When you add or remove hardware from your computer and reboot Fedora, a window appears during the reboot process advising that hardware has either been added or removed and asking if you want to reconfigure it. The program that detects and reconfigures your hardware is called kudzu.

The kudzu program is a hardware autodetection and configuration tool that runs automatically at boot time. If you like, you can also start kudzu while Fedora is running. In either case, here is what kudzu does:

+   1.  It checks the hardware connected to your computer.
+   2.  It compares the hardware it finds to the database of hardware information stored in the `/etc/sysconfig/hwconf` file.
+   3.  It prompts you to change your system configuration, based on new or removed hardware that was detected.

The following is a list of hardware that kudzu can detect (according to the kudzu README file), followed by a description of what kudzu does to configure the device. Other devices may be detected as well (such as USB devices).

+   • **Network devices** — Adds an Ethernet interface alias (eth0, eth1, and so on) if necessary and either migrates the old device configuration or creates a new one.
+   • **SCSI** — Adds an alias for `scsi_hostadapter`.