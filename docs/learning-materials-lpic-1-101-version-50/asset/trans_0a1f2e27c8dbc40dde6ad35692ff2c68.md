
## 设置 UID

SUID，也称为 Set User ID（设置用户 ID），其八进制值为 4，在符号模式下通过用户权限中的 `s` 表示。它仅适用于文件，对目录没有影响。其行为与 SGID 位类似，但进程将以文件所有者的权限运行。带有 SUID 位的文件在 `ls -l` 的输出中，其用户权限上的 `x` 会被替换为 `s`：

```bash
$ ls -ld test.sh
-rwsr-xr-x 1 carol carol 33 Dec 11 10:36 test.sh
```

你可以在一个参数中组合多个特殊权限。因此，要在八进制模式下为权限为 755 的脚本 test.sh 设置 SGID（值为 2）和 SUID（值为 4），你应该输入：

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

   ```
   drwxr-xr-t 2 carol carol 4,0K Dec 20 18:46 Another_Directory
   ---r--r--  1 carol carol     0 Dec 11 10:55 foo.bar
   -rw-rw-r--  1 carol carol 1,2G Dec 20 18:22 HugeFile.zip
   drwxr-sr-x  2 carol users  4.0K Jan 18 17:26 Sample_Directory
   ```

   使用四位表示法的八进制模式，写下每个文件和目录对应的权限。

### 探索练习

1. 在终端上尝试以下操作：使用命令 `touch emptyfile` 创建一个名为 `emptyfile` 的空文件。现在，使用 `chmod 000 emptyfile` 将文件的权限“清零”。如果在八进制模式下只传递 *一个* 值给 `chmod` 来更改 `emptyfile` 的权限，例如 `chmod 4 emptyfile`，会发生什么？如果使用两个值，如 `chmod 44 emptyfile`，又会发生什么？我们可以从 `chmod` 读取数值的方式中学到什么？
2. 考虑 Linux 系统中临时目录的权限，`/tmp`：

   ```
   $ ls -l /tmp
   drwxrwxrwt 19 root root 16K Dec 21 18:58 tmp
   ```

   用户、组和其他人都具有完整权限。但是普通用户可以删除此目录内的 *任何* 文件吗？为什么会这样？
3. 一个名为 `test.sh` 的文件具有以下权限：`–rwsr-xr-x`，这意味着 SUID 位已设置。现在，运行以下命令：

   ```
   $ chmod u-x test.sh
   $ ls -l test.sh
   -rwsr-xr-x 1 carol carol 33 Dec 11 10:36 test.sh
   ```

   我们做了什么？大写的 S 意味着什么？
4. 如何创建一个名为 Box 的目录，使其中的所有文件自动由组 users 拥有，并且只能由创建它们的用户删除？

### 总结

在本课中，你学习了如何使用 `ls` 获取（并解码）关于文件权限的信息，如何使用 `chmod` 控制或更改谁可以创建、删除或修改文件（包括八进制和符号模式），如何使用 `chown` 和 `chgrp` 更改文件的所有权，以及如何查询和更改文件和目录的默认权限掩码 `umask`。

本课中讨论了以下命令：

- **ls**：列出文件，可选地包含详细信息，如权限。
- **chmod**：更改文件或目录的权限。
- **chown**：更改文件或目录的所有者用户和/或组。
- **chgrp**：更改文件或目录的所有者组。
- **umask**：查询或设置文件和目录的默认权限掩码。

## 引导练习答案

1. 使用命令 `mkdir emptydir` 创建一个名为 `emptydir` 的目录。现在，使用 `ls` 列出目录 `emptydir` 的权限。

   在 `ls` 中添加 `-d` 参数可以查看目录的文件属性，而不是列出其内容。因此，答案是：

   ```text
   ls -l -d emptydir
   ```

   如果你将这两个参数合并为一个，如 `ls -ld emptydir`，则可以获得额外分数。

2. 使用命令 `touch emptyfile` 创建一个名为 `emptyfile` 的空文件。现在，使用符号模式的 `chmod`，为文件 `emptyfile` 的所有者添加执行权限，并移除其他所有人的写入和执行权限。请使用一条 `chmod` 命令完成此操作。

   请这样思考：

   - “为文件所有者 (u) 添加 (+) 执行 (x) 权限”，即 u+x。
   - “为组 (g) 和其他用户 (o) 移除 (-) 写入 (w) 和执行 (x) 权限”，即 go-wx。

   要合并这两组权限，我们在它们之间添加一个逗号。因此，最终结果是：

   ```text
   chmod u+x,go-wx emptyfile
   ```

3. 如果 `umask` 值设置为 `027`，文件的默认权限是什么？

   权限将是 `rw-r----`

4. 假设一个名为 `test.sh` 的文件是一个 shell 脚本，具有以下权限和所有权：

   ```text
   -rwxr-sr-x 1 carol root      33 Dec 11 10:36 test.sh
   ```

   - 文件所有者的权限是什么？

     文件所有者的权限（`ls -l` 输出中的第 2 到第 4 个字符）是 `rwx`，因此答案是：“读取、写入和执行文件的权限”。

   - 使用八进制表示法，取消授予此文件的特殊权限的 chmod 语法应该是什么？

     我们可以通过向 chmod 传递第 4 位数字 0 来“取消”特殊权限。当前权限是 755，因此命令应该是 chmod 0755。

5. 考虑这个文件：

   ```
   $ ls -l /dev/sdb1
   brw-rw---- 1 root disk 8, 17 Dec 21 18:51 /dev/sdb1
   ```

   sdb1 是什么类型的文件？谁可以向其写入？

   `ls -l` 输出的第一个字符显示文件类型。`b` 是块设备，通常是连接到机器的磁盘（内部或外部）。所有者 (root) 和属于 disk 组的任何用户都可以向其写入。

6. 考虑以下 4 个文件：

   ```
   drwxr-xr-t 2 carol carol 4,0K Dec 20 18:46 Another_Directory
   ---r--r-- 1 carol carol 0 Dec 11 10:55 foo.bar
   -rw-rw-r-- 1 carol carol 1,2G Dec 20 18:22 HugeFile.zip
   drwxr-sr-x 2 carol users 4,0K Jan 18 17:26 Sample_Directory
   ```

   使用四位表示法的八进制模式，写下每个文件和目录对应的权限。

   八进制模式下对应的权限如下：

   | 文件/目录 | 八进制表示 | 说明 |
   | :--- | :--- | :--- |
   | Another_Directory | 1755 | 1 代表粘滞位，755 代表常规权限（用户 rwx，组和其他人 r-x）。 |
   | foo.bar | 0044 | 无特殊权限（因此第一位是 0），用户无权限 (--)，组和其他人仅有读取权限 (r--)。 |
   | HugeFile.zip | 0664 | 无特殊权限，因此第一位是 0。用户和组为 6 (rw-)，其他人为 4 (r--)。 |
   | Sample_Directory | 2755 | 2 代表 SGID 位，755 代表常规权限（用户 rwx，组和其他人 r-x）。 |

