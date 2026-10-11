
## Fixed driver ver – 0day

Let’s take a look at our target system to see if that particular version of the driver is installed.

To begin, we will list the contents of the **Program Files** directory, in search of the USBPcap directory:

```text
C:\Users\n00b> cd "C:\Program Files"

C:\Program Files> dir
...
08/13/2015  04:04 PM    <DIR>          MSBuild
07/14/2009  06:52 AM    <DIR>          Reference Assemblies
01/24/2018  02:30 AM    <DIR>          USBPcap
12/22/2017  04:11 PM    <DIR>          VMware
04/12/2011  04:16 AM    <DIR>          Windows Defender
...
```

As we can see, there is a **USBPcap** directory in C:\Program Files. However, keep in mind that the driver directory is often found under C:\Windows\System32\DRIVERS. Let’s inspect the contents of **USBPcap.inf** [537] to learn more about the driver version:

```text
C:\Program Files\USBPcap> type USBPcap.inf
[Version]
Signature    = "$WINDOWS_NT$"
Class        = USB
ClassGuid    = {36FC9E60-C465-11CF-8056-444553540000}
DriverPackageType = ClassFilter
Provider     = %PROVIDER%
CatalogFile.NTx86  = usbpccpx86.cat
CatalogFile.NTamd64 = usbpccpamd64.cat
DriverVer=18/02/2015,1.1.0.8

[DestinationDirs]
DefaultDestDir = 12
...
```

Based on the version information, our driver should be vulnerable. Before we try to exploit it, we first have to compile the exploit since it’s written in C.

### 18.2.6.1 Compiling C/C++ Code on Windows

The vast majority of exploits targeting kernel-level vulnerabilities (including the one we have selected) are written in a low-level programming language such as C or C++ and therefore require compilation. Ideally, we would compile the code on the platform version it is intended to run on. In those cases, we would simply create a virtual machine that matches our target and compile the code there. However, we can also cross-compile the code on an operating system entirely different from the one we are targeting. For example, we could compile a Windows binary on our Kali system.

![](img/ec25e59d75726b7041242a56d3376832_556_0.png)

For the purposes of this module however, we will use Min gw-w64, [538] which provides us with the GCC compiler on Windows.

Since our Windows client has Min gw-w64 pre-installed, we can run the min gw-w64.bat script that sets up the PATH environment variable for the gcc executable. Once the script is finished, we can execute gcc.exe to confirm that everything is working properly:

```text
C:\Program Files \ mingw-w64 \ i686-7.2.0-posix-dwarf-rt_v5-rev1> mingw-w64.bat
C:\Program Files\mingw-w64\i686-7.2.0-posix-dwarf-rt_v5-rev1>echo off
Microsoft Windows [Version 10.0.10240]
(c) 2015 Microsoft Corporation. All rights reserved.

C:\> gcc
gcc: fatal error: no input files
compilation terminated.

C:\> gcc --help
Usage: gcc [options] file...
Options:
--pass-exit-codes          Exit with highest error code from a phase.
--help                     Display this information.
--target-help              Display target specific command line options.
--help={common|optimizers|params|target|warnings[=^
{joined|separate|undocumented}]}
{common|optimizers|params|target|warnings[=^
Display specific types of command line options.
(Use '-v --help' to display command line options of sub-processes).
--version                  Display compiler version information.
...
```
*Listing 581 - gcc works after running min gw-w64.bat*

Good. The compiler seems to be working. Now let's transfer the exploit code to our Windows client and attempt to compile it. Since the author did not mention any particular compilation options, we will try to run gcc without any arguments other than specifying the output file name with -o:

```text
C:\Windows\system32\cmd.exe
C:\Users\admin\Desktop>gcc 41542.c -o exploit.exe
41542.c: In function 'main':
41542.c:175:80: warning: passing argument 4 of 'NtAllocateVirtualMemory' from incompatible pointer type [WinIncompatible-pointer-type]
 allocstatus = NRAllocateVirtualMemory(INVALID_HANDLE_VALUE, &Base_addr, 0, &Size, MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
41542.c:175:80: note: expected 'PULONG (aka long unsigned int *)' but argument is of type 'int **'
41542.c:212:15: warning: implicit declaration of function 'getch'; did you mean 'getc'? [-Wimplicit-function-declaration]
 getch();
 getch
C:\Users\admin\Desktop>dir
 Volume in drive C has no label.
 Volume Serial Number is 9E6A-47F8
 Directory of C:\Users\admin\Desktop
 09/16/2019 06:34 AM <DIR> .
 09/16/2019 06:34 AM <DIR> ..
 09/16/2019 06:20 AM 8,546 41542.c
 09/16/2019 06:34 AM 52,980 exploit.exe
 2 File(s) 61,534 bytes
 2 Dir(s) 2,750,805,376 bytes free
C:\Users\admin\Desktop>
```
*Figure 291: Compiling the exploit using gcc*

