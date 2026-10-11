

## 密码审计

每当您需要检查当前文件状态的完整性时，只需发出以下命令：

```
[ramon]$ /usr/TSS/bin/tripwire --check
```

这将导致报告写入标准输出（stdout），并保存到 `REPORTFILE` 环境变量指定的文件位置（参见列表 3.6）。

如果您希望以电子邮件形式接收报告，请使用以下前一命令的变体：

```
[ramon]$ /usr/TSS/bin/tripwire --check --email-report
```

审查完报告后，您可以通过将新的完整性结果写入数据库来确认已注意到任何完整性差异。使用以下命令执行此操作：

```
[ramon]$ /usr/TSS/bin/tripwire --update
```

最后，当您更改策略文件时，需要使用以下命令强制 tripwire 重新加载其策略定义：

```
[ramon]$ /usr/TSS/bin/tripwire --update-policy
```

> **提示**：我建议您每天至少运行两次 tripwire，并在更新签名数据库之前仔细检查完整性报告。理想情况下，您只需将 `tripwire --check --email-report` 命令添加到 cron 作业中。该命令应在早晨第一时间执行，并在系统管理员下班前 shortly 执行。

跟踪日志并确保文件完整性可以显著增强您的服务器安全性，但很容易陷入“外酥里软”的困境。当今大多数 Linux 服务器最薄弱的环节是用户，更具体地说，是他们选择密码的方式。虽然您的安全策略应始终包含一节关于良好密码特性的说明，但您还应采取积极主动的方式对待密码安全，并定期对所有用户的密码进行审计。

与其他 Unix 系统一样，Linux 密码存储为对原始明文密码执行单向 DES 加密操作的结果。（某些 Linux 系统还支持 MD5 散列用于密码保护。）这意味着实际密码永远不会以明文形式存储。每当用户尝试登录系统时，登录程序会对输入的密码进行加密，并将结果与 `/etc/passwd`（或 `/etc/shadow`）中找到的结果进行比较。只有当两个密码匹配时，才允许用户访问系统。

Linux 有几种可用的密码审计工具。这些工具以加密的密码文件作为输入，并通过发起*字典攻击*来尝试猜测每个用户的密码，即将一组常用单词逐一进行 DES 加密，并将结果与 `/etc/passwd` 条目进行比较。如果找到匹配项，则记录用户名并将其包含在输出报告中供安全管理员参考。

本节介绍这些工具之一的 John the Ripper，它是作为 Openwall 项目（www.openwall.com）的一部分开发的。

## John the Ripper

John the Ripper 是原始 crack 程序的替代方案，它是一个强大的密码猜测工具，使用自己的例程来尝试破解密码，而不是使用 Linux `crypt(3)` 系统调用。这使得它比早期版本的 crack 工具具有明显的性能优势。另一个优点是 John the Ripper 可以在多种平台（大多数 Unix、DOS 和 Windows 系统）上运行，因此您可以使用网络中的其他机器来尝试破解 Linux 服务器的密码。

通过使用 John the Ripper 尝试猜测您自己的用户密码，您可以提醒他们他们选择了太短或太弱的密码，并敦促他们在拥有相同工具的攻击者猜中密码并入侵其账户之前更改密码。

## 安装 john

john 的安装非常简单。从 www.openwall.com/john 下载它（没有 RPM 形式），解压缩并展开存档（参见列表 3.7 中的*步骤*）。一旦将源代码展开到自己的目录中，进入 `src` 目录并运行 `make` 命令。请注意，您有几种目标可执行文件的选项（输入不带参数的 `make` 以查看选项）。列表 3.7 显示了在 i386 架构上为 ELF 格式可执行文件的构建过程。

### 列表 3.7 安装和编译 *john*

