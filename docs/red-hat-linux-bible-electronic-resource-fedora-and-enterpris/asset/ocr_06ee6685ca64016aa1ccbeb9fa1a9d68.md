+   4. Reboot your computer. You should see the LILO boot screen.

To change your boot loader from LILO to GRUB, do the following:

+   1. Configure the `/boot/grub/grub.conf` file as described in the “Booting your computer with GRUB” section.

+   2. You need to know the device on which you want to install GRUB. For example, to install GRUB on the master boot record of the first disk, type the following as root user from a Terminal window:

```
# grub-install /dev/hda
```

The new Master Boot Record is written to boot with the GRUB boot loader.

+   3. Reboot your computer. You should see the GRUB boot screen.

# Troubleshooting Your Installation

After you have finished installing Red Hat Linux, you can check how the installation went by checking your log files. There are three places to look once the system comes up:

+   - `/tmp/upgrade.log` — When upgrading packages, output from each installed package is sent to this file. You can see what packages were installed and if any failed.

+   - `/var/log/dmesg` — This file contains the messages that are sent to the console terminal as the system boots up, including messages relating to the kernel being started and hardware being recognized. If a piece of hardware isn't working, you can check here to make sure that the kernel found the hardware and configured it properly.

+   - `/var/log/boot.log` — This file contains information about each service that is started up at boot time. You can see if each service started successfully. If a service fails to start properly, there may be clues in this file that will help you learn what went wrong.

If something was set wrong (such as your mouse) or just isn't working quite right (such as your video display), you can always go back after Red Hat Linux is running and correct the problem. Here is a list of utilities you can use to reconfigure different features that were set during installation:

+   - **Changing or adding a mouse**: `redhat-config-mouse`

+   - **Changing a keyboard language**: `redhat-config-keyboard`

+   - **Adding or deleting software packages**: `redhat-config-packages` or `rpm`

+   - **Partitioning**: `fdisk` or `sfdisk`

+   - **Boot loader**: `/boot/grub/grub.conf` (for GRUB); `lilo` and `/etc/lilo.conf` (for LILO)

+   - **Networking (Ethernet & TCP/IP)**: `redhat-config-network`