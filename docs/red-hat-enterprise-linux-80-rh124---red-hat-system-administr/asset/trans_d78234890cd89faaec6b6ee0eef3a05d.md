

- 6. 使用 `man` 命令研究 `lp(1)`，以确定如何从特定页面打印任何文档。在不实际输入任何命令的情况下（因为没有打印机），学习使用一条命令仅打印你的 PostScript 文件的第 2 和第 3 页。

- 7. 使用 `quinto` 查找关于 `evince` 查看器的 GNU Info 文档。

- 8. 使用 Firefox 打开系统的软件包文档目录，并进入 `man-db` 包子目录。查看提供的手册。

- 9. 使用 Firefox 浏览器定位并浏览到 `initscripts` 包子目录。查看 `sysconfig.txt` 文件，该文件描述了存储在 /etc/sysconfig 目录中的重要系统配置选项。

# 评估

在工作站上运行 `lab help-review grade` 以确认本次练习是否成功。

```
[student@workstation ~]$ lab help-review grade own
```

# 结束

在工作站上运行 `lab help-review finish` 脚本以完成本次练习。

```
[student@workstation ~]$ lab help-review finish
```

本实验结束。

# 第 4 章 | 在 Red Hat Enterprise Linux 中获取帮助

# 解决方案

# 在 RED HAT ENTERPRISE LINUX 中获取帮助

性能清单
在本实验中，你将查找信息来帮助你在 man 页面和 GNU 文档中完成任务。

成果
你应该能够：

- 通过搜索 man 页面和 Info 节点定位相关命令。
- 学习常用文档命令的新选项。
- 使用适当的工具查看和打印文档以及非文本格式的文件。

开始之前
使用密码 `student` 以 student 身份登录工作站。
在工作站上，运行 `lab help-review start` 命令。

```
[student@workstation ~]$ help-review start
```

1. 在工作站上，确定如何为打印准备 man 页面。具体来说，找到打印使用的是什么格式或渲染语言。

1.1 使用 `man` 命令确定如何为打印准备 man 页面。

```
[student@workstation ~]$ man man
```

> 注意
man 使用 -t 使用 PostScript 准备 man 页面以供打印。

- 2. 创建 `passwd` man 页的格式化输出文件。将文件命名为 `passwd.ps`。确定文件内容格式。检查 `passwd.ps` 文件的内容。

# 第 4 章 | 获取 Red Hat Linux 帮助

> 注意
使用以下命令创建 `passwd` 页的格式化输出：

```
[student@workstation] $ man -t passwd > passwd.ps
```

符号 `>` 将 man 页面的内容重定向到 `passwd.ps` 文件。
该命令将在后续章节中详细介绍。

2.1. 使用 `man -t` 创建 `passwd` 页的格式化文件。

```
[student@workstation] $ man -t passwd > passwd.ps
[student@workstation] $ ls -al
...省略输出...
--rw-rw-r-- 1 student 19947 Feb 26 11:14 passwd.ps
...省略输出...
```

2.2. 使用 `file` 命令确定文件内容。

```
[student@workstation] $ ls /home/student/passwd
passwd.ps: PostScript document text conforming DSC level 3.0
```

2.3. 使用 `less` 命令查看 /home/student/passwd.ps 文件。

```
[student@workstation] $ less /home/student/passwd.ps
%%PS-Adobe-3.0
%%Creator: groff version 1.22.3
%%CreationDate: Tue Feb 26 11:14:40 2019
%%DocumentNeededResources: font Times-Roman
%%+ font Times-Bold
%%+ font Times-Italic
%%+ font Symbol
%%SuppliedResources: procset groups 1.22 3
...省略输出...
```

> 注意
`file` 的输出确认文件为 PostScript 格式，你已通过查看内容确认了这一点。注意 PostScript 信息的头部行。使用 Q 退出 less 命令。

3. 使用 `man` 用于查看和打印 PostScript 文件的命令。

3.1. 使用 man 查看查看和打印 PostScript 文件的命令。

```
[student@workstation] -# man -k postscript viewer
evince (1)
GNOME document viewer
evince-preview (1) - 显示 PostScript 和 PDF 文档的打印预览
evince-thumbnail (1) - 从 PostScript 和 PDF 文档创建 png 缩略图

gcm-viewer (1) - GNOME 颜色管理器查看工具

gnome-logs (1) - systemd 日志查看器
grops (1) - groff 的 PostScript 驱动
pango-view (1) - Tango 文本查看器
pluginviewer (8) - 列出可下载的 SASL 插件及其属性

> 注意
在 -k 选项中使用多个词可以匹配每个单词的页面；描述中包含 "postscript" 或 "viewer" 的页面。注意输出中的 evince(l) 命令。

- 4. 学习在预览模式下使用 `evince(1)` 查看器。还要确定如何打开从特定页面开始的文档。

- 4.1 使用 `man` 命令学习如何在预览模式下使用查看器。

```
[student@workstation ~]$ evince
```

> 注意
-w（或 --preview）选项在预览模式下打开 evince。-i 选项用于指定起始页。

- 5. 使用你研究的各种 evince 选项查看你的 PostScript 文件。完成后关闭文档文件。

- 5.1 使用 `evince` 命令打开 /home/student/passwd.ps

``````
[student@workstation ~]$ evince /home/student/passwd.ps
```

- 5.2 使用 `evince -w /home/student/passwd.ps` 命令在预览模式下打开文件。

```
[student@workstation ~]$ evince -w /home/student/passwd.ps
```

- 5.3 使用 `evince -i 3 /home/student/passwd.ps` 命令从第 3 页打开文件。

```
[student@workstation ~]$ evince -i 3 /home/student/passwd.ps
```

> 注意
虽然普通 evince 允许全屏和演示式查看，但 evince 预览模式适用于快速浏览和打印。注意顶部的打印图标。

