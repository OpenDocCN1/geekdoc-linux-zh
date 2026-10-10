
## Part III Administration

### Administrative Log Files

One of the things that Linux does well is keep track of itself. This is a good thing, when you consider how much can go wrong with a complex operating system. Sometimes you are trying to get a new facility to work and it fails without giving you the foggiest reason why. Other times you want to monitor your system to see if people are trying to access your computer illegally. In any of those cases, you can use log files to help track down the problem.

The main utilities for logging error and debugging messages for Linux are the *syslog* and *klogd* daemons. General system logging is done by *syslog*. Logging that is specific to kernel activity is done by *klogd*. Logging is done according to information in the */etc/syslog.conf* file. Messages are typically directed to log files that are usually in the */var/log* directory.

As *root* user, you can view log files with the *less* command or watch messages as they enter log file using the *tail* command (*tail* -f */var/log/messages*).

### Using Other Administrative Logins

You don’t hear much about other administrative logins (besides *root*) being used with Linux. It was a fairly common practice in UNIX systems to have several different administrative logins that allowed administrative tasks to be split among several users.

In any case, these administrative logins are available with Linux, so you may want to look into using them. At the very least, because individual software packages such as *bind*, *suid*, and *Amanda* set up permissions for their log files and configuration files based on their administrative logins, maintaining those permissions can impede someone who hacks into one of those services from gaining control of the whole computer.

> **TIP** Because most administrative features are expected to be administered by the *root* user, e-mail for other administrative accounts is routed to the *root* user. If you want other administrative users to receive their own e-mail, delete the aliases for those users from the */etc/aliases* file.

### Understanding Administrative Logins

Here are some of the administrative logins that are configured automatically for Linux systems. By tradition, these logins are assigned *UID* numbers under 100. Here are examples:

> **TIP** Most administrative logins have no passwords by default. They also typically have */sbin/nologin* assigned as their shell, so if you try to log in as one of these users, you see a “This account is currently not available” message. That’s why you can’t use an administrative login separately until you assign it a password and shell (such as */bin/bash*).

- *1p* — This user can control some printing features. Having a separate *lp* administrator allows someone other than the super user to do such things as move or remove *lp* logs and print spool files. The home directory for *lp* is */var/spool/lpd*.
- *mail* — This user can work with administrative e-mail features. The mail group has group permissions to use mail files in /var/spool/mail (which is also the mail user’s home directory).
- *uucp* — This user owns various uucp commands (once used as the primary method for dial-up serial communications). It is the owner of log files in /var/log/uucp, spool files in /var/spool, administrative commands (such as uuckw, uuctld, uucvny, and uuxql) in /usr/sbin, and user commands (uucp, cu, uuname, uustat, and uux) in /usr/bin. The home directory for uucp is /var/spool/uucp.
- *bin* — This user owns many commands in /bin in traditional UNIX systems. (This is not the case in CentOS because root tends to own most executable files.) The home directory for bin is /bin.
- *news* — This user could do administration of Internet news services, depending on how you set permission for /var/spool/news and other news-related resources. The home directory for news is /etc/news.

### Using sudo for Assigning Administrative Privilege

One way to give full or limited root privileges to any non-root user is to set up the sudo facility. It simply entails adding the user to /etc/sudoers and defining what privilege you want that user to have. Then the user can run any command he or she is privileged to use by preceding that command with the sudo command.

The following is an example of how to use the sudo facility to cause any users that are added to the wheel group to have full root privileges:

1. As the *root* user, edit the /etc/sudoers file by running the visudo command:
    ```bash
    # /usr/sbin/visudo
    ```
2. By default, the file is opened in vi, unless your EDITOR variable happens to be set to some other editor acceptable to visudo (e.g., export EDITOR=gedit). The reason for using visudo is that the command will lock the /etc/sudoers file and do some basic sanity-checking of the file to ensure it was edited correctly.

    > If you are stuck here, refer to the vi tutorial (“Using the vi Text Editor”) in Chapter 4 for information.

