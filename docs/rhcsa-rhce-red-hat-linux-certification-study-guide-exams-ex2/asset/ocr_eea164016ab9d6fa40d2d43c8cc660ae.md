/var/ftp directory. This is a security concept known as a chroot jail. It's often used on other systems such as the Domain Name Service (DNS) server to increase security on the host system.

If port 21 is open in the local firewall, this FTP server should also be accessible from remote systems. In addition, you'll need to make sure the vsFTP server starts automatically the next time RHEL 6 is booted. One way to do so is with the following command:

```
# chkconfig vsftpd on
```

The d at the end of vsFTP refers to its daemon. For more information on how services like vsFTP are controlled during the boot process, see Chapter 11. While that is an RHCE chapter, it should not be hard to remember this one chkconfig command.

# CERTIFICATION SUMMARY

The RHCSA and RHCE exams are not for beginners. This chapter helps you install a basic RHEL system, with the packages and settings suitable for the remainder of this book. Both exams are practical, hands-on exams. When you sit for either exam, you'll be faced with a live RHEL system with a series of problems to solve and systems to configure. The RHCSA covers core system administration skills.

The Red Hat exams now assume the use of 64-bit system. Red Hat configures the default VM system, KVM, only in the 64-bit build of RHEL 6. And you're required to configure RHEL 6 as a virtual host for the RHCSA.

With a subscription to the RHN, you can download RHEL installation ISO files from the associated account. Since RHEL software is released under open-source licenses, third parties such as CentOS and Scientific Linux have used that source code without Red Hat trademarks. You can also use such rebuild distributions to study for the RHCSA and RHCE exams.

It will be helpful to create multiple installations of RHEL 6 to practice the skills you'll learn in later chapters. To that end, I recommend the configuration of three systems. While many users don't have three spare physical computers to dedicate to their studies, VMs make it possible to set up these systems on a single physical computer. As the installation of RHEL 6 is relatively easy even for newer Linux users, not every detail is covered in this chapter. However, it is based on the network installation source created in Lab 2. After installation comes the First Boot process, which varies depending on whether you've installed a GUI.