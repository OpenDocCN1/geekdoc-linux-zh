

## 管理任务

### 图 6–13
/proc/scsi/scsi 文件。

```bash
root@Styx (/proc/scsi)
[root@Styx scsi]# cd /proc/scsi
[root@Styx scsi]# cat scsi
Attached devices:
Host: scsi0 Channel: 00 Id: 06 Lun: 00
  Vendor: QUANTUM Model: DLX7000  Rev: 2150
  Type:  Sequential-Access
Host: scsi2 Channel: 00 Id: 06 Lun: 00
  Vendor: NEC  Model: CD-ROM DRIVE:466 Rev: 1.06
  Type:  CD-ROM
Host: scsi3 Channel: 00 Id: 00 Lun: 00
  Vendor: DELL  Model: PERC/RAID RAID5  Rev: V1.0
  Type:  Direct-Access
[root@Styx scsi]# 
```

```bash
mt -f /dev/st0 rewind
# Perform an incremental backup of the /home directory.
tar cvglpf /dev/st0 /home
# Unload the tape
mt -f /dev/st0 offline
```

在周二执行以下命令：

```bash
# Tuesday's backup
# Rewind the tape
mt -f /dev/st0 rewind
# Skip the first file on the tape. (Skip over Monday's backup.)
mt -f /dev/st0 fsf 1
tar cvglpf /dev/st0 /home
mt -f /dev/st0 offline
```

在周三执行以下命令：

```bash
# Wednesday's backup
# Rewind the tape
mt -f /dev/st0 rewind
# Skip the first two files on the tape. (Skip over Monday's and Tuesday's backups.)
mt -f /dev/st0 fsf 2
tar cvglpf /dev/st0 /home
mt -f /dev/st0 offline
```

在周四执行以下命令：

```bash
# Thursday's backup
# Rewind the tape
mt -f /dev/st0 rewind
# Skip the first three files on the tape. (Skip over Monday's through
# Wednesday's backup)
mt -f /dev/st0 fsf 3
tar cvglpf /dev/st0 /home
mt -f /dev/st0 offline
```

在周五执行以下命令以执行完整备份：

```bash
# Friday's backup - Use a new tape or an old tape to overwrite.
# Rewind the tape
mt -f /dev/st0 rewind

# Perform a full backup.
tar cvglpf /dev/st0 /home
mt -f /dev/st0 offline
```

## SHELL 编程

在计算机中输入信息时，你有两种选择——命令行或图形用户界面。对于新手用户来说，GUI 更容易使用，但它不具备命令行接口的强大功能。Shell 编程能发挥命令行接口的真正威力。

想象一下使用 GUI 或 useradd 命令输入数百个新用户。这对管理员来说可能是一个非常耗时且繁琐的任务。Shell 编程使这项任务变得容易得多。

Shell 编程通过 shell 脚本来完成。顾名思义，shell 脚本是一组 shell 命令的列表。Linux 还有其他 shell 可用，例如 csh 和 korn，但默认 shell 是 bash。每种 shell 都有自己的脚本语言，但这些不同的 shell 非常相似。在许多情况下，为一种 shell 编写的 shell 脚本可以在另一种 shell 中运行。

许多 Linux 启动脚本实际上就是 shell 脚本。因此，如果需要修改 Linux，理解 shell 脚本是必要的。

### 构建 Shell 脚本

bash shell 脚本的结构非常简单。编写 shell 脚本只需要三样东西。

- 1. shell 脚本需要第一行来标识用于运行它的 shell 名称。默认情况下 Linux 使用 bash，因此第一行是 **#!/bin/bash**
  #! 字符是特殊字符，它们让内核知道这是一个 shell 脚本。/bin/bash 条目告诉内核 shell 程序的位置。如果 shell 程序不在指定位置，运行脚本时将显示 **Command not found** 错误。在这种情况下，发出命令 **whereis bash** 来查找 bash。此命令将返回 bash 命令的所有位置。
- 2. 编写成功脚本需要的第二件事是让脚本有一些要执行的操作。这可以是几乎任何命令行语句；例如，**echo Hello World**。在这种情况下，echo 命令显示一行文本，Hello World。
- 3. 创建脚本所需的最后一步是更改创建的文件权限以允许执行。如果创建的文件名为 **hello**，设置执行权限的命令是 **chmod +x hello**。

要创建此脚本，使用 vi 编辑器输入步骤 1 和 2 中描述的行；然后将文件保存为名为 **hello** 的文件。退出编辑器，然后执行步骤 3 中的命令以更改文件权限。

要运行脚本，从包含 hello 文件的目录输入 **./hello** 命令。

图 6–14 显示了输入了脚本的 vi 屏幕。

### 图 6-14
使用 vi 创建脚本。

```bash
#!/bin/bash
echo Hello World
```

