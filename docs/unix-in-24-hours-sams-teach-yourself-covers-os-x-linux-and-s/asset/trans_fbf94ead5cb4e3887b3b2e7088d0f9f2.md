

## Note

这个最新示例演示了你可以在单个 Unix 命令行上给出多个命令。要做到这一点，请用分号分隔命令。与其在单独的行上给出命令 `ls -ld test` 和 `ls -lR test`，我选择了更高效的 `ls -ld test; ls -lR test`，它会一个接一个地执行命令。

Unix 上相当于碎纸机的 `rm` 命令允许轻松删除文件。使用 `-r` 标志，你可以清理整个目录，即使它包含子目录和这些子目录中的文件。使用 `-f` 标志，任何警告消息或其他权限问题将被忽略，使命令更加危险。你绝对不想在 Unix 系统上运行的命令是 `rm -rf /`，原因我希望是显而易见的！

再次提醒，事后无法恢复任何东西，因此在任何时候调用 `rm` 时都要格外谨慎。

## Task 6.7: Minimizing the Danger of the rm Command

到目前为止，你可能会想知道我为什么如此大肆渲染 `rm` 命令以及它确实做到了它所宣传的事情——即删除文件。答案是，现在学习一点偏执可以在未来为你节省巨大的痛苦。它可以防止你销毁一个包含你真的需要保存的信息的文件。

对于 Windows，存在商业程序（例如 Norton Utilities）可以检索意外删除的文件。与 Mac 一样，Windows 回收站是一个可以打开并从中提取文件的文件夹，直到它被“清空”。用于 Macintosh 的 Norton Utilities 等程序可用于恢复通过清空废纸篓而被删除的文件。然而，如果你在命令行上工作，Unix 却没有这种能力，被删除的文件将永远消失。

唯一的例外是，如果你使用的是具有自动、可靠的云备份或本地设备备份计划的 Unix 系统。在这种情况下，你可能能够检索到文件的旧版本（也许）。

话虽如此，你可以做一些事情来降低使用 `rm` 的危险，同时仍然让你能够删除不需要的文件。

- 1. 你可以使用简写，即 shell 别名，自动将 `-i` 标志附加到每次使用 `rm`。要做到这一点，请确定你正在运行哪种类型的登录 shell，最简单的方法是使用以下命令：

```
% grep taylor /etc/passwd
 taylor:x:19989:1412:Dave Taylor:/users/taylor:/bin/csh
```

（现在不要担心这到底做了什么。你将在几个小时后学习 `grep` 命令。）该行上的最后一个词很重要。`/etc/passwd` 文件是 Unix 用于跟踪

账户的数据库文件之一。文件中的每个文件称为 *password entry* 或 *password file entry*。在我的密码条目中，你可以看到指定的登录 shell 是 `/bin/csh`。如果你尝试此操作并且没有相同的条目，你应该有 `/bin/sh` 或 `/bin/ksh`。

- 2. 如果你的条目是 `/bin/csh` 或 `/bin/tcsh`，请输入此处显示的确切内容：

```
  % echo "alias rm /bin/rm -i" >> ~/.cshrc
  % source ~/.cshrc
```

现在每次使用 `rm` 时都包含 `-i` 标志：

```
  % touch testme
  % rm testme
  rm: remove testme? N
```

- 3. 如果你的条目是 `/bin/bash`，请输入此处显示的确切内容，注意示例中使用的两种不同的引号字符：

```
  $ echo ‘alias rm="/bin/rm -i"’ >> ~/.profile
  $ . ~/.profile
```

现在每次使用 `rm` 时都包含 `-i` 标志。

## Note

有一件事需要特别注意，那就是单引号 (`)、双引号 ("）和反引号 (`) 之间的区别。Unix 对每种引号的解释都不同，尽管单引号和双引号通常可以互换。反引号，也称为反引号，较为少见，用于在其他命令中界定命令。

- 4. 如果你的条目是 `/bin/sh`，你无法将系统编程为每次使用 `rm` 时都包含 `-i` 标志。Bourne shell（sh）是 Unix 的原始命令 shell。Bourne shell 缺少别名功能，而 Bash shell（bash）和 C shell（csh/tcsh）都包含此功能。因此，我建议你将登录 shell 更改为其中一种替代方案（如果可用）。

要查看有哪些可用选项，请在你的机器上的 `/bin` 目录中查找特定的 shell：

```
  % ls -lF /bin/*sh
  -rwxr-xr-x  1 root  wheel  603488  3 Nov 22:35 /bin/bash*
  -r-xr-xr-x  1 root  wheel  348068  3 Nov 22:35 /bin/csh*
  -r-xr-xr-x  1 root  wheel  603488  3 Nov 22:35 /bin/sh*
  -r-xr-xr-x  1 root  wheel  348068  3 Nov 22:35 /bin/tcsh*
  -rwxr-xr-x  1 root  wheel  479120  3 Nov 22:35 /bin/zsh*
```

本书中的大多数示例都集中在 Bash shell 上，因为我认为它是最容易使用的 shell，而且它无疑是最广泛使用的。要更改你的登录 shell，你需要向系统管理员发送电子邮件提出请求，尽管某些版本的 Unix 提供 `chsh`（change shell）或在 Solaris 中，

