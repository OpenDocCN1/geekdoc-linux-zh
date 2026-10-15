
```
C:\Users\n0b> cd "C:\Program Files"

C:\Program Files dir

08/13/2015 04:04 PM <DIR> MSBuild
07/14/2009 06:52 AM <DIR> Reference Assemblies
01/24/2018 02:30 AM <DIR> USBPcap
```

正如我们所见，`C:\Program Files` 中没有 `USBPcap` 文件夹。然而，我们应该检查通常位于驱动程序的 `System32` 目录。

```
C:\Users\n0b> cd "C:\Windows\System32"

C:\Windows\System32 dir USBPcap

11/20/2010 12:37:52 AM 2,176 <> USBPcap.sys
```

我们在 `System32` 目录中找到了 `USBPcap.sys` 驱动程序。现在让我们检查驱动程序的版本：

```
C:\Users\n0b> driverquery /v | findstr /i USBCap
```

输出显示驱动版本为 1.1.0.0。这与我们找到找到漏洞所需的版本匹配。

```
C:\Users\n0b> driverquery /v | findstr /i USBCap
Module Name            : USBCap
Display Description     : USBCap Service
Type                   : KERNELDRIVER
Start                 : 0x00 (SERVICE_BOOT_START)
```

现在我们可以开始利用漏洞。该利用涉及触发 `USBCcap` 驱动中的空指针引用，允许我们以内核权限执行代码。我们将使用从 `Exploit-DB` 找到漏洞代码并在 Windows 上进行编译。

```bash
C:\Users\n0b> gcc -o exploit.exe exploit.c
```

编译完成后，我们将运行漏洞以获取 `SYSTEM` 权限。

```bash
C:\Users\n0b> exploit.exe
```

如果利用成功，我们将获得一个 `SYSTEM` shell。然后可以使用此 shell 在目标系统上执行进一步的操作。

# 攻击性安全

www.offensecurity.com

# 基于 Kali Linux 2.0 的渗透测试

```
C:\Users\admin\Desktop>gcc 4152.c -o exploit
4152.c:15:5: error in function 'main'
4152.c:17:170: warning: passing argument 4 of 'NtAllocateVirtualMemory' from incompatible pointer type [incompatible pointer type]
alloc = NtAllocateVirtualMemory(INVALID_HANDLE_VALUE, Abase, 0, &size, MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READ)
4152.c:17:180: warning: expected 'ULONG' (as long unsigned int) but argument is of type '*'
4152.c:22:115: warning: implicit declaration of function 'getc'; did you mean 'getc'? [implicit-function-declaration]
getch();
getc
c:\Users\admin\desktop>
Volume in C has no label.
Volume Serial Number is 9E6A-7F78
Directory of C:\Users\admin\desktop
09/16/2019 06:34 AM    <DIR>
09/16/2019 06:34 AM    <DIR>
09/16/2019 06:29 AM    4152.c                52,988 bytes
09/16/2019 06:29 AM    exploit.exe         61,534 bytes
09/16/2019 06:29 AM    2 Dir(s)         2,758,089,376 bytes free
c:\Users\admin\desktop->
```

> 图 21：使用 `gcc` 成功编译漏洞利用程序

尽管有两个警告信息，漏洞利用程序仍然成功编译，`gcc` 创建了漏洞的可执行文件。如果该过程生成了错误消息，编译将终止，我们必须尝试修复漏洞程序并重新编译。

现在我们已经编译了漏洞程序，可以将其传输到目标机器并尝试运行它。为了确定我们的权限提升是否成功，我们可以在运行漏洞程序的前后使用 `whoami` 命令。

539 (GCC, 2019), https://gcc.gnu.org/onlinedocs/gcc/Warnings-and-Errors.html

PWK 2.0 版权 © Offensive Security Ltd. 保留所有权利。564

# 基于 Kali Linux 2.0 的渗透测试

![](img/f99f528ca9845f4c256ce54e882b1345_564_0.png)

图 292：通过权限提升漏洞在 Windows 上提升权限

太好了！我们成功地将权限从 `admin-pc-n00b` 提升到了 `nt authority\system`，这是 Windows 中权限最高的账户。

## 18.3 权限提升示例

在本节中，我们将注意力转向基于 Linux 的目标。我们将讨论 Linux 权限并演示一些基于 Linux 的权限提升技术。

### 18.3.1 理解 Linux 权限

在讨论权限提升技术之前，让我们花一点时间简要讨论 Linux 权限、访问控制和用户。

Linux 及其衍生系统的定义特征之一是大多数资源（包括文件、目录、设备甚至网络通信）都在文件系统中表示出来。

> 540 (Microsoft, 2018), msdn.microsoft.com/en-us/library/windows/desktop/ms684190(v=vs.85) aspx

541 (Arch Linux, 2019), https://wiki.archlinux.org/index.php/users_and_groups

PWK 2.0 版权 © Offensive Security Ltd. 保留所有权利。565

# 攻击性安全

用俗语来说，“一切皆文件”（通过此类推，Linux 系统的每一个元素）都遵循基于三个主要属性的用户和用户组权限：读取、写入和执行。

### 18.3.2 不安全的文件权限：Cron 案例研究

当我们把注意力转向权限提升技术时，首先将利用不安全的文件权限。在 Windows 示例中，我们假设已经以非特权用户的身份访问了 Linux 目标机器。

为了利用不安全的文件权限，我们必须找到一个不仅允许写入访问而且以高权限运行的文件。在 Linux 系统上，基于 `cron` 的调度器是一个首要目标，系统级计划任务是以 `root` 权限执行的。

为了本示例的目的，我们将 `SSH` 到我们的 Debian 客户端。在之前的节中，我们展示了在目标系统中哪里查找 `cron` 任务。我们也可以检查日志文件 (`/var/log/cron.log`) 中的 `cron` 任务：

```
student@debian:- grep "CRON" /var/log/cron.log
Jan 27 15:55:26 cron[719]: (CRON) INFO (pid = 3)
Jan 27 15:55:26 cron[719]: (CRON) INFO (Running)
Jan 27 17:45:01 cron[2615]: (ROOT) CMD (cd /var/scripts && ./userbackups.sh)
Jan 27 17:50:01 cron[2621]: (ROOT) CMD (cd /var/scripts && ./userbackups.sh)
Jan 27 17:55:01 cron[2656]: (ROOT) CMD (cd /var/scripts && ./userbackups.sh)
Jan 27 18:00:01 cron[2671]: (ROOT) CMD (cd /var/scripts && ./userbackups.sh)
```

似乎位于 `/var/scripts/` 下的脚本 `user_backups.sh` 在 `root` 用户的上下文中执行。由于我们知道脚本的位置，可以检查它的权限，并且该任务每五分钟运行一次。
