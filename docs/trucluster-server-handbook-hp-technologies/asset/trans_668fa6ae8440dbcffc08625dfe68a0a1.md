

## 5.4.1 从安装 CD 启动

在我们实际从 Tru64 UNIX 安装 CD 启动之前（该 CD 名称为 Compaq Tru64 UNIX Version 5.1A Operating System Volume 1），让我们先初始化系统。在控制台提示符下，使用 init 命令。

```
P00>>> init
```

让我们通过在控制台提示符下使用 “show device” 命令来识别我们将要启动的 CDROM。

```
P00>>> show device
dqa62.1.0.0.7.1      $1$DGA62          HSG80   V86F
dkc0.0.0.0.7.0     DKC0              COMPAQ BD009635CB BDC4
dqa0.0.0.1.0.5.0    DQA0              CD-224E 9.5B ← CDROM
dva5.0.0.0.0.0      DVA0
eia0.0.0.0.9.1      EIA0              00-50-8B-AE-PB-DC
pga0.0.0.0.7.1      PGA0              WWN 2000-0000-c924-3514
pka0.7.0.6.0        PKA0              SCSI Bus ID 7
pkb0.7.0.1.0.6.0    PKB0              SCSI Bus ID 7
pkc0.7.0.7.0        PKC0              SCSI Bus ID 7
```

现在我们已经识别出 CDROM，让我们启动 Tru64 UNIX 操作系统 CD 并开始安装。

### CAUTION：

继续之前，请确保您已在第 4 章中执行了必要的准备步骤，例如设置环境变量和安装最新的固件。

```
P00>>> boot dqa0
...
*** Performing CDROM Installation
```

## 5.4.2 开始安装

从 Tru64 UNIX 操作系统安装 CD 启动后，您必须做出的第一个决定如下：

```
Remember, you can always get extra information by typing help.

1) U.S. English Installation
2) Installation with Worldwide Language Support
3) Exit Installation

Enter your choice: 1
```

通过选择“1”，我们选择执行 Tru64 UNIX 的“U.S. English Installation”。

> **NOTE:**
> 
> 如果您使用的是非 GUI 安装程序，并且需要在安装磁盘上使用自定义磁盘标签，您将选择选项“3”并按照第 4.2.1 节所述继续标记磁盘。

## 5.4.3 完整安装的设置信息

安装程序会提示输入构建系统所需的信息，如以下输出所示。

```
Enter a password to use as the root (superuser) password.
Be sure to remember this password, because it is needed to
log in as the user “root” following installation.  The
password must be at least six characters long, and at least
one of the first eight characters must be a number, special
character, or uppercase letter (A-Z).

Enter root password: xxxxxxxx
Retype root password: xxxxxxxx
```

安装软件做的第一件事之一，除了询问您想要什么类型的安装外，就是提示输入 root 密码。虽然我们鼓励为任何计算机系统上的任何用户使用“good and strong passwords”³，但对于 root 用户来说尤其重要。而且请，请不要把你的密码写在便签上并贴在显示器上！

```
Choose a hostname for this system. The hostname identifies the
system on the network. The hostname must start with a letter,
and may include letters, numbers, periods and hyphens.

Enter the hostname for this system: molari
```

接下来，我们会被提示输入我们正在安装的系统的主机名。

接下来的几个提示是用于选择系统所在的位置和区域（或时区）。

```
Select the location that best describes your site. This is to
determine what time zone your site is in. If your location includes
multiple time zones (for example, Asia), the next question will
ask you which of those you want.

 1) Africa        7) Australia     13) Etc          19) MST
 2) America       8) CET           14) Europe       20) MST7MDT
 3) Antarctica    9) CST6CDT       15) Factory      21) PST8PDT
 4) Arctic       10) EET           16) HST          22) Pacific
 5) Asia         11) EST           17) Indian       23) SystemV
 6) Atlantic     12) EST5EDT       18) MET          24) WET
```

```
Enter your choice: 12
```

接下来，您将被提示输入日期和时间。

```
Enter the current date (as mm/dd/[cc]yy): 08/17/2002
```

```
Enter the current time in 24-hour format (as hh:mm): 23:22
```

```
The date and time has been set to: Sat Aug 17 23:22:00 EDT 2002
Is this correct (y/n)? y
```

> ³ “good and strong password” 是指包含大小写字母和数字的密码。在安装的这个阶段，仅支持基础安全，因此只有密码的前八个字符才有意义。

## Chapter 5

