
嗯，默认情况下为每个文件设置全局执行权限对所有人都没有意义，对吧？目录需要执行权限（否则你无法进入它们），但文件不需要，因此它们不会获得执行权限。因此是 `rw-r--r--`。

除了显示默认权限外，`umask` 还可以用于更改当前 shell 会话的权限。例如，如果我们使用命令：

```
$ umask u=rwx,g=rwx,o=
```

每个新目录都将继承权限 `rwxrwx---`，每个文件为 `rw-rw---`（因为它们不会获得执行权限）。如果你重复上面的示例来创建 `testfile` 和 `testdir` 并检查权限，你应该得到：

```
$ ls -lhd test*
drwxrwx--- 2 carol carol 4,0K jul 13 22:25 testdir
-rw-rw---- 1 carol carol   0 jul 13 22:25 testfile
```

如果你在检查 `umask` 时不使用 `-S`（符号模式）参数，你会得到：

```
$ umask
0007
```

结果看起来不熟悉，因为使用的值不同。下面是一个包含每个值及其相应含义的表格：

| 值 | 文件权限 | 目录权限 |
| :--- | :--- | :--- |
| 0 | rw- | rwx |
| 1 | rw- | rw- |
| 2 | r-- | r-x |
| 3 | r-- | r-- |
| 4 | -w- | -wx |
| 5 | -w- | -w- |
| 6 | --- | --x |
| 7 | --- | --- |

正如你所见，`007` 对应 `rwxrwx---`，正如我们请求的那样。前导零可以忽略。

### 特殊权限

除了针对用户、组和其他用户的读取、写入和执行权限外，每个文件还可以拥有其他三种*特殊权限*，这些权限可以改变目录的工作方式或程序的运行方式。它们可以在符号模式或八进制模式下指定，如下所示：

#### 粘滞位

粘滞位（sticky bit），也称为*受限删除标志*，八进制值为 1，在符号模式下由其他用户权限中的 `t` 表示。这仅适用于目录，对普通文件没有影响。在 Linux 上，它阻止用户删除或重命名目录中的文件，除非他们拥有该文件或目录。

设置了粘滞位的目录在 `ls -l` 的输出中，*其他用户*权限中的 `x` 会被 `t` 取代：

```
$ ls -ld Sample_Directory/
drwxr-xr-t 2 carol carol 4096 Dec 20 18:46 Sample_Directory/
```

在八进制模式下，特殊权限使用 4 位表示法指定，第一位代表要操作的特殊权限。例如，要在八进制模式下为目录 `AnOther_Directory` 设置粘滞位（值 1），权限为 755，命令应为：

```
$ chmod 1755 AnOther_Directory
$ ls -ld AnOther_Directory
drwxr-xr-t 2 carol carol 4,0K Dec 20 18:46 AnOther_Directory
```

#### Set GID

Set GID（又称 SGID 或 Set Group ID 位），八进制值为 2，在符号模式下由*组*权限中的 `s` 表示。这可以应用于可执行文件或目录。在文件上，它使进程以拥有该文件的组的权限运行。当应用于目录时，它使在其下创建的每个文件或目录继承父目录的组。

带有 SGID 位的文件和目录在 `ls -l` 的输出中，*组*权限中的 `x` 会被 `s` 取代：

```
$ ls -l test.sh
-rwxr-sr-x 1 carol root 33 Dec 11 10:36 test.sh
```

要在符号模式下为文件添加 SGID 权限，命令应为：

```
$ chmod g+s test.sh
$ ls -l test.sh
-rwxr-sr-x 1 carol root 33 Dec 11 10:36 test.sh
```

以下示例将帮助你更好地理解 SGID 对目录的影响。假设我们有一个名为 `Sample_Directory` 的目录，由用户 `carol` 和组 `users` 拥有，具有以下权限结构：

```
$ ls -ldh Sample_Directory/
drwxr-xr-x 2 carol users 4,0K Jan 18 17:06 Sample_Directory/
```

现在，让我们切换到该目录，并使用命令 `touch` 在其中创建一个空文件。结果将是：

```
$ cd Sample_Directory/
$ touch newfile
$ ls -lh newfile
-rw-r--r-- 1 carol carol 0 Jan 18 17:11 newfile
```

我们可以看到，文件由用户 `carol` 和组 `carol` 拥有。但是，如果目录设置了 SGID 权限，结果将会不同。首先，让我们为 `Sample_Directory` 添加 SGID 位并检查结果：

```
$ sudo chmod g+s Sample_Directory/
$ ls -ldh Sample_Directory/
drwxr-sr-x 2 carol users 4,0K Jan 18 17:17 Sample_Directory/
```

组权限中的 `s` 表示已设置 SGID 位。现在，我们将切换到该目录，再次使用 `touch` 命令创建一个空文件：

```
$ cd Sample_Directory/
$ touch emptyfile
$ ls -lh emptyfile
-rw-r--r-- 1 carol users 0 Jan 18 17:20 emptyfile
```

文件所属的组是 `users`。这是因为 SGID 位使文件继承了其父目录的组所有者，即 `users`。

#### 设置 UID

SUID，也称为 Set User ID（设置用户 ID），其八进制值为 4，在符号模式下通过用户权限中的 `s` 表示。它仅适用于文件，对目录没有影响。其行为与 SGID 位类似，但进程将以文件所有者的权限运行。带有 SUID 位的文件在 `ls -l` 的输出中，其用户权限上的 `x` 会被替换为 `s`：

```bash
$ ls -ld test.sh
-rwsr-xr-x 1 carol carol 33 Dec 11 10:36 test.sh
```

你可以在一个参数中组合多个特殊权限。因此，要在八进制模式下为权限为 755 的脚本 `test.sh` 设置 SGID（值为 2）和 SUID（值为 4），你应该输入：

```bash
$ chmod 6755 test.sh
```

结果将是：

```bash
$ ls -lh test.sh
-rwsr-sr-x 1 carol carol 66 Jan 18 17:29 test.sh
```

> **提示**
>
> 如果你的终端支持颜色，而现在的终端大多都支持，你可以通过查看 `ls -l` 的输出快速判断这些特殊权限是否已设置。对于粘滞位（sticky bit），目录名可能以黑色字体显示在蓝色背景上。同样适用于带有 SGID（黄色背景）和 SUID（红色背景）位的文件。颜色可能因你使用的 Linux 发行版和终端设置而异。

### 引导练习

1. 使用命令 `mkdir emptydir` 创建一个名为 `emptydir` 的目录。现在，使用 `ls` 列出目录 `emptydir` 的权限。

2. 使用命令 `touch emptyfile` 创建一个名为 `emptyfile` 的空文件。现在，使用符号模式的 `chmod`，为文件 `emptyfile` 的所有者添加执行权限，并移除其他所有人的写入和执行权限。请使用一条 `chmod` 命令完成此操作。

3. 如果 `umask` 值设置为 `027`，文件的默认权限是什么？

4. 假设一个名为 `test.sh` 的文件是一个 shell 脚本，具有以下权限和所有权：
```
-rwxr-sr-x 1 carol root       33 Dec 11 10:36 test.sh
```
- 文件所有者的权限是什么？
- 使用八进制表示法，`chmod` 的语法应该是什么才能“取消”授予此文件的特殊权限？

5. 考虑这个文件：
```
$ ls -l /dev/sdb1
brw-rw---- 1 root disk 8, 17 Dec 21 18:51 /dev/sdb1
```
`sdb1` 是什么类型的文件？谁可以向其写入？

6. 考虑以下 4 个文件：
