**LINUX SERVICES DEPLOYMENT**

**Tested in Red Hat Linux 8.x**

**FABIAN MESTRE SOCARRAS**

Copyright © 2021 Aptiva Labs SAS

The texts related in this material are part of the Intellectual Property of Aptiva Labs SAS in the Republic of Colombia and outside of it; its distribution and use is under the authorization of Aptiva Labs SAS. This material is licensed under a Creative Commons CC-BY-NC-ND license.

Red Hat Inc, Red Hat Enterprise Linux, their logos and other identifying elements are registered in the United States of America and other countries.

Linux is a registered trademark of Linus Torvalds in the United States of America and other countries.

XFS is a registered trademark of Silicon Graphics International Corp and its subsidiaries in the United States of America and other countries.

PostgreSQL, MariaDB, Microsoft Windows Server, Oracle, Ubuntu, Debian, CentOs, Ansible are trademarks of their manufacturer owners.

**Dedication**

This book is dedicated to God, the source of all knowledge and source of all inspiration, who has given me the intellectual capacity to address these issues and to be able to share them with other people.

I dedicate this book to my wife Gina, for her support and motivation in starting and finishing this book.

To my mother, Elsy, for her effort and commitment to make her children good people. To my dad, Neil, in the presence of God, an example of resilience.

To my daughters and nieces, the future of the family.

My family, my support.

**Acknowledgments**

I want to thank all those who have accompanied me in my professional career in each of the companies where I have been a collaborator, the company of each of them has been for the growth and formation of the background that today allows me to publish this work.

Special recognition for Farid Boudez, Miguel Higuera, Jairo Rodríguez, Fause Rizcala, Fabio Ramírez, Freddy Mosquera, Helmuth Corzo, Edgard Polo and Gerardo Solorzano, who at various moments in life have believed in my professional qualities and have entrusted me with important responsibilities.

Special thanks to Juan Carlos Velez and Liliana Hoyos, for their care and prayers for so many years.

**Reader Profile**

This book is aimed at:

*   > Information Technology Infrastructure Administrators who have or project their technological ecosystem with Linux tools.

*   > Trainers of human talent in Information Technology whose focus is related to teaching operating systems.

*   > Infrastructure Solutions Integrators that support their services on Linux platforms.

*   > Information Technology Architects responsible for the technological operation in companies and institutions in any sector.

*   > Students who are trained to manage Information Technology platforms.

**Table of Contents**

