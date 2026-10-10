# ANSWERS

identifier, although it’s not strictly unique) that you can see with `lsblk`: $ lsblk -o UUID /dev/sdc15

Now you can use the UUID instead of the device name in fstab, like this: UUID=xxxxxx /mountpoint ....

This works, but it is not very readable, which is why distros that use UUIDs often have copious comments in `/etc/fstab`. You can solve this by using filesystem labels instead. Filesystems are not given labels when formatted unless one is specified, but you can add one later without affecting the filesystem. This is handy if running multiple distros as you can name each distro’s **root** partition accordingly and know what everything is. To add a label to an ext4 filesystem, use `e2label`: $ sudo e2label /dev/sdc15 ubuntu

If you don’t specify a label, `e2label` returns the current label. Then you can mount it from `fstab` with: LABEL=ubuntu /mountpoint ....

![](bbox=[0.36, 0.11, 0.95, 0.36])

If you want a fresh start, Ubuntu’s installer, along with most others, lets you erase everything on the disk.

# **Su-per GUI**

I have a shell script I need to run with root privileges. When I run it from a terminal with `sudo`, it works, but I want to be able to run it from the GUI, using an icon on a toolbar. In the past I would have used `gksu` to gain root privileges, but that is no longer present in Linux Mint. Is there an alternative that doesn’t require a terminal in which to input the password?

*Alex Barnett*

Yes, `gksu` is no longer supported, although KDE users still have `kdesu`. The program to use now is `pkexec`, part of `policykit`. You can run it like this: $ `pkexec` env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY HOME=$HOME yourscript

This pulls relevant settings from the environment. Similar steps are required with `sudo` unless you use `-E`, then run the program as the user specified with `--user`, or as root if no user is specified, like here. There is another way to address this, by configuring `sudo` to allow this script to be run as root without giving a password. Providing it is acceptable to allow this script to run as root without a password, edit the `/etc/sudoers` file, by running `$ sudo visudo`, and add this line: username All=(ALL) NOPASSWD: /full/path/to/your/script

This allows you to run your script with `sudo` without giving a password. You may need to use `sudo -E` to preserve environment variables when doing so. The script name is hard-coded into `sudoers`, which can only be edited by root, but you need to make sure the same is true of the script itself. Otherwise, someone could edit the script to do anything they want, with full root privileges. Either put it somewhere only root can edit it, such as `/usr/local/bin`, and owned by root, or make the script immutable with: $ `chattr` +i /full/path/to/your/script

# **Mystery Ubuntu**

I bought an old but Linux-compatible system. It’s good enough for now, but the guy I bought it from had built it and loaded Ubuntu 22.04. It runs well, but I can’t install any new programs or tweak the existing stuff. I can’t get past authentication and can’t update anything. When I picked it up, my friend said he could not remember if there was a password on it, but didn’t think so. Apparently, it does and he can’t remember the password.

*Ava Bell*

You don’t know exactly what is on this computer and, apparently, the person who installed it doesn’t know either. While it is possible to reset the password on a system like this, a safer option would be a fresh installation. If you have used it, back up your **home** directory to an external drive or USB stick. There won’t be anything else customised on the system as you don’t have the password. Your best option is to download your preferred Ubuntu flavour, copy it to a USB stick, or a DVD if the computer has a DVD drive, and boot from it. Run the installer and select the option to use the whole disk. This erases anything already on there and sets up a fresh Ubuntu install. It asks you to set a password, the Ubuntu installer always does, when creating your user, but this is one you choose and can, hopefully, remember. All trace of the previous installation is erased. If you backed up files from your **home** directory, you can restore them after booting the new system.

If you want to reset the password without re-installing, you need the **root** partition’s username and location. Get the latter by running `findmnt /` in a terminal. Boot the live distro and open a terminal. Replacing `/dev/sdXN` with the root partition, mount the root filesystem with: $ `mkdir` -p /mnt/root $ `mount` /dev/sdXN /mnt/root

Now you can set the password with: $ `passwd` --root=/mnt/root username You are prompted for a password and changes are written to the system specified by the `--root` option rather than the running system. Reboot and your user should have a brand new password.

# GET HELP NOW!

We’d love to try to answer any questions you send to `answers@linuxformat.com`, no matter what the level. We’ve all been stuck before, so don’t be shy. However, we’re very human (many suspect Neil checked out long ago), so it’s important that you include as much information as you can. If something works on one distro but not another, tell us. If you get an error message, then please tell us the exact message and precisely what you did to invoke it.

If you have, or suspect, a hardware problem, let us know about the hardware. Consider installing `hardinfo` or `lshw`. These programs list the hardware on your machine, so send us your output. If you’re unwilling, or unable, to install these, run the following commands in a root terminal and send us the `system.txt` file, too. `uname` -a > system.txt `lspci` >> system.txt `lsmod` -vv >> system.txt