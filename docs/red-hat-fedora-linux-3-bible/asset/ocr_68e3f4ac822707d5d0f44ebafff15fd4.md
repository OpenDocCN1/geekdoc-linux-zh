+   7.  If you said Yes, choose DHCP, or type in a static IP address and Netmask for your computer. Also, identify your gateway (the machine that connects you to the Internet) and one or more DNS servers you need for address resolution.

+   8.  When you enter the rescue environment, you need to choose whether or not to mount your Linux installation (under `/mnt/sysimage` directory) by selecting Continue, to mount it as read-only (select Read-Only), or to not mount it (select Skip).

If everything went well, you should receive the message: `Your system is mounted under the /mnt/sysimage directory. You will see a shell prompt.` Now you can:

+   - Try to fix any errors in your Linux configuration, beginning at `/mnt/sysimage` to find your normal root (`/`) directory.

+   - Backup or transfer files from your computer to other media or computers, if your system remains unbootable, so you can save any critical files.

When you are done, remove the CD and reboot your computer.

NOTE: Everything you do with the rescue CD you can also do with the Fedora DVD or first CD in your Fedora Core 3 installation CD set. The rescue CD is just more convenient in some cases because it is smaller to copy (only about 74MB as compared with over 4GB for the Fedora DVD) and quicker to boot up. It will also fit on a medium that is smaller than a full-size CD.