Despite two warning messages [539], the exploit compiled successfully and gcc created the **exploit.exe** executable. If the process had generated an error message, the compilation would have aborted and we would have to attempt to fix the exploit code and recompile it.

Now that we have compiled our exploit, we can transfer it to our target machine and attempt to run it. In order to determine if our privilege escalation was successful, we can use the **whoami** command before and after running our exploit:

![](img/ec25e59d75726b7041242a56d3376832_558_0.png)
*Figure 292: Elevating privileges on Windows through a privilege escalation exploit*

Great! We have successfully elevated our privileges from admin-pc\n00b to nt authority\system, [540] which is the Windows account with the highest privilege level.

## 18.3 Linux Privilege Escalation Examples

In this section, we will turn our attention to Linux-based targets. We will discuss Linux privileges and demonstrate a few common Linux-based privilege escalation techniques.

### 18.3.1 Understanding Linux Privileges

Before discussing privilege escalation techniques, let's take a moment to briefly discuss Linux privileges, access controls, and users.

One of the defining features of Linux and other UNIX derivatives is that most resources, including files, directories, devices, and even network communications are represented in the filesystem. [541]

Put colloquially, “everything is a file”. Every file (and by extension every element of a Linux system) abides by user and group permissions [542] based on three primary abilities: read, write, and execute.

### 18.3.2 Insecure File Permissions: Cron Case Study

As we turn our attention to privilege escalation techniques, we will first leverage insecure file permissions. As with our Windows examples, we will assume that we have already gained access to our Linux target machine as an unprivileged user.

In order to leverage insecure file permissions, we must locate an executable file that not only allows us write access but also runs at an elevated privilege level. On a Linux system, the cron [543] time-based job scheduler is a prime target, as system-level scheduled jobs are executed with root user privileges and system administrators often create scripts for cron jobs with insecure permissions.

For the purpose of this example, we will SSH to our dedicated Debian client. In a previous section, we showed where to look on the filesystem for installed cron jobs on a target system. We could also inspect the cron log file (*var/log/cron.log*) for running cron jobs:

```text
student@debian:~$ grep "CRON" /var/log/cron.log
Jan27 15:55:26 victim cron[719]: (CRON) INFO (pidfile fd = 3)
Jan27 15:55:26 victim cron[719]: (CRON) INFO (Running @reboot jobs)
....
Jan27 17:45:01 victim CRON[2615]: (root) CMD (cd /var/scripts/ &&& . /user_backups.sh)
Jan27 17:50:01 victim CRON[2631]: (root) CMD (cd /var/scripts/ &&& . /user_backups.sh)
Jan27 17:55:01 victim CRON[2656]: (root) CMD (cd /var/scripts/ &&& . /user_backups.sh)
Jan27 18:00:01 victim CRON[2671]: (root) CMD (cd /var/scripts/ &&& . /user_backups.sh)
```
*Listing 582 - Inspecting the cron log file*

It appears that a script called *user_backups.sh* under */var/scripts/* is executed in the context of the root user. Judging by the timestamps, it seems that this job runs once every five minutes.

Since we know the location of the script, we can inspect its contents and permissions.

```bash
student@debian:~$ cat /var/scripts/user_backups.sh
#!/bin/bash

cp -rf /home/student/ /var/backups/student/

student@debian:~$ ls -lah /var/scripts/user_backups.sh
-rwxrwxrwx- 1 root root 52 Jan 27 17:02 /var/scripts/user_backups.sh
```
*Listing 583 - Showing the content and permissions of the user_backups.sh script*

The script itself is fairly straight-forward: it simply copies the student user’s **home** directory to the **backups** subdirectory. The permissions [544] of the script reveal that every local user can write to the file.

[537] (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-hardware/drivers/install/overview-of-inf-files
[538] (Mingw-w64, 2019), https://mingw-w64.org/doku.php
[539] (GCC, 2019), https://gcc.gnu.org/onlinedocs/gcc/Warnings-and-Errors.html
[541] (Ubuntu, 2013). https://help.ubuntu.com/community/FilePermissions
[542] (Ubuntu, 2013). https://help.ubuntu.com/community/FilePermissions
[543] (Wikipedia, 2019). https://en.wikipedia.org/wiki/Cron
[544] (Arch Linux, 2019). https://wiki.archlinux.org/index.php/File_permissions_and_attributes
