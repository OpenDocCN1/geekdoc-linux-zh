
```
#!/bin/bash
# put other system startup commands here
/opt/lampp/lampp start
/opt/rc.firewall
```

If you installed the XAMPP tarball and copied the rc.firewall script as described earlier, both those services are now set up to start automatically the next time DSL boots.

If you also want to add a static IP address for your server, instead of getting addresses assigned from a DHCP server, you can add commands for that to your bootlocal.sh script. For example, you could add the following lines to set your IP address for the eth0 interface to 192.168.0.10, set the default router (gateway) to 192.168.0.1, and identify your DNS servers as 192.168.0.5 and 192.168.0.6.

```
ifconfig eth0 192.168.0.10
route add default gw 192.168.0.1
echo nameserver 192.168.0.5 > /etc/resolv.conf
echo nameserver 192.168.0.6 >> /etc/resolv.conf
```

Note that the addresses used here are all private IP addresses. If you are configuring a public server, you either need to have public IP addresses assigned or use some sort of port forwarding from a public IP address to a machine behind a firewall/router.

## 2. Create DSL on USB flash drive

Insert your USB flash drive, that you are prepared to erase and use for your Web server, into your computer's USB port (don't mount it). Next, from the DSL menu on the desktop, select Apps, Tools, Install to USB Pendrive. Then, select either For USB-ZIP Pendrive (if you expect to run the server on an older PC) or For USB-HDD Pendrive (to run the server on newer PCs).

This procedure erases everything on your USB drive! So make sure you've removed everything you need from the drive. Answer the questions as prompted. (See Chapter 6, "Running a Native Pen Drive Install," for details on installing DSL to a pen drive.)

## 3. Select files/directories to back up

The files and directories that DSL backs up for you need to be listed in the /home/dsl/.filetool.lst file. Several entries are already in that file. Open that file using any text editor and add the last lines shown here in bold:

```
opt/ppp
opt/bootlocal.sh
opt/powerdown.sh
opt/.dslrc
opt/.mydsl_dir
opt/lamp/
opt/rc.firewall
```

- **4. Back up files and directories**—To back up the files that you just added in your `.filetool.lst` file to your USB flash drive, from the desktop select DSLpanel, Backup/Restore. You are prompted to enter the device on which you want to back up your files. It’s important to get this right.

  For a system that has no other SCSI or SATA drives on it, the USB flash drive device will probably be `sda1` (for a USB-HDD drive) or `sda2` (for a USB-ZIP drive). After typing in the device name, select Backup.

  The result is a `backup.tar.gz` file in the root of the USB drive device you entered.

- **5. Save MyDSL packages**—Any MyDSL packages that you want restored can also be copied on to the USB flash drive. If you just downloaded them, they should still be in the `/tmp` directory.

  You will have the opportunity to copy your MyDSL packages when you reboot DSL. Or you can copy them manually. For example, you could mount the USB flash device, using the mounting tool in the lower-right corner of the screen. Then, for example, to copy the files needed for this project to a `mydsl` directory on `sda1`, you could type the following from a Terminal window:

  ```
  # cd /tmp
  # mkdir /mnt/sda1/mydsl/
  # cp gnu-utils* firewall* /mnt/sda1/mydsl/
  ```

At this point, everything you need should be installed on your USB flash drive. Before adding web content, my XAMPP installation required 50MB of space for DSL and 61MB of space for XAMPP and the other packages I added. On a 256MB USB flash drive, that would leave me more than 140MB for web content or other packages I want to add.

When you reboot your computer (select Power Down→ Reboot from the DSL menu), DSL backs up your settings again and asks if you want to save your MyDSL packages.

## OTHER WAYS OF STORING YOUR WEB SERVER

Although having a complete DSL web server on a USB flash drive is fun, a more practical, permanent solution is to put some, or all, of the project on hard disk. Using the procedure just shown as your guide, here are ideas for changing that procedure to store your server in different ways:

- **Save MyDSL packages to hard disk**—Instead of downloading the MyDSL packages to /tmp, then copying them to storage, you can directly download the pages to the permanent storage. For example, use the desktop mount tool to mount a hard disk partition (such as hda1 for your first IDE hard disk partition). Then, create a mydsl directory on the device (mkdir /mnt/hda1/mydsl). When asked where to download the package, type /mnt/hda1/mydsl.

  Later, when you reboot, DSL should automatically find and restore the packages in the /mnt/hda1/mydsl directory. To specifically identify that directory from the boot prompt (in case you have MyDSL packages in multiple places), use the mydsl=/mnt/hda1/mydsl option at the boot prompt.

- **Save your backup archive to hard disk**—Instead of using sda1 or sda2 (presuming they represent your USB flash drive), when you choose where to back up your files, select a hard disk partition (such as hda1, hda2, etc.). The backup.tar.gz archive is placed in the root of that partition, so it can be restored later.

- **Create a persistent /opt**—By dedicating a disk partition to your /opt directory, you can save yourself the trouble of restoring the files when you reboot. Instead, you just tell DSL to mount the dedicated partition to /opt and it’s ready to roll.

To set up your persistent /opt partition to work with your XAMPP server, you need to modify several steps from the setup procedure. First, create an empty hard disk partition (for example, /dev/hda2) and boot DSL as follows:

```
boot: dsl opt=hda2
```

Next, install the XAMPP software to the /opt directory and copy your MyDSL packages to a /opt/mydsl directory. Edit the .filetool.lst file and remove references to backing up files from the /opt directory. When you go to reboot your system later, start DSL and the XAMPP server with the following boot options:
