
![](img/75f39fc91296b889c0653851accdfd46_51_0.png)

我们将在本书的各章中介绍许多命令。`passwd` 命令对于你的初始登录很重要，因为你可能需要立即更改你的密码。

如果你通过图形用户界面登录屏幕获得系统访问权限，你只需像在命令行中那样输入你的用户名和密码即可。如果你犯了错误，可以重新输入你的用户名和密码，就像在命令行中那样。登录成功后，你将拥有一个可工作的图形环境。图 1-1 显示了打开了许多窗口的通用桌面环境。

### 多用户 UNIX

![](img/75f39fc91296b889c0653851accdfd46_52_0.png)

图 1-1 成功登录后的通用桌面环境

从图 1-1 中可以看到，图形界面环境中正在进行许多活动。第四章专门介绍通用桌面环境，详细涵盖了图 1-1 中的许多组件。

### 在线手册页

![](img/75f39fc91296b889c0653851accdfd46_53_0.png)

大多数 UNIX 变种都附带了一组在线手册页。这些被称为 "man" 页面的文档通常内容完整、时效性强，且是出色的综合参考资料。大多数其他操作系统提供的在线帮助只是操作手册中完整帮助内容的一个小子集。另一方面，"man" 页面非常有用，大多数 UNIX 用户在遇到与命令相关的问题时，首先都会查阅 "man" 页面。如果你不知道所需的命令，但知道某个与希望执行的功能相关的命令，你可以查看已知命令的 "man" 页面，并查看其中引用的其他相关命令。

要查看某个命令的 "man" 页面，只需输入 `man` 以及你要使用的命令名称，如下面来自 Solaris 系统的示例所示：

```text
martyp $ man passwd
Reformatting page. Wait... done

User Commands                                passwd(1)

NAME
       passwd - change login password and password attributes

SYNOPSIS
       passwd [ -r | files | -r nis | -r nisplus ] [ name ]
       passwd [ -r files ] [ -egh ] [ name ]
       passwd [ -r files ] -s [ -a ]
       passwd [ -r files ] -s [ name ]
       passwd [ -r files ] [ -d | -l ] [ -f ] [ -n min ] [ -w warn ] [ -x max ] name
       passwd -r nis [ -egh ] [ name ]
       passwd -r nisplus [ -egh ] [ -D domainname ] [ name ]
       passwd -r nisplus -s [ -a ]
       passwd -r nisplus [ -D domainname ] -s [ name ]
       passwd -r nisplus [ -l ] [ -f ] [ -n min ] [ -w warn ]
           [ -x max ] [ -D domainname ] name
```

**描述**

`passwd` 命令用于更改与用户登录名关联的密码或列出密码属性。此外，特权用户可以使用 `passwd` 安装或更改与任何登录 *名称* 关联的密码和属性。

当用于更改密码时，`passwd` 会提示用户输入旧密码（如果存在）。然后它会提示两次输入新密码。当输入旧密码时，`passwd` 会检查其是否已“老化”足够的时间。如果“老化”时间不足，`passwd` 将终止；有关详细信息，请参阅 `pwnconv`(1M)、`nist-bladm`(1) 和 `shadow`(4)。

当系统中启用了 NIS 或 NIS+ 时，`passwd` 会更改 NIS 或 NIS+ 数据库。NIS 或 NIS+ 密码可能与本机上的密码不同。如果正在运行 NIS 或 NIS+，请使用 `passwd -r` 来更改本机的密码信息。

`pwnconv` 命令利用 `/etc/passwd` 中的信息创建并更新 `/etc/shadow`。`pwnconv` 依赖于 `/etc/passwd` 密码字段中 'x' 的特殊值。该 'x' 值表示该用户的密码已存在于 `/etc/shadow` 中，不应被修改。

User Commands                          passwd(1)

如果老化时间充足，系统会进行检查以确保新密码符合构造要求。当第二次输入新密码时，系统会比较两个新密码副本。如果两个副本不完全一致，则新密码的提示循环将最多再重复两次。

密码必须构造以满足以下要求——More--(17%)

这个不完整的列表（如示例末尾所示的“17%”）显示了本章前面提到的 `passwd` 命令的 "man" 页面。您可以对其他主题（不仅仅是命令）发出 `man` 命令。您还可以获取有关系统调用、库例程和其他信息。甚至还可以获取有关 `man` 命令本身的信息，如下面来自同一系统的示例所示：

![](img/75f39fc91296b889c0653851accdfd46_54_0.png)