3. Uncomment the following line to allow users in the group named wheel to have full root privileges on the computer:
    ```bash
    %wheel    ALL=(ALL)  ALL
    ```
    The previous line causes the user to be prompted for a password to be allowed to use administrative commands. To allow users in the wheel group to have that privilege without using a password, uncomment the following line instead:
    ```bash
    %wheel    ALL=(ALL)  NOPASSWD: ALL
    ```
4. Save the changes to the /etc/sudoers file.
5. Still as *root* user, open the /etc/group file in any text editor and add the users you want to have root privilege to the wheel line. For example, if you were to add the users mary and jake to the wheel group, the line would appear as follows:
    ```text
    wheel:x:10:root,mary,jake
    ```

At this point, the users mary and jake can run the sudo command to run commands, or parts of commands, that are normally restricted to the root user. The following is an example of a session by the user jake after he has been assigned sudo privileges.

```bash
[jake]$ sudo umount /mnt/win
We trust you have received the usual lecture from the local System Administrator. It usually boils down to these two things:
#1) Respect the privacy of others.
#2) Think before you type.
Password: ********
[jake]$ mount /mnt/win
mount: only root can mount /dev/sda1 on /mnt/win
[jake]$ sudo mount /mnt/win
[jake]$
```

In the preceding session, the user jake runs the sudo command so he can unmount the /mnt/win file system (using the umount command). He is given a warning and asked to provide his password (this is jake's password, not the root user's password).

Notice that even after jake has given the password, he must still use the sudo command to run the command as root (the first mount fails, but the second succeeds). Notice that he was not prompted for a password for the second sudo. That's because after entering his password successfully, he can enter as many sudo commands as he wants for the next 5 minutes without having to enter it again. (You can change the time-out value from 5 minutes to however long you want by setting the passwd_timeout value in the /etc/sudoers file.)

The preceding example grants a simple all-or-nothing administrative privilege to everyone you put in the wheel group. However, the /etc/sudoers file gives you an incredible amount of flexibility in permitting individual users and groups to use individual applications or groups of applications. I recommend you refer to the sudoers and sudo man pages for information about how to tune your sudo facility.

### Administering Your Linux System

Your Linux system administrator duties don't end after you have installed CentOS. Your ongoing job as a Linux system administrator includes the following tasks:

- **Configuring Hardware** — Often when you add hardware to your CentOS computer, that hardware will be automatically detected and configured by tools such as HAL. In those cases in which the hardware was not properly set up, you can use commands such as lsmod, modprobe, insmod, and rmmod to configure the right modules to get the hardware working.
- **Managing File Systems and Disk Space** — You must keep track of the disk space being consumed, especially if your CentOS system is shared by multiple users. At some point, you may need to add a hard disk or track down what is eating up your disk space (you can use commands like find, du, and df to do this).
- **Monitoring System Performance** — You may have a runaway process on your system, or you may just be experiencing slow performance. Tools that come with CentOS can help you determine how much of your CPU and memory are being consumed.

The aforementioned administrative tasks are described in the rest of this chapter. Other chapters cover other administrative topics, such as managing user accounts (Chapter 10), automating system tasks (Chapter 11), system backups and restores (Chapter 12), and securing your system (Chapter 13). Tasks related to network and server administration are covered in Chapters 14 through 24. Ways of getting updates to your Linux software (using the Add/Remove Software window and yum command) are described in Chapter 5.

### Configuring Hardware

For many hardware items that you attach to your computer, Linux will simply detect them and configure them. During system boot time, the kernel will probe and identify your IDE drives, SCSI drives, PCI cards, and other hardware. After the Linux desktop is running, USB devices that you plug in (such as pen drives or digital cameras) will be detected, and any file systems they contain will be automatically mounted.

The following section describes how to add and reconfigure hardware in Linux. This includes sections on checking your hardware, using HAL (for detecting and configuring hardware) and commands for working with loadable modules when hardware isn't being detected and configured properly.

#### Checking Your Hardware

Sometimes the fact that CentOS can't properly detect and configure your hardware may make it impossible for you to install Linux. In those cases, I suggest you try to determine what hardware you have before you install. See Chapter 2 for information on checking your hardware before installing CentOS.

#### Managing Hardware with HAL

HAL, short for Hardware Abstraction Layer, maintains a list of devices on your system and provides a programming API for applications to access. A background process, hald, looks for changes to your installed hardware.
