
# 理解时间戳

## 实验 10.4 理解时间戳

```text
-rw-r--r-- 1 root root 0 Oct 23 08:40 file1
-rw-r--r-- 1 root root 0 Oct 23 08:47 file1
```

11. 打开 `file1` 查看时间戳如何受影响，输入 `cat file1` 并按回车。（文件是空的，所以 `cat` 命令没有输出，但由于文件被访问过，`atime` 发生了变化。）输入 `dir` 并按回车。只有 `atime` 应该发生了变化，正如你：

```text
-rw-r--r-- 1 root root 0 Oct 23 08:40 file1
-rw-r--r-- 1 root root 0 Oct 23 08:40 file1
-rw-r--r-- 1 root root 0 Oct 23 08:47 file1
```

12. 使用编辑器修改文件，输入 `vi file1` 并按回车。通过输入 `i` 进入插入模式并添加内容。按 `Esc` 回到命令模式，然后输入 `:wq` 并按回车。

```text
-rw-r--r-- 1 root root 0 Oct 23 08:40 file1
-rw-r--r-- 1 root root 0 Oct 23 08:40 file1
-rw-r--r-- 1 root root 0 Oct 23 08:47 file1
```

13. 模拟访问文件，输入 `touch file1` 并按回车。输入 `dir` 并按回车。你会看到：

```text
-rw-r--r-- 1 root root 0 Oct 23 08:50 file1
-rw-r--r-- 1 root root 0 Oct 23 08:50 file1
-rw-r--r-- 1 root root 0 Oct 23 08:50 file1
```

14. 修改文件的权限，输入 `chmod 700 file1` 并按回车。你会看到 `ctime` 发生了：

```text
-rwx------ 1 root root 0 Oct 23 09:15 file1
-rw-r--r-- 1 root root 0 Oct 23 09:13 file1
-rw-r--r-- 1 root root 0 Oct 23 09:15 file1
```

15. 更改文件的所有者，输入 `chown nobody file1` 并按回车。输入 `dir` 并按回车。你会发现 `ctime` 发生了：

```text
-rwx------ 1 nobody root 0 Oct 23 09:15 file1
-rwx------ 1 nobody root 0 Oct 23 09:13 file1
-rwx------ 1 nobody root 0 Oct 23 09:15 file1
```

16. 设置该属性，输入 `chattr +A file1` 并按回车。输入 `dir` 并按回车。你会发现 `atime` 没有被更新：

```text
-rwx------ 1 nobody root 0 Oct 23 09:15 file1
-rwx------ 1 nobody root 0 Oct 23 09:13 file1
-rwx------ 1 nobody root 0 Oct 23 09:15 file1
```

17. 访问文件，使用 `cat file1` 并按回车。输入 `dir` 并按回车。你会发现 `atime` 没有被更新：

```text
-rwx------ 1 nobody root 0 Oct 23 09:15 file1
-rwx------ 1 nobody root 0 Oct 23 09:13 file1
-rwx------ 1 nobody root 0 Oct 23 09:15 file1
```

18. 你可以使用 `atime` 搜索一年内未访问过的文件，例如，输入 `find -atime 365` 并按回车。365 是自上次访问以来的天数。

19. 要根据 `mtime` 值搜索文件，请使用 `find -mtime 5` 并按回车，这会搜索五天内未修改的文件。

20. 除了打开和读取之外，对文件进行的任何操作都会导致 `ctime` 更改。因此，`ctime` 可以作为文件发生了某些操作的指示。

你也可以配合命令使用 `-exec` 或 `-or` 选项来对找到的文件执行某些操作，例如删除或备份，正如实验 10.3 所示。

# 第十一章 压缩、系统备份和软件安装

本章包含以下实验：

- 实验 11.1 使用 gzip 压缩程序
- 实验 11.2 压缩图像文件
- 实验 11.3 安装和删除包
- 实验 11.4 检测并替换缺失的包文件
- 实验 11.5 备份到 SAMBA 共享

| 目标 | 实验 |
|---|---|
| 104.3 | 执行基本文件管理 | 11.1, 11.2, 11.5 |
| 103.3 | 使用 RPM 和 YUM 包管理 | 11.3, 11.4 |
| 102.5 | 控制文件系统的挂载和卸载 | 11.5 |

## 实验 11.1 使用 gzexe 压缩程序

### 目标

将文件尽可能减小是非常有用的，特别是当它们必须存储在磁盘上，或必须通过慢速网络或调制解调器链路传输时。Linux 程序文件也可以出于同样的原因进行压缩。在本实验中，你将学习如何使用 `gzexe` 命令来压缩二进制程序。

### 所需材料

本实验需要：

- 一台运行 Fedora 20 Linux 的计算机

预计完成时间：15 分钟

### 活动步骤

1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，如有必要，以 root 用户身份登录。

2. 输入 `cd ~` 确保你在主目录中。接下来，输入 `cp /bin/rpm ~/` 并按回车，将 `/bin` 目录下的 rpm 程序复制到你的主目录。

3. 输入 `ls -l rpm` 并按回车查找 rpm 程序的文件大小。文件大小应在 15,000 到 16,000 字节之间。

4. 输入 `gzexe rpm` 并按回车来压缩程序。此过程需要几秒钟。完成后，你会看到类似 `rpm: 58%` 的输出。该数字表示压缩率，因此在本例中，rpm 程序被压缩了 58%。

5. 原文件被重命名为 `rpm-`，新的压缩文件名为 `rpm`。输入 `ls -l rpm` 查看两个文件的大小。会有显著差异，如下：

```text
-rwxr-xr-x 1 root root 7615 10:22 rpm
-rwxr-xr-x 1 root root 16152 10:21 rpm-
```

6. 两个文件都运行相同的程序。输入 `./rpm --version` 并按回车。你会看到类似 `RPM version 4.11.1` 的输出，表示 rpm 程序的版本。接下来，输入 `./rpm- --version` 并按回车。你会看到未压缩文件 (`rpm-`) 和压缩文件 (`rpm`) 均可工作。（请确保在前面的命令中输入两个 "-" 字符）

7. 当你压缩程序时，启动时间会稍微长一点，因为它必须先解压缩。首先使用 `time` 命令比较两个程序运行所需的时间。首先输入 `./rpm --version` 并按回车，查看压缩程序运行所需的时间。rpm 输出如下：

```text
RPM version 4.11.1
real 0.0024s
user 0.0013s
sys 0.0003s
```
