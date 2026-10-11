
# journalctl -k

Logs begin at Sun 2019-06-09 18:59:23 EDT, end at

Sun 2019-10-20 18:11:06 EDT.

Oct 19 11:43:04 localhost.localdomain kernel:

Linux version 5.0.9-301.fc30.x86_64

(mockbuilt+dkms-0.4.20190312-fedoraproject.org)

(gcc version 9.2.120190312 (Red Hat 9.0.1-0.1 (GCC))

#1 SMP Wed Apr 23 05:37:35 UTC

Oct 19 11:43:04 localhost.localdomain kernel: Command line:

boot=dev/mapper;vmlinuz-5.0.9-301.fc30.x86_64

root=/dev/mapper/fedora-live-root root

resume=/dev/mapper/fedora-localhost-live-swap

rd.lv=fedora-localhost-live/root

rd.lv=fedora-localhost-live/rhgb quiet

要查看特定服务的消息，请使用 `-u` 选项后跟服务名称以查看该服务的所有消息，例如所示：

```bash
# journalctl -u NetworkManager.service
# journalctl -u httpd.service
# journalctl -u avahi-daemon.service
```

如果你认为正在发生安全入侵，可以在消息进入时实时查看所有或选定的消息，添加 `-f` 选项（完成后按 Ctrl+C）：

```bash
# journalctl -k -f
# journalctl -f -u NetworkManager.service
```

要仅检查启动消息，你可以列出所有系统启动的列表，然后显示所选启动项的特定启动项：

```bash
# journalctl --list-boots
-3 6b968e820df345a781cb6935d483374c
Sun 2019-08-25 12:42:08 EDT-Mon 2019-08-26 14:30:53 EDT
-2 2fc5a74fbe9b4c1laec06ac1c24e89b
```

## 第五部分：学习 Linux 安全技术

```text
Mon 2019-09-02 15:43:03 EDT-2019-09-12 13:08:26 EDT
-1 5d26eecfb7481a9e4a3dd7f8a0a0
Sun 2019-10-13 12:30:27 EDT-2019-10-17 13:37:22 EDT
-0c88e7f472492
```

# 第 22 章：理解基础 Linux 安全性

为了使用 John the Ripper 测试用户密码，你必须首先使用 `unshadow` 命令提取名称和密码。这些信息需要被重定向到一个文件中供 john 运行，如下所示：

```
# unshadow /etc/passwd /etc/shadow > password.file
```

现在，使用你喜喜欢的文本编辑器编辑 `password.file`，删除任何没有密码的账户。由于一次只让 John the Ripper 测试几个账户是明智之举，请删除任何你当前不想测试的账户。

**注意**

`john` 实用程序极度消耗 CPU。它将自己的 `nice` 值设置为 19 以降低其优先级。然而，在非生产系统上或在非高峰时段运行它，并且一次只处理几个账户，是明智的。

现在使用 `john` 命令尝试破解密码。要对创建的密码文件运行 john，请执行命令 `filename`。在下面的代码段中，你可以看到运行 john 处理示例 `password.file` 的输出。为了演示之目的，示例文件中只留了一个账户。此外，该账户 Samantha 使用了错误的密码 password。你可以看到 John the Ripper 破解该密码花了多长时间。

```
# password.file
Loaded 1 hash (crypt (3) [?])password (Samantha)
guesses: 1 time: 00:00:44 100% (2) c/s: 20.87
trying 12345 - miss
Use the "show" to display all of the
acked passwords reliably
```

为了证明强密码有多重要，请考虑当 Samantha 的账户密码从 password 改为 Password1234 时会发生什么。尽管 Password1234 是一个弱密码，但破解它需要的时间超过 7 天的 CPU 时间。在接后的代码中，john 最终被终止以结束破解尝试。

```
# passwd Samantha
Changing password for user Samantha.
...
```

```
# password.file
Loaded 1 password hash (generic crypt (3) [?])
...
time: 00:21:55 (3) c/s: 119 trying: tth675 - tth787
Session aborted
```

一旦密码破解完成，应从系统中删除 `password.file`。要了解更多关于 John the Ripper 的信息，请访问 www.openwall.com/john。

# 监控文件系统

恶意程序经常修改文件。它们还可以尝试通过伪装成普通文件和程序来掩盖踪迹。然而，可以通过后续章节使用的各种监控策略来发现它们。

# 第五部分：学习 Linux 安全软件包

# 验证软件软件包

通常，如果你从标准存储库安装软件包或下载信誉良好的软件包，将不会遇到任何问题。但双检已安装的软件软件包以查看它们是否被破坏始终是好的。完成此操作的命令是 `rpm -V package_name`。

当你验证软件时，会将已安装软件包的信息与 rpm 数据库中的软件包元数据（参见第 10 章“获取和管理软件”）进行比较。如果没有问题，`rpm -V` 命令将返回空内容。然而，如果存在差异，你将得到一个编码列表。表 22.5 显示了所使用的代码以及差异的描述。

## 表 22.5 软件包验证差异

| 代码 | 差异 |
|---|---|
| S | 文件大小 |
| M | 文件权限和类型 |
| 5 | MD5 校验 |
| D | 设备文件的主号和次号 |
| L | 符号链接 |
| U | 用户所有权 |
| G | 组所有权 |
| T | 文件修改时间 (mtime) |
| P | 此软件包依赖的其他已软件包（又称能力） |

在接下来的列表中，所有安装的软件包都经过了验证检查。你可以看到返回代码 5、S 和 T，这表示存在潜在问题。

```
# rpm -qV
5S.T.... c /etc/hba.conf
      ...T.... /lib/modules/3.2.1-3-fc16.1686/modules.devname
      ...T.... /lib/modules/3.2.1-3-fc16.1686/modules.softdep
```

你不需要验证所有的软件包。你可以一次只验证一个软件包。例如，如果你想验证 nmap 软件包，只需输入 `rpm -V nmap` 即可。

要在 Ubuntu 上验证软件包，你需要安装 `debsums` 实用程序。它默认没有安装。要安装 `debsums`，使用命令 `sudo apt-get install debsums`。检查所有已安装的软件包，使用 `debsums -a` 命令。检查一个软件包，输入 `debsums packagename`。

# 扫描文件系统

除非你最近更新了系统，否则二进制文件不应由于任何原因被修改。`find` 和 `rpm -V` 等命令可以帮助你判断二进制文件是否被篡改。

要检查二进制文件的修改，`find` 可以使用文件的修改时间或 `mtime`。文件的 `mtime` 是文件内容最后一次修改的时间。还可以查找文件的创建/更改时间，或 `ctime`。

如果你怀疑有恶意活动，可以快速扫描文件系统，查看今天是否有任何二进制文件被修改或更改（昨天，取决于你认为入侵发生在何时）。要做到这一点，请使用 `find` 命令。

在下面的示例中，对 `/sbin` 目录进行了扫描。如果任何二进制文件在 24 小时内被修改，则使用 `find /sbin -mtime -1`。使用 `stat` 命令显示如下：

```
# find /sbin -mtime -1
/sbin/init
/sbin
reboot/halt
halt stat / stat/init
```
