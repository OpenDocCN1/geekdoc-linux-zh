
![](img/b2b6702758c230ce537468351fc8af15_70_0.png)

Figure 4.5 VMware needs your name and email address to send you a trial license key.

## Installing the Trial License Key

At this stage, you need to get the license key out of your email and into the location where VMware expects to find it:

- 1. Open the email sent by VMware. It should contain a brief welcome message, followed by the license information itself.
- 2. Depending on your mail program, the license might appear to be a small attached text file. If you have the option to save the attachment, save it with the filename license and proceed to Step 4.
- 3. If you are not prompted to save the attachment, you have to cut and paste the license information from the email. You should see two lines that read "Cut Here" above and below the license data. Be sure you cut everything in between (but not including) those lines. The first line of the clip should read "# VMware software license," and the last should read "Hash" followed by a long alphanumeric string. Save this clip with the filename license. The license file should look very much like the one shown in Figure 4.6.
- 4. VMware expects to find this license file in a directory called .vmware, which should be located on your home directory. Use the command mkdir ~/.vmware to create this directory.
- 5. Copy the license file to your new .vmware directory.
- 6. When you start VMware, it will be able to read the license key and start up appropriately.

![](img/b2b6702758c230ce537468351fc8af15_71_0.png)

Figure 4.6 The VMware license key is simply a small text file that tells VMware who you are and how long your license should last, along with a unique host ID code.

## Troubleshooting the Install

On a Linux PC that adheres to the VMware requirements outlined in Chapter 3, this installation process should pose no problems. However, the world is not a perfect place. Here are some tips for dealing with common VMware installation ailments:

- Remember that VMware will not install unless you are either logged in as root or have run the su (superuser) command in the same terminal you are using to install VMware.
- VMware will not install or update if you are running a VMware virtual machine.
- VMware won't run under Caldera OpenLinux 1.3: OpenLinux 1.3 is not on the VMware approved list. But if you decide to try anyway, you need to install the version of glibc that VMware needs. You'll find glibc-2.06-1.i386.rpm in the col/contrib/RPMS directory on your OpenLinux 1.3 CD-ROM. Typing the command rpm -i glibc-2.06-1.i386.rpm will install glibc and possibly fix your problem. None of the VMware-approved host operating systems has this problem, however.
- VMware won't run under Slackware: Why not just run one of the distributions VMware supports? But if you are a Slackware purist, this should help: Edit your rc.local file and add this:

```
if [ -x /etc/rc.d/init.d/vmware ]
then
    /etc/rc.d/init.d/vmware start
fi
```

VMware needs to be reinstalled every time you upgrade your host PC's Linux kernel. If you're planning a kernel upgrade, follow this procedure:

- 1. Invoke the VMware uninstallation script with the command `./vmware-uninstall.pl`.
- 2. Perform the kernel upgrade.
- 3. Reinstall VMware with the command `vmware-config.pl`.

Understand that this will not affect your guest operating systems, only the VMware launch program.

## Checking for Updates Online

VMware, Inc. is constantly improving VMware, and from time to time, new versions become available. VMware releases incremental upgrades, beta test versions, and complete version steps. By reading the News & Events page on VMware's Web site (http://www.vmware.com/news), you can stay up-to-date with the latest VMware feature changes, improvements, and upgrades.

Unless you are a seasoned VMware user, however, it is best to wait to install any upgrades of VMware over the version that came with this book, especially if it is a beta version. Beta versions are not only less stable, but often are slower than full release versions because they have extra debugging capabilities enabled. Plus running the version of VMware that comes with this book ensures that you can follow along; future versions might make subtle changes to the installation and configure process.

## Conclusion

If all went well, VMware is now installed on your PC. All you need to do is enter one little command, and VMware is at your service.

The next chapter covers what you can expect to see, and what you need to do, the first time you run VMware. Although you could plow blindly ahead and get a virtual machine to boot, give me a little more of your time first. You'll see what the VMware configuration interface does for you and finally be able to apply some of the intricate knowledge you've picked up about virtual machines and resource allocations.
