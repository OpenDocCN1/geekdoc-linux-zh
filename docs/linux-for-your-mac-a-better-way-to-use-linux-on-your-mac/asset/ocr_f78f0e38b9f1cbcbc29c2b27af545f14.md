software installs, SuSE Linux runs a configuration script that can take some time
to configure software and files on your system (possibly several minutes).
You are asked if you want to view the installation log. Click No to continue. You
are asked if you want to configure a printer, sound, or modem (all these may be
configured after installation if you wish).
When finished, click the Finish installation button. A dialog box appears. Click
the OK button.
You now reboot directly to SuSE Linux. You should configure the LILO bootloader.
At the command line, open the file /etc/lilo.conf using the pico editor, like this:

```
# pico -w /etc/lilo.conf
```

> The version of lilo installed with PPC Linux is vastly different than the lilo
> distributed with Intel-based Linux distributions. The PPC lilo creates and modi-
> fies Apple Open Firmware scripts for booting.

![](bbox=[0.82, 0.32, 0.96, 0.44])

After you press Enter, scroll through the file and look for the following entries:

+   - boot=
+   - default=
+   - root=
+   - other=

Edit these entries to point to your HFS boot partition, the default Linux kernel,
the root Linux partition, and the partition used by Mac OS:

+   - boot= /dev/hda9
+   - default= linux
+   - root= /dev/hda10
+   - other= /dev/hda8

After making these changes, run the lilo command:

```
# lilo
```

Next, use the shutdown command at the command line of a terminal window to
reboot:

```
# shutdown -r now
```

After you press Enter, Linux reboots to Mac OS. To configure your computer to
boot Linux, insert CD-ROM 1, and drag a copy of the suseboot folder to your