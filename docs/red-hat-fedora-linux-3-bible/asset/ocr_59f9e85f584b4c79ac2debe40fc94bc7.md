```
```text
[jake]$ sudo mount /mnt/win```
```

We trust you have received the usual lecture from the local System Administrator. It usually boils down to these two things:

+       1.  Respect the privacy of others.
+       2.  Think before you type.

Password: *********

```
```text
[jake]$ mount /mnt/win
mount: only root can mount /dev/hda1 on /mnt/win
[jake]$ sudo mount /mnt/win
[jake]$```
```

In the above session, the user jake runs the sudo command so he can unmount the /mnt/win file system (using the mount command). He is given a warning and asked to provide his password (this is jake’s password, not the root password).

Notice that even after jake has given the password, he must still use the sudo command to run the command as root (the first mount fails, but the second succeeds). Notice that he was not prompted for a password for the second sudo. That’s because after entering his password successfully he can enter as many sudo commands as he wants for the next five minutes without having to enter it again. (You can change the timeout value from five minutes to however long you want by setting the passwd_timeout value in the /etc/sudoers file).

The preceding example grants a simple all-or-nothing administrative privilege to everyone you put in the wheel group. However, the /etc/sudoers file gives you an incredible amount of flexibility in permitting individual users and groups to use individual applications or groups of applications. I recommend you refer to the sudoers and sudo man pages for information about how to tune your sudo facility.

# ## Administering Your Fedora System

Your Linux system administrator duties don’t end after you have installed Fedora. Your ongoing job as a Linux system administrator includes the following tasks:

+   *   **Configuring hardware** — Often when you add hardware to your Fedora computer, that hardware will be automatically detected and configured by tools such as kudzu. In those cases where the hardware was not properly set up, you can use commands such as lsmod, modprobe, insmod, and rmmod to configure the right modules to get the hardware working.

+   *   **Managing file systems and disk space** — You must keep track of the disk space being consumed, especially if your Fedora system is shared by multiple users. At some point, you may need to add a hard disk or track down what is eating up your disk space (you can use commands like find to do this).