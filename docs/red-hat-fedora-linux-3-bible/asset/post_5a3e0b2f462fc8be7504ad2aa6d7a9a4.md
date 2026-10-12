
- **news** — This could do administration of Internet news services, depending on how you set permission for `/var/spool/news` and other news-related resources. The home directory for news is `/etc/news`.

## Using *sudo* for assigning administrative privilege

One way to give full or limited root privileges to any non-root user is to set up the *sudo* facility. That simply entails adding the user to `/etc/sudoers` and defining what privilege you want that user to have. Then the user can run any command he or she is privileged to use by preceding that command with the *sudo* command.

The following is an example of how to use the *sudo* facility to cause any users that are added to the *wheel* group to have full root privileges:

1. As the root user, edit the `/etc/sudoers` file by running the `visudo` command:

   ```bash
   # /usr/sbin/visudo
   ```

   By default, the file is opened in `vi`, unless your `EDITOR` variable *happens* to be set to some other editor acceptable to `visudo` (for example, `export EDITOR=gedit`). The reason for using `visudo` is that the command will lock the `/etc/sudoers` file and do some basic sanity-checking of the file to ensure it was edited correctly.

   > **NOTE:** If you are stuck here, refer to the `vi` tutorial in Chapter 4 for information on using the `vi` editor.

2. Uncomment the following line to allow users in the group named `wheel` to have full root privileges on the computer:

   ```bash
   %wheel    ALL=(ALL)     ALL
   ```

   The previous line causes the user to be prompted for a password to be allowed to use administrative commands. To allow users in the `wheel` group to have that privilege without using a password, uncomment the following line instead:

   ```bash
   %wheel    ALL=(ALL)     NOPASSWD: ALL
   ```

   *Note: The OCR text contained `$wheel1`, which is likely a misinterpretation of `%wheel` given the context of group configuration in sudoers and the typo in the instruction text "group named `wheel1`". Standard sudoers syntax uses `%` for groups. The number `1` in `wheel1` and `%wheel1` in the code block is almost certainly an OCR error for `wheel`.*

3. Save the changes to the `/etc/sudoers` file (in `vi`, type `ZZ`).

4. Still as root user, open the `/etc/group` file in any text editor and add the users you want to have root privilege to the `wheel` line. For example, if you were to add the users `mary` and `jake` to the `wheel` group, the line would appear as follows:

   ```text
   wheel::10:root,mary,jake
   ```

At this point, the users `mary` and `jake` can run the `sudo` command to run commands, or parts of commands, that are normally restricted to the root user. The following is an example of a session by the user `jake` after he has been assigned `sudo` privileges:

```text
[jake]$ sudo mount /mnt/win

We trust you have received the usual lecture from the local System Administrator. It usually boils down to these two things:

    1.  Respect the privacy of others.
    2.  Think before you type.

Password: *********

[jake]$ mount /mnt/win
mount: only root can mount /dev/hda1 on /mnt/win
[jake]$ sudo mount /mnt/win
[jake]$
```

In the above session, the user `jake` runs the `sudo` command so he can unmount the `/mnt/win` file system (using the `mount` command). He is given a warning and asked to provide his password (this is `jake`’s password, not the root password).

Notice that even after `jake` has given the password, he must still use the `sudo` command to run the command as root (the first `mount` fails, but the second succeeds). Notice that he was not prompted for a password for the second `sudo`. That’s because after entering his password successfully he can enter as many `sudo` commands as he wants for the next five minutes without having to enter it again. (You can change the timeout value from five minutes to however long you want by setting the `passwd_timeout` value in the `/etc/sudoers` file).

The preceding example grants a simple all-or-nothing administrative privilege to everyone you put in the `wheel` group. However, the `/etc/sudoers` file gives you an incredible amount of flexibility in permitting individual users and groups to use individual applications or groups of applications. I recommend you refer to the `sudoers` and `sudo` man pages for information about how to tune your `sudo` facility.

## Administering Your Fedora System

Your Linux system administrator duties don’t end after you have installed Fedora. Your ongoing job as a Linux system administrator includes the following tasks:

- **Configuring hardware** — Often when you add hardware to your Fedora computer, that hardware will be automatically detected and configured by tools such as `kudzu`. In those cases where the hardware was not properly set up, you can use commands such as `lsmod`, `modprobe`, `insmod`, and `rmmod` to configure the right modules to get the hardware working.

