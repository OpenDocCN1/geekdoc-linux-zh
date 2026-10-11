
`lpr` 命令有许多选项和参数。我们建议查阅手册页（man pages）和其他来源以获取更多信息。另外两个重要的打印命令 `lpq` 和 `lprm` 在示例 5.10 中展示。

### 示例 5.10 使用 `lpr` 打印文件

唐·吉诃德想要阅读和回顾他写的一首关于风车的诗，那些风车曾在“高尚行为部”的一次冒险中彻底击败了他。他还想在将每周报告（名为 `mon_rept` 的文件）以纸质形式发送给杜尔西内娅小姐之前，先审阅一下。以下是他将这两个打印任务发送到默认打印机的方式：

```
$ lpr windmills mon_rept
```

### 列出和取消打印任务

要列出默认打印队列中的打印任务并显示其当前状态：

```
$ lpq
```

要检查非默认队列的状态（再次假设 `lp1` 是备用打印机）：

```
$ lpq -P lp1
```

```
$ lpq -P lp1
```

要取消打印任务：

```
$ lprm jobnumber
```

要查找任务编号，请事先执行 `lpq` 命令。

#### 示例 5.11 使用 `lpq` 列出打印任务

唐·吉诃德将打印任务发送到队列后，快速检查打印队列，看看他是否需要长时间等待打印完成，以及他的两个打印请求的当前状态：

```
$ lpq
Rank Owner Job Files Total Size
active quixote3 301 windmills 255 bytes
active quixote3 302 mon_rept 2537 bytes
```

唐吉诃德看到他的两个打印任务排在最前面。它们都很小，所以应该很快完成。

#### 示例 5.12 使用 lprm 取消打印任务

在最后一刻，唐·吉诃德决定给他的每周报告添加一些内容。因此，他暂时取消了 *mon_rep* 的打印：

```
$ lprm 302
```

### cat 也可以打印

在我们离开这个主题和本章之前，值得指出的是 `cat` 命令也可以用于打印文本和文件。以此方式使用 `cat` 也需要重定向，我们之前在*查看文件内容*部分提到过。

## 练习

- 1. 切换到 `/home/mydirectory/mydir` 目录。使用 `touch` 命令在你的 `mydir` 目录中创建两个零长度文件 `myfile1` 和 `myfile2`：

  ```
  $ cd mydir
  $ touch myfile1
  $ touch myfile2
  ```

- 2. 显示 your `mydir` 目录内容的详细列表。`myfile1` 和 `myfile2` 的大小是多少？

  ```
  $ ls -l
  ```

- 3. 再次查看详细列表，但这次也显示 inode 号。每个文件的 inode 号是多少？

  ```
  $ ls -li
  ```

- 4. 使用 `pwd` 命令，确认你在主目录 `/home/directoryname` 中。

  ```
  $ pwd
  ```

- 5. 列出你主目录的内容，包括隐藏文件。

  ```
  $ ls -a
  ```

- 6. 查看 `/etc/motd` 和 `/etc/passwd` 文件的内容。使用 `cat`、`more` 和 `less` 命令查看每个命令如何处理输出。`/etc/motd` 文件包含每日信息（即首次登录后看到的信息）。`/etc/passwd` 文件包含所有获授权使用该系统的用户列表。

  ```
  $ cat /etc/motd
  $ cat /etc/passwd
  $ more /etc/motd
  $ less /etc/motd
  $ more /etc/passwd
  $ less /etc/passwd
  ```

- 7. 关闭连接到你的系统的打印机。在系统打印机上打印 `/etc/motd` 文件。

  ```
  $ lpr /etc/motd
  ```

- 8. 检查你的打印任务状态。

  ```
  $ lpq
  ```

- 9. 重新打开打印机。

- 10. 将 `/bin/cat` 文件复制到你的当前目录（即主目录）：

  ```
  $ cp /bin/cat /home/teambxc
  ```

  或者

  ```
  $ cp /bin/cat .
  ```

- 11. 将 `/usr/bin/cal` 文件复制到你的当前目录（主目录）：

  ```
  $ cp /usr/bin/cal /home/teampoc
  ```

  或者

  ```
  $ cp /usr/bin/cal .
  ```

- 12. 列出当前目录中的文件。你应该能看到刚刚复制的两个文件。

  ```
  $ ls
  ```

- 13. 在你的主目录中创建一个名为 `bin` 的子目录：

  ```
  $ mkdir bin
  ```

- 14. 将你练习 5 和 6 中复制的两个文件移动并重命名到你的新子目录中。分别命名为 `mycat` 和 `mycal`。

  ```
  $ mv cat bin/mycat
  $ mv cal bin/mycal
  ```

- 15. 将新的子目录 `bin` 设为你当前的目录：

  ```
  $ cd bin
  ```

- 16. 列出目录内容以验证文件是否已复制。

  ```
  $ ls
  ```

- 17. 使用 `mycat` 命令列出你主目录中的 `.bash_profile` 文件：

  ```
  $ mycat ../.bash_profile
  ```

  或者

  ```
  $ mycat /home/tealnx/.bash_profile
  ```

- 18. 将你的主目录设为当前目录：

  ```
  $ cd
  ```

- 19. 在你的主目录中创建另一个名为 `goodstuff` 的子目录：

  ```
  $ mkdir goodstuff
  ```

- 20. 将一个名为 `/etc/profile` 的文件复制到新目录，并将新文件命名为 `newprofile`：

  ```
  $ cp /etc/profile goodstuff/newprofile
  ```

- 21. 使用 `cat` 命令查看该文件：

  ```
  $ cat goodstuff/newprofile
  ```

- 22. 是否难以阅读？尝试 `more` 和 `less` 命令：

  ```
  $ more goodstuff/newprofile
  ```

  或者

  ```
  $ less goodstuff/newprofile
  ```

- 23. `newprofile` 文件名太长，每次输入都很麻烦。将其改名为 `np`。列出 `goodstuff` 目录的内容，以确保你已完成任务：

  ```
  $ mv goodstuff/newprofile goodstuff/np
  $ ls goodstuff
  ```

- 24. 这是一个检查一切的好机会。从你的主目录开始向下，显示你的文件和子目录的层次结构树。

- 25. 确保你在你的主目录中。删除 `goodstuff` 目录：

  ```
  $ pwd
  $ rmdir goodstuff
  ```

  你能做到吗？为什么？