> [RECOVERING ACCESS AS "root" USER](#text00000.html_filepos0000013241)

> [RELAX & RECOVER - BACK UP AND RESTORE A LINUX SYSTEM](#text00000.html_filepos0000022257)

> [INSTALLING VIRTUALIZATION CAPABILITIES (KVM / VIRT-MANAGER)](#text00000.html_filepos0000032856)

> [INSTALLING A VIRTUAL MACHINE BY VIRT-MANAGER](#text00000.html_filepos0000058227)

> [INSTALLING AND CONFIGURING A WEBSERVER - NGINX](#text00000.html_filepos0000063707)

> [*VIRTUAL HOSTS IN NGINX*](#text00000.html_filepos0000073408)

> [*PROXY REVERSO FOR HTTP TRAFIC*](#text00000.html_filepos0000079065)

> [*HTTP LOAD BALANCER WITH NGINX*](#text00000.html_filepos0000084333)

> [*ENCRYPTING COMMUNICATION  WITH TLS*](#text00000.html_filepos0000095909)

> [UNATTENDED INSTALATIONS - KICKSTART](#text00000.html_filepos0000102129)

> [DEPLOYING A FILESERVER WITH SAMBA](#text00000.html_filepos0000110714)

> [*SMB CLIENTS*](#text00000.html_filepos0000125905)

> [RED HAT LINUX AS A WINDOWS SERVER MEMBER DOMAIN](#text00000.html_filepos0000130038)

> [POSTFIX AND GMAIL RELAY IN RED HAT LINUX](#text00000.html_filepos0000155079)

> [INTEGRATION BEETWEEN RED HAT LINUX AND AMAZON WEB SERVICES S3](#text00000.html_filepos0000164999)

> [POSTGRESQL – INSTALATION AND DEPLOYMENT](#text00000.html_filepos0000176387)

> [*POSTGRESQL – NEW DATABASE AND DUMP*](#text00000.html_filepos0000184456)

> [*DATABASE RESTORATION EXERCISE*](#text00000.html_filepos0000189083)

> [*METADATA QUERY IN POSTGRESQL*](#text00000.html_filepos0000191713)

> [*INSTALLING POSTGRESQL IN A SECUNDARY FILESYSTEM*](#text00000.html_filepos0000195115)

> [*DEFINITION OF ACCESS TO THE DATABASES*](#text00000.html_filepos0000216241)

> [*POSTGRESQL - STREAMING REPLICATION*](#text00000.html_filepos0000221149)

> [RECORDING USERS SESSIONS](#text00000.html_filepos0000231254)

> [CONTAINERS IN RED HAT LINUX – PODMAN/SKOPEO](#text00001.html)

> [DEPLOYING A FTP SERVER - VSFTP](#text00001.html_filepos0000256857)

> [DEPLOYING A NFS SERVER](#text00001.html_filepos0000262143)

> [MARIADB - RELATIONAL DATABASE SERVICE](#text00001.html_filepos0000270088)

> [*INSTALLATION AND CONFIGURATION*](#text00001.html_filepos0000270778)

> [*INITIAL INSURANCE*](#text00001.html_filepos0000277834)

> [*CONFIGURATION FOR THE NETWORK*](#text00001.html_filepos0000283128)

> [*CREATION OF DATABASE AND INSERTION OF RECORDS*](#text00001.html_filepos0000286064)

> [*BACKUP MANAGEMENT*](#text00001.html_filepos0000293660)

> [*LOGIC BACKUP AND RESTORATION*](#text00001.html_filepos0000298545)

> [*PERFORMING A PHYSICAL BACKUP AND RESTORATION*](#text00001.html_filepos0000308832)

> [*GALERA – MARIADB - SYNCHRONOUS REPLICATION*](#text00001.html_filepos0000323405)

> [CREATING A REPOSITORY WITH LOCAL MEDIA](#text00001.html_filepos0000356665)

> [AUDIT IN LINUX SYSTEMS](#text00001.html_filepos0000366520)

> [*AUDIT RULES WITH AUDIT*](#text00001.html_filepos0000372739)

> [*PERSISTENT AUDIT RULES*](#text00001.html_filepos0000380458)

> [*RULES PRESET IN AUDIT*](#text00001.html_filepos0000381767)

> [*GENERATION OF REPORTS WITH AUDIT*](#text00001.html_filepos0000385743)

About of Author

Fabian Mestre Socarras is a Strategic Consultant in Information Technology and Linux Technical Writer. Systems Engineer with a Postgraduate Degree in Information Technology Management, with RHCSA, RHCVA, ITIL, Xorcom certifications, among others. Implementer of IP Telephony and Data Storage solutions on Linux systems. CEO & Founder at Aptiva Labs SAS where he has developed consulting activities for companies such as Bioagricola del Llano SA ESP, Emdupar SA ESP, LlanoGas SA ESP, Compgenioss SAS, Ejército Nacional del Colombia, Electrocom SAS, SINGS SAS, Thomas Processing Systems SAS, AppFuture SAS, among others. Write to the author at fabian.mestre@gmail.com.

About This Document

This document is intended for all those whose task is to administer Linux servers and who in one way or another are searching the Internet for how to develop certain technical procedures, however, they are aware that the information published on the Internet may or may not be true.

The labs developed in this document follow the guide recommended by Red Hat Linux and can be applied in distributions such as Oracle Linux 8.x, Centos 8.x, Rocky Linux, Amazon Linux 2, as well as in any other distribution derived from the base distribution. Red Hat Enterprise Linux 8.x.

RECOVERING ACCESS AS "root" USER

Having to recover the password of the "root" user is an unfortunate event, but it does have a procedure defined for this purpose. Recovering the password of the "root" user is something easy to do when the system administrator is still "logged in" in the console or from any type of terminal; Different is the case when the system has not yet been entered and it is required to perform administration tasks.

When GRUB2 prompts you to choose a kernel to start, you must stop the kernel startup process by defautl pressing any key on the keyboard; With the positioning keys ("arrows"), you will choose the kernel to execute, in this example "4.18.0-240.15.1" is chosen; Once chosen, press the letter "e", as indicated in the menu below:

![](Image00000.jpg) 

After pressing the letter "e" (edit), locate the line with the word "linux" as the first word of a line; scroll to the end of that line and add a space, as shown below:

![](Image00001.jpg) 

This is the line where parameters are sent to the kernel. Go to the end of that line and add the expression "rd.break" to start in console mode. At the end press CTRL + X to boot.

Once the system has booted, Linux has left us at a prompt similar to the one in the following image:

![](Image00002.jpg) 

At this moment the standard file system is mounted on / sysroot in read-only form, which makes it necessary to make changes to remount in read-write mode, as follows:

![](Image00003.jpg) 

It is necessary to do a Jail (caging of the file system, so that nobody bothers it while the operation is running) of the root file system (/ sysroot) and then change the administrator password.

It is necessary to create the empty file “/.autorelabel”. Following this, it is necessary to exit the mode where we were (chroot and GRUB mode) by typing “exit” twice:

This will immediately cause the system to reboot, where initially SELinux will do the job of re-labeling the corresponding contexts where appropriate (files, directories, ports, and processes), if this operating system functionality is enabled.

> KERNEL DATA DUMP FOR POST ANALYSIS

To analyze why a system failed, you can use the kdump service to save the contents of system memory for later analysis. In this sub section we will see a brief introduction to kdump using the RHEL Web Console. Kdump is a service that provides a crash-dump mechanism for the kernel. The service allows you to save the contents of the memory. Kdump uses the kexec system call to boot into a second kernel without rebooting, thus capturing the content of the failing kernel and saving the data for analysis. The second kernel resides in a reserved part of memory.

A kernel crash dump may be the only information available in the event of a system failure (a critical error), therefore ensuring that kdump is operational is important in mission critical environments. The procedure below shows you how to use the Kernel Dump tab in the Cockpit tool to configure the amount of memory reserved for the kdump kernel. The procedure also describes how to specify the destination location of the vmcore dump file and how to test its configuration.

![](Image00004.jpg) 

Once registered in the Cockpit, proceed to the Kernel Dump section:

![](Image00005.jpg) ![](Image00006.jpg) 

Through the following instructions you can see the result of this test dump (the **"Test Configuration"** button was pressed):

> [root@pruebas ~]# cd /var/crash/

> [root@pruebas ~]# ll

> total 0

> drwxr-xr-x. 2 root root 44 Feb 20 11:53 **127.0.0.1-2021-02-20-09:53:46**

As detailed, the dump generated a folder with the localhost IP address and the date and time when the simulated crash originated. We will enter that folder and observe its content, as shown below:

> [root@pruebas ~]#  cd 127.0.0.1-2021-02-20-09\:53\:46/

> [root@pruebas 127.0.0.1-2021-02-20-09:53:46]# ll -h

> total 172M

> -rw-------. 1 root root 172M Feb 20 11:53 vmcore

> -rw-r--r--. 1 root root  45K Feb 20 11:53 vmcore-dmesg.txt

> [root@pruebas ~]# more vmcore-dmesg.txt

> [    0.000000] Linux version 4.18.0-240.15.1.el8_3.x86_64 (mockbuild@x86-vm-07.build.eng.bos.redhat.com) (gcc version 8.3.1 2

> 0191121 (Red Hat 8.3.1-5) (GCC)) #1 SMP Wed Feb 3 03:12:15 EST 2021

> [    0.000000] Command line: BOOT_IMAGE=(hd0,msdos1)/vmlinuz-4.18.0-240.15.1.el8_3.x86_64 root=/dev/mapper/rhel-root ro crash

> kernel=auto resume=/dev/mapper/rhel-swap rd.lvm.lv=rhel/root rd.lvm.lv=rhel/swap rhgb quiet

> [    0.000000] x86/fpu: x87 FPU will use FXSAVE

> [    0.000000] BIOS-provided physical RAM map:

> [    0.000000] BIOS-e820: [mem 0x0000000000000000-0x000000000009fbff] usable

> [    0.000000] BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved

> [    0.000000] BIOS-e820: [mem 0x00000000000f0000-0x00000000000fffff] reserved

> [    0.000000] BIOS-e820: [mem 0x0000000000100000-0x00000000bffd9fff] usable

> [    0.000000] BIOS-e820: [mem 0x00000000bffda000-0x00000000bfffffff] reserved

> [    0.000000] BIOS-e820: [mem 0x00000000feffc000-0x00000000feffffff] reserved

> [    0.000000] BIOS-e820: [mem 0x00000000fffc0000-0x00000000ffffffff] reserved

> [    0.000000] BIOS-e820: [mem 0x0000000100000000-0x0000000792ffffff] usable

> [    0.000000] NX (Execute Disable) protection: active

> [    0.000000] SMBIOS 2.8 present.

> [    0.000000] DMI: QEMU Standard PC (i440FX + PIIX, 1996), BIOS rel-1.13.0-48-gd9c812dda519-prebuilt.qemu.org 04/01/2014

> [    0.000000] Hypervisor detected: KVM

> [    0.000000] kvm-clock: Using msrs 4b564d01 and 4b564d00

> [    0.000000] kvm-clock: cpu 0, msr 2a2601001, primary cpu clock

> [    0.000000] kvm-clock: using sched offset of 13033004839 cycles

> …

This data is used for subsequent analysis by troubleshooting experts. There is also a 172Mb binary file which is essential for further analysis.

> RELAX & RECOVER - BACK UP AND RESTORE A LINUX SYSTEM

To recover and restore a system using an existing backup, Red Hat Enterprise Linux (can also be installed by other distributions) provides the Relax-and-Recover (ReaR) option. You can use the utility as a disaster recovery solution and also for system migration.

The utility allows you to perform the following tasks:

> •  Build a boot image and restore the system from an existing backup, using the image.

> •  Replicate the original storage design.

> •  Restore user and system files.

> •  Restore the system to different hardware.

In addition, for disaster recovery, you can also integrate certain backup software with ReaR. The following steps are used to create a rescue image of your Linux system along with a backup of the data, the time of this operation depends on the amount of data to be saved. It is important to mention that this backup remains in an ISO file in the path that the Administrator establishes.

Initially, the necessary applications are installed to carry out this activity:

> [root@pruebas ~]#  yum install rear genisoimage syslinux

Once the software is installed, it is necessary to tell “rear” how to generate the rescue disk and the system backup, editing its configuration file and adding the following statements:

> [root@pruebas ~]#  vim /etc/rear/local.conf

> OUTPUT=ISO

> OUTPUT_URL=file:///root

> BACKUP=NETFS

> BACKUP_URL=iso:///root

It is interesting before sending the backup to know the total size of the system to be backed up:

> [root@s1 rear]# df -hT

> Filesystem          Type      Size  Used Avail Use% Mounted on

> devtmpfs            devtmpfs   15G     0   15G   0% /dev

> tmpfs               tmpfs      15G     0   15G   0% /dev/shm

> tmpfs               tmpfs      15G  9.2M   15G   1% /run

> tmpfs               tmpfs      15G     0   15G   0% /sys/fs/cgroup

> **/dev/mapper/ol-root xfs        44G   20G   25G  44% /**

> /dev/sda1           xfs      1014M  593M  422M  59% /boot

> tmpfs               tmpfs     2.9G  1.2M  2.9G   1% /run/user/42

> tmpfs               tmpfs     2.9G     0  2.9G   0% /run/user/0

Following this, it is necessary to make the rescue and backup ISO of the Linux system (a single file), this ISO will remain in the path /root/system-name, as shown below:

> [root@s1 rear]# rear -d -v mkbackup

> Relax-and-Recover 2.4 / Git

> Using log file: /var/log/rear/rear-s1.log

> Using backup archive '/tmp/rear.w0E22PfRdLwJCFg/tmp/isofs/root/backup.tar.gz'

> Creating disk layout

> Using guessed bootloader 'GRUB' (found in first bytes on /dev/sda)

> Creating root filesystem layout

> Handling network interface 'ens18'

> ens18 is a physical device

> Handled network interface 'ens18'

> Skipping 'virbr0': not bound to any physical interface.

> To log into the recovery system via ssh set up /root/.ssh/authorized_keys or specify SSH_ROOT_PASSWORD

> Copying logfile /var/log/rear/rear-s1.log into initramfs as '/tmp/rear-s1-partial-2021-02-22T10:47:38-05:00.log'

> Copying files and directories

> Copying binaries and libraries

> Copying kernel modules

> Copying all files in /lib*/firmware/

> Creating recovery/rescue system initramfs/initrd initrd.cgz with gzip default compression

> Created initrd.cgz with gzip default compression (340662414 bytes) in 35 seconds

> Creating tar archive '/tmp/rear.w0E22PfRdLwJCFg/tmp/isofs/root/backup.tar.gz'

> Archived 3282 MiB [avg 6654 KiB/sec] OK

> Archived 3282 MiB in 506 seconds [avg 6641 KiB/sec]

> Making ISO image

> Wrote ISO image: /var/lib/rear/output/rear-s1.iso (3.6G)

> Copying resulting files to file location

> Saving /var/log/rear/rear-s1.log as rear-s1.log to file location

> Exiting rear mkbackup (PID 63025) and its descendant processes

> Running exit tasks

> You should also rm -Rf /tmp/rear.w0E22PfRdLwJCFg

The location of the ISO file is verified:

> [root@s1 ~]# pwd

> /root

> [root@s1 ~]# ll

> total 8

> -rw-------. 1 root root 1279 Feb 15 10:15 anaconda-ks.cfg

> -rw-r--r--. 1 root root 1566 Feb 15 10:17 initial-setup-ks.cfg

> drwxr-x---. 2 root root   73 Feb 22 10:57 s1

> [root@s1 ~]# cd s1/

> [root@s1 s1]# ll -h

> total 3.6G

> -rw-------. 1 root root  202 Feb 22 10:57 README

> -rw-------. 1 root root  274 Feb 22 10:57 VERSION

> -rw-------. 1 root root 3.6G Feb 22 10:57 rear-s1.iso

> -rw-------. 1 root root 967K Feb 22 10:57 rear-s1.log

The "rear" application has generated an ISO file, from which a bootable USB can be generated or taken to a Virtualization system, as is preferred, in this exercise a virtualization platform will be used.

![](Image00007.jpg) 

When booting from the ISO, the following image results:

![](Image00008.jpg) 

The first option is chosen and the Linux system recovery process begins, as shown below:

![](Image00009.jpg) 

As we can see, a "login" is requested, in this case "root" is entered and enter is pressed. Next we see the promp to introduce a command that in this case will be “rear -v recover”, which triggers the restoration of the operating system, as detailed below:

![](Image00010.jpg) 

Following this, it is necessary to wait for the restoration to run. Once the restoration procedure is finished, we will see an image like the following:

![](Image00011.jpg) 

Here the system returns us a prompt, where we will send a "reboot" and start the process of the restored system. It is important to clarify that SELinux will relabel the system and will delay the process a little while this happens.

![](Image00012.jpg) 

Once this process is finished, the system reboots and starts in its normal operation, equal to the moment when the “rear -v mkbackup” was generated.

> INSTALLING VIRTUALIZATION CAPABILITIES (KVM / VIRT-MANAGER)

In the following material you will see how to convert a RHEL 8 host into a thick Virtualization hypervisor. It is important to clarify that "libvirt" is what makes all the magic around Virtualization happen, from there it is that tools such as virsh, virt-manager, Cockpit and OVirt, can do their job.

Since version 2.6 of the Linux kernel, virtualization functionalities are already integrated, it is not necessary to install a new kernel to have these capabilities.

The exercise below first shows a preflight on the host processor, to establish whether or not it is possible to Virtualize on it; This processor must support the active virtualization flags, the flag being "vmx" for Intel processors and "svm" for AMD processors. If any of these flags are present, it is possible to virtualize on the host. Once the flags are validated, we proceed with the initial installation of "libvirt" and then continue with the Hypervisor and client functionalities, which in this case is the virt-manager. The procedure used to perform the installation is as follows:

> [root@pruebas ~]# yum groupinfo Virtualization*

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:12:38 ago on Sun 21 Mar 2021 12:13:24 PM EDT.

> Environment Group: Virtualization Host

> Description: Minimal virtualization host.

> Mandatory Groups:

> Base

> Core

> Standard

> Virtualization Hypervisor

> Virtualization Tools

> Optional Groups:

> Debugging Tools

> Network File System Client

> Remote Management for Linux

> Virtualization Platform

> Group: Virtualization Hypervisor

> Description: Smallest possible virtualization host installation.

> Mandatory Packages:

> libvirt

> qemu-kvm

> Group: Virtualization Client

> Description: Clients for installing and managing virtualization instances.

> Mandatory Packages:

> gnome-boxes

> virt-install

> virt-manager

> virt-viewer

> Default Packages:

> virt-top

> Optional Packages:

> libguestfs-inspect-icons

> libguestfs-tools

> libguestfs-tools-c

> Group: Virtualization Tools

> Description: Tools for offline virtual image management.

> Default Packages:

> libguestfs

> virtio-win

> Optional Packages:

> libguestfs-inspect-icons

> libguestfs-java

> libguestfs-tools

> libguestfs-tools-c

> Group: Virtualization Platform

> Description: Provides an interface for accessing and controlling virtualized guests and containers.

> Mandatory Packages:

> libvirt

> libvirt-client

> virt-who

> Optional Packages:

> fence-virtd-libvirt

> fence-virtd-multicast

> fence-virtd-serial

> perl-Sys-Virt

The virtualization flag is checked on the processor:

> [root@pruebas ~]# cat /proc/cpuinfo

> processor ​ : 0

> --- salida omitida ---

> cpuid level ​ : 11

> wp ​ ​ : yes

> flags ​ ​ : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon rep_good nopl xtopology cpuid tsc_known_freq pni pclmulqdq ssse3 cx16 pcid sse4_1 sse4_2 x2apic popcnt tsc_deadline_timer aes **vmx** lahf_lm cpuid_fault pti tsc_adjust arat umip arch_capabilities

> --- skipped output ---

Another way to validate if the host has the capabilities to virtualize is the following:

> [root@pruebas ~]# virt-host-validate

> QEMU: Checking for hardware virtualization                                 : PASS

> QEMU: Checking if device /dev/vhost-net exists                           : PASS

> QEMU: Checking if device /dev/net/tun exists                               : PASS

> QEMU: Checking for cgroup 'cpu' controller support                    : PASS

> QEMU: Checking for cgroup 'cpuacct' controller support                   : PASS

> QEMU: Checking for cgroup 'cpuset' controller support                     : PASS

> QEMU: Checking for cgroup 'memory' controller support                  : PASS

> QEMU: Checking for cgroup 'devices' controller support                    : PASS

> QEMU: Checking for cgroup 'blkio' controller support                         : PASS

> QEMU: Checking for secure guest support                                             : PASS

It is time to install the Hypervisor capabilities on the host:

> [root@pruebas ~]# yum groupinstall "Virtualization Hypervisor" -y

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:13:55 ago on Sun 21 Mar 2021 12:13:24 PM EDT.

> Dependencies resolved.

> --- skipped output ---

> Installed:

> autogen-libopts-5.18.12-8.el8.x86_64

> gnutls-dane-3.6.14-7.el8_3.x86_64

> gnutls-utils-3.6.14-7.el8_3.x86_64

> libvirt-6.0.0-28.module+el8.3.0+7827+5e65edd7.x86_64

> libvirt-bash-completion-6.0.0-28.module+el8.3.0+7827+5e65edd7.x86_64

> libvirt-client-6.0.0-28.module+el8.3.0+7827+5e65edd7.x86_64

> libvirt-daemon-config-nwfilter-6.0.0-28.module+el8.3.0+7827+5e65edd7.x86_64

> Complete!

It is necessary to install the communication tools with "libvirt", as follows:

> [root@pruebas ~]# yum groupinstall "Virtualization Client" -y --with-optional

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:15:46 ago on Sun 21 Mar 2021 12:13:24 PM EDT.

> Dependencies resolved.

> --- skipped output ---

> Installed:

> hexedit-1.2.13-12.el8.x86_64

> hivex-1.3.18-20.module+el8.3.0+6423+e4cb6418.x86_64

> icoutils-0.32.3-2.el8.x86_64

> libgovirt-0.3.7-3.el8.x86_64

> libguestfs-1:1.40.2-25.module+el8.3.0+7421+642fe24f.x86_64

> libguestfs-inspect-icons-1:1.40.2-25.module+el8.3.0+7421+642fe24f.noarch

> libguestfs-tools-1:1.40.2-25.module+el8.3.0+7421+642fe24f.noarch

> libguestfs-tools-c-1:1.40.2-25.module+el8.3.0+7421+642fe24f.x86_64

> libguestfs-xfs-1:1.40.2-25.module+el8.3.0+7421+642fe24f.x86_64

> netpbm-10.82.00-6.el8.x86_64

> netpbm-progs-10.82.00-6.el8.x86_64

> perl-Class-Inspector-1.32-2.el8.noarch

> perl-Compress-Raw-Bzip2-2.081-1.el8.x86_64

> perl-Compress-Raw-Zlib-2.081-1.el8.x86_64

> perl-Data-Dump-1.23-7.module+el8.3.0+6498+9eecfe51.noarch

> perl-Digest-HMAC-1.03-17.module+el8.3.0+6498+9eecfe51.noarch

> perl-Digest-SHA-1:6.02-1.el8.x86_64

> perl-Encode-Locale-1.05-10.module+el8.3.0+6498+9eecfe51.noarch

> perl-File-Listing-6.04-17.module+el8.3.0+6498+9eecfe51.noarch

> perl-File-ShareDir-1.104-3.el8.noarch

> perl-HTML-Parser-3.72-15.module+el8.3.0+6498+9eecfe51.x86_64

> perl-HTML-Tagset-3.20-34.module+el8.3.0+6498+9eecfe51.noarch

> perl-HTTP-Cookies-6.04-2.module+el8.3.0+6498+9eecfe51.noarch

> perl-HTTP-Date-6.02-19.module+el8.3.0+6498+9eecfe51.noarch

> perl-HTTP-Message-6.18-1.module+el8.3.0+6498+9eecfe51.noarch

> perl-HTTP-Negotiate-6.01-19.module+el8.3.0+6498+9eecfe51.noarch

> perl-IO-Compress-2.081-1.el8.noarch

> perl-IO-HTML-1.001-11.module+el8.3.0+6498+9eecfe51.noarch

> perl-LWP-MediaTypes-6.02-15.module+el8.3.0+6498+9eecfe51.noarch

> perl-NTLM-1.09-17.module+el8.3.0+6498+9eecfe51.noarch

> perl-Net-HTTP-6.17-2.module+el8.3.0+6498+9eecfe51.noarch

> perl-Sys-Guestfs-1:1.40.2-25.module+el8.3.0+7421+642fe24f.x86_64

> perl-Sys-Virt-6.0.0-1.module+el8.3.0+6423+e4cb6418.x86_64

> perl-TimeDate-1:2.30-15.module+el8.3.0+6498+9eecfe51.noarch

> perl-Try-Tiny-0.30-7.module+el8.3.0+6498+9eecfe51.noarch

> perl-WWW-RobotRules-6.02-18.module+el8.3.0+6498+9eecfe51.noarch

> perl-hivex-1.3.18-20.module+el8.3.0+6423+e4cb6418.x86_64

> perl-libintl-perl-1.29-2.el8.x86_64

> perl-libwww-perl-6.34-1.module+el8.3.0+6498+9eecfe51.noarch

> python3-argcomplete-1.9.3-6.el8.noarch

> python3-libvirt-6.0.0-1.module+el8.3.0+6423+e4cb6418.x86_64

> scrub-2.5.2-14.el8.x86_64

> supermin-5.1.19-10.module+el8.3.0+6423+e4cb6418.x86_64

> syslinux-6.04-4.el8.x86_64

> syslinux-extlinux-6.04-4.el8.x86_64

> syslinux-extlinux-nonlinux-6.04-4.el8.noarch

> syslinux-nonlinux-6.04-4.el8.noarch

> virt-install-2.2.1-3.el8.noarch

> virt-manager-2.2.1-3.el8.noarch

> virt-manager-common-2.2.1-3.el8.noarch

> virt-top-1.0.8-32.el8.x86_64

> virt-viewer-9.0-4.el8.x86_64

At the end of this installation you have the necessary capabilities to host virtual machines thanks to the virtualization platform, for this you can use the applications "virsh", "virt-manager" (graphical interface) or cockpit (web console).

> INSTALLING A VIRTUAL MACHINE BY VIRT-MANAGER

The exercise that will be carried out below corresponds to the installation of a virtual machine from the ISO “proxmox-ve_6.3-1.iso” located in the path “/ tmp”. The installation of this virtual machine will be carried out on an XFS filesystems mounted (/ machines) on an LVM structure. We start by verifying the existence of the installation ISO:

> [root@bd2 ~]# ll -h /tmp/proxmox-ve_6.3-1.iso

> -rw-r--r--. 1 root root 813M Mar 28 10:41 /tmp/proxmox-ve_6.3-1.iso

The LVM structure is identified and created to host the virtual machines:

> [root@bd2 ~]# lsblk

> NAME          MAJ:MIN RM  SIZE RO TYPE

> --- salida omitida ---

> sdc             8:32   0  100G  0 disk

> [root@bd2 ~]# pvcreate /dev/sdc

> Physical volume "/dev/sdc" successfully created.

> [root@bd2 ~]# vgcreate mv /dev/sdc

> Volume group "mv" successfully created

> [root@bd2 ~]# lvcreate -l 100%free -n kvm mv

> Logical volume "kvm" created.

The XFS file system is assigned and made available persistently:

> [root@bd2 ~]# mkfs.xfs /dev/mv/kvm

> [root@bd2 ~]# blkid | grep sdc >> /etc/fstab

> [root@bd2 ~]# mkdir /maquinas

> [root@bd2 ~]# vim /etc/fstab

> UUID="be82828b-ce08-4a38-bc1c-093284b1464c" /maquinas xfs defaults 0 0

> [root@bd2 ~]# udevadm settle

> [root@bd2 ~]# systemctl daemon-reload

Once the process is finished, it is defined that "/ maquinas" is a mounting point where you can save virtual machines created from the virt-manager, as shown below:

> [root@bd2 ~]# df -hT

> Filesystem            Type      Size  Used Avail Use% Mounted on

> --- salida omitida ---

> /dev/mapper/mv-kvm    xfs       100G  746M  100G   1% /maquinas

Then through "virt-manager" the mount point is added, in "virt-manager" this is known as adding a "pool":

![](Image00013.jpg) 

In the upper tab you can see the “storage” option, having chosen it, click on the “+” icon where a screen is presented that offers the possibility of naming the “pool” and choosing the mounting point:

![](Image00014.jpg) 

When adding the pool (filesystem in the mount point) you should see a screen like the following:

![](Image00015.jpg) 

Next, the virtual machine is created by searching for the installation ISO in /tmp, defining Linux Debian 10 as the operating system to install:

![](Image00016.jpg) 

It is necessary to establish the RAM memory to use, as detailed:

![](Image00017.jpg) 

Next, the virtual machine hosting site is defined, taking the option "Select or create custom storage":

![](Image00018.jpg) 

We are presented with a screen where the "+" icon is chosen to create the virtual machine file:

![](Image00019.jpg) ![](Image00020.jpg) 

At the end of the process of defining the name, format and size of the virtual machine file, you should see an image like the one above and when you click on the option "Choose Volume" you should see an image like the following:

![](Image00021.jpg) 

The last screen will allow us to name the virtual machine and define the network:

![](Image00022.jpg) 

Finally, clicking on the "Finish" button will start the installation of the preferred ISO, in this case the Proxmox platform:

![](Image00023.jpg) 

> INSTALLING AND CONFIGURING A WEBSERVER - NGINX

The different modules to install Nginx are listed:

> [root@pruebas ~]# yum module list nginx

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:44:06 ago on Mon 22 Mar 2021 08:46:03 AM EDT.

> Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)

> Name                     Stream                     Profiles                     Summary

> nginx                    1.14 [d]                 common [d]                   nginx webserver

> nginx                    1.16                       common [d]                   nginx webserver

> nginx                    1.18                       common [d]                   nginx webserver

The profiles available for this module are reviewed:

> [root@pruebas ~]# yum module info nginx:1.14 --profile

> Updating Subscription Management repositories.

> Last metadata expiration check: 1:01:04 ago on Mon 22 Mar 2021 08:46:03 AM EDT.

> Name   : nginx:1.14:8000020190830002848:f8e95b4e:x86_64

> common : nginx

> : nginx-all-modules

> : nginx-filesystem

> : nginx-mod-http-image-filter

> : nginx-mod-http-perl

> : nginx-mod-http-xslt-filter

> : nginx-mod-mail

> : nginx-mod-stream

It is time to install "nginx: 1.14", you can install the version that corresponds to your requirements:

> [root@pruebas ~]# yum module install nginx:1.14

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:58:57 ago on Mon 22 Mar 2021 08:46:03 AM EDT.

> Dependencies resolved.

> ==================================================================================================

> Package                    Arch   Version                                 Repository                        Size

> =========================================================================

> Installing group/module packages:

> nginx                      x86_64 1:1.14.1-9.module+el8.0.0+4108+af250afe rhel-8-for-x86_64-appstream-rpms 570 k

> nginx-all-modules          noarch 1:1.14.1-9.module+el8.0.0+4108+af250afe rhel-8-for-x86_64-appstream-rpms  24 k

> Installed:

> nginx-1:1.14.1-9.module+el8.0.0+4108+af250afe.x86_64

> nginx-all-modules-1:1.14.1-9.module+el8.0.0+4108+af250afe.noarch

> nginx-filesystem-1:1.14.1-9.module+el8.0.0+4108+af250afe.noarch

> nginx-mod-http-image-filter-1:1.14.1-9.module+el8.0.0+4108+af250afe.x86_64

> nginx-mod-http-perl-1:1.14.1-9.module+el8.0.0+4108+af250afe.x86_64

> nginx-mod-http-xslt-filter-1:1.14.1-9.module+el8.0.0+4108+af250afe.x86_64

> nginx-mod-mail-1:1.14.1-9.module+el8.0.0+4108+af250afe.x86_64

> nginx-mod-stream-1:1.14.1-9.module+el8.0.0+4108+af250afe.x86_64

It is necessary to open the ports in FirewallD to receive connection requests:

> [root@pruebas ~]# firewall-cmd --permanent --add-service=http

> success

> [root@pruebas ~]# firewall-cmd --reload

> success

Enable the "nginx" service at system startup and run it immediately:

> [root@pruebas ~]# systemctl enable nginx --now

> Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /usr/lib/systemd/system/nginx.service.

The "nginx" service is verified in operation by listing the system processes:

> [root@pruebas ~]# ps -fe

> root       10798       1  0 09:03 ?        00:00:00 nginx: master process /usr/sbin/nginx

> nginx      10799   10798  0 09:03 ?        00:00:00 nginx: worker process

> nginx      10800   10798  0 09:03 ?        00:00:00 nginx: worker process

> nginx      10801   10798  0 09:03 ?        00:00:00 nginx: worker process

> nginx      10802   10798  0 09:03 ?        00:00:00 nginx: worker process

> nginx      10803   10798  0 09:03 ?        00:00:00 nginx: worker process

> nginx      10804   10798  0 09:03 ?        00:00:00 nginx: worker process

> nginx      10805   10798  0 09:03 ?        00:00:00 nginx: worker process

> nginx      10806   10798  0 09:03 ?        00:00:00 nginx: worker process

At the end of the procedure and to verify the start-up of the “nginx” web server, take the IP address of the RHEL server and open the HTTP client of your choice on a computer other than RHEL 8, you will see an image similar to the following:

![](Image00024.jpg) 

The "nginx" service uses the path "/usr/share/nginx/html" as the content publishing directory, if you need to publish some type of content you can place your HTML files there, as shown below:

> [root@pruebas html]# pwd

> /usr/share/nginx/html

> [root@pruebas html]# ll

> total 24

> -rw-r--r--. 1 root root 3971 Aug 30  2019 404.html

> -rw-r--r--. 1 root root 4020 Aug 30  2019 50x.html

> -rw-r--r--. 1 root root 4057 Aug 30  2019 index.html

> -rw-r--r--. 1 root root  368 Aug 30  2019 nginx-logo.png

> -rw-r--r--. 1 root root 4148 Aug 30  2019 poweredby.png

To configure the “nginx” service use the /etc/nginx/nginx.conf file:

> [root@pruebas ~]# ll /etc/nginx/nginx.conf

> -rw-r--r--. 1 root root 2469 Aug 30  2019 /etc/nginx/nginx.conf

VIRTUAL HOSTS IN NGINX

One of the great benefits of using a web server, be it Apache Web Server or Nginx, is to be able to take this service to configure different web sites within the same host; The procedure to be executed is based on the traditional scheme of the vast majority of companies where I have done consultancies: a network with a Microsoft Windows Server performing the functions of Active Directory and DNS, in this case with the direct zone “aptivalabs.net ”And the DNS records w1.aptivalabs.net, w2.aptivalabs.net and w3.aptivalabs.net pointing to host 192.168.1.201\. In this case, the host 192.168.1.201 will host the different websites.

The procedure begins by creating the folders that will host the html files:

> [root@pruebas ~]# mkdir /w1

> [root@pruebas ~]# mkdir /w2

> [root@pruebas ~]# mkdir /w3

Next, the directories are created to host the logs based on the access to the virtual hosts:

> [root@pruebas ~]# mkdir /var/log/nginx/w1/

> [root@pruebas ~]# mkdir /var/log/nginx/w2/

> [root@pruebas ~]# mkdir /var/log/nginx/w3/

It is necessary to change the SELinux policy for the directories that will host the websites and apply it immediately to them:

> [root@pruebas ~]# semanage fcontext -a -t httpd_sys_content_t "/w1(/.*)?"

> [root@pruebas ~]# semanage fcontext -a -t httpd_sys_content_t "/w2(/.*)?"

> [root@pruebas ~]# semanage fcontext -a -t httpd_sys_content_t "/w3(/.*)?"

> [root@pruebas ~]# restorecon -Rv /w1

> Relabeled /w1 from unconfined_u:object_r:default_t:s0 to unconfined_u:object_r:httpd_sys_content_t:s0

> [root@pruebas ~]# restorecon -Rv /w2

> Relabeled /w2 from unconfined_u:object_r:default_t:s0 to unconfined_u:object_r:httpd_sys_content_t:s0

> [root@pruebas ~]# restorecon -Rv /w3

> Relabeled /w3 from unconfined_u:object_r:default_t:s0 to unconfined_u:object_r:httpd_sys_content_t:s0

Before editing the "nginx" service configuration file, create a copy of it:

> [root@pruebas ~]# cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.ori

In the "nginx" configuration file you will find a section like the one shown:

![](Image00025.jpg) 

Add the following content to the file “/etc/nginx/nginx.conf” as blocks under the “server” section, which is shown below:

> [root@pruebas ~]# vim /etc/nginx/nginx.conf

> server {

> server_name w1.aptivalabs.net;

> root /w1;

> access_log /var/log/nginx/w1/access.log;

> error_log /var/log/nginx/w1/error.log;

> }

> server {

> server_name w2.aptivalabs.net;

> root /w2;

> access_log /var/log/nginx/w2/access.log;

> error_log /var/log/nginx/w2/error.log;

> }

> server {

> server_name w3.aptivalabs.net;

> root /w3;

> access_log /var/log/nginx/w3/access.log;

> error_log /var/log/nginx/w3/error.log;

> }

Restart the "nginx" service:

> [root@pruebas ~]# systemctl restart nginx.service

Next, three (3) "html" files are created as index files for each of the websites, these will be the default files or pages to show once the clients make requests about them:

> [root@pruebas ~]# echo "<h1>Server 1 </h1>" >> /w1/index.html

> [root@pruebas ~]# echo "<h1>Server 2 </h1>" >> /w2/index.html

> [root@pruebas ~]# echo "<h1>Server 3 </h1>" >> /w3/index.html

To verify that the procedure has been effective and successful, please validate on your own server as follows:

> [root@pruebas ~]# curl w1.aptivalabs.net

> <h1>Server 1 </h1>

> [root@pruebas ~]# curl w2.aptivalabs.net

> <h1>Server 2 </h1>

> [root@pruebas ~]# curl w3.aptivalabs.net

> <h1>Server 3 </h1>

Please use a web browser to verify the response from each of these web sites.

REVERSE PROXY  FOR HTTP TRAFIC

You can configure the NGINX web server to act as a reverse proxy for HTTP traffic. You can use this functionality to forward requests to a specific subdirectory on a remote server, the client assumes that it loads the content from the host it accesses, however the "nginx" service loads the actual content from the remote server and forwards it to the client.

For the example below, there are two web servers running at 192.168.1.202 and 192.168.1.201; The exercise consists in that if a user requests to see the content on the server 192.168.1.201/test, this server will actually show the public content at the URL http://192.168.1.202/test.html; In this sense, let's run the web server at 192.168.1.202 creating the file "test.html":

> [root@ap2 ~]# cd /usr/share/nginx/

> [root@ap2 nginx]# ll

> total 0

> drwxr-xr-x. 2 root root  99 Mar 22 09:44 html

> drwxr-xr-x. 2 root root 143 Mar 22 09:44 modules

> [root@ap2 nginx]# cd html/

> [root@ap2 html]# echo "<h1>Contenido 1 en 192.168.1.202</h1>" >> test.html

> [root@ap2 html]# echo "<h1>Contenido 2 en 192.168.1.202</h1>" >> test.html

> [root@ap2 html]# echo "<h1>Contenido 3 en 192.168.1.202</h1>" >> test.html

The 192.168.1.202 server is verified to be publishing the resource (test.html), as follows:

![](Image00026.jpg) 

Next, on the server 192.168.1.201, we edit the “nginx” configuration file to add the following lines:

> [root@pruebas html]# vim /etc/nginx/nginx.conf

> location /test {

> proxy_pass http://192.168.1.202/test.html;

> }

In the “nginx” configuration file, the configuration block should look like this:

> server {

> listen       80 default_server;

> listen       [::]:80 default_server;

> server_name  _;

> root         /usr/share/nginx/html;

> # Load configuration files for the default server block.

> include /etc/nginx/default.d/*.conf;

> #location / {

> #}

> location /test {

> proxy_pass http://192.168.1.202/test.html;

> }

> error_page 404 /404.html;

> location = /40x.html {

> }

> error_page 500 502 503 504 /50x.html;

> location = /50x.html {

> }

> }

Next, the Boolean variable "httpd_can_network_connect" is enabled in SELinux and the service is launched again:

> [root@pruebas html]# setsebool -P httpd_can_network_connect 1

> [root@pruebas html]# systemctl restart nginx.service

To confirm this setting on an HTTP client make a request at http://192.168.1.201/test, as shown below:

![](Image00027.jpg) 

With the exercise previously developed, in one way or another the server that actually gives the answer to the client has been hidden, this being 192.168.1.202; Users go to the 192.168.1.201 web server to look for answers and it displays the content of another web server.

HTTP LOAD BALANCER WITH NGINX

This procedure describes the configuration of the NGINX service as an HTTP load balancer that sends requests to different servers, depending on which one has the least number of active connections, that is, it is about determining which of the servers within the balancing group has better health to send you http requests. It is a useful scenario when handling web applications within a company and it is necessary to have at least a high availability scenario for that application.

To develop this functionality there is the following group of servers:

*   > 192.168.1.201 = load balancer

*   > 192.168.1.202 = server

*   > 192.168.1.203 = server

In order to validate that the balancer is actually doing its job, on servers 192.168.1.202 and 192.168.1.203 (with the "nginx" service running) change the default index page (index.html), as shown below:

> [root@sr2 ~]# cd /usr/share/nginx/html/

> [root@sr2 html]# mv index.html index.html.ori

> [root@sr2 html]# echo "<h1>soy 192.168.1.202</h1>" >> index.html

The same instructions are executed on the 192.168.1.203 server:

> [root@sr3 ~]# cd /usr/share/nginx/html/

> [root@sr3 html]# mv index.html index.html.ori

> [root@sr3 html]# echo "<h1>soy 192.168.1.203</h1>" >> index.html

On the server that will be doing load balancing, the configuration file for “nginx” should look like this:

> http {

> log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '

> '$status $body_bytes_sent "$http_referer" '

> '"$http_user_agent" "$http_x_forwarded_for"';

> access_log  /var/log/nginx/access.log  main;

> sendfile            on;

> tcp_nopush          on;

> tcp_nodelay         on;

> keepalive_timeout   65;

> types_hash_max_size 2048;

> include             /etc/nginx/mime.types;

> default_type        application/octet-stream;

> # Load modular configuration files from the /etc/nginx/conf.d directory.

> # See http://nginx.org/en/docs/ngx_core_module.html#include

> # for more information.

> include /etc/nginx/conf.d/*.conf;

> upstream loadbalancer.aptivalabs.net {

> least_conn;

> server 192.168.1.202;

> server 192.168.1.203;

> }

> server {

> listen       80 default_server;

> listen       [::]:80 default_server;

> server_name  _;

> root         /usr/share/nginx/html;

> # Load configuration files for the default server block.

> include /etc/nginx/default.d/*.conf;

> #location / {

> #}

> location / {

> proxy_pass http://loadbalancer.aptivalabs.net;

> }

> error_page 404 /404.html;

> location = /40x.html {

> }

> error_page 500 502 503 504 /50x.html;

> location = /50x.html {

> }

> }

> # Settings for a TLS enabled server.

> #

> #    server {

> #        listen       443 ssl http2 default_server;

> #        listen       [::]:443 ssl http2 default_server;

> #        server_name  _;

> #        root         /usr/share/nginx/html;

> #

> #        ssl_certificate "/etc/pki/nginx/server.crt";

> #        ssl_certificate_key "/etc/pki/nginx/private/server.key";

> #        ssl_session_cache shared:SSL:1m;

> #        ssl_session_timeout  10m;

> #        ssl_ciphers PROFILE=SYSTEM;

> #        ssl_prefer_server_ciphers on;

> #

> #        # Load configuration files for the default server block.

> #        include /etc/nginx/default.d/*.conf;

> #

> #        location / {

> #        }

> #

> #        error_page 404 /404.html;

> #            location = /40x.html {

> #        }

> #

> #        error_page 500 502 503 504 /50x.html;

> #            location = /50x.html {

> #        }

> #    }

> }

The lines "upstream" and "location" can then be highlighted from the content of the file, which indicate that at the moment that any user who tries to reach http://loadbalancer.aptivalabs.net (DNS record previously configured pointing to 192.168\. 1.201), the ip 192.168.1.201 will balance the load of requests it receives; the lines are related:

> upstream loadbalancer.aptivalabs.net {

> least_conn;

> server 192.168.1.202;

> server 192.168.1.203;

> }

> location / {

> proxy_pass http://loadbalancer.aptivalabs.net;

> }

One way to validate this configuration is by using the “curl” application, as shown below:

> [root@sr1 ~]# curl http://loadbalancer.aptivalabs.net

> <h1>soy 192.168.1.202</h1>

> [root@sr1 ~]# curl http://loadbalancer.aptivalabs.net

> <h1>soy 192.168.1.203</h1>

> [root@sr1 ~]# curl http://loadbalancer.aptivalabs.net

> <h1>soy 192.168.1.202</h1>

> [root@sr1 ~]# curl http://loadbalancer.aptivalabs.net

> <h1>soy 192.168.1.203</h1>

> [root@sr1 ~]# curl http://loadbalancer.aptivalabs.net

> <h1>soy 192.168.1.202</h1>

It can then be seen that by requesting the URL http://loadbalancer.aptivalabs.net with the command "curl" the "nginx" service always shows a different page. For a better visualization you could use any HTTP client.

ENCRYPTING COMMUNICATION  WITH TLS

TLS (Transport Layer Security) is an encryption method for network communications and is the successor to SSL (Secure Socket Layer). TLS allows the client to verify the identity of the server and the server to verify the identity of the client.

Features:

*   > TLS is based on the concept of certificates.

*   > A certificate has multiple parts: public key, server identity and a signature of an authority certificate

*   > The corresponding private key is never made public

*   > Any data encrypted with a private key can only be decrypted with a public key and vice versa

The stages of communication involve the development of various activities; the client and the server agree on the encryption rules supported by both and exchange random bits of data. The client uses this data to generate a session key, a key that will be used for faster symmetric encryption, where the same key is used for encryption and decryption. To ensure that this key is not compromised, it is sent to the server encrypted with the server's public key.

The certificates necessary to encrypt the communication are generated below, as shown:

> [root@loadbalancer ~]# openssl req -x509 **-out localhost.crt -keyout localhost.key**    -newkey rsa:2048 -nodes -sha256   -subj '/CN=localhost' -extensions EXT -config <( \

> printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")

It is necessary to copy the certificates to the corresponding path for the "nginx" service to read them, this path must be defined in the "nginx" configuration file:

> [root@loadbalancer ~]# cp localhost.crt /etc/pki/tls/certs/localhost.crt

> [root@loadbalancer ~]# cp localhost.key /etc/pki/tls/private/localhost.key

The configuration file for the “nginx” service should look like this:

> [root@loadbalancer ~]# cat /etc/nginx/nginx.conf

> server {

> listen       443 ssl http2 default_server;

> listen       [::]:443 ssl http2 default_server;

> server_name  _;

> root         /usr/share/nginx/html;

> ssl_certificate "/etc/pki/tls/certs/localhost.crt";

> ssl_certificate_key "/etc/pki/tls/private/localhost.key";

> listen       80 default_server;

> listen       [::]:80 default_server;

> #server_name  _;

> ​ #server_name loadbalancer.aptivalabs.net;

> #root         /usr/share/nginx/html;

> # Load configuration files for the default server block.

> include /etc/nginx/default.d/*.conf;

> location / {

> }

> error_page 404 /404.html;

> location = /40x.html {

> }

> error_page 500 502 503 504 /50x.html;

> location = /50x.html {

> }

> }

It can be seen that the "nginx" service is left configured to receive requests on ports 80 and 443 using the same publication path, which is "/ usr / share / nginx / html". In the same way, the routes where "nginx" will look for the certificates are listed. The operation indicates that it is necessary to tell FirewallD to accept HTTPS requests in the default zone, the HTTP requests were already added in FirewallD:

> [root@loadbalancer ~]# firewall-cmd --permanent --add-service=https

> success

> [root@loadbalancer ~]# firewall-cmd --reload

> success

To verify the configuration, run an HTTP client of your choice and try to communicate with the server via HTTP, as shown below:

![](Image00028.jpg) 

Next, in your HTTP client, try to communicate via HTTPS:

![](Image00029.jpg) 

> UNATTENDED INSTALATIONS - KICKSTART

In an environment where it is frequently necessary to perform RHEL 8 installations (a procedure that could also be emulated in Oracle Linux and CentOS 8), it can be a bit tiring to run a manual process when trying to install many systems; It may be the case, for example, of installing an entire training environment for 20 students to carry out Linux labor, or the case of a company that needs to implement a cluster of services (storage, virtualization, etc.) where many Linux systems intervene.

Faced with this situation, the Kickstart tool allows generating an unattended, automated installation, where it will only be necessary to tell the installer where to find the file with the definition of the installation and the installer executes this activity without the Administrator having the need to be present according to the installation of each system.

For the development of this activity it is necessary to execute the following steps:

1.  > Generate the kickstart file (installation definition file)

2.  > Publish the kickstart file to a visible resource

3.  > Publish the installation package

4.  > Start the installation from an installation ISO

In the scenario of the exercise to be implemented, it is related to the server with IP address 192.168.0.200, which has the “Nginx” service implemented and the RHEL 8 installation ISO mounted within the Nginx publication path.

The first step consists of generating a kickstart file, which is a text file where the required characteristics of the installation are defined in its own format. The generation of this file can be done using a tool that Red Hat provides for this purpose, which can be found at the URL https://access.redhat.com/labs/kickstartconfig/. In the same way, RHEL 8 and derived systems, once they have finished their installation, leave a file in “/root” called “anaconda-ks.cfg” which is a kickstart file:

> [root@loadbalancer ~]# pwd

> /root

> [root@loadbalancer ~]# ll anaconda-ks.cfg

> -rw-------. 1 root root 1275 Dec 17 17:21 anaconda-ks.cfg

In the development of this exercise, the tool https://access.redhat.com/labs/kickstartconfig/ has been used, where a file has been generated and downloaded to the RHEL 8 server; the generated file defines the deployment of a “minimal installation” environment; the generated file is detailed:

> [root@loadbalancer html]# cat ks.cfg

> lang en_US

> keyboard us

> timezone America/Bogota --isUtc

> rootpw $1$wRe6mImL$eyda8JWudogBZ5pMTTVU9/ --iscrypted

> #platform x86, AMD64, or Intel EM64T

> reboot

> url --url=http://192.168.0.200/repo

> bootloader --location=mbr --append="rhgb quiet crashkernel=auto"

> zerombr

> clearpart --all --initlabel

> autopart

> auth --passalgo=sha512 --useshadow

> selinux --enforcing

> firewall --enabled

> firstboot --disable

> %packages

> @^minimal-environment

> %end

The file can take any name, the important thing is that the ending ".cfg" is used; It defines the language, the password of the “root” user, the URL where the installation packages are located, the auto-partitioning, the SELinux and FirewallD operating mode, among other data. These settings can be customized as required.

This generated file must be published in a visible resource, in this case and taking advantage of the “Nginx” web server installation, we will use the path “/usr/share/nginx/html” to publish the kickstart file.

The installation package refers to the installers for the Linux distribution; For this exercise, the installed web server (Nginx) is used; in this sense, the DVD drive will be made available within the web server's publication path (“/usr/share/nginx/html/repo):

> [root@loadbalancer html]# mkdir /usr/share/nginx/html/repo

> [root@loadbalancer html]# echo “/dev/sr0 /usr/share/nginx/html/repo iso9660 defaults 0 0” >> /etc/fstab

> [root@loadbalancer html]# udevadm settle

> [root@loadbalancer html]# systemctl daemon-reload

> [root@loadbalancer html]# mount -a

> [root@loadbalancer html]# cat /etc/fstab

> /dev/sr0 /usr/share/nginx/html/repo iso9660 defaults 0 0

Before submitting the installation, validate that the kickstart file is available via HTTP, as shown below:

> [root@loadbalancer ~]# curl http://192.168.0.200/ks.cfg

> lang en_US

> keyboard us

> timezone America/Bogota --isUtc

> rootpw $1$wRe6mImL$eyda8JWudogBZ5pMTTVU9/ --iscrypted

> #platform x86, AMD64, or Intel EM64T

> reboot

> url --url=http://192.168.0.200/repo

> bootloader --location=mbr --append="rhgb quiet crashkernel=auto"

> zerombr

> clearpart --all --initlabel

> autopart

> auth --passalgo=sha512 --useshadow

> selinux --enforcing

> firewall --enabled

> firstboot --disable

> %packages

> @^minimal-environment

> %end

It is then time to generate the installation; enter the RHEL 8 installation ISO and power on your hardware or virtual machine keeping in mind to boot through the installation ISO. You should see the familiar installation image for Red Hat Enterprise Linux systems. Choose the option "Troubleshooting" and then press the "TAB" key, at which point the installer will show you a command line interface where at the end it will add the following parameters:

> inst.ks=http://192.168.0.200/ks.cfg

It is all you need to do; if you have a USB you can move on to another installation.  The following image shows the procedure explained above:

![](Image00030.jpg) 

The installation will start automatically without the need for you to be aware of it, as shown in the following image:

![](Image00031.jpg) 

> DEPLOYING A FILESERVER WITH SAMBA

Samba implements the Server Message Block (SMB) protocol in RHEL. This protocol is used to access a server's resources such as shared files and printers. The deployment of an SMB server such as Samba implies, as appropriate, some of the services that Samba has associated with, such as "smbd", "nmbd" and "winbind".

The “smbd” service provides file sharing and printing services using the SMB protocol, and is also responsible for blocking resources and authenticating users who connect to Samba.

The “nmbd” service provides the hostname and IP resolution using the NetBIOS over IPv4 protocol. In addition to name resolution, the nmbd service allows you to browse the SMB network to locate domains, workgroups, hosts, file shares, and printers.

The "winbind" service provides an interface for the Name Exchange Service (NSS - Network Service Switch) to integrate local and AD (Active Directory) users and groups into the local system. This allows domain users to authenticate to services managed by the Samba server or other local services. If you configure Samba as a domain member, “winbind” must be started before the “smbd” service, otherwise the domain users and groups will not be available to the local system.

For a better understanding of how to implement Samba in its role as file server, we will take the server with IP 192.168.0.201 as the Samba server; We will simulate a scenario of some work groups (treasury and hr - human resources) within a company that require having permissions on folders within the system to save files. People who will access these will use Linux Red Hat, Microsoft Windows 10, and Apple Mac OSX systems. These people will be able to save personal information in personal folders and in group folders; at no time will they be able to access the Shell on the Linux server.

The exercise begins with the installation of Samba, as shown:

> [root@sr1 ~]# yum -y install samba

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:35:00 ago on Wed 24 Mar 2021 03:19:16 PM EDT.

> Dependencies resolved.

> ========================================================================

> Package                    Architecture   Version                    Repository                             Size

> ========================================================================

> Installing:

> samba                      x86_64         4.12.3-14.el8_3            rhel-8-for-x86_64-baseos-rpms         840 k

> Installing dependencies:

> samba-common-tools         x86_64         4.12.3-14.el8_3            rhel-8-for-x86_64-baseos-rpms         484 k

> samba-libs                 x86_64         4.12.3-14.el8_3            rhel-8-for-x86_64-baseos-rpms         188 k

> Transaction Summary

> ========================================================================

> Install  3 Packages

> Total download size: 1.5 M

> Installed size: 4.0 M

> Installed:

> samba-4.12.3-14.el8_3.x86_64   samba-common-tools-4.12.3-14.el8_3.x86_64   samba-libs-4.12.3-14.el8_3.x86_64

We proceed to create the folders that will contain the information of the work groups; It is important to mention that in a real scenario it would be recommended that /datos be the mount point of an XFS filesystem mounted on an LVM structure with LV Thin; the folders are created:

> [root@sr1 ~]# mkdir -p /datos/tesoreria

> [root@sr1 ~]# mkdir /datos/rrhh

The workgroups are created and the respective permissions are assigned on the created folders:

> [root@sr1 ~]# groupadd -r tesoreria

> [root@sr1 ~]# groupadd -r rrhh

> [root@sr1 ~]# chgrp tesoreria /datos/tesoreria

> [root@sr1 ~]# chgrp rrhh /datos/rrhh

> [root@sr1 ~]# chmod 2770 /datos/tesoreria

> [root@sr1 ~]# chmod 2770 /datos/rrhh

You can see in the previous instruction the creation of "setgid" permissions so that the files created in each of the group folders continue to belong to the same group once created; The same is done by declaring ACL’s by default so that files and directories in the future retain the necessary attributes so that the users of the “treasury” and “hr” groups continue to have rights over the resources:

> [root@sr1 ~]# setfacl -m g:tesoreria:rwx /datos/tesoreria

> [root@sr1 ~]# setfacl -m d:g:tesoreria:rwx /datos/tesoreria

> [root@sr1 ~]# setfacl -m g:rrhh:rwx /datos/rrhh

> [root@sr1 ~]# setfacl -m d:g:rrhh:rwx /datos/rrhh

It is time to control access to these directories using SELinux, which must be in "enforcing" mode:

> [root@sr1 ~]# semanage fcontext -a -t samba_share_t ‘/datos/tesoreria(/.*)?’

> [root@sr1 ~]# semanage fcontext -a -t samba_share_t ‘/datos/rrhh(/.*)?’

> [root@sr1 ~]# restorecon -vvFR /datos/tesoreria

> [root@sr1 ~]# restorecon -vvFR /datos/rrhh

The above statement immediately creates and applies SELinux policies on the folders that will contain the workgroup data. Then the SELinux Booleans are activated that will allow the export of the /home folder and the workgroup folders:

> [root@sr1 ~]# setsebool -P samba_export_all_rw on

> [root@sr1 ~]# setsebool -P samba_export_all_ro on

> [root@sr1 ~]# setsebool -P samba_enable_home_dirs on

Next, the users of the Linux system corresponding to each workgroup are created, which must be created without access to Shell, without a primary group since their main group must be their workgroup; in the same way and immediately the Samba user is created with the same name as the user in Linux and the same password.

> [root@sr1 ~]# adduser -N -s /sbin/nologin -g tesoreria t1

> [root@sr1 ~]# smbpasswd -a t1

> New SMB password:

> Retype new SMB password:

> Added user t1.

> [root@sr1 ~]# adduser -N -s /sbin/nologin -g rrhh r1

> [root@sr1 ~]# smbpasswd -a r1

> New SMB password:

> Retype new SMB password:

> Added user r1.

If you take a look at / home, the users directory, you will see the following:

> [root@sr1 ~]# ll /home/

> total 4

> drwx------.  3 r1      rrhh        78 Mar 24 16:49 r1

> drwx------.  3 t1      tesoreria   78 Mar 24 16:48 t1

Once the entire structure that the file server will support has been defined, it is necessary to save a copy of the original Samba file for backup reasons. The Samba installation created the path “/etc/samba” which is where its configuration files are hosted, as shown:

> [root@sr1 ~]# cd /etc/samba/

> [root@sr1 samba]# pwd

> /etc/samba

> [root@sr1 samba]# mv smb.conf smb.conf.original

> [root@sr1 samba]# mv smb.conf.example smb.conf

The file "smb.conf.example" is the one that contains the configuration we need for Samba, so that when it is renamed it remains as the main configuration file, "smb.conf". Following these steps, it is necessary to edit this configuration file to establish the following guidelines:

> [root@sr1 ~]# vim /etc/samba/smb.conf

​ workgroup = WORKGROUP

> interfaces = lo ens18

> host allow = 127\. 192.168.0.

> security = user

> passdb backend = tdbsam

The previous definition sets the following properties for Samba in the [global] section:

> •  Security: indicates how clients will be able to access Samba services, "user" defines what it will be using username and passwords.

> •  interfaces: interface that Samba will use to listen to requests

> •  host allow: host or networks that will be able to use the service

Following the edition of the Samba configuration file (at the end of it) it is necessary to add the resources to share, in this case the folders previously created:

> [tesoreria]

> ​ comment = Grupo Tesorería

> ​ path = /datos/tesoreria

> ​ writable = yes

> ​ valid users =  @tesoreria

> [rrhh]

> ​ comment = Grupo RRHH

> ​ path = /datos/rrhh

> ​ writable = yes

> ​ valid users =  @rrhh

In this case are two resources, one called "treasury" and another called "hr", which will be allowed only to the corresponding groups, which are written with the character "@". Keep in mind that each user created, in this case "t1" and "r1" will have a folder in /home where they can save information that only they can see and manipulate.

Once the edition of the configuration file is finished, a “testparm” is executed to validate the edition of the Samba configuration file.

> [root@sr1 ~]# testparm

Once the Samba configuration file is successfully validated, the service is started and the service is activated to start the Linux server, as well as the FirewallD rule is established to allow receiving this type of requests:

> [root@sr1 ~]# systemctl enable smb

> [root@sr1 ~]# systemctl start smb

> [root@sr1 ~]# firewall-cmd  --permanent  --add-service=samba

> [root@sr1 ~]# firewall-cmd  --reload

SMB CLIENTS

To access the services of this file server you can from a computer with Apple Mac Osx system make a connection from the “Finder” application, “Go / Connect to Server…” menu; this time we will register using the user "t1" previously created, as shown below:

![](Image00032.jpg)![](Image00033.jpg)

In the case of Microsoft Windows clients, as in the case of Windows 10, you can use "Windows Explorer" to connect to the Samba server from the address bar of this tool, entering a \\ 192.168.0.201, as shown in the following images:

![](Image00034.jpg) 

Once you have entered the corresponding credentials, you will be able to save files accordingly.

In the event that it is required to connect a Linux RHEL 8 server to the file server deployed in Samba previously, you must do the following on that server:

> [root@loadbalancer ~]# yum -y install cifs-utils

> Updating Subscription Management repositories.

> Last metadata expiration check: 5:42:05 ago on Wed 24 Mar 2021 10:46:12 AM -05.

> ------

> Complete!

> [root@loadbalancer ~]# mkdir /mnt/t1

> [root@loadbalancer ~]# mount -o username=t1 //192.168.0.201/tesoreria /mnt/t1

> Password for t1@//192.168.0.201/tesoreria:  ******

> [root@loadbalancer ~]# df -hT

> Filesystem                Type      Size  Used Avail Use% Mounted on

> --- salida omitida ---

> //192.168.0.201/tesoreria cifs       44G  5.1G   39G  12% /mnt/t1

To carry out a persistent mount it is necessary to create a file with the access credentials (in this case those of the user “t1”), set a permission on the file and edit “/ etc / fstab”, as shown below:

> [root@loadbalancer ~]# vim credenciales.smb

> username=t1

> password=123456

> [root@loadbalancer ~]# chmod 600 credenciales.smb

> [root@loadbalancer ~]# vim /etc/fstab

> //192.168.0.201/tesoreria  /mnt/t1  cifs credentials=/root/credenciales.smb 0 0

> [root@loadbalancer ~]# udevadm settle

> [root@loadbalancer ~]# systemctl daemon-reload

> [root@loadbalancer ~]# mount -a

To verify conectivity with the server 192.168.0.201 run the following:

> [root@loadbalancer ~]# df -hT

> Filesystem                Type      Size  Used

> --- salida omitida ---

> //192.168.0.201/tesoreria cifs       44G  5.1G   39G  12% /mnt/t1

> RED HAT LINUX AS A WINDOWS SERVER MEMBER DOMAIN

From RHEL 8 the tools are provided to generate an integration with Microsoft Windows Server and its Active Directory; having this integration allows to offer domain users some of the following features:

> •  Authenticate domain users to local services, such as sshd

> •  Share directories and printers hosted on the Linux server so that domain users can access these resources.

However, before enjoying these privileges, it is necessary to introduce the RHEL server into the Windows Server domain, the procedure begins by declaring the update of the cryptographic policies, as shown below:

> [root@loadbalancer ~]# update-crypto-policies --set DEFAULT:AD-SUPPORT

> Setting system policy to DEFAULT:AD-SUPPORT

> Note: System-wide crypto policies are applied on application start-up.

> It is recommended to restart the system for the change of policies

> to fully take place.

This update requests a "reboot" of the system:

> [root@loadbalancer ~]# systemctl reboot

It is necessary to install some applications, as follows:

> [root@loadbalancer ~]# yum install realmd oddjob-mkhomedir oddjob samba-winbind-clients samba-winbind samba-common-tools samba-winbind-krb5-locator

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:59:36 ago on Wed 24 Mar 2021 04:33:08 PM -05.

> Package realmd-0.16.3-19.el8.x86_64 is already installed.

> Package oddjob-mkhomedir-0.34.5-3.el8.x86_64 is already installed.

> Package oddjob-0.34.5-3.el8.x86_64 is already installed.

> Dependencies resolved.

> ========================================================================

> Package                          Architecture Version                  Repository                           Size

> ========================================================================

> Installing:

> samba-common-tools               x86_64       4.12.3-14.el8_3          rhel-8-for-x86_64-baseos-rpms       484 k

> samba-winbind                    x86_64       4.12.3-14.el8_3          rhel-8-for-x86_64-baseos-rpms       567 k

> samba-winbind-clients            x86_64       4.12.3-14.el8_3          rhel-8-for-x86_64-baseos-rpms       149 k

> samba-winbind-krb5-locator       x86_64       4.12.3-14.el8_3          rhel-8-for-x86_64-baseos-rpms        95 k

> Installing dependencies:

> samba-libs                       x86_64       4.12.3-14.el8_3          rhel-8-for-x86_64-baseos-rpms       188 k

> samba-winbind-modules            x86_64       4.12.3-14.el8_3          rhel-8-for-x86_64-baseos-rpms       124 k

> Transaction Summary

> ==================================================================================================================

> Install  6 Packages

> Total download size: 1.6 M

> Installed size: 3.4 M

> Is this ok [y/N]: y

> Installed:

> samba-common-tools-4.12.3-14.el8_3.x86_64                  samba-libs-4.12.3-14.el8_3.x86_64

> samba-winbind-4.12.3-14.el8_3.x86_64                       samba-winbind-clients-4.12.3-14.el8_3.x86_64

> samba-winbind-krb5-locator-4.12.3-14.el8_3.x86_64          samba-winbind-modules-4.12.3-14.el8_3.x86_64

You need to install Samba to perform the integration:

[root@loadbalancer ~]# yum install samba

> Updating Subscription Management repositories.

> Last metadata expiration check: 1:01:28 ago on Wed 24 Mar 2021 04:33:08 PM -05.

> Dependencies resolved.

> ================================================================================================

> Package           Architecture       Version                     Repository                                 Size

> ================================================================================================

> Installing:

> samba             x86_64             4.12.3-14.el8_3             rhel-8-for-x86_64-baseos-rpms             840 k

> Transaction Summary

> ================================================================================================

> Install  1 Package

> Total download size: 840 k

> Installed size: 2.5 M

> Is this ok [y/N]: y

> Downloading Packages:

> samba-4.12.3-14.el8_3.x86_64.rpm                                                  602 kB/s | 840 kB     00:01

> ------------------------------------------------------------------------------------------------------------------

> Total                                                                             602 kB/s | 840 kB     00:01

> Running transaction check

> Transaction check succeeded.

> Running transaction test

> Transaction test succeeded.

> Running transaction

> Preparing        :                                                                                          1/1

> Installing       : samba-4.12.3-14.el8_3.x86_64                                                             1/1

> Running scriptlet: samba-4.12.3-14.el8_3.x86_64                                                             1/1

> Verifying        : samba-4.12.3-14.el8_3.x86_64                                                             1/1

> Installed products updated.

> Installed:

> samba-4.12.3-14.el8_3.x86_64

> Complete!

With the installation of the packages carried out, we proceed to rename the Samba configuration file, at the time of integration a new configuration file is generated:

> [root@loadbalancer ~]# cd /etc/samba/

> [root@loadbalancer samba]# ll

> total 20

> -rw-r--r--. 1 root root    20 Dec  4 13:04 lmhosts

> -rw-r--r--. 1 root root   706 Dec  4 13:04 smb.conf

> -rw-r--r--. 1 root root 11327 Dec  4 13:04 smb.conf.example

> [root@loadbalancer samba]# mv smb.conf smb.conf.original

> [root@loadbalancer samba]# ll

> total 20

> -rw-r--r--. 1 root root    20 Dec  4 13:04 lmhosts

> -rw-r--r--. 1 root root 11327 Dec  4 13:04 smb.conf.example

> -rw-r--r--. 1 root root   706 Dec  4 13:04 smb.conf.original

Before integrating the RHEL server to the domain, it is verified by different methods that the Linux server can reach the Microsoft Active Directory server:

> [root@loadbalancer samba]# ping ad1.aptivalabs.net

> PING ad1.aptivalabs.net (192.168.1.200) 56(84) bytes of data.

> 64 bytes from ad1.aptivalabs.net (192.168.1.200): icmp_seq=1 ttl=128 time=0.809 ms

> 64 bytes from ad1.aptivalabs.net (192.168.1.200): icmp_seq=2 ttl=128 time=0.815 ms

> 64 bytes from ad1.aptivalabs.net (192.168.1.200): icmp_seq=3 ttl=128 time=0.777 ms

> ^C

> --- ad1.aptivalabs.net ping statistics ---

> 3 packets transmitted, 3 received, 0% packet loss, time 4ms

> rtt min/avg/max/mdev = 0.777/0.800/0.815/0.028 ms

> [root@loadbalancer samba]# nslookup ad1.aptivalabs.net

> Server: ​ ​ 192.168.1.200

> Address: ​ 192.168.1.200#53

> Name: ​ ad1.aptivalabs.net

> Address: 192.168.1.200

We register the RHEL server within the Windows Server domain:

> [root@loadbalancer samba]# realm join --membership-software=samba --client-software=winbind ad1.aptivalabs.net

> Password for Administrator:

Once the domain has been entered, the status of the "winbind" service is reviewed and it is relaunched, taking advantage of it to activate it at startup of the operating system:

> [root@loadbalancer samba]# systemctl status winbind

> ● winbind.service - Samba Winbind Daemon

> Loaded: loaded (/usr/lib/systemd/system/winbind.service; enabled; vendor preset: disabled)

> Active: active (running) since Wed 2021-03-24 17:43:44 -05; 43s ago

> Docs: man:winbindd(8)

> man:samba(7)

> man:smb.conf(5)

> Main PID: 9302 (winbindd)

> Status: "winbindd: ready to serve connections..."

> Tasks: 4 (limit: 186419)

> Memory: 10.8M

> CGroup: /system.slice/winbind.service

> ├─9302 /usr/sbin/winbindd --foreground --no-process-group

> ├─9307 /usr/sbin/winbindd --foreground --no-process-group

> ├─9365 /usr/sbin/winbindd --foreground --no-process-group

> └─9367 /usr/sbin/winbindd --foreground --no-process-group

> [root@loadbalancer samba]# systemctl enable winbind --now

Already as a member of the domain we list the integration parameters:

> [root@loadbalancer ~]# realm list

> aptivalabs.net

> type: kerberos

> realm-name: APTIVALABS.NET

> domain-name: aptivalabs.net

> configured: kerberos-member

> server-software: active-directory

> client-software: winbind

> required-package: oddjob-mkhomedir

> required-package: oddjob

> required-package: samba-winbind-clients

> required-package: samba-winbind

> required-package: samba-common-tools

> login-formats: APTIVALABS\%U

> login-policy: allow-any-login

To verify established connectivity, it is time to list users and groups in Microsoft Active Directory, as shown below:

> [root@loadbalancer samba]# wbinfo -u

> APTIVALABS\administrator

> APTIVALABS\guest

> APTIVALABS\krbtgt

The groups defined in Windows Server are listed:

> [root@loadbalancer samba]# wbinfo -g

> APTIVALABS\domain computers

> APTIVALABS\domain controllers

> APTIVALABS\schema admins

> APTIVALABS\enterprise admins

> APTIVALABS\cert publishers

> APTIVALABS\domain admins

> APTIVALABS\domain users

> APTIVALABS\domain guests

> APTIVALABS\group policy creator owners

> APTIVALABS\ras and ias servers

> APTIVALABS\allowed rodc password replication group

> APTIVALABS\denied rodc password replication group

> APTIVALABS\read-only domain controllers

> APTIVALABS\enterprise read-only domain controllers

> APTIVALABS\cloneable domain controllers

> APTIVALABS\protected users

> APTIVALABS\key admins

> APTIVALABS\enterprise key admins

> APTIVALABS\dnsadmins

> APTIVALABS\dnsupdateproxy

> APTIVALABS\dhcp users

> APTIVALABS\dhcp administrators

In the following way it is possible to know the identity of Windows Server users, it could even be registered in the system with the user "Administrator", as shown:

> [root@loadbalancer samba]# getent passwd "ad1\Administrator"

> AD1\administrator:*:10000:10000::/home/administrator@AD1:/bin/bash

> [root@loadbalancer samba]# su - "ad1\Administrator"

> Creating home directory for AD1\administrator.

> [AD1\administrator@loadbalancer ~]$ id

> uid=10000(AD1\administrator) gid=10000(AD1\none) groups=10000(AD1\none) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

> [AD1\administrator@loadbalancer ~]$ exit

Within Microsoft Active Directory, the user “jarus” is created to verify that it can be listed on the Linux server, as shown below:

> [root@loadbalancer samba]# wbinfo -u

> APTIVALABS\administrator

> APTIVALABS\guest

> APTIVALABS\krbtgt

> APTIVALABS\jarus

We take the opportunity to learn a little more about the identity of this user and register with within the Linux system:

> [root@loadbalancer samba]# getent passwd "APTIVALABS\jarus"

> APTIVALABS\jarus:*:2001106:2000513::/home/jarus@APTIVALABS:/bin/bash

> [root@loadbalancer samba]# su - "APTIVALABS\jarus"

> Creating home directory for APTIVALABS\jarus.

> [APTIVALABS\jarus@loadbalancer ~]$

> [APTIVALABS\jarus@loadbalancer ~]$ id

> uid=2001106(APTIVALABS\jarus) gid=2000513(APTIVALABS\domain users) groups=2000513(APTIVALABS\domain users),2001106(APTIVALABS\jarus) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

> [APTIVALABS\jarus@loadbalancer ~]$ exit

Finally, in the folder "/ root" we find a file called "credentials.smb" to which the permissions will be established so that users and groups created in Microsoft Windows Server can act on it, as evidenced:

> [root@loadbalancer ~]# ll

> total 12

> -rw-------. 1 root root   28 Mar 24 16:35 credenciales.smb

> [root@loadbalancer ~]# chown "APTIVALABS\Administrator":"APTIVALABS\Domain Users" /root/credenciales.smb

> [root@loadbalancer ~]# ll

> total 12

> -rw-------. 1 APTIVALABS\administrator APTIVALABS\domain users   28 Mar 24 16:35 credenciales.smb

> POSTFIX AND GMAIL RELAY IN RED HAT LINUX

On many occasions it is necessary for a Linux server to be able to notify the events that occur in the system through e-mail; Some companies have purchased the Gmail console with their business email account manager and prefer to use this service to send notifications from their servers. This exercise explains how to use a local mail service (Postfix) so that in its Gmail integration, Linux servers can send email safely.

The procedure begins with the installation of the necessary applications to achieve the objective: Postfix, the cyrus-sasl tools and the “mailx” application:

> [root@sr1 ~]# yum install postfix -y

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:04:26 ago on Thu 25 Mar 2021 11:59:53 AM EDT.

> Dependencies resolved.

> ========================================================================

> Package              Architecture        Version                           Repository                                  Size

> ========================================================================

> Installing:

> postfix              x86_64              2:3.3.1-12.el8_3.1                rhel-8-for-x86_64-baseos-rpms              1.5 M

> postfix-2:3.3.1-12.el8_3.1.x86_64

> Complete!

When Postfix was installed, the folder with the service configuration files (including main.cf, the Postfix configuration file) was created, as shown below:

> [root@sr1 ~]# cd /etc/postfix/

> [root@sr1 postfix]# ll

> total 216

> -rw-r--r--. 1 root root 29374 Jan 26 10:39 main.cf

Next, the Cyrus-SASL tools are installed, which is an implementation of SASL that makes it easier for application developers to integrate authentication mechanisms in their applications:

> [root@sr1 postfix]# yum install  cyrus-sasl-* -y

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:08:43 ago on Thu 25 Mar 2021 11:59:53 AM EDT.

The client is installed for sending emails and validation of the configuration:

> [root@sr1 postfix]# yum install mailx -y

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:29:03 ago on Thu 25 Mar 2021 11:59:53 AM EDT.

It is time to define the credentials that Postfix will use to authenticate with Gmail, this communication is encrypted but it is necessary to define the credentials (you must have the application password generated in the Google Account platform) in a text file from which Postfix will generate a table search, as shown below:

> [root@sr1 postfix]# vim sasl_passwd

> [smtp.gmail.com]:587 username@gmail.com: **aplicationpassword**

> [root@sr1 postfix]# chmod 600 /etc/postfix/sasl_passwd

> [root@sr1 postfix]# postmap hash:/etc/postfix/sasl_passwd

This lookup table is captured in the file generated by the "postmap" command, as shown:

> [root@sr2 postfix]# ll sasl_passwd.db

> -rw-------. 1 root root 12288 Mar 25 13:46 sasl_passwd.db

It is important to note that the " **aplicationpassword** " field is part of the Gmail security mechanisms; Do not define your Gmail password in this field, but rather the application password, which must be generated in the Google Account platform, as related below:

![](Image00035.jpg) 

It is necessary to configure the TLS encryption as a policy, for that the file "tls_policy" is created and registered in the Postfix lookup table:

> [root@sr1 postfix]# vim tls_policy

> [smtp.gmail.com]:587 encrypt

> [root@sr1 postfix]# postmap /etc/postfix/tls_policy

It is time to edit the Postfix configuration file which is “main.cf”, however for backup reasons a copy of the original file is made:

> [root@sr1 postfix]# cp main.cf main.cf.original

Editing "main.cf" validate that the following lines are related as indicated below:

> [root@sr1 postfix]# vim main.cf

> #smtpd_tls_cert_file = /etc/pki/tls/certs/postfix.pem

> #smtpd_tls_key_file = /etc/pki/tls/private/postfix.key

> #smtpd_tls_security_level = may

> smtp_tls_CApath = /etc/pki/tls/certs

> smtp_tls_CAfile = /etc/pki/tls/certs/ca-bundle.crt

> #smtp_tls_security_level = may

> meta_directory = /etc/postfix

> shlib_directory = /usr/lib64/postfix

> relayhost = [smtp.gmail.com]:587

> smtp_use_tls = yes

> smtp_sasl_auth_enable = yes

> smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd

> smtp_sasl_security_options = noanonymous

> smtp_sasl_tls_security_options = noanonymous

> smtp_tls_policy_maps = hash:/etc/postfix/tls_policy

It is time to restart the "postfix" service and validate the functionality:

> [root@sr2 postfix]# systemctl restart postfix.service

> [root@sr2 postfix]# echo mailtest | mail -s mailtest fmestre@aptivalabs.com

In a second console you will be able to validate that the emails are going out effectively until smtp.gmail.com:587, as shown:

> [root@sr1 ~]# tail -f /var/log/maillog

> Mar 25 13:15:42 sr1 postfix/pickup[8203]: 656C620AACA7: uid=0 from=<root>

> Mar 25 13:15:42 sr1 postfix/cleanup[8209]: 656C620AACA7: message-id=<20210325171542.656C620AACA7@sr1.aptivalabs.net>

> Mar 25 13:15:42 sr1 postfix/qmgr[8204]: 656C620AACA7: from=<root@sr1.aptivalabs.net>, size=449, nrcpt=1 (queue active)

> Mar 25 13:15:44 sr1 postfix/smtp[8211]: 656C620AACA7: to=<fmestre@aptivalabs.com>, relay=smtp.gmail.com[108.177.11.109]:587, delay=2.1, delays=0.03/0.05/0.9/1.1, dsn=2.0.0, status=sent ( **250** 2.0.0 OK  1616692544 70sm726442uas.9 - gsmtp)

> Mar 25 13:15:44 sr1 postfix/qmgr[8204]: 656C620AACA7: removed

Within the communication rules of the SMTP protocol, code 250 indicates that the mail has been sent satisfactorily.

> INTEGRATION BEETWEEN RED HAT LINUX AND AMAZON WEB SERVICES S3

An interesting functionality for those who are combining On-Premise environments with Public Cloud services, especially with the storage services that are available in those clouds, is to be able to carry out a local assembly and through it place the data that is required in the storage service.

This time the Amazon Web Services S3 storage service will be used as a service to host the data generated on a RHEL 8 server, this is interesting for example to save in AWS S3 through a crontab the daily backups generated by applications or dumps made on databases, actually what you need to save, in addition to taking advantage of the functionalities of this storage service such as the life cycle of the data for cost optimization, etc.

The exercise to be developed below shows us an object (bucket) in AWS S3 called "aptiva" in which data of any type can be stored; what will be executed in this procedure is that a RHEL server can save information in that bucket through the definition of a local mount point. The following image shows us the AWS S3 bucket called "aptiva":

![](Image00036.jpg) 

To install the package that will allow us to mount the AWS S3 bucket on the Linux server, it is necessary to install an additional repository since this application is not part of the group of packages supported by Red Hat. This repository is called EPEL.

The EPEL 8 installation is performed, as shown:

> [root@sr2 ~]# yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

> Updating Subscription Management repositories.

> Last metadata expiration check: 1:59:33 ago on Thu 25 Mar 2021 01:41:29 PM EDT.

> epel-release-latest-8.noarch.rpm                                                              54 kB/s |  22 kB     00:00

> Dependencies resolved.

> =========================================================================

> Package                         Architecture              Version                     Repository                       Size

> =========================================================================

> Installing:

> epel-release                    noarch                    8-10.el8                    @commandline                     22 k

> Transaction Summary

> =========================================================================

> Install  1 Package

> Total size: 22 k

> Installed size: 32 k

> Is this ok [y/N]: y

Once the EPEL repository has been deployed, it is time to install the application "s3fs" as shown below:

> [root@sr2 ~]# yum install s3fs-fuse

> Updating Subscription Management repositories.

> Extra Packages for Enterprise Linux Modular 8 - x86_64                                       226 kB/s | 557 kB     00:02

> Extra Packages for Enterprise Linux 8 - x86_64                                               1.6 MB/s | 9.1 MB     00:05

> Last metadata expiration check: 0:00:01 ago on Thu 25 Mar 2021 03:41:32 PM EDT.

> Dependencies resolved.

> =========================================================================

> Package                        Architecture                Version                          Repository                 Size

> =========================================================================

> Installing:

> s3fs-fuse                      x86_64                      1.89-1.el8                       epel                      344 k

> Transaction Summary

> =========================================================================

> Install  1 Package

> Total download size: 344 k

> Installed size: 908 k

> Is this ok [y/N]: y

AWS through the identity management service allows you to generate the access credentials to register with AWS and be able to use its services. For the development of this exercise, a test credential is used which must be saved in the file "/etc/passwd-s3fs" in the format described below:

> [root@sr2 s3fs-fuse]# echo "AKIA2IXLZ7Q4EDGEEC73:W0c/PWvHbn8liNj2BNN869JhdvPaRtXj8SSsmm1J" > /etc/passwd-s3fs

We verify the creation of the file:

> [root@sr2 s3fs-fuse]# ll /etc/passwd-s3fs

> -rw-r--r--. 1 root root 62 Mar 25 15:22 /etc/passwd-s3fs

> [root@sr2 s3fs-fuse]# cat /etc/passwd-s3fs

> AKIA2IXLZ7Q4EDGEEC73:W0c/PWvHbn8liNj2BNN869JhdvPaRtXj8SSsmm1J

You need to set read and write permissions to the owner of the file:

> [root@sr2 s3fs-fuse]# chmod 600 /etc/passwd-s3fs

The mount point through which the AWS S3 bucket will be accessed is created:

> [root@sr2 s3fs-fuse]# mkdir /mnt/aptiva

The persistent mount of the bucket is defined in "/etc/fstab" and verified, as shown below:

> [root@sr2 s3fs-fuse]# echo "s3fs#aptiva /mnt/aptiva fuse _netdev,rw,nosuid,nodev,allow_other,nonempty 0 0" >> /etc/fstab

> [root@sr2 s3fs-fuse]# cat /etc/fstab

> #

> # /etc/fstab

> # Created by anaconda on Thu Mar 18 14:56:05 2021

> **s3fs#aptiva /mnt/aptiva fuse _netdev,rw,nosuid,nodev,allow_other,nonempty 0 0**

Then the activities for the assembly are carried out:

> [root@sr2 s3fs-fuse]# udevadm settle

> [root@sr2 s3fs-fuse]# systemctl daemon-reload

> [root@sr1 ~]# mount -a

Once the assembly is done, it is verified with the following instruction:

> [root@sr1 ~]# df -hT

> Filesystem            Type       Size  Used Avail Use% Mounted on

> --- salida omitida ---

> s3fs                  fuse.s3fs **256T     0  256T**   0% /mnt/aptiva

With the previous instruction it can be detailed that the mount point has been defined in / mnt / aptiva with an availability of 256T of storage; At this time, as a Linux Administrator, you will be able to place data in that mounting point, taking into account the quality and speed of the information transfer is defined by the Internet connection that you have contracted with your service provider. A look at the contents of the S3 bucket is as follows:

> [root@sr1 ~]# ll /mnt/aptiva/

> total 1581057

> -rw-r--r--. 1 root root          0 Feb 19  2020 1

> -rw-r--r--. 1 root root     136882 Feb 19  2020 archivo.tar

> -rw-r-----. 1 root root      11894 Feb 19  2020 synologic.jpg

To end the exercise, the “tests” folder will be created within the mounting point and empty files will be created from the command line interface, the objective of this is to verify that the data is actually being saved in the S3 bucket, as shown detailed below:

> [root@sr1 ~]# cd /mnt/aptiva/

> [root@sr1 aptiva]# mkdir pruebas

> [root@sr1 aptiva]# cd pruebas/

> [root@sr1 pruebas]# touch 1 2 3 4 5 6

Presenting a screenshot of the AWS web administration console, we can verify that the practice has been satisfactory when seeing the same data in the two scenarios:

![](Image00037.jpg) 

> POSTGRESQL – INSTALATION AND DEPLOYMENT

It is recurrent in the corporate scenario to find information systems deployed on application servers that perform transactions on local databases, in this case databases installed and configured on RHEL 8 or some derived system. In this exercise, the PostgreSQL version 10 database engine will be deployed, which is the default stream since there is the option to install version 9.6 or 12.

We start by changing the hostname:

> [root@loadbalancer ~]# hostnamectl set-hostname bd1.aptivalabs.net

> [root@loadbalancer ~]# exit

> logout

> $ ssh -l root 192.168.0.200

> [root@bd1 ~]#

The different streams of the PostgreSQL module are listed:

> [root@bd1 ~]# yum module list postgresql

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:06:02 ago on Fri 26 Mar 2021 09:31:55 AM -05.

> Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)

> Name                     Stream              Profiles                        Summary

> postgresql               9.6                 client, server [d]              PostgreSQL server and client module

> postgresql               10 [d]              client, server [d]              PostgreSQL server and client module

> postgresql               12                  client, server [d]              PostgreSQL server and client module

> Hint: [d]efault, [e]nabled, [x]disabled, [i]nstalled

It is verified if the stream "postgresql: 10" has "profiles" that specify the installation:

> [root@bd1 ~]# yum module info postgresql:10 --profile

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:06:33 ago on Fri 26 Mar 2021 09:31:55 AM -05.

> Name   : postgresql:10:8020020200825115746:4cda2c84:x86_64

> client : postgresql

> server : postgresql-server

Defined the preference to install the stream "postgresql: 10", we proceed to install PostgreSQL in that version:

> [root@bd1 ~]# yum install postgresql-server

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:07:24 ago on Fri 26 Mar 2021 09:31:55 AM -05.

> Dependencies resolved.

> Installed:

> libpq-12.5-1.el8_3.x86_64                                        postgresql-10.15-1.module+el8.3.0+8944+1ca16b1f.x86_64

> postgresql-server-10.15-1.module+el8.3.0+8944+1ca16b1f.x86_64

> Complete!

The next step is to initialize the database, start the service and activate the database engine startup at startup, as shown below:

> [root@bd1 ~]# postgresql-setup --initdb

> * Initializing database in '/var/lib/pgsql/data'

> * Initialized, logs are in /var/lib/pgsql/initdb_postgresql.log

> [root@bd1 ~]# systemctl enable postgresql.service --now

> Created symlink /etc/systemd/system/multi-user.target.wants/postgresql.service → /usr/lib/systemd/system/postgresql.service.

The system processes are verified to validate that the service is running:

> [root@bd1 ~]# ps -fe

> UID          PID    PPID  C STIME TTY          TIME CMD

> --- salida omitida ---

> postgres    5973       1  0 09:41 ?        00:00:00 /usr/bin/postmaster -D /var/lib/pgsql/data

> postgres    5974    5973  0 09:41 ?        00:00:00 postgres: logger process

> postgres    5976    5973  0 09:41 ?        00:00:00 postgres: checkpointer process

> postgres    5977    5973  0 09:41 ?        00:00:00 postgres: writer process

> postgres    5978    5973  0 09:41 ?        00:00:00 postgres: wal writer process

> postgres    5979    5973  0 09:41 ?        00:00:00 postgres: autovacuum launcher process

> postgres    5980    5973  0 09:41 ?        00:00:00 postgres: stats collector process

> postgres    5981    5973  0 09:41 ?        00:00:00 postgres: bgworker: logical replication launcher

FirewallD rules are set to receive connections to the database engine:

> [root@bd1 ~]# firewall-cmd --add-service=postgresql --permanent

> success

> [root@bd1 ~]# firewall-cmd --reload

> success

Before putting the database into production we verify that in a possible system boot the database engine starts with the operating system:

> [root@bd1 ~]# systemctl reboot

> [root@bd1 ~]# systemctl status postgresql.service

> ● postgresql.service - PostgreSQL database server

> Loaded: loaded (/usr/lib/systemd/system/postgresql.service; enabled; vendor preset: disabled)

> Active: active (running) since Fri 2021-03-26 09:43:18 -05; 33s ago

It is validated that the user "postgres" which is the superuser can access the service, as shown below:

> [root@bd1 ~]# su - postgres

> [postgres@bd1 ~]$ psql

> psql (10.15)

> Type "help" for help.

> postgres=# \q

> [postgres@bd1 ~]$ exit

> logout

POSTGRESQL – NEW DATABASE AND DUMP

Taking advantage of the previously generated deployment, a test database will be created and a backup will be made for verification purposes, bearing in mind that this procedure will be carried out with the super user of the database, as shown below:

> [root@bd1 ~]# su - postgres

> Last login: Fri Mar 26 09:44:24 -05 2021 on pts/0

A new database called "test" is created:

> [postgres@bd1 ~]$ createdb test

We enter the PostgreSQL CLI, exactly to the database that has just been created:

> [postgres@bd1 ~]$ psql test

> psql (10.15)

> Type "help" for help.

The following instruction creates the table "users" and its respective structure, then we will list this structure of the catalog:

> test=# create table usuarios ( nombre varchar(30), clave varchar(10) );

> CREATE TABLE

> test=# select table_name,column_name,udt_name,character_maximum_length from information_schema.columns where table_name = 'usuarios';

> table_name | column_name | udt_name | character_maximum_length

> ------------+-------------+----------+--------------------------

> usuarios   | nombre      | varchar  |                       30

> usuarios   | clave       | varchar  |                       10

> (2 rows)

The following instructions will insert records in the database and then list them:

> test=# insert into usuarios (nombre, clave) values ('Mariano','payaso');

> INSERT 0 1

> test=# insert into usuarios (nombre, clave) values ('Pablo','jfx344');

> INSERT 0 1

> test=# insert into usuarios (nombre, clave) values ('Ana','tru3fal');

> INSERT 0 1

> test=# select * from usuarios;

> nombre  |  clave

> ---------+---------

> Mariano | payaso

> Pablo   | jfx344

> Ana     | tru3fal

> (3 rows)

It is necessary to exit the PostgreSQL CLI:

> test=# \q

A dump of the database is generated below and the contents of the file are listed:

> [postgres@bd1 ~]$ pg_dump test > /tmp/backup.sql

> [postgres@bd1 ~]$ cat /tmp/backup.sql

> --

> -- PostgreSQL database dump

> --

> -- Dumped from database version 10.15

> -- Dumped by pg_dump version 10.15

> SET statement_timeout = 0;

> SET lock_timeout = 0;

> --- omited ---

DATABASE RESTORATION EXERCISE

A common activity in PostgreSQL database administration is restoring a large database, an activity that could take hours to implement. In the following exercise, a backup made at the dump level will be restored, which has a size of 1.56; To carry out this activity, a new database will be created in which the dump will be restored, as shown below:

> [postgres@bd1 ~]$ ll -h /tmp/BD-historico20180828.sql

> -rw-r--r--. 1 root root 1.6G Mar 26 10:45 /tmp/BD-historico20180828.sql

The database called "empresa" is created:

> [postgres@bd1 ~]$ createdb empresa

The restoration process is launched in the "empresa" database of the previously generated dump:

> [postgres@bd1 ~]$ pg_restore -d empresa /tmp/BD-historico20180828.sql

Once the restoration is complete, it is verified that the tables have been created, as shown below:

> [postgres@bd1 ~]$ psql empresa

> psql (10.15)

> Type "help" for help.

> empresa=# \d

> List of relations

> Schema |          Name          |   Type   |  Owner

> --------+------------------------+----------+----------

> public | cartera ​ ​ | table    | postgres

> public | ciudades ​ ​ | table    | postgres

> public | departamentos ​ ​ | table    | postgres

> public | barrios ​ ​ | table    | postgres

> --- omited ---

METADATA QUERY IN POSTGRESQL

Once the restoration has been carried out, it is possible to ask the database engine for information related to the spaces occupied in it, as is done in the following instruction where it asks for the sizes of all the databases in the engine:

> empresa=# SELECT pg_database.datname, pg_size_pretty(pg_database_size(pg_database.datname)) AS SIZE FROM pg_database;

> datname  |  size

> -----------+---------

> postgres ​ | 7335 kB

> test ​ | 7343 kB

> template1 ​ | 7201 kB

> template0 ​ | 7201 kB

> empresa ​ | 15 GB

As follows, the size of a specific database is queried:

> empresa=# SELECT pg_size_pretty( pg_database_size('empresa') );

> pg_size_pretty

> ----------------

> 15 GB

> (1 row)

In the following way we can see the size of the tables in a database:

> empresa=# SELECT  schemaname, tablename,pg_size_pretty(pg_total_relation_size(tablename::regclass::oid))

> FROM    pg_tables

> WHERE   schemaname NOT IN('pg_catalog', 'information_schema')

> ;

> schemaname |       tablename        | pg_size_pretty

> ------------+------------------------+----------------

> public     | cartera ​ ​ | 357 MB

> public     | ciudades ​ ​ | 240 kB

> public     | departamentos ​ ​ | 608 kB

> public     | barrios ​ ​ | 96 kB

INSTALLING POSTGRESQL IN A SECUNDARY FILESYSTEM

In the following exercise PostgreSQL will be installed using a different path for data storage, the default path for creating the PostgreSQL cluster is /var/lib/pgsql data, the path that will be used in this exercise is /pgsql-data; For the development of this practice, a new disk (it will appear as /dev/sdb) is added to the system which is taken to an LV formatted with XFS and established on the /pgsql-data mount point; such preparation is carried out as follows:

The 100GB disk that will be taken to the LVM2 structure is identified, as shown in the following instructions:

> [root@bd2 ~]# lsblk

> NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT

> --- salida omitida ---

> sdb             8:16   0  100G  0 disk

> [root@bd2 ~]# pvcreate /dev/sdb

> Physical volume "/dev/sdb" successfully created.

> [root@bd2 ~]# vgcreate datos /dev/sdb

> Volume group "datos" successfully created

> [root@bd2 ~]# lvcreate -l 100%free -n bd2 datos

> Logical volume "bd2" created.

> [root@bd2 ~]# lvs

> LV   VG    Attr       LSize    Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert

> bd2  datos -wi-a----- <100.00g

> root rhel  -wi-ao----  <44.00g

> swap rhel  -wi-ao----    5.00g

The XFS file system is mapped to the newly created logical device:

> [root@bd2 ~]# mkfs.xfs /dev/datos/bd2

> meta-data=/dev/datos/bd2         isize=512    agcount=4, agsize=6553344 blks

> =                       sectsz=512   attr=2, projid32bit=1

> --- salida omitida ---

“/pgsql-data” is created as the mount point of the previously created file system:

> [root@bd2 ~]# mkdir /pgsql-data

It's time to persistently set the mount point set to host PostgreSQL data:

> [root@bd2 ~]# blkid | grep bd2 >> /etc/fstab

> [root@bd2 ~]# vim /etc/fstab

> UUID="f32b947b-5203-43dd-9751-c81980584207" /pgsql-data xfs defaults 0 0

> [root@bd2 ~]# udevadm settle

> [root@bd2 ~]# systemctl daemon-reload

> [root@bd2 ~]# mount -a

The mount point is verified to be available for database initialization:

> [root@bd2 ~]# df -hT

> Filesystem            Type      Size  Used Avail Use% Mounted on

> --- salida omitida ---

> /dev/mapper/datos-bd2 xfs       100G  746M  100G   1% /pgsql-data

It is necessary to disable the RHEL module that installs PostgreSQL because the installation will be done by adding the official repository of the PostgreSQL developers:

> [root@bd2 ~]# yum module disable postgresql

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:19:53 ago on Fri 26 Mar 2021 01:07:38 PM EDT.

> --- omited ---

> The official repository of the PostgreSQL developers is installed:

> [root@bd2 ~]# yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:20:55 ago on Fri 26 Mar 2021 01:07:38 PM EDT.

> pgdg-redhat-repo-latest.noarch.rpm                                                           1.2 kB/s | 6.8 kB     00:05

> Dependencies resolved.

> =========================================================================

> Package                            Architecture             Version                    Repository                      Size

> =========================================================================

> Installing:

> pgdg-redhat-repo                   noarch                   42.0-14                    @commandline                   6.8 k

The new system repository is displayed in “/etc/yum.repos.d/”; moving to this path edits such repository file to only enable the PostgreSQL version 10 repo.

> [root@bd2 ~]# cd /etc/yum.repos.d/

> [root@bd2 yum.repos.d]# ll

> total 104

> -rw-r--r--. 1 root root  9738 Sep 24  2020 pgdg-redhat-all.repo

> -rw-r--r--. 1 root root 94154 Mar 26 13:05 redhat.repo

In the edition of the repository file "pgdg-redhat-all.repo" it is necessary to carry the field "enabled = 0" for those repositories of versions 12, 11 and 9.6 of PostgreSQL, only the repository of version 10 must have " enabled = 1 "; It shows how the repos should not be used:

> [root@bd2 yum.repos.d]# vim pgdg-redhat-all.repo

> [pgdg12]

> name=PostgreSQL 12 for RHEL/CentOS $releasever - $basearch

> baseurl=https://download.postgresql.org/pub/repos/yum/12/redhat/rhel-$releasever-$basearch

> enabled=0

> gpgcheck=1

> gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-PGDG

It is time to install PostgreSQL, as detailed below:

> [root@bd2 yum.repos.d]# yum install -y postgresql10-server postgresql10-contrib

> Updating Subscription Management repositories.

> PostgreSQL common RPMs for RHEL/CentOS 8 - x86_64                                            172 kB/s | 461 kB     00:02

> PostgreSQL 10 for RHEL/CentOS 8 - x86_64                                                     201 kB/s | 448 kB     00:02

> PostgreSQL 9.5 for RHEL/CentOS 8 - x86_64                                                    223 kB/s | 384 kB     00:01

> Dependencies resolved.

> =====================================================================================================

> Package                              Architecture           Version                            Repository              Size

> =====================================================================================================

> Installing:

> postgresql10-contrib                 x86_64                 10.16-1PGDG.rhel8                  pgdg10                 619 k

> postgresql10-server                  x86_64                 10.16-1PGDG.rhel8                  pgdg10                 4.7 M

> Installing dependencies:

> postgresql10                         x86_64                 10.16-1PGDG.rhel8                  pgdg10                 1.6 M

> postgresql10-libs                    x86_64                 10.16-1PGDG.rhel8                  pgdg10                 384 k

Before initializing the database, it is necessary to assign the permissions to the folder to host the data:

> [root@bd2 ~]# chown postgres:postgres /pgsql-data

PostgreSQL is initialized observing a “failed” message in the activity, however this is related to the default path which will not be used:

> [root@bd2 ~]# sudo PGSETUP_INITDB_OPTIONS="-D /pgsql-data/" /usr/pgsql-10/bin/postgresql-10-setup initdb

> Initializing database ... failed, see /var/lib/pgsql/10/initdb.log

Taking a look at the cluster creation log we can see the details of the initialization:

> [root@bd2 ~]# more /var/lib/pgsql/10/initdb.log

> The files belonging to this database system will be owned by user "postgres".

> This user must also own the server process.

> The database cluster will be initialized with locale "en_US.UTF-8".

> The default database encoding has accordingly been set to "UTF8".

> The default text search configuration will be set to "english".

> Data page checksums are disabled.

> fixing permissions on existing directory /pgsql-data ... ok

> creating subdirectories ... ok

> selecting default max_connections ... 100

> selecting default shared_buffers ... 128MB

> selecting default timezone ... America/New_York

> selecting dynamic shared memory implementation ... posix

> creating configuration files ... ok

> running bootstrap script ... ok

> performing post-bootstrap initialization ... ok

> syncing data to disk ... ok

> Success. You can now start the database server using:

> /usr/pgsql-10/bin/pg_ctl -D /pgsql-data/ -l logfile start

The creation of the cluster leaves us the following content in /pgsql-data:

> [root@bd2 ~]# ll /pgsql-data/

> total 48

> -rw-------. 1 postgres postgres     3 Mar 26 13:35 PG_VERSION

> drwx------. 5 postgres postgres    41 Mar 26 13:35 base

> drwx------. 2 postgres postgres  4096 Mar 26 13:35 global

> drwx------. 2 postgres postgres     6 Mar 26 13:35 pg_commit_ts

> drwx------. 2 postgres postgres     6 Mar 26 13:35 pg_dynshmem

> -rw-------. 1 postgres postgres  4269 Mar 26 13:35 pg_hba.conf

> -rw-------. 1 postgres postgres  1636 Mar 26 13:35 pg_ident.conf

> --- salida omitida ---

The unit "postgresql-10.service" is edited so that the system takes the path /pgsql-data on reboots:

> [root@bd2 ~]# systemctl edit postgresql-10.service

​ [Service]

​ Environment=PGDATA=/pgsql-data/

> [root@bd2 ~]# cat /etc/systemd/system/postgresql-10.service.d/override.conf

> [Service]

> Environment=PGDATA=/pgsql-data/sudo systemctl daemon-reload

> We start PostgreSQL and activate the start of the service at startup of the operating system:

> [root@bd2 ~]# systemctl enable postgresql-10.service --now

> Created symlink /etc/systemd/system/multi-user.target.wants/postgresql-10.service → /usr/lib/systemd/system/postgresql-10.service.

When consulting the status we can see that the "postgresql-10.service" service is active:

> [root@bd2 ~]# systemctl status postgresql-10.service

> ● postgresql-10.service - PostgreSQL 10 database server

> Loaded: loaded (/usr/lib/systemd/system/postgresql-10.service; enabled; vendor preset: disabled)

> Drop-In: /etc/systemd/system/postgresql-10.service.d

> └─override.conf

> **Active: active (running)** since Fri 2021-03-26 13:39:55 EDT; 9s ago

FirewallD is told to accept requests in the default zone:

> [root@bd2 pgsql-data]# firewall-cmd --add-service=postgresql --permanent

> success

> [root@bd2 pgsql-data]# firewall-cmd --reload

> success

It is time to impersonate the user "postgres" and connect to the database:

> [root@bd2 ~]# su - postgres

> [postgres@bd2 ~]$ psql

> psql (10.16)

> Type "help" for help.

> postgres=# \q

> [postgres@bd2 ~]$ exit

> logout

The purpose of rebooting is to validate that when the operating system starts the database engine, it does so successfully with it, as is the case in this exercise:

> [root@bd2 ~]# systemctl reboot

> [root@bd2 ~]# systemctl status postgresql-10.service

> ● postgresql-10.service - PostgreSQL 10 database server

> Loaded: loaded (/usr/lib/systemd/system/postgresql-10.service; enabled; vendor preset: disabled)

> Drop-In: /etc/systemd/system/postgresql-10.service.d

> └─override.conf

> Active: active (running) since Fri 2021-03-26 13:42:30 EDT; 40s ago

> Docs: https://www.postgresql.org/docs/10/static/

> Process: 1013 ExecStartPre=/usr/pgsql-10/bin/postgresql-10-check-db-dir ${PGDATA} (code=exited, status=0/SUCCESS)

> Main PID: 1033 (postmaster)

> Tasks: 8 (limit: 123745)

> Memory: 23.9M

> CGroup: /system.slice/postgresql-10.service

> ├─1033 /usr/pgsql-10/bin/postmaster -D /pgsql-data/

> ├─1045 postgres: logger process

> ├─1047 postgres: checkpointer process

> ├─1048 postgres: writer process

> ├─1049 postgres: wal writer process

> ├─1050 postgres: autovacuum launcher process

> ├─1051 postgres: stats collector process

> └─1052 postgres: bgworker: logical replication launcher

DEFINITION OF ACCESS TO THE DATABASES

In the previous sections, PostgreSQL was installed in various ways, databases were created, dumps were made, a restore was performed, and the database engine was installed using a secondary file system, however, the database data is closed to your customers, which needs to be changed so that the engine can receive requests and perform transactions.

In this sense, we will first check FirewallD to verify that the default zone is allowing the entry of requests, as shown below:

> [root@bd2 pgsql-data]# firewall-cmd --list-all

> public (active)

> target: default

> icmp-block-inversion: no

> interfaces: ens18

> sources:

> services: cockpit dhcpv6-client **postgresql** ssh

> ports:

> protocols:

> masquerade: no

> forward-ports:

> source-ports:

> icmp-blocks:

> rich rules:

In the path where PostgreSQL was initialized (/ pgsql-data) there are the files to configure the database engine; there you will find the files "postgresql.conf" and "pg_hba.conf", the first one manages the general configuration of the database engine and the second one manages the accesses to the databases. To receive requests it is necessary to edit them, as detailed below:

> [root@bd2 pgsql-data]# pwd

> /pgsql-data

> [root@bd2 pgsql-data]# ll postgresql.conf

> -rw-------. 1 postgres postgres 22982 Mar 26 15:41 postgresql.conf

In the postgresql.conf file, the parameters "listen_addresses" and "port = 5432" must be activated:

> [root@bd2 pgsql-data]# vim postgresql.conf

> listen_addresses = '*' ​ ​ # what IP address(es) to listen on;

> port = 5432 ​ ​ ​ # (change requires restart)

Following this, the file "pg_hba.conf" must contain the pertinent authorizations to or to the engine databases:

> [root@bd2 pgsql-data]# ll pg_hba.conf

> -rw-------. 1 postgres postgres 4305 Mar 26 15:38 pg_hba.conf

The specific case observed in the following instruction is a "host" type authorization to all databases governed by PostgreSQL, allowing access to all users but closing the connection to the host 192.168.0.200 through an encrypted method of password entry:

> [root@bd2 pgsql-data]# vim pg_hba.conf

> **# TYPE  DATABASE        USER            ADDRESS                 METHOD**

> ---

> host ​ all ​ ​ all ​ ​ 192.168.0.200/32 ​ md5

After the changes made, it is necessary to restart the "postgresql-10.service" service:

> [root@bd2 pgsql-data]# systemctl restart postgresql-10.service

POSTGRESQL - STREAMING REPLICATION

Streaming Replication (SR) provides the ability to continuously send and apply WAL XLOG logs to a number of standby servers to keep them up to date. This feature was added to PostgreSQL 9.0.

The demonstration exercise is carried out on two servers, the 192.168.0.38 (sr1), which would be the main server, and the server 192.168.0.39 (sr2) which is where the respective replication is taking place.

PostgreSQL is installed and secured on the server "sr1" (the default stream is 10):

> [root@sr1 ~]# yum install postgresql-server

> [root@sr1 ~]# postgresql-setup --initdb

> [root@sr1 ~]# systemctl enable postgresql.service --now

> [root@sr1 ~]# firewall-cmd --add-service=postgresql --permanent

> [root@sr1 ~]# firewall-cmd --reload

> [root@sr1 ~]# reboot

Once the postgresql service startup is installed and verified at system startup, the configuration file is edited, where the following configuration lines should look like this:

> [root@sr1 ~]# vim /var/lib/pgsql/data/postgresql.conf

> ​ listen_addresses = '*'

> ​ wal_level = replica

> ​ synchronous_commit = on

> ​ max_wal_senders = 10

> ​ synchronous_standby_names = '*'

Regarding access to postgresql services, it is necessary to define the replica hosts, as shown at the end of the “pg_hba.conf” file (it should look as shown):

> [root@sr1 ~]# vim /var/lib/pgsql/data/pg_hba.conf

> ​ # host replication [replication user] [allowed network] [authentication method]

> ​ #host    replication     all             127.0.0.1/32            ident

> ​ #host    replication     all             ::1/128                 ident

> ​ host    replication     rep_user        192.168.0.38/32            md5

> ​ host    replication     rep_user        192.168.0.39/32           md5

Next, the user "rep_user" (user for replication) is created with its respective PostgreSQL role defined:

> [root@sr1 ~]# su - postgres

> [postgres@sr1 ~]$ createuser --replication -P rep_user

> Enter password for new role:

> Enter it again:

We exit the postgres user and restart the service:

> [postgres@sr1 ~]$ exit

> logout

> [root@sr1 ~]# systemctl restart postgresql

Next we start the procedures on the “sr2” server, installing and securing the postgresql service:

> [root@sr2 ~]# yum install postgresql-server

> [root@sr2 ~]# postgresql-setup --initdb

> [root@sr2 ~]# systemctl enable postgresql.service --now

> [root@sr2 ~]# firewall-cmd --add-service=postgresql --permanent

> [root@sr2 ~]# firewall-cmd --reload

> [root@sr2 ~]# reboot

Once the postgresql service has been installed, initialized and put into production, we stop it, save the configuration folder and transfer the configuration made on the “sr1” server, as shown below:

> [root@sr2 ~]# systemctl stop postgresql.service

> [root@sr2 ~]# cp -R /var/lib/pgsql/data/ /root/

> [root@sr2 ~]# rm -rf /var/lib/pgsql/data/*

> [root@sr2 ~]# ll /var/lib/pgsql/data/

> total 0

> [root@sr2 ~]# su - postgres

> [postgres@sr2 ~]$ pg_basebackup -R -h 192.168.0.38 -U rep_user -D /var/lib/pgsql/data -P

> Password:

> 22858/22858 kB (100%), 1/1 tablespace

> [postgres@sr2 ~]$ pwd

> /var/lib/pgsql

We can verify the previous steps by listing the content of /var/lib/pgsql again:

> [postgres@sr2 ~]$ ll data/

> total 60

> -rw-------. 1 postgres postgres   206 Jul 27 19:36 backup_label

> drwx------. 5 postgres postgres    41 Jul 27 19:36 base

> -rw-------. 1 postgres postgres    30 Jul 27 19:36 current_logfiles

> --- salida omitida ---

The impersonation of the user “postgres” is terminated:

> [postgres@sr2 ~]$ exit

We start editing the PostgreSQL configuration files, which should be as follows according to our exercise (make sure that the lines with the following variables remain as defined):

> [root@sr2 ~]# vi /var/lib/pgsql/data/postgresql.conf

> ​ listen_addresses = '*'

> ​ hot_standby = on

> [root@sr2 ~]# vi /var/lib/pgsql/data/pg_hba.conf

> ​ # host replication [replication user] [allowed network] [authentication method]

> ​ #host    replication     all             127.0.0.1/32            ident

> ​ #host    replication     all             ::1/128                 ident

> ​ host    replication     rep_user        192.168.0.38/32            md5

> ​ host    replication     rep_user        192.168.0.39/32            md5

Once the files have been modified, it is necessary to start the PostgreSQL service:

> [root@sr2 ~]# systemctl start postgresql

It is time to test the configuration made, trying to create a database and insert some records which should be replicated asynchronously on the “sr2” server, as shown below:

In server “sr1”, a database is created with a table and two records are inserted:

> [root@sr1 ~]# su - postgres

> [postgres@sr1 ~]$ createdb test

> [postgres@sr1 ~]$ psql test

> psql (10.17)

> Type "help" for help.

> test=# create table usuarios ( nombre varchar(30), clave varchar(10) );

> CREATE TABLE

> test=# insert into usuarios (nombre, clave) values ('Mariano','payaso');

> INSERT 0 1

> test=# insert into usuarios (nombre, clave) values ('Sara','Mestre');

> INSERT 0 1

Entering "sr2" we can see if the replication was successful, as shown below:

> [root@sr2 ~]# su - postgres

> [postgres@sr2 ~]$ psql

> psql (10.17)

> Type "help" for help.

> postgres=#

> postgres-# \c test

> test=# select * from usuarios;

> nombre  | clave

> ---------+--------

> Mariano | payaso

> Sara    | Mestre

> (2 rows)

> test=# \q

> RECORDING USERS SESSIONS

The session recording functionality is possible thanks to the “tlog” package which provides the ability to record and reproduce sessions from the user's terminal; "Tlog" provides the ability to perform this recording by user or user groups, storing the standard input and output in a text file. It is important to clarify that the recording is disabled by default so it would intercept sensitive information. This solution is useful for user audits, review of security incidents or any eventuality related to forensic procedures. The key components of the recording solution are the “tlog” application, the SSSD service and the Cockpit. The procedure starts with the installation of the “tlog” and “cockpit-session-recording” applications:

> [root@bd2 ~]# yum install tlog

> Updating Subscription Management repositories.

> Last metadata expiration check: 3:09:12 ago on Fri 26 Mar 2021 01:32:39 PM EDT.

> --- salida omitida ---

> Installed:

> tlog-8-2.el8.x86_64

> [root@bd2 ~]# yum install cockpit-session-recording

> Updating Subscription Management repositories.

> Last metadata expiration check: 3:09:54 ago on Fri 26 Mar 2021 01:32:39 PM EDT.

> --- omited ---

> Installed:

> cockpit-session-recording-4-2.el8.noarch

Once the applications have been installed from the Cockpit console, we will see the item "Session Recording" in the left menu:

![](Image00038.jpg) 

A user will be created to demonstrate the session recording:

> [root@bd2 ssh]# useradd admin-backups

> [root@bd2 ssh]# passwd admin-backups

> Changing password for user admin-backups.

> New password:

> BAD PASSWORD: The password is shorter than 8 characters

> Retype new password:

> passwd: all authentication tokens updated successfully.

Through Cockpit the parameters of the session recording are defined. In the graphic console in the “Session Recording” section, locate the “configuration” icon which will take you to the configuration section:

![](Image00039.jpg)

In the "SSSD Configuration" section the user name or groups to be monitored are written and saved, this configuration is registered in /etc/sssd/conf.d/sssd-session-recording.conf. Following this in the SSH configuration file the lines detailed below are commented:

> [root@bd2 ~]# vim /etc/ssh/sshd_config

> # Accept locale-related environment variables

> #AcceptEnv LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES

> #AcceptEnv LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT

> #AcceptEnv LC_IDENTIFICATION LC_ALL LANGUAGE

> #AcceptEnv XMODIFIERS

These lines are related to the environment variables that each user takes when they login via SSH and it has been discovered that "tlog" conflicts with the default configuration. Once the lines are commented, allow SSH to reread its configuration file:

> [root@bd2 ~]# systemctl reload sshd.service

To check the functionality, the user "admin-backups" is registered in the system and once the access credential is entered, the user will be able to see a message like the following:

> $ ssh -l admin-backups 192.168.0.201

> admin-backups@192.168.0.201's password:

> Web console: https://bd2.aptivalabs.net:9090/ or https://192.168.0.201:9090/

> Locale charset is ANSI_X3.4-1968 (ASCII)

> Assuming locale environment is lost and charset is UTF-8

> ATTENTION! Your session is being recorded!

> [admin-backups@bd2 ~]$

Everything that the “admin-backups” user does on the system will be recorded and that recording can be viewed in the cockpit or through the “tlog-play” application.

> CONTAINERS IN RED HAT LINUX – PODMAN/SKOPEO

A container is an isolated, running process that takes network resources and integrates with its integrated storage; some come to compare it with virtual machines because the objective is the same, however they are significantly far from being similar technologies.

Container management in RHEL8 is done thanks to applications like "podman", "skopeo" and "buildah"; the "podman" program is used to manage containers and images, the "skopeo" application inspects, copies, deletes and signs container images, and the "buildah" application is used to create new containers, all this represents the new way of they manage containers since in previous versions the tool for this management was made by Docker.

The following exercise will allow us to install the container platform, download an image and then launch it as a container, manage that container and manage its image, the purpose of this is to contextualize the capacities for the individual handling of containers since the clustered and high management availability is given with platforms such as Kubernetes and Openshift; We start by listing the modules associated with the container platform:

> [root@bd1 ~]# yum module list --available container-tools

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:19:21 ago on Thu 08 Apr 2021 05:18:38 PM -03.

> Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)

> Name            Stream       Profiles Summary

> container-tools rhel8 [d][e] common [ Most recent (rolling) versions of podman, buildah, skopeo, runc, conmon, runc, conmon,

> d]       CRIU, Udica, etc as well as dependencies such as container-selinux built and tested tog

> ether, and updated as frequently as every 12 weeks.

> container-tools 1.0          common [ Stable versions of podman 1.0, buildah 1.5, skopeo 0.1, runc, conmon, CRIU, Udica, etc

> d]       as well as dependencies such as container-selinux built and tested together, and suppor

> ted for 24 months.

> container-tools 2.0          common [ Stable versions of podman 1.6, buildah 1.11, skopeo 0.1, runc, conmon, etc as well as d

> d]       ependencies such as container-selinux built and tested together, and supported as docum

> ented on the Application Stream lifecycle page.

> Hint: [d]efault, [e]nabled, [x]disabled, [i]nstalled

For this case, it is observed that the "container-tools" module presents various streams; We will install the default stream:

> [root@bd1 ~]# yum module install container-tools -y

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:22:47 ago on Thu 08 Apr 2021 05:18:38 PM -03.

> Dependencies resolved.

> ============================================================================================================

> Package             Arch     Version                                               Repository                          Size

> ============================================================================================================

> Installing group/module packages:

> crun                x86_64   0.16-2.module+el8.3.1+9857+68fb1526                   rhel-8-for-x86_64-appstream-rpms   181 k

> python-podman-api   noarch   1.2.0-0.2.gitd0a45fe.module+el8.3.1+9857+68fb1526     rhel-8-for-x86_64-appstream-rpms    43 k

> skopeo              x86_64   1:1.2.0-9.module+el8.3.1+9857+68fb1526                rhel-8-for-x86_64-appstream-rpms   7.1 M

> toolbox             noarch   0.0.8-1.module+el8.3.1+9857+68fb1526                  rhel-8-for-x86_64-appstream-rpms    16 k

> udica               noarch   0.2.4-1.module+el8.3.1+9857+68fb1526                  rhel-8-for-x86_64-appstream-rpms    51 k

> Installing dependencies:

> python3-psutil      x86_64   5.4.3-10.el8                                          rhel-8-for-x86_64-appstream-rpms   373 k

> Installing module profiles:

> container-tools/common

> Transaction Summary

> =============================================================================================================================

> Install  6 Packages

> Total download size: 7.7 M

> Installed size: 28 M

Once the module is installed, we can validate that the container tools are available, as is the case of the “podman” application, validating their availability as follows:

> [root@bd1 ~]# podman –help | more

> Manage pods, containers and images

> Usage:

> podman [options] [command]

> Available Commands:

> attach      Attach to a running container

> auto-update Auto update containers according to their auto-update policy

> build       Build an image using instructions from Containerfiles

> commit      Create new image based on the changed container

> container   Manage containers

> cp          Copy files/folders between a container and the local filesystem

> create      Create but do not start a container

> --- omiteda ---

> [root@bd1 ~]# podman info

> host:

> arch: amd64

> buildahVersion: 1.18.0

> cgroupManager: 1ystem

> cgroupVersion: v1

> conmon:

> package: conmon-2.0.22-3.module+el8.3.1+9857+68fb1526.x86_64

> path: /usr/bin/conmon

> version: ‘conmon version 2.0.22, commit: a40e3092dbe499ea1d85ab339caea023b74829b9’

> cpus: 8

> distribution:

> distribution: ‘”rhel”’

> version: “8.3”

> eventLogger: file

> hostname: bd1.aptivalabs.net

Working with containers requires the use of a registry where the images that are later deployed as containers are stored, in this case Red Hat provides the registry "registry.access.redhat.com" which you can use using your login credentials. Red Hat portal, this registration is done as follows:

> [root@bd1 ~]# podman login registry.access.redhat.com

> Username: **your.user**

> Password:

> Login Succeeded!

Once registered you will be able to search for container images, in this case we are interested in the image called “ubi8”, as shown below:

> [root@bd1 ~]# podman search registry.access.redhat.com/ubi8 | more

> INDEX       NAME                                         DESCRIPTION                                      STARS   OFFICIAL  A

> UTOMATED

> redhat.com  registry.access.redhat.com/ubi8/ubi-minimal  Provides the latest release of the Minimal R...  0

> **redhat.com  registry.access.redhat.com/ubi8              The Universal Base Image is designed and eng...  0                **

> redhat.com  registry.access.redhat.com/ubi7/ubi          The Universal Base Image is designed and eng...  0

> redhat.com  registry.access.redhat.com/ubi8/ubi-init     Provides the latest release of the Red Hat U...  0

> redhat.com  registry.access.redhat.com/ubi8-minimal      The Universal Base Image Minimal is a stripp...  0

> redhat.com  registry.access.redhat.com/ubi8-init         The Universal Base Image Init is designed to...  0

Once the image is identified, it is brought to the local environment with the “pull” parameter of the “podman” command, as shown:

> [root@bd1 ~]# podman pull registry.access.redhat.com/ubi8/ubi:latest

> Trying to pull registry.access.redhat.com/ubi8/ubi:latest...

> Getting image source signatures

> Copying blob 13897c84ca57 done

> Copying blob 64607cc74f9c done

> Copying config 9992f11c61 done

> Writing manifest to image destination

> Storing signatures

> 9992f11c61c5fa38a691f80c7e13b75960b536aade4cce8543433b24623bce68

Once the image is downloaded, we can list it as shown:

> [root@bd1 ~]# podman images

> REPOSITORY                           TAG     IMAGE ID      CREATED     SIZE

> registry.access.redhat.com/ubi8/ubi  latest  9992f11c61c5  9 days ago  213 MB

The “skopeo” application is used to inspect the image to be used:

> [root@bd1 ~]# skopeo inspect docker://registry.access.redhat.com/ubi8/ubi:latest | more

> {

> "Name": "registry.access.redhat.com/ubi8/ubi",

> "Digest": "sha256:17ff29c0747eade777e8b9868f97ba37e6b8b43f5ed2dbf504ff9277e1c1d1ca",

> "RepoTags": [

> "8.2-343-source",

> "8.1-328",

> "8.2-265-source",

> "8.2-347-source",

> "8.2-299.1592810498",

After having carried out the inspection, the container is displayed from the preferred image, obtaining access to it through CLI, as shown in the following instruction:

> [root@bd1 ~]# podman run -it registry.access.redhat.com/ubi8/ubi:latest

> [root@f1103f0c82ed /]#

> [root@f1103f0c82ed /]# exit

> exit

With the container running, it is possible to carry out the activities of stop, elimination, visualization, etc., in this case, the container in execution is displayed and then eliminated and then re-listed in order to validate that the container has been eliminated, as shown:

> [root@bd1 ~]# podman ps --all

> CONTAINER ID  IMAGE                                       COMMAND    CREATED             STATUS                      PORTS   NAMES

> f1103f0c82ed  registry.access.redhat.com/ubi8/ubi:latest  /bin/bash  About a minute ago  Exited (127) 9 seconds ago          reverent_varahamihira

> [root@bd1 ~]# podman rm -a

> f1103f0c82ed107c4b4a887d31eeb3b9b8a1727938971f2da3581bb75107db13

> [root@bd1 ~]# podman ps --all

> CONTAINER ID  IMAGE   COMMAND  CREATED  STATUS  PORTS   NAMES

The container image previously downloaded is listed below and then deleted with the “rmi” subcommand of “podman”:

> [root@bd1 ~]# podman images

> REPOSITORY                           TAG     IMAGE ID      CREATED     SIZE

> registry.access.redhat.com/ubi8/ubi  latest  9992f11c61c5  9 days ago  213 MB

> [root@bd1 ~]# podman rmi registry.access.redhat.com/ubi8/ubi:latest

> Untagged: registry.access.redhat.com/ubi8/ubi:latest

> Deleted: 9992f11c61c5fa38a691f80c7e13b75960b536aade4cce8543433b24623bce68

> [root@bd1 ~]# podman images

> REPOSITORY  TAG     IMAGE ID  CREATED  SIZE

As mentioned in previous sections, Red Hat has left Docker as a platform for container management and has brought other tools for this purpose, the reason becomes a decision based on providing better functionalities for those who manage container platforms as well as for those who develop applications on these platforms.

> DEPLOYING A FTP SERVER - VSFTP

One of the very common use cases in Linux system administration has to do with transferring files from a client to a server and vice versa. In this exercise we will install the VSFTP software as an FTP server to obtain the aforementioned functionality, which will listen to requests on port 21, giving local users the ability to connect and transfer files in any direction. We start by installing the VSFTP software:

> **[root@s1 ~]# yum install vsftpd**

> --- salida omitida ---

> Preparing        :                                                                                           1/1

> Installing       : vsftpd-3.0.3-33.el8.x86_64                                                                1/1

> Running scriptlet: vsftpd-3.0.3-33.el8.x86_64                                                                1/1

> Verifying        : vsftpd-3.0.3-33.el8.x86_64                                                                1/1

> Installed products updated.

> Installed:

> vsftpd-3.0.3-33.el8.x86_64

> Complete!

It is necessary to review the configuration of the service configuration file, which is where we can adjust the configuration at our discretion; the configuration file is located in the path /etc/vsftpd/vsftpd.conf. The default configuration defines restricted access for anonymous users but allows access for local users, as shown:

> # Allow anonymous FTP? (Beware - allowed by default if you comment this out).

> anonymous_enable=NO

> # Uncomment this to allow local users to log in.

> local_enable=YES

Taking advantage of this initial configuration, a standard user will be created which will be able to register in the system via FTP on port 21, as shown below:

> [root@s1 vsftpd]# adduser fmestre

> [root@s1 vsftpd]# passwd fmestre

> Changing password for user fmestre.

> New password:

> BAD PASSWORD: The password is shorter than 8 characters

> Retype new password:

> passwd: all authentication tokens updated successfully.

Once the user is created, we proceed to activate the service at the start of the machine and start it immediately, reviewing the corresponding process, as shown below:

> [root@s1 ~]# systemctl enable --now vsftpd

> [root@s1 ~]# ps -fe

> root       52471       1  0 19:23 ?        00:00:00 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf

Then we activate the security settings associated with SELinux and FirewallD, as follows

> [root@s1 ~]# setsebool -P ftpd_full_access on

> [root@s1 ~]# firewall-cmd --add-service=ftp --permanent

> [root@s1 ~]# firewall-cmd --reload

> [root@s1 ~]# firewall-cmd --info-zone=public

> --- salida omitida ---

> services: cockpit dhcpv6-client **ftp** http ssh

Finally, any FTP client is used to make the connection and transfer files from one place to another:

![](Image00040.jpg) 

> DEPLOYING A NFS SERVER

In the definition of network services, the functionality that we obtain by NFS is very useful for administrators of Linux servers. Following is the definition and description of the NFS service from the Red Hat Linux 8 documentation:

“A network file system (NFS) allows remote hosts to mount file systems over a network and interact with those file systems as if they were mounted locally. This makes it possible to consolidate resources on centralized servers on the network.

The NFS server consults the /etc/export configuration file to determine if the client can access any exported file systems. Once verified, all file and directory operations are available to the user. NFS version 4 (NFSv4) works through firewalls and on the Internet, does not require an rpcbind service, supports access control lists (ACLs), and uses stateful operations.

The default NFS version in Red Hat Enterprise Linux 8 is 4.2\. NFS clients try to mount using NFSv4.2 by default, and fall back to NFSv4.1 when the server does not support NFSv4.2\. The mount reverts to NFSv4.0 and then NFSv3\. The /etc/export file controls which file systems are exported to remote hosts and specifies the options. "

**Default options**

The default options for an export entry are:

*   > ro - The exported file system is read-only. Remote hosts cannot change shared data on the file system. To allow hosts to make file system changes (that is, read and write), specify the rw option.

*   > sync - The NFS server will not respond to requests before the changes made by previous requests are written to disk. To enable asynchronous writes instead, specify the async option.

*   > wdelay - The NFS server will delay writing to the disk if it suspects that another write request is imminent. This can improve performance by reducing the number of times the disk must be accessed by separate write commands, thus reducing write overhead. To disable this, specify the no_wdelay option, which is only available if the default sync option is also specified.

*   > root_squash - This prevents root users logged in remotely (rather than locally) from having root privileges; instead, the NFS server assigns them user ID nobody. This effectively "squashes" the power from the remote root user to the lowest local user, preventing possible unauthorized writes on the remote server. To disable root squashing, specify the no_root_squash option.

The deployment of the NFS service is shown in the following procedure.  The folder “/aptivalabs” is created, which will be the path to export:

> [root@sr1 ~]# mkdir /aptivalabs

The "nfs-utils" software is installed, which is normally already installed on Red Hat Linux and derived systems:

> [root@sr1 ~]# yum install nfs-utils -y

We edit the NFS service configuration file:

> [root@sr1 ~]# vim /etc/exports

> ​ /aptivalabs 192.168.0.0/24(rw,sync,wdelay,no_root_squash)

For servers that support NFSv2 or NFSv3 connections, the rpcbind service must be running. To verify that rpcbind is active, use the following command:

> [root@sr1 ~]# systemctl status rpcbind

If the service is stopped, start it and activate it:

> [root@sr1 ~]# systemctl enable --now rpcbind

It is time to start the NFS service, as shown below:

> [root@sr1 ~]# systemctl enable --now nfs-server

It is necessary to tell FirewallD to allow listening on the following services:

> [root@sr1 ~]# firewall-cmd --permanent --add-service mountd

> [root@sr1 ~]# firewall-cmd --permanent --add-service rpc-bind

> [root@sr1 ~]# firewall-cmd --permanent --add-service nfs

> [root@sr1 ~]# firewall-cmd --list-all

> public (active)

> target: default

> icmp-block-inversion: no

> interfaces: ens18

> sources:

> services: cockpit dhcpv6-client mountd nfs postgresql rpc-bind ssh

To verify the configuration established in the NFS server, in a second Linux system we will carry out the temporary and persistent mounting of the exported resource. We start by installing the "nfs-utils" package and viewing the exported resource:

> [root@sr2 ~]# yum -y install nfs-utils

> [root@sr2 ~]# showmount -e 192.168.0.38

> Export list for 192.168.0.38:

> /aptivalabs 192.168.0.0/24

The exported resource is temporarily mounted in the /mnt folder and it is displayed:

> [root@sr2 ~]# mount -t nfs 192.168.0.38:/aptivalabs /mnt

> [root@sr2 ~]# df -hT

> Filesystem               Type      Size  Used Avail Use% Mounted on

> …

> 192.168.0.38:/aptivalabs nfs4       44G  5.1G   39G  12% /mnt

Persistent mount is done, as shown:

> [root@sr2 ~]# vim /etc/fstab

> ​ 192.168.0.38:/aptivalabs /mnt               nfs     defaults        0 0

> [root@sr2 ~]# systemctl daemon-reload

> [root@sr2 ~]# udevadm settle

> [root@sr2 ~]# mount -a

To verify the persistent mount, a reboot is performed and once the system is available, the mount points are verified:

> [root@sr2 ~]# reboot

> [root@sr2 ~]# df -hT

> Filesystem               Type      Size  Used Avail Use% Mounted on

> …

> 192.168.0.38:/aptivalabs nfs4       44G  5.1G   39G  12% /mnt

> MARIADB - RELATIONAL DATABASE SERVICE

MariaDB is a database server based on the technology that for some time was deployed in MySQL. The default version of Red Hat Enterprise Linux 8 is MariaDB 10.3.

In subsequent chapters, the documentation developed by Red Hat Inc will be used literally to describe the characteristics and functionalities of MariaDB, however, there is the profile of this author to give this documentation an air of step-by-step instructional use to perform the different activities on MariaDB.

INSTALLATION AND CONFIGURATION

To install MariaDB we can see the streams defined by the system for this purpose; The Red Hat Linux version brings version 10.3 as the default version, as shown below:

> [root@sr1 ~]# yum module info mariadb

> Updating Subscription Management repositories.

> Last metadata expiration check: 19:56:41 ago on Wed 28 Jul 2021 01:43:09 PM EDT.

> Name             : mariadb

> Stream           : 10.3 [d][a]

> Version          : 8010020190902091509

> Context          : cdc1202b

> Architecture     : x86_64

> Profiles         : client, galera, server [d]

> Default profiles : server

> Repo             : rhel-8-for-x86_64-appstream-rpms

> Summary          : MariaDB Module

> Description      : MariaDB is a community developed branch of MySQL. MariaDB is a multi-user, multi-threaded SQL database server. It is a client/server implementation consisting of a server daemon (mysqld) and many different client programs and libraries. The base package contains the standard MariaDB/MySQL client programs and generic MySQL files.

> ...

Next we proceed with the installation of MariaDB:

> [root@sr1 ~]# yum module install mariadb:10.3/server

> Updating Subscription Management repositories.

> Last metadata expiration check: 19:58:16 ago on Wed 28 Jul 2021 01:43:09 PM EDT.

> Dependencies resolved.

> ==================================================================================================

> Package                      Architecture  Version                                            Repository                               Size

> ==================================================================================================

> Installing group/module packages:

> mariadb-server               x86_64        3:10.3.28-1.module+el8.3.0+10472+7adc332a          rhel-8-for-x86_64-appstream-rpms         16 M

> Installing dependencies:

> mariadb                      x86_64        3:10.3.28-1.module+el8.3.0+10472+7adc332a          rhel-8-for-x86_64-appstream-rpms        6.0 M

> …

The service is then started and the start of the service is enabled at startup of the operating system:

> [root@sr1 ~]# systemctl enable mariadb.service --now

> Created symlink /etc/systemd/system/mysql.service → /usr/lib/systemd/system/mariadb.service.

> Created symlink /etc/systemd/system/mysqld.service → /usr/lib/systemd/system/mariadb.service.

> Created symlink /etc/systemd/system/multi-user.target.wants/mariadb.service → /usr/lib/systemd/system/mariadb.service.

The status of the service is validated:

> **[root@sr1 ~]# systemctl status mariadb.service**

> ● mariadb.service - MariaDB 10.3 database server

> Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)

> Active: active (running) since Thu 2021-07-29 09:42:40 EDT; 50s ago

> Docs: man:mysqld(8)

> https://mariadb.com/kb/en/library/systemd/

> Process: 3991 ExecStartPost=/usr/libexec/mysql-check-upgrade (code=exited, status=0/SUCCESS)

> Process: 3855 ExecStartPre=/usr/libexec/mysql-prepare-db-dir mariadb.service (code=exited, status=0/SUCCESS)

> Process: 3830 ExecStartPre=/usr/libexec/mysql-check-socket (code=exited, status=0/SUCCESS)

> Main PID: 3959 (mysqld)

> …

Note that MariaDB and MySQL database servers cannot be installed side by side on Red Hat Enterprise Linux 8.0 due to conflicting RPM packages. A local connection to the database engine will then be established using the database superuser (root):

> **[root@sr1 ~]# mysql -u root -p**

> Enter password:

> Welcome to the MariaDB monitor.  Commands end with ; or \g.

> Your MariaDB connection id is 8

> Server version: 10.3.28-MariaDB MariaDB Server

> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

> MariaDB [(none)]> exit

> Bye

INITIAL INSURANCE

At the end of the database engine installation and the validation of its respective connection, MariaDB gives us the opportunity to perform a configuration hardening for security reasons, as described below:

> [root@sr1 ~]# mysql_secure_installation

> NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB

> SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

> In order to log into MariaDB to secure it, we'll need the current

> password for the root user.  If you've just installed MariaDB, and

> you haven't set the root password yet, the password will be blank,

> so you should just press enter here.

> Enter current password for root (enter for none):

> OK, successfully used password, moving on...

> Setting the root password ensures that nobody can log into the MariaDB

> root user without the proper authorisation.

> Set root password? [Y/n] **Y**

> New password:

> Re-enter new password:

> Password updated successfully!

> Reloading privilege tables..

> ... Success!

> By default, a MariaDB installation has an anonymous user, allowing anyone

> to log into MariaDB without having to have a user account created for

> them.  This is intended only for testing, and to make the installation

> go a bit smoother.  You should remove them before moving into a

> production environment.

> Remove anonymous users? [Y/n] **Y**

> ... Success!

> Normally, root should only be allowed to connect from 'localhost'.  This

> ensures that someone cannot guess at the root password from the network.

> Disallow root login remotely? [Y/n] **n**

> ... skipping.

> By default, MariaDB comes with a database named 'test' that anyone can

> access.  This is also intended only for testing, and should be removed

> before moving into a production environment.

> Remove test database and access to it? [Y/n] **Y**

> - Dropping test database...

> ... Success!

> - Removing privileges on test database...

> ... Success!

> Reloading the privilege tables will ensure that all changes made so far

> will take effect immediately.

> Reload privilege tables now? [Y/n] **Y**

> ... Success!

> Cleaning up...

> All done!  If you've completed all of the above steps, your MariaDB

> installation should now be secure.

> Thanks for using MariaDB!

CONFIGURATION FOR THE NETWORK

To configure the MariaDB server for network connection, use the [mysqld] section of the /etc/my.cnf.d/mariadb-server.cnf file, where you can set the following configuration directives:

*   > bind-address - Bind-address is the address where the server will listen. Possible options are: a host name, an IPv4 address, or an IPv6 address.

*   > skip-networking - Possible values ​​are:

> 0 - to listen to all clients

> 1 - to hear only local clients

*   > port - The port on which MariaDB listens for TCP / IP connections; the default port associated with this service is 3306 in tcp.

A look at the configuration file could show us the following information:

> [root@sr1 ~]# vim /etc/my.cnf.d/mariadb-server.cnf

> ​ [mysqld]

> ​ datadir=/var/lib/mysql

> ​ socket=/var/lib/mysql/mysql.sock

> ​ log-error=/var/log/mariadb/mariadb.log

> ​ pid-file=/run/mariadb/mariadb.pid

> ​ bind-address=0.0.0.0

> ​ skip-networking=0

> ​ port=3306

If you have made any changes to this file and require it to be applied, remember that you must restart the service (bear in mind the implications that a restart of the service could have):

> [root@sr1 ~]# systemctl restart mariadb.service

CREATION OF DATABASE AND INSERTION OF RECORDS

For demonstration purposes and taking advantage of the installation and assurance of the MariaDB database engine, the creation of a database and the insertion of records in MariaDB is detailed, as shown below:

> **[root@sr1 ~]# mysql -u root -p**

> Enter password:

> Welcome to the MariaDB monitor.  Commands end with ; or \g.

> Your MariaDB connection id is 8

> Server version: 10.3.28-MariaDB MariaDB Server

> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

> MariaDB [(none)]>

The following statement creates the database named "empresa":

> MariaDB [(none)]> CREATE DATABASE empresa;

> Query OK, 1 row affected (0.001 sec)

The following instruction shows the databases that MAriaDB has:

> MariaDB [(none)]> show databases;

> +--------------------+

> | Database           |

> +--------------------+

> | empresa            |

> | information_schema |

> | mysql              |

> | performance_schema |

> +--------------------+

> 4 rows in set (0.001 sec)

Once the “empresa” database has been created, we proceed to operate within it, as shown:

> MariaDB [(none)]> use empresa

> Reading table information for completion of table and column names

> You can turn off this feature to get a quicker startup with -A

> Database changed

Next we create a table in MariaDB, which will be called "alumnos", just to introduce basic data:

> MariaDB [empresa]> CREATE TABLE alumnos ( Id INT NOT NULL AUTO_INCREMENT, Nombre VARCHAR(100), Sexo INT, PRIMARY KEY(Id));

> Query OK, 0 rows affected (0.009 sec)

Once the table is created, we describe it, as shown below:

> MariaDB [empresa]> desc alumnos ;

> +--------+--------------+------+-----+---------+----------------+

> | Field  | Type         | Null | Key | Default | Extra          |

> +--------+--------------+------+-----+---------+----------------+

> | Id     | int(11)      | NO   | PRI | NULL    | auto_increment |

> | Nombre | varchar(100) | YES  |     | NULL    |                |

> | Sexo   | int(11)      | YES  |     | NULL    |                |

> +--------+--------------+------+-----+---------+----------------+

> 3 rows in set (0.002 sec)

We proceed to insert four (4) records in the “alumnos” table, listing them at the end, as shown:

> MariaDB [empresa]> insert into alumnos (Nombre, Sexo) values ('Fabian Mestre',1);

> Query OK, 1 row affected (0.003 sec)

> MariaDB [empresa]> insert into alumnos (Nombre, Sexo) values ('Juana Mestre',0);

> Query OK, 1 row affected (0.002 sec)

> MariaDB [empresa]> insert into alumnos (Nombre, Sexo) values ('Carlos Perez',1);

> Query OK, 1 row affected (0.002 sec)

> MariaDB [empresa]> insert into alumnos (Nombre, Sexo) values ('Camila Calderon',0);

> Query OK, 1 row affected (0.002 sec)

> MariaDB [empresa]> select * from alumnos;

> +----+-----------------+------+

> | Id | Nombre          | Sexo |

> +----+-----------------+------+

> |  1 | Fabian Mestre   |    1 |

> |  2 | Juana Mestre    |    0 |

> |  3 | Carlos Perez    |    1 |

> |  4 | Camila Calderon |    0 |

> +----+-----------------+------+

> 4 rows in set (0.000 sec)

For the purposes of publishing knowledge, the way in which a database is eliminated is listed below, however, if you are doing the labs and exercises proposed, we recommend not deleting the previously created database, so that you can continue doing the exercises:

> MariaDB [empresa]> DROP DATABASE empresa;

> Query OK, 2 rows affected (0.019 sec)

> MariaDB [(none)]> show databases;

> +--------------------+

> | Database           |

> +--------------------+

> | information_schema |

> | mysql              |

> | performance_schema |

> +--------------------+

> 3 rows in set (0.001 sec)

BACKUP MANAGEMENT

There are two main ways to back up data in a MariaDB database:

> •  Logical backup

> •  Physical backup

Logical backup consists of the SQL statements required to restore the data. This type of backup exports the information and logs in plain text files. The main advantage of logical backup over physical is portability and flexibility. Data can be restored to other hardware configurations, versions of MariaDB, or database management system (DBMS), which is not possible with physical backups. Note that logical backup can be done if the service “mariadb.service” is running. Logical backup does not include log and configuration files.

Physical backup consists of copies of files and directories that store content. Physical backup has the following advantages compared to logical backup:

> •  The outlet is more compact.

> •  The backup is smaller.

> •  Backup and restore are faster.

> •  The backup includes configuration and log files.

Note that the physical backup should be done when the service "mariadb.service" is not running or all the database tables are locked to prevent changes during the backup.

You can use one of the following MariaDB backup approaches to back up the data from a MariaDB database:

> •  Logical backup with mysqldump

> •  Online physical backup with Mariabackup tool

> •  File system backup

> •  Replication as a backup solution

The mysqldump client is a backup utility, which can be used to dump a database or a collection of databases for backup or transfer to another database server. The output of mysqldump usually consists of SQL statements to recreate the structure of the server tables, fill them with data, or both. As an alternative, mysqldump can also generate files in other formats, including CSV or other delimited text formats, and XML.

To perform backups with mysqldump, you can use one of the following options:

> •  Backup of a selected database

> •  Backup of a subset of tables in a database

LOGIC BACKUP AND RESTORATION

To back up a full database, run the following:

> [root@sr1 ~]# mysqldump empresa > /root/backup-empresa.sql -p

> Enter password:

> [root@sr1 ~]# ll

> total 36

> -rw-r--r--. 1 root root  2026 Jul 29 10:51 backup-empresa.sql

You can take a look at the resulting backup file, as shown below:

> [root@sr1 ~]# more backup-empresa.sql

> -- MySQL dump 10.19  Distrib 10.3.28-MariaDB, for Linux (x86_64)

> --

> -- Host: localhost    Database: empresa

> -- ------------------------------------------------------

> -- Server version ​ 10.3.28-MariaDB

> /*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;

> /*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;

> /*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;

> /*!40101 SET NAMES utf8mb4 */;

> /*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;

> /*!40103 SET TIME_ZONE='+00:00' */;

> /*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;

> /*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;

> /*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;

> /*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

> --

> -- Table structure for table `alumnos`

> --

> DROP TABLE IF EXISTS `alumnos`;

> /*!40101 SET @saved_cs_client     = @@character_set_client */;

> /*!40101 SET character_set_client = utf8 */;

> CREATE TABLE `alumnos` (

> `Id` int(11) NOT NULL AUTO_INCREMENT,

> `Nombre` varchar(100) DEFAULT NULL,

> `Sexo` int(11) DEFAULT NULL,

> PRIMARY KEY (`Id`)

> ) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=latin1;

> /*!40101 SET character_set_client = @saved_cs_client */;

> --

> -- Dumping data for table `alumnos`

> --

> LOCK TABLES `alumnos` WRITE;

> /*!40000 ALTER TABLE `alumnos` DISABLE KEYS */;

> INSERT INTO `alumnos` VALUES (1,'Fabian Mestre',1),(2,'Juana Mestre',0),(3,'Carlos Perez',1),(4,'Camila Calderon',0);

> /*!40000 ALTER TABLE `alumnos` ENABLE KEYS */;

> UNLOCK TABLES;

> /*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

> /*!40101 SET SQL_MODE=@OLD_SQL_MODE */;

> /*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;

> /*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;

> /*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;

> /*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;

> /*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

> /*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

> -- Dump completed on 2021-07-29 10:51:29

Next we will carry out a Database restoration exercise, for them we will create an empty database and in it we will restore the previously backed up ones, as shown below:

> MariaDB [(none)]> CREATE DATABASE empresa2;

> MariaDB [(none)]> show databases;

> +--------------------+

> | Database           |

> +--------------------+

> | empresa            |

> | empresa2           |

> | information_schema |

> | mysql              |

> | performance_schema |

> +--------------------+

> 5 rows in set (0.001 sec)

> MariaDB [(none)]> exit

We execute the restoration:

> [root@sr1 ~]# mysql empresa2 < /root/backup-empresa.sql -p

> Enter password:

We proceed to verify the restoration, as shown:

> [root@sr1 ~]# **mysql -u root -p**

> Enter password:

> Welcome to the MariaDB monitor.  Commands end with ; or \g.

> Your MariaDB connection id is 18

> Server version: 10.3.28-MariaDB MariaDB Server

> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

> MariaDB [(none)]> **use empresa2**

> Reading table information for completion of table and column names

> You can turn off this feature to get a quicker startup with -A

> Database changed

> MariaDB [empresa2]> **select * from alumnos;**

> +----+-----------------+------+

> | Id | Nombre          | Sexo |

> +----+-----------------+------+

> |  1 | Fabian Mestre   |    1 |

> |  2 | Juana Mestre    |    0 |

> |  3 | Carlos Perez    |    1 |

> |  4 | Camila Calderon |    0 |

> +----+-----------------+------+

> 4 rows in set (0.000 sec)

In the previous exercise we dumped a single database; to dump all databases, run the following:

> [root@sr1 ~]# mysqldump  --all-databases > all_databases.sql -p

> Enter password:

> [root@sr1 ~]# wc -l all_databases.sql

> 981 all_databases.sql

You can view the contents of the dump as follows:

> [root@sr1 ~]# more all_databases.sql

> -- MySQL dump 10.19  Distrib 10.3.28-MariaDB, for Linux (x86_64)

> --

> -- Host: localhost    Database:

> -- ------------------------------------------------------

> -- Server version ​ 10.3.28-MariaDB

> /*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;

> /*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;

> /*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;

> ...

PERFORMING A PHYSICAL BACKUP AND RESTORATION

Then we proceed to make a physical backup of the database, this we will do with the application called "mariadb-backup" and we will see its deployment in the exercise below, starting with the installation of the application itself:

> [root@sr1 ~]# **yum install mariadb-backup -y**

> Updating Subscription Management repositories.

> Last metadata expiration check: 21:23:21 ago on Wed 28 Jul 2021 01:43:09 PM EDT.

> Package mariadb-backup-3:10.3.28-1.module+el8.3.0+10472+7adc332a.x86_64 is already installed.

> Dependencies resolved.

> Nothing to do.

> Complete!

**mariabackup** needs to be provided with the credentials of the user under which the backup will run. You can provide the credentials on the command line or through a configuration file before applying the procedure. To set the credentials using the configuration file, first create the file (for example, /etc/my.cnf.d/mariabackup.cnf), and then add the following lines in the [xtrabackup] or [mysqld] section of the new archive:

> [xtrabackup]

> user=root

> password=123456

Next create the path where the backups will be saved:

> [root@sr1 ~]# mkdir /maria-backup

Then run a physical backup of the database, as shown:

> [root@sr1 ~]# **mariabackup --backup --target-dir /maria-backup/**

> [00] 2021-07-29 11:14:40 Connecting to MySQL server host: localhost, user: root, password: set, port: not set, socket: not set

> [00] 2021-07-29 11:14:40 Using server version 10.3.28-MariaDB

> mariabackup based on MariaDB server 10.3.28-MariaDB Linux (x86_64)

> [00] 2021-07-29 11:14:40 uses posix_fadvise().

> [00] 2021-07-29 11:14:40 cd to /var/lib/mysql/

> [00] 2021-07-29 11:14:40 open files limit requested 0, set to 1024

> [00] 2021-07-29 11:14:40 mariabackup: using the following InnoDB configuration:

> [00] 2021-07-29 11:14:40 innodb_data_home_dir =

> [00] 2021-07-29 11:14:40 innodb_data_file_path = ibdata1:12M:autoextend

> [00] 2021-07-29 11:14:40 innodb_log_group_home_dir = ./

> [00] 2021-07-29 11:14:40 InnoDB: Using Linux native AIO

> 2021-07-29 11:14:40 0 [Note] InnoDB: Number of pools: 1

> [00] 2021-07-29 11:14:40 mariabackup: Generating a list of tablespaces

> 2021-07-29 11:14:40 0 [Warning] InnoDB: Allocated tablespace ID 1 for mysql/innodb_table_stats, old maximum was 0

> [00] 2021-07-29 11:14:40 >> log scanned up to (1678108)

> [01] 2021-07-29 11:14:40 Copying ibdata1 to /maria-backup/ibdata1

> [01] 2021-07-29 11:14:40         ...done

> ...

> [01] 2021-07-29 11:14:41 Copying ./aria_log_control to /maria-backup/aria_log_control

> [01] 2021-07-29 11:14:41         ...done

> [01] 2021-07-29 11:14:41 Copying ./aria_log.00000001 to /maria-backup/aria_log.00000001

> [01] 2021-07-29 11:14:41         ...done

> [00] 2021-07-29 11:14:41 Waiting for log copy thread to read lsn 1678108

> [00] 2021-07-29 11:14:42 >> log scanned up to (1678108)

> [00] 2021-07-29 11:14:42 Executing FLUSH NO_WRITE_TO_BINLOG ENGINE LOGS...

> [00] 2021-07-29 11:14:42 mariabackup: The latest check point (for incremental): '1678099'

> mariabackup: Stopping log copying thread.[00] 2021-07-29 11:14:42 >> log scanned up to (1678108)

> [00] 2021-07-29 11:14:42 >> log scanned up to (1678108)

> [00] 2021-07-29 11:14:42 Executing UNLOCK TABLES

> [00] 2021-07-29 11:14:42 All tables unlocked

> [00] 2021-07-29 11:14:42 Copying ib_buffer_pool to /maria-backup/ib_buffer_pool

> [00] 2021-07-29 11:14:42         ...done

> [00] 2021-07-29 11:14:42 Backup created in directory '/maria-backup/'

> [00] 2021-07-29 11:14:42 Writing backup-my.cnf

> [00] 2021-07-29 11:14:42         ...done

> [00] 2021-07-29 11:14:42 Writing xtrabackup_info

> [00] 2021-07-29 11:14:42         ...done

> [00] 2021-07-29 11:14:42 Redo log (from LSN 1678099 to 1678108) was copied.

> [00] 2021-07-29 11:14:42 completed OK!

Next we will apply a simulation of elimination of the databases and restoration of the database with which we have been working since the beginning of the chapter; we start by deleting the databases that the engine has, as shown below:

> [root@sr1 ~]# mysql -u root -p

> Enter password:

> Welcome to the MariaDB monitor.  Commands end with ; or \g.

> Your MariaDB connection id is 25

> Server version: 10.3.28-MariaDB MariaDB Server

> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

> MariaDB [(none)]> DROP DATABASE empresa;

> Query OK, 1 row affected (0.022 sec)

> MariaDB [(none)]> DROP DATABASE empresa2;

> Query OK, 1 row affected (0.008 sec)

Then the "mariadb.service" service is stopped, and we delete all the files that make up the MariaDB data (please bear in mind that this is a test exercise) as shown below:

> [root@sr1 ~]# systemctl stop mariadb.service

> [root@sr1 ~]# cd /var/lib/mysql

> [root@sr1 mysql]# ll

> total 110624

> -rw-rw----. 1 mysql mysql    16384 Jul 29 11:24 aria_log.00000001

> -rw-rw----. 1 mysql mysql       52 Jul 29 11:24 aria_log_control

> -rw-rw----. 1 mysql mysql     1256 Jul 29 11:24 ib_buffer_pool

> -rw-rw----. 1 mysql mysql 50331648 Jul 29 11:24 ib_logfile0

> -rw-rw----. 1 mysql mysql 50331648 Jul 29 09:42 ib_logfile1

> -rw-rw----. 1 mysql mysql 12582912 Jul 29 11:24 ibdata1

> -rw-rw----. 1 mysql mysql        0 Jul 29 09:42 multi-master.info

> drwx------. 2 mysql mysql     4096 Jul 29 09:42 mysql

> -rw-rw----. 1 mysql mysql       16 Jul 29 09:42 mysql_upgrade_info

> drwx------. 2 mysql mysql       20 Jul 29 09:42 performance_schema

> [root@sr1 mysql]# rm -rf *

> [root@sr1 mysql]# ll

> total 0

In the previous instructions we have created a problem, but the simulation needed it to be like this in order to demonstrate the effectiveness of the restoration; then we will restore the physical backup generated at the beginning of this explanation, as shown:

> [root@sr1 mysql]# **mariabackup --copy-back --target-dir=/maria-backup**

> mariabackup based on MariaDB server 10.3.28-MariaDB Linux (x86_64)

> [01] 2021-07-29 11:25:41 Copying ib_logfile0 to /var/lib/mysql/ib_logfile0

> [01] 2021-07-29 11:25:41         ...done

> [01] 2021-07-29 11:25:41 Copying ibdata1 to /var/lib/mysql/ibdata1

> [01] 2021-07-29 11:25:41         ...done

> ...

> [01] 2021-07-29 11:25:41 Copying ./aria_log.00000001 to /var/lib/mysql/aria_log.00000001

> [01] 2021-07-29 11:25:41         ...done

> [01] 2021-07-29 11:25:41 Copying ./ib_buffer_pool to /var/lib/mysql/ib_buffer_pool

> [01] 2021-07-29 11:25:41         ...done

> [01] 2021-07-29 11:25:41 Copying ./xtrabackup_info to /var/lib/mysql/xtrabackup_info

> [01] 2021-07-29 11:25:41         ...done

> [00] 2021-07-29 11:25:41 completed OK!

Once the restoration has been carried out, it is necessary to define the permissions of the restored files and start the MariaDB service:

> [root@sr1 mysql]# chown -R mysql:mysql /var/lib/mysql/

> [root@sr1 mysql]# systemctl start mariadb.service

To verify the effectiveness of the restoration, we connect to the database and take a look at the "empresa" database:

> [root@sr1 ~]# **mysql -u root -p**

> Enter password:

> Welcome to the MariaDB monitor.  Commands end with ; or \g.

> Your MariaDB connection id is 8

> Server version: 10.3.28-MariaDB MariaDB Server

> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

> **MariaDB [(none)]> use empresa;**

> Reading table information for completion of table and column names

> You can turn off this feature to get a quicker startup with -A

> Database changed

> **MariaDB [empresa]> select * from alumnos;**

> +----+-----------------+------+

> | Id | Nombre          | Sexo |

> +----+-----------------+------+

> |  1 | Fabian Mestre   |    1 |

> |  2 | Juana Mestre    |    0 |

> |  3 | Carlos Perez    |    1 |

> |  4 | Camila Calderon |    0 |

> +----+-----------------+------+

> 4 rows in set (0.000 sec)

> MariaDB [empresa]> exit

> Bye

GALERA – MARIADB - SYNCHRONOUS REPLICATION

Galera-MariaDB replication is based on the creation of a synchronous multimaster cluster which is composed of several MariaDB servers. The interface between Galera replication and a MariaDB database is defined by the Write Set Replication API (wsrep API).

The main features of MariaDB Galera Cluster are:

> •  Synchronous replication

> •  Active-active multimaster topology

> •  Read and write to any node in the cluster

> •  Automatic member control, failing nodes are removed from the cluster

> •  Automatic node joining

> •  Parallel replication at the row level

> •  Direct client connections (users can connect to cluster nodes and work with nodes directly while replication is running)

Synchronous replication means that a server replicates a transaction at commit time, transmitting the write set associated with the transaction to all nodes in the cluster. The client (user application) connects directly to the database management system (DBMS), and experiences similar behavior to native MariaDB. Synchronous replication ensures that a change that occurs on one node in the cluster occurs on other nodes in the cluster at the same time.

Therefore, synchronous replication has the following advantages over asynchronous:

> •  There is no delay in propagation of changes between particular cluster nodes

> •  All nodes in the cluster are always consistent

> •  The latest changes are not lost if one of the cluster nodes crashes

> •  Transactions on all nodes in the cluster run in parallel

In order to build MariaDB Galera Cluster, the following packages must be installed on your system: mariadb-server-galera, mariadb-server and galera. The mariadb-server-galera package contains support files and scripts for MariaDB Galera Cluster. MariaDB upstream patches the mariadb-server package to include the Write Set Replication API (wsrep API). This API provides the interface between Galera replication and MariaDB. MariaDB upstream also patches the galera package to add full support for MariaDB. The galley package contains the Galera Replication Library tool and the Galera Arbitrator. Galera Replication Library provides all the replication functionality. Galera Arbitrator can be used as a member of the cluster participating in voting in split brain scenarios. However, Galera Arbitrator cannot participate in the actual replication.

The exercise below displays the creation of a MariaDB multimaster cluster which will run on three servers described like this (replace names and addresses according to your test scenario):

*   > 192.168.0.48 named sr1.aptivalabs (primer master)

*   > 192.168.0.49 named sr2.aptivalabs

*   > 192.168.0.50 named sr3.aptivalabs

It is necessary to execute the following instructions on all the nodes that will be part of the cluster:

> [root@sr1 ~]# yum module install mariadb:10.3/galera -y

> [root@sr1 ~]# systemctl enable mariadb --now

> [root@sr1 ~]# mysql_secure_installation

> [root@sr1 ~]# firewall-cmd --add-service=mysql --permanent

> [root@sr1 ~]# firewall-cmd --add-port={3306/tcp,4567/udp,4567/tcp,4568/tcp,4444/tcp} --permanent

> [root@sr1 ~]# firewall-cmd --reload

> [root@sr1 ~]# firewall-cmd --list-all

For ease of operation, in each node of the cluster add the following lines to the /etc/hosts file:

> 192.168.0.48 sr1 sr1.aptivalabs

> 192.168.0.49 sr2 sr2.aptivalabs

> 192.168.0.50 sr3 sr3.aptivalabs

In each of the three nodes save the main Galera configuration file, as shown:

> [root@sr1 ~]# cp /etc/my.cnf.d/galera.cnf /root/

To deploy the cluster, in node sr1, sr2 and sr3 the service "mariadb.service" was stopped:

> [root@sr1 ~]# systemctl stop mariadb.service

You should verify that the Galera configuration files contain configuration lines similar to those presented below, on each of the three nodes:

> [root@sr1 ~]# vim /etc/my.cnf.d/galera.cnf

> wsrep_on=1

> wsrep_provider=/usr/lib64/galera/libgalera_smm.so

> wsrep_cluster_name="aptivalabs"

> wsrep_cluster_address="gcomm://192.168.0.48,192.168.0.49,192.168.0.50"

> wsrep_node_name=sr1.aptivalabs

> wsrep_node_address=192.168.0.48

In node sr2 verify that the following parameters are like this:

> [root@sr2 ~]# vim /etc/my.cnf.d/galera.cnf

> wsrep_on=1

> wsrep_provider=/usr/lib64/galera/libgalera_smm.so

> wsrep_cluster_name="aptivalabs"

> wsrep_cluster_address="gcomm:// 192.168.0.48,192.168.0.49,192.168.0.50"

> wsrep_node_name=sr2.aptivalabs

> wsrep_node_address=192.168.0.49

In node sr3 verify that the following parameters are like this:

> **[root@sr3 ~]# vim /etc/my.cnf.d/galera.cnf**

> wsrep_on=1

> wsrep_provider=/usr/lib64/galera/libgalera_smm.so

> wsrep_cluster_name="aptivalabs"

> wsrep_cluster_address="gcomm:// 192.168.0.48,192.168.0.49,192.168.0.50"

> wsrep_node_name=sr3.aptivalabs

> wsrep_node_address=192.168.0.50

Once the configuration has been validated on all nodes, return to node sr1 to create the cluster and activate the service “mariadb.service” previously stopped on all nodes; run the following steps below:

> **[root@sr1 ~]# galera_new_cluster**

The previous instruction creates the cluster and activates the mariadb service, which we will check with the following command:

> **[root@sr1 ~]# systemctl status mariadb.service**

> ● mariadb.service - MariaDB 10.3 database server

> Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)

> Active: active (running) since Thu 2021-07-29 17:20:59 EDT; 8s ago

> Docs: man:mysqld(8)

> https://mariadb.com/kb/en/library/systemd/

> Process: 76770 ExecStartPost=/usr/libexec/mysql-check-upgrade (code=exited, status=0/SUCCESS)

> Process: 76695 ExecStartPre=/usr/libexec/mysql-prepare-db-dir mariadb.service (code=exited, status=0/SUCCESS)

> Process: 76671 ExecStartPre=/usr/libexec/mysql-check-socket (code=exited, status=0/SUCCESS)

> Main PID: 76734 (mysqld)

> Status: "Taking your SQL requests now..."

> Tasks: 35 (limit: 60721)

> Memory: 103.9M

> CGroup: /system.slice/mariadb.service

> └─76734 /usr/libexec/mysqld --basedir=/usr --wsrep-new-cluster

> Jul 29 17:20:58 sr1.aptivalabs systemd[1]: Starting MariaDB 10.3 database server...

> Jul 29 17:20:58 sr1.aptivalabs mysqld[76734]: 2021-07-29 17:20:58 0 [Note] /usr/libexec/mysqld (mysqld 10.3.28-MariaDB) starting as process >

> Jul 29 17:20:59 sr1.aptivalabs systemd[1]: Started MariaDB 10.3 database server.

Activate the mariadb service at startup of the operating system:

> **[root@sr1 ~]# systemctl enable mariadb**

> Created symlink /etc/systemd/system/mysql.service → /usr/lib/systemd/system/mariadb.service.

> Created symlink /etc/systemd/system/mysqld.service → /usr/lib/systemd/system/mariadb.service.

> Created symlink /etc/systemd/system/multi-user.target.wants/mariadb.service → /usr/lib/systemd/system/mariadb.service.

It is then time to enter the sr2 and sr3 nodes to the cluster, simply by starting the mariadb.service service, as shown below:

> **[root@sr2 ~]#  systemctl enable --now mariadb**

> **[root@sr3 ~]#  systemctl enable --now mariadb**

To validate the creation of the cluster, go to node sr3, as shown:

> [root@sr3 ~]# mysql -u root -p

> Enter password:

> Welcome to the MariaDB monitor.  Commands end with ; or \g.

> Your MariaDB connection id is 10

> Server version: 10.3.28-MariaDB MariaDB Server

> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

The following command in MariaDB will allow you to know the status of the cluster:

> MariaDB [(none)]> show status like 'wsrep_cluster_size';

> +--------------------+-------+

> | Variable_name      | Value |

> +--------------------+-------+

> | wsrep_cluster_size | 3     |

> +--------------------+-------+

> 1 row in set (0.002 sec)

The following command in MariaDB will allow you to know more in detail the status of the cluster:

> MariaDB [(none)]> show status like 'wsrep%';

> +-------------------------------+-------------------------------------------------------+

> | Variable_name                 | Value                                                 |

> +-------------------------------+-------------------------------------------------------+

> | wsrep_applier_thread_count    | 1                                                     |

> | wsrep_apply_oooe              | 0.000000                                              |

> | wsrep_apply_oool              | 0.000000                                              |

> | wsrep_apply_window            | 0.000000                                              |

> | wsrep_causal_reads            | 0                                                     |

> | wsrep_cert_deps_distance      | 0.000000                                              |

> | wsrep_cert_index_size         | 0                                                     |

> | wsrep_cert_interval           | 0.000000                                              |

> | wsrep_cluster_conf_id         | 3                                                     |

> | wsrep_cluster_size            | 3                                                     |

> | wsrep_cluster_state_uuid      | 4c7b44a7-f0a7-11eb-b187-032be70fd573                  |

> | wsrep_cluster_status          | Primary                                               |

> | wsrep_cluster_weight          | 3                                                     |

> | wsrep_commit_oooe             | 0.000000                                              |

> | wsrep_commit_oool             | 0.000000                                              |

> | wsrep_commit_window           | 0.000000                                              |

> | wsrep_connected               | ON                                                    |

> | wsrep_desync_count            | 0                                                     |

> | wsrep_evs_delayed             |                                                       |

> | wsrep_evs_evict_list          |                                                       |

> | wsrep_evs_repl_latency        | 0/0/0/0/0                                             |

> | wsrep_evs_state               | OPERATIONAL                                           |

> | wsrep_flow_control_active     | false                                                 |

> | wsrep_flow_control_paused     | 0.000000                                              |

> | wsrep_flow_control_paused_ns  | 0                                                     |

> | wsrep_flow_control_recv       | 0                                                     |

> | wsrep_flow_control_requested  | false                                                 |

> | wsrep_flow_control_sent       | 0                                                     |

> | wsrep_gcomm_uuid              | 6188634d-f0a7-11eb-b68d-727e5b871d11                  |

> | wsrep_gmcast_segment          | 0                                                     |

> | wsrep_incoming_addresses      | 192.168.0.39:3306,192.168.0.46:3306,192.168.0.47:3306 |

> | wsrep_last_committed          | 0                                                     |

> | wsrep_local_bf_aborts         | 0                                                     |

> | wsrep_local_cached_downto     | 18446744073709551615                                  |

> | wsrep_local_cert_failures     | 0                                                     |

> | wsrep_local_commits           | 0                                                     |

> | wsrep_local_index             | 1                                                     |

> | wsrep_local_recv_queue        | 0                                                     |

> | wsrep_local_recv_queue_avg    | 0.000000                                              |

> | wsrep_local_recv_queue_max    | 1                                                     |

> | wsrep_local_recv_queue_min    | 0                                                     |

> | wsrep_local_replays           | 0                                                     |

> | wsrep_local_send_queue        | 0                                                     |

> | wsrep_local_send_queue_avg    | 0.000000                                              |

> | wsrep_local_send_queue_max    | 1                                                     |

> | wsrep_local_send_queue_min    | 0                                                     |

> | wsrep_local_state             | 4                                                     |

> | wsrep_local_state_comment     | Synced                                                |

> | wsrep_local_state_uuid        | 4c7b44a7-f0a7-11eb-b187-032be70fd573                  |

> | wsrep_open_connections        | 0                                                     |

> | wsrep_open_transactions       | 0                                                     |

> | wsrep_protocol_version        | 9                                                     |

> | wsrep_provider_name           | Galera                                                |

> | wsrep_provider_vendor         | Codership Oy <info@codership.com>                     |

> | wsrep_provider_version        | 3.32(rXXXX)                                           |

> | wsrep_ready                   | ON                                                    |

> | wsrep_received                | 4                                                     |

> | wsrep_received_bytes          | 534                                                   |

> | wsrep_repl_data_bytes         | 0                                                     |

> | wsrep_repl_keys               | 0                                                     |

> | wsrep_repl_keys_bytes         | 0                                                     |

> | wsrep_repl_other_bytes        | 0                                                     |

> | wsrep_replicated              | 0                                                     |

> | wsrep_replicated_bytes        | 0                                                     |

> | wsrep_rollbacker_thread_count | 1                                                     |

> | wsrep_thread_count            | 2                                                     |

> +-------------------------------+-------------------------------------------------------+

> 66 rows in set (0.001 sec)

It is time then to test the replication, for this in node sr3 we will create a database which must be replicated in each node of the cluster; We start by creating an example database in sr3, as shown:

> [root@sr3 ~]# mysql -u root -p

> Enter password:

> Welcome to the MariaDB monitor.  Commands end with ; or \g.

> Your MariaDB connection id is 10

> Server version: 10.3.28-MariaDB MariaDB Server

> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

The database is created:

> MariaDB [(none)]> CREATE DATABASE empresa;

> Query OK, 1 row affected (0.007 sec)

We select the database created, and create a table called “alumnos”;

> MariaDB [(none)]> use empresa;

> Database changed

> MariaDB [empresa]> CREATE TABLE alumnos ( Id INT NOT NULL AUTO_INCREMENT, Nombre VARCHAR(100), Sexo INT, PRIMARY KEY(Id));

> Query OK, 0 rows affected (0.022 sec)

A couple of records are inserted into the database and displayed:

> MariaDB [empresa]> insert into alumnos (Nombre, Sexo) values ('Fabian Mestre',1);

> Query OK, 1 row affected (0.004 sec)

> MariaDB [empresa]> insert into alumnos (Nombre, Sexo) values ('Juana Mestre',0);

> Query OK, 1 row affected (0.004 sec)

> MariaDB [empresa]> select * from alumnos;

> +----+---------------+------+

> | Id | Nombre        | Sexo |

> +----+---------------+------+

> |  2 | Fabian Mestre |    1 |

> |  5 | Juana Mestre  |    0 |

> +----+---------------+------+

> 2 rows in set (0.000 sec)

To validate the replication we leave sr3 and go to sr2, there we can see the replicated data thanks to the configuration of the Galera-MariaDB cluster:

> [root@sr2 ~]# mysql -u root -p

> Enter password:

> Welcome to the MariaDB monitor.  Commands end with ; or \g.

> Your MariaDB connection id is 10

> Server version: 10.3.28-MariaDB MariaDB Server

> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

> MariaDB [(none)]> use empresa;

> Reading table information for completion of table and column names

> You can turn off this feature to get a quicker startup with -A

> Database changed

> MariaDB [empresa]> select * from alumnos;

> +----+---------------+------+

> | Id | Nombre        | Sexo |

> +----+---------------+------+

> |  2 | Fabian Mestre |    1 |

> |  5 | Juana Mestre  |    0 |

> +----+---------------+------+

> 2 rows in set (0.001 sec)

> MariaDB [empresa]>

> The following observations are given after the tests carried out:

> •  If the additional nodes are rebooted and the first master is kept on, when the additional nodes come back they will connect to the cluster.

> •  If the first master is turned off, the cluster still remains alive in the two additional nodes

> •  When the master is turned off and any of the nodes are in service, the master starts without problem.

> •  In a cluster of 3, the first master and one of the nodes is turned off, and one node is left on; when the nodes are turned off, the cluster starts without problems.

> •  In a cluster of 3, when the three nodes are turned off and on, or restarted, when starting the cluster nodes, none of the mariadb services come up, therefore the cluster is not deployed and we get into problems. At the date of preparation of this manual, an attempt was made to recover the cluster of three without any success; We will continue to try to detail this anomaly presented, the correct way to recover the cluster will be documented and published.

> CREATING A REPOSITORY WITH LOCAL MEDIA

As follows, it is possible to establish a local software repository using the ISO image with which you installed the operating system:

1.  > Create the / repo folder on your system:

> [root@pruebas ~]# mkdir /repo

2.  > Insert the installation media, be it USB or DVD..

> [root@pruebas ~]# lsblk

> NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT

> sda             8:0    0   50G  0 disk

> |-sda1          8:1    0    1G  0 part /boot

> `-sda2          8:2    0   49G  0 part

> |-rhel-root 253:0    0   44G  0 lvm  /

> `-rhel-swap 253:1    0    5G  0 lvm  [SWAP]

> sr0            11:0    1  8.8G  0 rom

After verifying the devices recognized by the Linux system, we are told that the /dev/sr0 device is the one with the installation ISO.

3.  > **Add the following line** to the /etc/fstab file: "/dev/sr0/repo iso9660 defaults 0 0" and then type "mount -a" **:**

> [root@pruebas ~]# echo "/dev/sr0 /repo iso9660 defaults 0 0" >> /etc/fstab

> [root@pruebas ~]# cat /etc/fstab

> #

> # /etc/fstab

> # Created by anaconda on Thu Dec 17 22:08:06 2020

> #

> …

> …

> /dev/sr0 /repo iso9660 defaults 0 0

> [root@pruebas ~]# mount -a

> mount: /repo: WARNING: device write-protected, mounted read-only.

This last message tells us that the / repo folder is available as read-only. If a list of the folder is made, we will obtain the following information:

> [root@pruebas ~]# ll /repo/

> total 48

> dr-xr-xr-x. 4 root root  2048 Oct  9 05:40 AppStream

> dr-xr-xr-x. 4 root root  2048 Oct  9 05:40 BaseOS

> dr-xr-xr-x. 3 root root  2048 Oct  9 05:40 EFI

> -r--r--r--. 1 root root  8266 Oct  9 05:37 EULA

> -r--r--r--. 1 root root 18092 Oct  9 05:37 GPL

> -r--r--r--. 1 root root  1669 Oct  9 05:37 RPM-GPG-KEY-redhat-beta

> -r--r--r--. 1 root root  5134 Oct  9 05:37 RPM-GPG-KEY-redhat-release

> -r--r--r--. 1 root root  1796 Oct  9 05:40 TRANS.TBL

> -r--r--r--. 1 root root  1455 Oct  9 05:37 extra_files.json

> dr-xr-xr-x. 3 root root  2048 Oct  9 05:40 images

> dr-xr-xr-x. 2 root root  2048 Oct  9 05:40 isolinux

> -r--r--r--. 1 root root   103 Oct  9 05:37 media.repo

> This "mount -a" permanently leaves the link between the /repo folder and the device on your system, in this case a CD/DVD drive. If you remove this medium and enter another, the /repo folder will show other information.

4.  > Create a file in /etc/yum.repos.d/ called repo1.repo and enter the following information:

> [BaseOS]

> name=BaseOS

> baseurl=file:///repo/BaseOS

> gpgcheck=0

5.  > Create a file in /etc/yum.repos.d/ called repo2.repo and enter the following information:

> [AppStream]

> name=AppStream

> baseurl=file:///repo/AppStream

> gpgcheck=0

6.  > Type "yum repolist" to verify repository recognition:

> [root@pruebas yum.repos.d]# yum repolist

> Updating Subscription Management repositories.

> repo id                                      repo name

> AppStream                                    AppStream

> BaseOS                                       BaseOS

> rhel-8-for-x86_64-appstream-rpms             Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)

> rhel-8-for-x86_64-baseos-rpms                Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)

Although repositories are being repeated in this exercise, this scenario is ideal when you lose Internet connection and cannot reach the official Red Hat repositories because you will be using the software that comes in the installation ISO.

> [root@pruebas yum.repos.d]# yum repoinfo

> Updating Subscription Management repositories.

> BaseOS                                                                             44 MB/s | 2.3 MB     00:00

> AppStream                                                                          60 MB/s | 6.3 MB     00:00

> Last metadata expiration check: 0:00:01 ago on Wed 24 Feb 2021 09:35:55 AM -05.

> Repo-id            : AppStream

> Repo-name          : AppStream

> Repo-revision      : 1602239687

> Repo-updated       : Fri 09 Oct 2020 05:34:17 AM -05

> Repo-pkgs          : 5,802

> Repo-available-pkgs: 5,071

> Repo-size          : 7.1 G

> Repo-baseurl       : file:///repo/AppStream

> Repo-expire        : 172,800 second(s) (last: Wed 24 Feb 2021 09:35:55 AM -05)

> Repo-filename      : /etc/yum.repos.d/repo2.repo

> Repo-id            : BaseOS

> Repo-name          : BaseOS

> Repo-revision      : 1602239724

> Repo-updated       : Fri 09 Oct 2020 05:34:52 AM -05

> Repo-pkgs          : 1,696

> Repo-available-pkgs: 1,694

> Repo-size          : 1.1 G

> Repo-baseurl       : file:///repo/BaseOS

> Repo-expire        : 172,800 second(s) (last: Wed 24 Feb 2021 09:35:54 AM -05)

> Repo-filename      : /etc/yum.repos.d/repo1.repo

> AUDIT IN LINUX SYSTEMS

Auditing Linux systems represents a great opportunity to record events related to system security. These audits allow a Linux Administrator to monitor access to the files he decides, to system calls (syscall), to record commands executed by a user, as well as to monitor issues related to the system's firewall. One of the tools that we will use to carry out auditing tasks will be “Audit”. This application compares the events registered in the system with rules that it has previously pre-established..

A system call (syscall - systemcall) refers to the methods used by an application to communicate with the Linux Kernel and have information related to the management of files, system processes and devices.

Audit allows you to generate rules and write them in the system console, rules that are not persistent, but that can be, being registered in /etc/autid/audit.rules. To install "audit" you can do it in the following way:

> [root@pruebas ~]# yum install audit -y

> Updating Subscription Management repositories.

> Last metadata expiration check: 0:53:36 ago on Thu 04 Mar 2021 10:29:20 AM -05.

> Package audit-3.0-0.17.20191104git1c2f876.el8.x86_64 is already installed.

> Dependencies resolved.

> Nothing to do.

> Complete!

As you could see, the package "audit-3.0-0.17" is already installed from the deployment of the operating system. The configuration file for this software is located in /etc/audit/audit.conf. 

> [root@pruebas audit]# pwd

> /etc/audit

> [root@pruebas audit]# ll

> total 12

> -rw-r-----. 1 root root 127 Jan  8  2020 audit-stop.rules

> -rw-r-----. 1 root root 107 Dec 17 17:13 audit.rules

> -rw-r-----. 1 root root 856 Jan  8  2020 **auditd.conf**

> drwxr-x---. 2 root root  49 Dec 17 17:13 plugins.d

> drwxr-x---. 2 root root  25 Dec 17 17:11 rules.d

This file defines the application parameters, parameters that we will be using as we advance in the subject.

The Audit installation generates the “audit” service in the system, as shown:

> [root@pruebas ~]# systemctl --type service | grep audit

> auditd.service                     loaded active running Security Auditing Service

> [root@pruebas ~]# systemctl status auditd.service

> ● auditd.service - Security Auditing Service

> Loaded: loaded (/usr/lib/systemd/system/auditd.service; enabled; vendor preset: enabled)

> Active: active (running) since Thu 2021-03-04 07:17:53 -05; 4h 10min ago

> --- salida omitida ---

> Mar 04 07:17:53 pruebas.aptivalabs augenrules[1081]: lost 0

> Mar 04 07:17:53 pruebas.aptivalabs augenrules[1081]: backlog 4

> Mar 04 07:17:53 pruebas.aptivalabs augenrules[1081]: backlog_wait_time 60000

> Mar 04 07:17:53 pruebas.aptivalabs systemd[1]: Started Security Auditing Service.

Audit provides a way to record relevant information from the system. Based on preconfigured rules, Audit generates log entries to record as much information as possible about the events that are happening on your system. This information is crucial in mission critical environments to identify security policy violators and the actions they took on the system. The following list summarizes some of the information that Audit is able to record in the log files:

> • Date and time, type and result of an event.

> • Association of an event with the identity of the user who triggered the event.

> • All modifications to the Audit configuration and attempts to access /var/log/audit/audit.log.

> • All uses of authentication mechanisms, such as SSH, Kerberos, and others.

> • Changes to any trusted database, such as / etc / passwd.

> • You try to import or export information to or from the system.

> • Include or exclude events based on user identity and other attributes.

Audit consists of two main parts: the applications and utilities in the user space, and on the kernel side, the processing of system calls. The kernel component receives system calls from applications in user space and filters them through one of the following filters: user, task, fstype, or exit.

By default, Audit stores the log entries in the /var/log/audit/audit.log file; if the rotation is activity in the configuration file, the rotated audit.log files are stored in the same directory.

AUDIT RULES WITH AUDIT

For the establishment of rules, Audit uses the command "auditctl", let's look at an example:

> [root@pruebas ~]# auditctl -w /etc/ssh/sshd_config -p warx -k sshd_config

The previous instruction uses certain parameters of the "auditctl" command, which are explained below:

*   > -w indicates the file or directory to be audited

*   > -p indicates the actions to be audited on the audit object (w-write, r-read, x-execute and change attributes)

*   > -k indicates a keyword for the results report

We will try to see the content of this file from a standard user, in this case the user "fmestre"; If the Audit service is running, in /var/log/audit/audit.log we must observe the record that the user “fmestre” tried to read the contents of the file; let's see:

> [root@pruebas ~]# su - fmestre

> [fmestre@pruebas ~]$ cat /etc/ssh/sshd_config

> cat: /etc/ssh/sshd_config: Permission denied

This audit event should generate four (4) records in the log file, as shown below:

> [root@pruebas ~]# tail -n 4 /var/log/audit/audit.log

> type=SYSCALL msg=audit(1614886599.538:116): arch=c000003e syscall=257 success=no exit=-13 a0=ffffff9c a1=7ffce1e84647 a2=0 a3=0 items=1 ppid=2622 pid=2668 auid=0 uid=1000 gid=1000 euid=1000 suid=1000 fsuid=1000 egid=1000 sgid=1000 fsgid=1000 tty=pts1 ses=3 comm="cat" exe="/usr/bin/cat" subj=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023 key="sshd_config"ARCH=x86_64 SYSCALL=openat AUID="root" UID="fmestre" GID="fmestre" EUID="fmestre" SUID="fmestre" FSUID="fmestre" EGID="fmestre" SGID="fmestre" FSGID="fmestre"

> type=CWD msg=audit(1614886599.538:116): cwd="/home/fmestre"

> type=PATH msg=audit(1614886599.538:116): item=0 name="/etc/ssh/sshd_config" inode=1993961 dev=fd:00 mode=0100600 ouid=0 ogid=0 rdev=00:00 obj=system_u:object_r:etc_t:s0 nametype=NORMAL cap_fp=0 cap_fi=0 cap_fe=0 cap_fver=0 cap_frootid=0OUID="root" OGID="root"

> type=PROCTITLE msg=audit(1614886599.538:116): proctitle=636174002F6574632F7373682F737368645F636F6E666967

The above event consists of four records, which share the same timestamp (in unixtime format) and serial number. Records always start with the keyword "type =". Each record consists of multiple name = value pairs separated by a blank space or a comma, such as the line “type = CWD msg = audit (1614886599.538: 116): cwd =" /home/fmestre "”.

On the website https://www.unixtimestamp.com/ you can convert this timestamp to a human readable format, showing you a result like the following:

![](Image00041.jpg) 

type=SYSCALL → In this example, the SYSCALL value specifies that this record was generated by a syscall to the kernel.

type=CWD → This type is used to record the working directory from which the process that invoked the specified system call in which the first record was executed.

type=PATH → An audit event contains a PATH record for each path that is passed to the syscall as an argument. In this audit event, only one path (/etc/ssh/sshd_config) was used as an argument.

type=PROCTITLE →   the PROCTITLE value specifies that this record provides the command that triggered this audit event, this number is in hexadecimal. A look at this command could expand the report a bit more:

> [root@pruebas ~]# ausearch -i | grep PROCTITLE

> ---

> type=PROCTITLE msg=audit(03/04/21 14:36:39.538:116) : proctitle= **cat /etc/ssh/sshd_config**

We can see that the command that generated the security event was the "cat /etc/ssh/ sshd_config".

You could create various audit rules on important files on your file system, as well as rules based on auditing system calls by applications, how you use Audit depends on the scenario you want to contemplate. Some example rules could be the following:

> [root@pruebas ~]# auditctl -w /etc/passwd -p wa -k passwd_changes

> [root@pruebas ~]# auditctl -w /etc/selinux/ -p wa -k selinux_changes

> [root@pruebas ~]# auditctl -a always,exit -F arch=b64 -S adjtimex -S settimeofday -k time_change

The last statement tells Audit to raise an audit event every time an application uses the "system calls" called "adjtimex" and "settimeofday" on systems that use 64-bit architectures. To list the rules uploaded to Audit you could send the following instruction:

> [root@pruebas ~]# auditctl -l

> -w /etc/passwd -p wa -k passwd_changes

To delete a temporary rule made with Autid look at the following instructions:

> [root@pruebas ~]# auditctl -l

> -w /etc/passwd -p wa -k passwd_changes

> [root@pruebas ~]# auditctl -W /etc/passwd -p wa -k passwd_changes

> [root@pruebas ~]# auditctl -l

> No rules

In the previous statement, the parameter "-W" was used to stop looking at the /etc/passwd file.

PERSISTENT AUDIT RULES

If you require that the rules established for Audit be persistent, you must insert them into the /etc/audit/rules.d/audit.rules file, without, the location shown as follows:

> [root@pruebas rules.d]# pwd

> /etc/audit/rules.d

> [root@pruebas rules.d]# ll

> total 4

> -rw-------. 1 root root 244 Dec 17 17:11 audit.rules

A look at the file "audit.rules" shows us some persistent rules:

> [root@pruebas rules.d]# cat audit.rules

> --- salida omitida ---

> ## Set failure mode to syslog

> -f 1

> -w /etc/passwd -p wa -k passwd_changes

> -w /etc/selinux/ -p wa -k selinux_changes

> -w /sbin/insmod -p x -k module_insertion

> -a always,exit -F arch=b64 -S adjtimex -S settimeofday -k time_change

RULES PRESET IN AUDIT

In the path /usr/share/audit/sample-rules it is possible to observe files whose content results in preconfigured rules to be inserted into Autid and that the software begins to perform audits based on them, as shown below:

> [root@pruebas ~]# cd /usr/share/audit/sample-rules

> [root@pruebas sample-rules]# ll

> total 156

> -rw-r--r--. 1 root root  244 Jan  8  2020 10-base-config.rules

> -rw-r--r--. 1 root root  284 Jan  8  2020 10-no-audit.rules

> -rw-r--r--. 1 root root   93 Jan  8  2020 11-loginuid.rules

> -rw-r--r--. 1 root root  333 Jan  8  2020 12-cont-fail.rules

> -rw-r--r--. 1 root root  327 Jan  8  2020 12-ignore-error.rules

> --- salida omitida ---

We can see the content of some of these files as follows:

> [root@pruebas sample-rules]# cat 30-stig.rules

> ## The purpose of these rules is to meet the stig auditing requirements

> ## These rules depends on having 10-base-config.rules & 99-finalize.rules

> ## installed.

> --- skipped output ---

> -a always,exit -F arch=b32 -S adjtimex,settimeofday,stime -F key=time-change

> -a always,exit -F arch=b64 -S adjtimex,settimeofday -F key=time-change

> -a always,exit -F arch=b32 -S clock_settime -F a0=0x0 -F key=time-change

> -a always,exit -F arch=b64 -S clock_settime -F a0=0x0 -F key=time-change

For Audit to recognize the content of these rules, it is only necessary to copy the corresponding file to /etc/audit/rules.d and reload the configuration, as shown in the following instruction:

> [root@pruebas sample-rules]# cp 30-stig.rules /etc/audit/rules.d

> [root@pruebas sample-rules]# augenrules --load

> No rules

> enabled 1

> failure 1

> pid 1061

> rate_limit 0

> backlog_limit 8192

> lost 0

> backlog 4

> backlog_wait_time 60000

> --- salida omitida ---

> [root@pruebas sample-rules]# auditctl -l

> -a always,exit -F arch=b32 -S stime,settimeofday,adjtimex -F key=time-change

> -a always,exit -F arch=b64 -S adjtimex,settimeofday -F key=time-change

> -a always,exit -F arch=b32 -S clock_settime -F a0=0x0 -F key=time-change

> -a always,exit -F arch=b64 -S clock_settime -F a0=0x0 -F key=time-change

> -w /etc/localtime -p wa -k time-change

> -w /etc/group -p wa -k identity

> -w /etc/passwd -p wa -k identity

> -w /etc/gshadow -p wa -k identity

> -w /etc/shadow -p wa -k identity

> -w /etc/security/opasswd -p wa -k identity

> -a always,exit -F arch=b32 -S sethostname,setdomainname -F key=system-locale

> --- omited ---

GENERATION OF REPORTS WITH AUDIT

To generate audit reports, Audit has the “aureport” tool. "Aureport" is a tool that produces summary reports from the audit system records. Different types of reports will be displayed to give you an idea of ​​the types of reports that can be generated.:

Report based on user authentication:

> [root@pruebas ~]# aureport -au

> Authentication Report

> ============================================

> # date time acct host term exe success event

> ============================================

> 159\. 03/03/21 11:37:22 fmestre pruebas.aptivalabs pts/0 /usr/bin/su yes 93

> 160\. 03/03/21 11:41:10 curri pruebas.aptivalabs pts/0 /usr/bin/su yes 103

> 161\. 03/03/21 11:42:40 root 192.168.0.35 ssh /usr/sbin/sshd yes 119

> 162\. 03/03/21 11:45:17 curri pruebas.aptivalabs tty1 /usr/bin/login yes 143

> 163\. 03/03/21 14:34:17 root ? ? /usr/libexec/cockpit-session yes 71

> 164\. 03/03/21 14:52:18 root 192.168.0.35 ssh /usr/sbin/sshd yes 96

> 165\. 03/03/21 17:52:23 root 192.168.0.35 ssh /usr/sbin/sshd yes 64

> 166\. 03/04/21 07:18:39 root 192.168.0.35 ssh /usr/sbin/sshd yes 68

> --- omited ---

System event report:

> [root@pruebas ~]# date

> Fri Mar  5 07:57:29 -05 2021

> [root@pruebas ~]# systemctl start httpd

> [root@pruebas ~]# aureport -e

> Event Report

> ===================================

> # date time event type auid success

> ===================================

> 13857\. 03/05/21 07:58:13 137 SERVICE_START -1 yes

> 13858\. 03/05/21 07:58:13 138 SERVICE_START -1 yes

Executable File Usage Summary:

> [root@pruebas ~]# aureport -x --summary

> Executable Summary Report

> =================================

> total  file

> =================================

> 9540  /usr/lib/systemd/systemd

> 2359  /usr/sbin/sshd

> 496  /usr/libexec/platform-python3.6

> 306  /usr/libexec/gdm-session-worker

> 173  /usr/sbin/auditctl

> 166  /usr/lib/systemd/systemd-update-utmp

> 98  /usr/bin/su

> 64  /usr/bin/pidof

> --- omited ---

Summary Report of Failed Events:

> [root@pruebas ~]# aureport --failed

> Failed Summary Report

> ======================

> Range of time in logs: 12/17/20 17:22:49.437 - 03/05/21 08:04:07.724

> Selected time for report: 12/17/20 17:22:49 - 03/05/21 08:04:07.724

> Number of changes in configuration: 0

> Number of changes to accounts, groups, or roles: 2

> Number of logins: 0

> Number of failed logins: 5

> Number of authentications: 0

> Number of failed authentications: 0

> Number of users: 3

> Number of terminals: 8

> Number of host names: 3

> Number of executables: 17

> Number of commands: 12

> Number of files: 12

> Number of AVC's: 143

> Number of MAC events: 0

> Number of failed syscalls: 149

> Number of anomaly events: 0

> Number of responses to anomaly events: 0

> Number of crypto events: 0

> Number of integrity events: 0

> Number of virt events: 0

> Number of keys: 2

> Number of process IDs: 50

> Number of events: 172

Summary of Failed Events by User:

> [root@pruebas ~]# aureport -u --failed --summary -i

> Failed User Summary Report

> ===========================

> total  auid

> ===========================

> 83  unset

> 80  fmestre

> 9  root