```bash
[ramon]$ ls -l john-1.6.tar.gz
-rw-r--r-- 1 ramon users 497354 Oct 3 19:27 john-1.6.tar.gz
[ramon]$ gunzip john-1.6.tar.gz
[ramon]$ tar xf john-1.6.tar
[ramon]$ cd john-1.6
[ramon]$ ls
README doc run src
[ramon]$ cd src
[ramon]$ make
To build John the Ripper, type:
make SYSTEM
where SYSTEM can be one of the following:
  linux-x86-any-elf     Linux, x86, ELF binaries
  linux-x86-mmx-elf     Linux, x86 with MMX, ELF binaries
  linux-x86-k6-elf      Linux, AMD K6, ELF binaries
  linux-x86-any-a.out   Linux, x86, a.out binaries
  linux-alpha           Linux, Alpha
  linux-sparc           Linux, SPARC
  generic               Any other UNIX system with gcc
[ramon]$ make linux-x86-any-elf
In -sf x86-any.h arch.h
make .. /run/john .. /run/unshadow .. /run/unafs .. /run/unique \
JOHN_OBJS="DES_fmt.o DES_std.o BSDI_fmt.o MD5_fmt.o MD5_std.o\ 
BF_fmt.o BF_std.o AFS_fmt.o LM_fmt.o batch.o bench.o charset.o\ 
common.o compiler.o config.o cracker.o external.o formats.o\ 
gotopt.o idle.o inc.o John.o list.o loader.o logger.o math.o\ 
memory.o misc.o options.o params.o path.o recovery.o rpp.o\ 
rules.o signals.o single.o status.o tty.o wordlist.o unshadow.o\ 
unafs.o unique.o x86.o \ \
CFLAGS="-c -Wall -02 -fomit-frame-pointer -m486"
make[1]: Entering directory `/home/ramon/john-1.6/src'
gcc -c -Wall -02 -fomit-frame-pointer -m486 -funroll-loops DES_fmt.c
gcc --c - DES_fmt.o DES_std.o BSDI_fmt.o MD5_fmt.o MD5_std.o BF_fmt.o\ 
BF_std.o AFS_fmt.o LM_fmt.o batch.o bench.o charset.o\ 
common.o compiler.o config.o cracker.o external.o formats.o\ 
gotopt.o idle.o inc.o john.o list.o loader.o logger.o math.o\ 
memory.o misc.o options.o params.o path.o recovery.o rpp.o\ 
rules.o signals.o single.o status.o tty.o wordlist.o unshadow.o\ 
unafs.o unique.o x86.o -o .. /run/john
In -s john .. /run/unshadow
In -s john .. /run/unafs
In -s john .. /run/unique
make[1]: Leaving directory `/home/ramon/john-1.6/src'
[ramon]$ ls -1 .. /run/john
-rwxr-xr-x 1 ramon users 148428 Oct 3 19:59 .. /run/john
There is no make installation step, so simply copy the executable to the appropriate place in your filesystem using the following command:
[ramon]$ sudo cp .. /run/john /usr/local/bin
```

## 配置 john

所有配置参数都保存在 `john.ini` 文件中，调用 **john** 时当前目录中必须存在该文件。该文件可以配置四个环境变量：

- `wordfile`：`**wordfile**` 变量是包含用于批处理模式破解密码的词列表的文件。
- `idle`：当设置为 `Y` 时，`**idle**` 变量强制 **john** 仅使用空闲 CPU 周期。如果您需要在生产服务器上运行 **john**，我推荐此设置。默认值为 `N`。
- `save`：`**save**` 变量是崩溃恢复文件的延迟（以秒为单位）。该文件包含到目前为止已完成工作的检查点，以防中断。默认值为 `600`。
- `beep`：当 `**beep**` 变量设置为 `Y` 时，**john** 每次成功破解密码时都会发出哔声。默认值为 `N`。

以下是包含这些环境变量的示例 **john.ini** 文件的 **[Options]** 部分：

```ini
[ramon]$ more john.ini
#
# This file is part of John the Ripper password cracker,
# Copyright (c) 1996-98 by Solar Designer
#
[Options]
# Wordlist file name, to be used in batch mode
Wordfile = ~/password.lst
# Use idle cycles only
Idle = N
# Crash recovery file saving delay in seconds
Save = 600
# Beep when a password is found (who needs this anyway?)
Beep = N
```

## 运行 john

通过不带选项调用 `john`，您可以让 `john` 生成足够的随机尝试来破解密码：

```
[ramon]$ john /etc/passwd
```

或者，您可以提供常用词列表供 `john` 尝试。词列表可以是文件；以下示例使用文件 `my_guesses`：

```
[ramon]$ john -wordfile:my_guesses /etc/passwd
```

第三种选择是，词列表可以通过 `stdin` 以管道方式输入，如下面的命令所示：

```
[ramon]$ cat my_guesses | john -stdin /etc/passwd
```

请注意，通常 `john` 运行时间较长，并且在运行过程中会将其发现的内容写入 `~/john.pot` 文件。如果您想查看 `john` 目前破解的密码，请发出以下命令：

```
[ramon]$ john -show /etc/passwd
```

另外，如果您使用影子密码，您需要将 `/etc/passwd` 和 `/etc/shadow` 合并到一个文件中，以便 `john` 能正常工作。（有关影子密码的信息，请参见第 2 章，“系统安装和设置”。）当作为 `unshadow` 调用时，`john` 可执行文件可以执行此转换。首先使用以下命令创建符号链接：

```
[ramon]$ sudo ln -s /usr/local/bin/john /usr/local/bin/unshadow
```

然后使用以下命令通过 `unshadow` 脚本调用这两个文件：

```
[ramon]$ unshadow /etc/passwd /etc/shadow > mypasswd
```

现在您有了一个文件（`mypasswd`），可以通过 `john` 尝试破解：

```
[ramon]$ john mypasswd
```

尽管 `john` 工具在当前形式下非常稳定，但它仍在积极开发中，新版本通常会带来性能的巨大提升。定期检查网站 www.openwall.com 以查找更新。

