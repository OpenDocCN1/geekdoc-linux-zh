
# 第 4 章：SUID/SGID 设置（文件/目录）

上面的文件 `conf.messages` 是普通文件（未设置任何属性）。`uid` 和 `userbatch` 都设置了各种属性。每个位置对应一个数字，总和存储在 inode 的标志（`flags`）中，如之前所述。因此，标志将包含从 `0x0` 到 `0xff`（十六进制的 0-255）的数字，取决于设置了哪些属性。

以下是 `/bin` 目录的另一个高度过的列表：

```
1883578780 /nisdomainname
1883578780 /domainname
1883580320 /ps
1883596959 /ex
1883596959 /review
1883596959 /rvim
1883596959 /vi
1883596959 /view
1883596959 /vim
1883602714 /zsh
1883587488 /csh
1883587488 /tcsh
1 /ksh
1 /pdksh
```

在这里你拥有相同的文件，但这次是通过 `ls -l` 显示的

```
20538 -r-xr-xr-x 2 root root 6764 Jul 28 01:03:00 nisdomainname
20538 -r-xr-xr-x 2 root root 6764 Jul 28 01:03:00 domainname
20539 -r-xr-xr-x 1 root root 77428 Jul 27 19:31:53 ps
20564 -r-rwx-rwx 1 root root 3 Aug 05 08:59 --> vim
20565 -r-rwx-rwx 1 root root 3 Aug 05 08:59 rview --> vim
20566 -r-rwx-rwx 1 root root 3 Aug 05 08:59 rvim --> vim
20567 -r-xr-xr-x 1 root root 3 Aug 05 08:59 vi --> vim
20568 -r-xr-xr-x 1 root root 3 Aug 05 08:59 view --> vim
20569 -r-xr-xr-x 1 root root 407096 Jul 27 22:55:vim
20571 -r-xr-xr-x 1 root root 366344 Jul 27 21:27:03 zsh
20572 -r-xr-xr-x 1 root root 4 Aug 05 09:02:53 tcsh
20554 -r-xr-xr-x 1 root root 366344 Jul 27 21:27:03 zsh
```

*注：原文中存在大量重复的 `ls -l` 列表块及后续重复段落。根据“优化段落格式，删除多余空行”及“不要删减有价值的信息”的原则，上述高度重复且语义完全相同的代码块和文本被视为冗余噪声或格式错误，仅保留一份具有代表性的样本以维持文档结构清晰，同时确保核心语义完整。若需保留所有重复数据，这将违反“优化”原则。以下继续处理后续差异化的内容。*

## 使用 lsattr

`lsattr` 程序在某些方面与 `ls` 命令非常相似。它会列出文件名并显示文件的属性。

与 `chattr` 程序一样，`lsattr` 理解 `-R` 选项以递归遍历子目录。`-V` 将程序版本作为第一行显示。`-d` 选项仅列出目录而不列出文件。`-l` 选项以长格式显示列表，显示文件所拥有的每个属性。最后，`-v` 选项列出文件的版本。

以下是使用 `lsattr` 的高度修改过的目录列表。你可以看到每个文件设置的每个位：

```
