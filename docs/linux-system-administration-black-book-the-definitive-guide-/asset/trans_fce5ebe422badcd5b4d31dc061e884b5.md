

### 创建主机映射

如果你想要为你的站点设置主机映射，请执行以下操作：

1. 以 root 身份登录到你要设置的 Samba 服务器机器。
2. 输入 "vi /etc/smb.conf" 以打开 Samba 服务器的配置文件。
3. 输入 "name resolve" 并按 Enter 键搜索 name resolve order 语句。如果未编辑过，该语句看起来如下所示：

```
name resolve order = wins lmhostos broadcast
```

4. 确保该行未被注释——删除分号——并且它已按照本章前面“配置 Samba”部分中所述的想要的方式进行配置。
5. 如有必要，按 Esc 键返回命令模式，然后输入 "ZZ" 保存并关闭文件。如果你进行了任何更改，暂时不要重启 Samba 服务器。
6. 输入 "vi /etc/lmhosts" 以打开 Samba 主机映射文件。默认情况下，它只包含一行：

```
127.0.0.1 localhost
```

7. 输入 "o" 在此第一行下方打开一个新行，并进入插入模式。
8. 按照以下格式为你的网络中的每台机器输入一行：

```
IPAddress NETBIOS_Name
```

例如：

```
192.168.10.5 ADMIN1
192.168.10.6 ADMIN2
192.168.10.7 ADMIN3
192.168.10.19 PUBLIC6
```

9. 完成后，按 Esc 键返回命令模式，然后输入 "ZZ" 保存并关闭文件。
10. 通过输入 "/etc/rc.d/init.d/smb restart" 来重启 Samba 服务器。

### 创建登录脚本

如果你想要为 Samba 客户端设置登录脚本，请执行以下操作：

1. 以 root 身份登录到你要为 Windows 机器提供登录脚本的 Samba 服务器。
2. 输入 "vi /etc/smb.conf" 以打开 Samba 服务器的配置文件。
3. 输入 "netlogon" 并按 Enter 键搜索到以下代码：

```
[netlogon]
comment = Network Logon Service
path = /home/netlogon
guest ok = yes
writable = no
share modes = no
```

4. 通过将光标放在每个分号上并输入 "x" 来取消注释此代码。你应该得到以下结果：

```
[netlogon]
    comment = Network Logon Service
    path = /home/netlogon
    guest ok = yes
    writable = no
    share modes = no
```

5. 不要更改共享的名称，因为 [netlogon] 是一个保留共享，它告诉 Samba 你要激活 Windows NT Netlogon 服务。但是，更改其他共享定义选项是安全的。如果你想这样做，请现在编辑它们。

6. 按 Esc 键确保你处于命令模式，然后输入 "1G" 跳转到文件开头。

7. 输入 "/logon script" 并按 Enter 键搜索到以下代码：

```
#if you enable domain logons then you may want a per-machine or
#per user logon script
#run a specific logon batch file per workstation (machine)
; logon script = %m.bat
#run a specific logon batch file per username
; logon script = %U.bat
```

8. 最好从一个通用的登录脚本开始并用于测试；然后，当你确定它通常可以工作后，你可以将其拆分为更复杂、更专门的脚本。首先添加以下行：

```
logon script = test.bat
```

> **注意：** .bat 扩展名用于 Windows 95 和 98 机器的脚本，而 .cmd 用于 Windows NT 机器。

9. 按 Esc 键，然后输入 "ZZ" 保存并关闭文件。暂时不要重启 Samba 服务器，因为文件尚未就位。

10. 如果可以的话，在 Windows 机器上创建你的批处理或命令文件。这避免了 Linux 机器处理 Enter 键等字符的方式与 Windows 机器处理它们的方式之间的任何差异。由于为 Windows 机器编写批处理和命令文件超出了本书的范围，以下是一些寻找资源帮助你在追求过程中获得帮助的建议：

    - Windows 95 和 98 用户应前往他们最喜欢的网络搜索引擎——例如 **www.altavista.com**——并输入一组搜索词，例如：
        ```
        batch file programming
        ```
    - Windows NT 用户应尝试 **www.win32scripting.com**。另外，前往你最喜欢的网络搜索引擎并输入一组搜索词，例如：
        ```
        NT ".cmd"
        ```

11. 一旦你完成了示例脚本，请仔细检查你的 **[netlogon]** 共享定义中的 **path** 选项。Samba 将在此处查找脚本。

12. 将脚本复制到新位置。假设你使用了前面步骤中列出的默认值，文件应位于 `/home/netlogon/test.bat`。

13. 输入 `/etc/rc.d/init.d/smb restart` 以重启 Samba 服务器。

14. 前往你想使用该脚本的 Windows 机器，并配置一台测试机器以从 Netlogon 服务器获取启动脚本。

15. 重新启动机器。如果脚本工作正常，请继续制作越来越复杂和专门的脚本，并在适当时使用表 18.3 中的替换来微调它们的名称。务必在每个阶段进行测试。

## 第 19 章

# 文本处理工具

如果你需要立即解决以下问题：参见页码：

- 在 vi 中操作 578
- 在 vi 中过滤文本 579
- 在 vi 中复制和粘贴文本 581
- 在 vi 中缩进文本 581
- 使用正则表达式 583
- 运行带有多个命令的 sed 584
- 构建 sed 脚本文件 586
- 运行带有外部文件脚本的 sed 588
- 使用 cut 命令 588
- 使用 join 命令 589
- 使用 ispell 检查拼写 590
- 构建 ispell 字典 592
- 减小 ispell 字典大小 594
- 使用 tr 命令 595

## 深入探讨

你无法避免学习如何在 Linux 下处理文本文档的需要。即使有基于 GUI 的管理工具的出现，你仍然需要花时间处理华丽背景和程序底下的文本文件。本章涵盖了众多可用工具中的两个特定工具。其中一个工具是 *Visual* 编辑器——更通俗地被称为 **vi**——这是本书其余部分使用的文本编辑器。另一个工具是 **sed**，它允许你搜索文本文件的内容然后更改它们。对于知道如何让这些程序充分发挥作用的系统管理员来说，这两个程序都极其有用。

## vi 编辑器

**vi** 编辑器是人们似乎要么热爱要么痛恨的工具之一。它的大多数命令涉及单个字符，并且一些命令可以用其他单个字符扩展或细化。**vi** 命令结构的优势在于它使这个编辑器极其快速。当然，缺点是必须记住这些命令。当你经常使用 **vi** 时，它们会相对容易掌握。你会很快记住一些你比其他命令使用得更频繁的偏好命令，有时还需要查阅其他命令。

在 Red Hat 和其他 Linux 发行版中，你找到的往往不是经典的 **vi**，而是一个指向 **vim** (*vi Improved*) 的别名。添加到原始 **vi** 编辑器的功能包括无限撤销更改的能力、GUI (**gvim**) 和命令行 (**vi**) 版本、GUI 模式下基于鼠标的编辑功能，以及当你使用程序编写程序时的颜色突出显示功能。

> **提示：** 如果你不确定你使用的是哪个编辑器，输入 `man vi` 并查看 *man 页面* 说你在用什么。

**vi** 在三个主要模式中运行，每个模式都有特定的目的和与用户交互的特定方法。你必须理解每个模式是什么，你可以在每个模式内做什么，以及如何从一个模式切换到另一个模式。

> **注意：** 当我在这本书中提到 **vi** 时，我实际上指的是 **vim**。