- **Managing file systems and disk space** — You must keep track of the disk space being consumed, especially if your Fedora system is shared by multiple users. At some point, you may need to add a hard disk or track down what is eating up your disk space (you can use commands like `find` to do this).

- **Monitoring system performance** — You may have a run-away process on your system or you may just be experiencing slow performance. Tools that come with Fedora can help you determine how much of your CPU and memory are being consumed.

- **Keeping software up-to-date** — Corrections to Fedora software, especially those related to security issues, should be incorporated into your system as time goes on. The Red Hat Network offers the up-to-date service for Red Hat Enterprise Linux systems and `yum` and `apt` repositories for Fedora systems to ensure that you get critical fixes.

The aforementioned administrative tasks are described in the rest of this chapter. Later chapters cover other administrative topics, such as managing user accounts (Chapter 11), automating system tasks (Chapter 12), system backups and restores (Chapter 13), and securing your system (Chapter 14). Tasks related to network administration are covered in Chapters 15 through 26.

## Configuring Hardware

The following section describes how to add and reconfigure hardware using `kudzu`. The section after that describes how to manage loadable modules when hardware isn't being detected and configured properly.

### Reconfiguring hardware with kudzu

When you add or remove hardware from your computer and reboot Fedora, a window appears during the reboot process advising that hardware has either been added or removed and asking if you want to reconfigure it. The program that detects and reconfigures your hardware is called `kudzu`.

The `kudzu` program is a hardware autodetection and configuration tool that runs automatically at boot time. If you like, you can also start `kudzu` while Fedora is running. In either case, here is what `kudzu` does:

1. It checks the hardware connected to your computer.
2. It compares the hardware it finds to the database of hardware information stored in the `/etc/sysconfig/hwconf` file.
3. It prompts you to change your system configuration, based on new or removed hardware that was detected.

The following is a list of hardware that `kudzu` can detect (according to the `kudzu` README file), followed by a description of what `kudzu` does to configure the device. Other devices may be detected as well (such as USB devices).

- **Network devices** — Adds an Ethernet interface alias (eth0, eth1, and so on) if necessary and either migrates the old device configuration or creates a new one.
- **SCSI** — Adds an alias for `scsi_hostadapter`.
- **Sound card** — Runs the `sndconfig` command to configure and test the sound card.
- **Mouse** — Links the new mouse device to `/dev/mouse` and runs the `mouseconfig` command to configure and test the mouse.
- **Modem** — Links the new modem device to `/dev/modem`.
- **CD-ROM** — Links the CD-ROM device to `/dev/cdrom`.
- **Scanner** — Links the new scanner device to `/dev/scanner`.
- **Keyboard** — Runs the `kbconfig` command to reconfigure the keyboard. Also, if you are using a serial console, it makes sure `/etc/inittab` and `/etc/security` are configured to be used by a serial console.

The following is a list of actions `kudzu` takes when a device is removed:

- **Network** — Removes the alias for the Ethernet interface (eth0, eth1, and so on).
- **SCSI** — Removes the alias for the SCSI host adapter (`scsi_hostadapter`).
- **Mouse** — Removes the link to `/dev/mouse`.
- **Modem** — Removes the link to `/dev/modem`.
- **CD-ROM** — Removes the link to `/dev/cdrom`.
- **Scanner** — Removes the link to `/dev/scanner`.

To run `kudzu`, either reboot (during the reboot, `kudzu` is run automatically) or switch to a virtual terminal (`Ctrl+Alt+F2`), log in as root, and run the `kudzu` command. For any hardware that has been added or removed since the last time `kudzu` was run, you are asked if you want to configure it, not configure it, or do nothing.

## Configuring modules

In a perfect world, after installing and booting Linux, all of your hardware should be detected and available for access. While Fedora and other Red Hat Linux systems are rapidly moving closer to that world, there are times when you must take special steps to get your computer hardware working.

Fedora systems come with tools for configuring the drivers that stand between the programs you run (such as CD players and Web browsers) and the hardware they use (such as CD-ROM drives and network cards). The intention is to have the drivers your system needs most often built into the kernel; these are called resident drivers. Other drivers that are added dynamically as needed are referred to as loadable modules.

## Finding available modules

If you have installed the Linux kernel source code that comes with Fedora (as described in Chapter 27), source code files for available drivers are stored in subdirectories of the
