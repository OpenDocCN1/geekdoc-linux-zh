
```
student@debian:-$ cat /var/scripts/user_backups.sh
#!/bin/bash
cp -rf /home/student/* /var/backups/student/

student@debian:-$ ls -lah /var/scripts/user_backups.sh
-rw-r--r-- 1 root root 522 Jan 27 17:02 /var/scripts/user_backups.sh
```

脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。

由于我们可以检查脚本的权限，且该任务每五分钟运行一次（注：原文此处有重复或乱码，翻译按原文逻辑处理）。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。

```
student@debian:-$ cat /var/scripts/user_backups.sh
#!/bin/bash
cp -rf /home/student/* /var/backups/student/

student@debian:-$ ls -lah /var/scripts/user_backups.sh
-rw-r--r-- 1 root root 522 Jan 27 17:02 /var/scripts/user_backups.sh
```

脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。由于我们可以检查脚本的权限，且该任务每五分钟运行一次（注：原文此处有重复或乱码，翻译按原文逻辑处理）。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。

脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身简单。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单。

```
student@debian:-$ cat /var/scripts/user_backups.sh
#!/bin/bash
cp -rf /home/student/* /var/backups/student/
```

（注：原文此处存在大量重复文本）

# 基于 Kali Linux 2.0 的渗透测试

![](img/f99f528ca9845f4c256ce54e882b1345_564_0.png)

太好了！我们成功地将权限从 `admin-pc-n00b` 提升到了 `nt authority\system`，这是 Windows 中权限最高的账户。

## 18.3 权限提升示例

在本节中，我们将注意力转向基于 Linux 的目标。我们将讨论 Linux 权限并演示一些基于 Linux 的权限提升技术。

### 18.3.1 理解 Linux 权限

在讨论权限提升技术之前，让我们花一点时间简要讨论 Linux 权限、访问控制和用户。

Linux 及其衍生系统的定义特征之一是大多数资源（包括文件、目录、设备甚至网络通信）都在文件系统中表示出来。

# 攻击性安全

用俗语来说，“一切皆文件”（通过此类推，Linux 系统的每一个元素）都遵循基于三个主要属性的用户和用户组权限：读取、写入和执行。

### 18.3.2 不安全的文件权限：Cron 案例研究

当我们把注意力转向权限提升技术时，首先将利用不安全的文件权限。在 Windows 示例中，我们假设已经以非特权用户的身份访问了 Linux 目标机器。

为了利用不安全的文件权限，我们必须找到一个不仅允许写入访问而且以高权限运行的文件。在 Linux 系统上，基于 `cron` 的调度器是一个首要目标，系统级计划任务是以 `root` 权限执行的。

为了本示例的目的，我们将 SSH 到我们的 Debian 客户端。在之前的节中，我们展示了在目标系统中哪里查找 `cron` 任务。我们也可以检查日志文件 (`/var/log/cron.log`) 中的 `cron` 任务：

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

```
student@debian:-$ cat /var/scripts/user_backups.sh
#!/bin/bash
cp -rf /home/student/* /var/backups/student/

student@debian:-$ ls -lah /var/scripts/user_backups.sh
-rw-r--r-- 1 root root 522 Jan 27 17:02 /var/scripts/user_backups.sh
```

脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。由于我们可以检查脚本的权限，且该任务每五分钟运行一次。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单；它只是简单地将学生目录的内容复制到 `/var/backups/student/`。脚本本身非常简单。

（此处省略重复内容）

# 基于 Kali Linux 2.0 的渗透测试

```
student@debian:-$ echo "root2:..."
```