图 6-15 显示了用于更改权限并执行 hello 脚本的命令。

### 图 6-15
更改权限并运行脚本。

```bash
[root@localhost root]# ls -l
total 104
-rw-r--r-- 1 root root 1544 Aug 22 23:29 anaconda-ks.cfg
-rw-r--r-- 1 root root 30 Oct 6 21:00 hello
-rw-r--r-- 1 root root 20654 Aug 22 23:21 install.log
-rw-r--r-- 1 root root 4223 Aug 22 23:21 install.log.syslog
-rw-r--r-- 1 root root 53760 Oct 5 22:57 jsmith-backup.cpio
drwxr-xr-x 2 root root 4096 Sep 11 21:10 screenshots

[root@localhost root]# chmod +x hello

[root@localhost root]# ls -l
total 104
-rw-r--r-- 1 root root 1544 Aug 22 23:29 anaconda-ks.cfg
-rwxr-xr-x 1 root root 30 Oct 6 21:00 hello
-rw-r--r-- 1 root root 20654 Aug 22 23:21 install.log
-rw-r--r-- 1 root root 4223 Aug 22 23:21 install.log.syslog
-rw-r--r-- 1 root root 53760 Oct 5 22:57 jsmith-backup.cpio
drwxr-xr-x 2 root root 4096 Sep 11 21:10 screenshots

[root@localhost root]# ./hello
Hello World
[root@localhost root]#
```

### Shell 脚本变量和参数

使用脚本的一个优点是，你可以在脚本执行前向脚本传递值。例如，如果你希望 hello 脚本显示 "Hello" 和一个名字，你可以更改脚本并按如下方式执行它：

```bash
./hello Jeff
```

名字 Jeff 将是 hello 脚本的一个**参数**。

脚本中的**变量**是一个被分配了值的标记。例如，hello 脚本的消息可以分配给变量 MSG，然后 MSG 可以在脚本内的任何命令中使用。

**参数** 命令行参数在执行时传递给脚本。参数的值通过参数符号 $（美元符号）和表示参数在行中位置的数字获取。例如，如果按照前面描述将名字传递给 hello 脚本，值被分配给参数字变量 $1。

- 要将 hello 程序改为使用参数，请遵循这些步骤：
  1. 将文件 hello 复制到 hello2，这样你就不必更改原始文件。
     ```bash
     cp hello hello2
     ```
     hello2 脚本将具有与 hello 脚本相同的权限。
  2. 编辑 hello2 脚本以反映以下更改：
     ```bash
     #!/bin/bash
     echo Hello $1
     ```
     $1 将被替换为命令行中使用的参数的值。
  3. 执行脚本，将命令行参数 *Jeff* 传递给脚本。例如，如果你输入 `/hello2 Jeff`，将显示 "Hello Jeff"。

允许在命令行上使用多个参数。例如，如果你希望向名为 args 的脚本传递四个参数，你可以使用以下语法：*args arg1 arg2 arg3 arg4*。要向 hello 脚本传递四个名字，你可能会输入 /hello3 Jeff Jones Sally Smith。

- 要将 hello 程序改为使用四个参数，请遵循这些步骤：
  1. 将文件 hello 复制到 hello3，这样你就不必更改原始文件。
     ```bash
     cp hello hello3
     ```
  2. 编辑 hello3 脚本以反映以下更改：
     ```bash
     #!/bin/bash
     echo Hello $2, $1
     echo Hello $4, $3
     ```
  3. 执行脚本，将四个参数 *Jeff*、*Jones*、*Sally* 和 *Smith* 传递给 hello3 脚本。例如：
     ```bash
     ./hello3 Jeff Jones Sally Smith
     ```
     结果应该是：
     ```bash
     Hello Jones, Jeff
     Hello Smith, Sally
     ```

注意，*literal* 值 Hello 和逗号 (,) 在脚本中标记的地方显示。

### 变量

所有编程语言和大多数脚本语言都支持变量。变量是脚本内被分配值的标记。变量和参数之间的区别可以通过值分配的方式看到。参数根据其在行中的位置从命令行分配值。值分配后，只能通过重新运行脚本才能更改它。变量在脚本内通过分配符号分配其值。变量可以在脚本内通过编程改变。

要在 hello 脚本中用变量 HW 替换字面量 "Hello World"，你可以这样做：

- 1. 将文件 hello 复制到 hello4，这样你就不必更改原始文件。
  ```bash
  cp hello hello4
  ```
- 2. 对 hello4 脚本进行以下更改。
  ```bash
  #!/bin/bash
  HW = "Hello World"
  echo $HW
  ```
  使用赋值符号 =（等号）将 "Hello World" 分配给变量 HW。脚本中的变量通常按惯例使用全大写，但这不是强制性的。当你引用变量时，在前面加上 $（美元符号）以表明它是一个变量而不是字面量值。

