
18. 选择您想要使用的四个选项之一：共享（share）、用户（user）、域（domain）或服务器（server）。如果您主要希望使用来宾连接，请将此行更改为：

    `security = share`

19. 下一项是：

    `; password server = <NT-Server-Name>`

20. 如果您希望指定某台特定机器来处理身份验证，请将其 NetBIOS 名称作为参数提供并取消该行的注释。例如：

    `password server = DOMAINSERVER`

    还请审查**名称解析顺序**（name resolve order）参数，以确保 Samba 服务器知道如何解析 NetBIOS 名称，除非该名称与其主机名相同。**密码服务器**（password server）的特殊条件包括：

    - 如果之前将 **security** 参数设置为 **domain**，则必须将域控制器（domain controller）引用为 **password server** 的值。
    - 您可以对 **password server** 的值使用变量替换。
    - 如果以逗号分隔，您可以列出多个服务器。
    - 如果您希望 Samba 自行尝试查找密码服务器，请星号（asterisk）作为 **password server** 的值。这将指示服务器在由**名称解析**（name resolution）参数设置的文件中查找域控制器。
    - 如果之前将 **security** 参数设置为 **server**，且您打算使用 NT 域控制器，则需要设置用户从 Samba 服务器访问该控制器的权限。

21. 继续到以下两行：

    `; password level = 8`
    `; username level = 8`

22. 如果您的密码或用户名倾向于混合大小写，请取消相应行的注释。考虑大小写可能混合的程度——例如，大写字母可能仅存在于前三个字符中——并根据您的需求更改列出的数字。

23. 继续到以下两行：

    `; encrypt passwords = yes`
    `; smb passwd file = /etc/smbpasswd`

24. 如果您有许多运行 Windows NT 4（服务包 3 或更高版本）或 Windows 98 的机器，请取消**加密密码**（encrypt passwords）语句的注释。有关如何与其他 Linux 机器配合使用加密密码，请参见本章后面“在 Samba 上实现加密密码”一节。

25. 如果您确实取消了**encrypt passwords**的注释，请也取消**smb passwd file**的注释。

26. 将光标向下移动至：

    ```text
    ; unix password sync = Yes
    ; passwd program = /usr/bin/passwd %u
    ; passwd chat = *NEW*UNIX*password* \n\n *ReType*new*UNIX*password*
    %\n *passwd:*all*authentication*tokens*updated*successfully*
    ```

27. 如果您选择加密密码，并希望确保每次更新 SMB 密码时，用户的登录密码也随之更新，请取消**unix password sync**语句的注释。

28. 如果您选择激活**unix password sync**语句，您还可以更改 Samba 服务器实际用于修改密码的程序。该程序由**passwd program**语句指定。值末尾的 **%u** 确保客户端提供的用户名会被传递给该程序。

29. 如果您激活了 **unix password sync**，您也有机会定制用于更新密码的聊天脚本（chat script）。您可以通过更改 **passwd chat** 值来实现这一点。首先运行 **passwd program** 并记录您看到的信息以及需要发送的内容。您有一些可用的工具来帮助您：

    - **passwd chat** 值中允许使用两个变量。您已经熟悉其中一个，**%n**，它包含您想要设置的新密码。另一个是 **%o**，包含旧密码。
    - 有四个宏可用。第一个是 **\n**，相当于按下旧的换行键（Linefeed key）——这通常用于换行宏。接下来是 **\r**，用于创建回车。另外两个宏是 **\t**（用于发送制表符 Tab）和 **\s**（用于包含一个空格）。
    - 有一个通配符可用。您可以使用星号来表示“任意字符”。
    - 可以使用双引号来引用包含空格的字符串，以便 Samba 不会认为它们是独立的实体。

30. 继续到：

    ```text
    ; username map = /etc/smbusers
    ```

31. 如果您打算构建用户映射表，如本章后面“创建用户映射表”一节所述，请取消此行的注释，并确保路径与您计划放置映射表文件的位置匹配。

32. 继续到这一行：

    ```text
    ; include = /etc/smb.conf.%m
    ```

33. 如果您希望为每台机器提供不同类型的配置文件，请取消此行的注释并调整其值。**include** 语句在您需要为特定一组机器设置特殊的配置选项而不想将其用于其他机器，或者需要设置 Samba 处理运行不同操作系统的机器的方式时特别有用。

34. 将光标移动到：

    ```text
    ; interfaces = 192.168.12.2/24 192.168.13.2/24
    ```

35. 如果您需要明确说明 Samba 应该使用哪些接口，以防止其使用其他接口，请取消此行代码的注释，并将 **interfaces** 值更改为您的网络所需的适当值。

36. 继续到以下行：

    ```text
    ; remote browse sync = 192.168.3.25 192.168.5.255
    ```

37. 如果您的网络中有多个 Linux 机器上运行着 Samba 服务器，请取消此行代码的注释，并将给出的 IP 地址更改为指向您自己的主 **nmbd** 服务器机器。

> **注意：** 示例中显示两个 IP 地址，因为您可以为不同的工作组拥有独立的主 **nmbd** 守护进程。

38. 继续向下移动到：

    ```text
    ; remote announce = 192.168.1.255 192.168.2.44
    ```

39. 如果您需要 Samba 服务器定期向特定网络或子网上的机器，甚至向单台机器广播其存在，请取消前面代码行的注释。然后，输入广播或 IP 地址，以便将公告发送给您希望接收广播的特定机器或网络。

40. 将光标向下移动到：

    `; local master = no`

41. 如果您不希望此机器作为网络上的主 **nmbd** 浏览服务器之一，请取消此行的注释。

42. 继续到：

    `; os level = 33`

43. 此服务器在浏览器选举中的表现取决于其浏览器级别——级别越高，选举中的优先级越高。关键级别的细分列在表 18.4 中。如果您希望此服务器的优先级不为零，请取消此行的注释并根据您的需求更改它。

44. 将光标移动到：

    `; domain master = yes`

45. 如果特定的工作组或子网上没有 Windows NT 机器，您需要另一台机器充当域主（domain master）。如果此机器位于该子网上或是该工作组的成员，且您希望它充当主服务器，请取消此行的注释。

46. 继续到以下行：

    `; preferred master = yes`

47. 如果您将此机器设置为**域主**（domain master），请也取消此行的注释。请注意，不要在同一工作组或子网上拥有 Windows NT 或其他**首选主**（preferred master）机器，因为这可能会导致许多不必要的选举。

表 18.4 Samba 浏览器选举的关键 os level 里程碑。

| 级别 | 区别 |
|:----|:----|
| 0 | 允许设置的最低级别。如果网络中存在任何 Windows 机器，此服务器将在浏览器选举中输给它们。这是默认值。 |
| 2 | 在浏览器选举中击败 Windows 3.11 和 Windows 95 机器。 |
| 33 | 在浏览器选举中击败 Windows NT 高级服务器机器。 |
| 255 | 最高级别。 |

48. 向下移动到：

    `; domain logons = yes`

49. 如果特定的子网或工作组中没有任何 Windows NT 机器，但您希望或需要提供工作组域登录服务，您可以让 Samba 服务器机器为您的 Windows 95 和 98 机器处理此项。如果您希望此特定机器提供此登录服务，请取消 domain logons 代码的注释。

50. 将光标向下移动到以下两行：

    `; logon script = %m.bat`
    `; logon script = %U.bat`

51. 如果您启用了域登录，您可以选择创建脚本，当 Windows 客户端机器与服务器登录时下载并执行这些脚本。有关如何制作在取消 logon script 语句注释时使用的脚本的信息，请参见本章后面的“创建登录脚本”一节。

    在命名脚本时，您需要考虑两个项目：

    - **文件扩展名**——对于不使用 NT 的 Windows 机器，批处理文件使用 .bat 扩展名。NT 机器要求命令文件使用 .cmb 扩展名。
    - **变量**——您可以使用表 18.3 中之前给出的任何替换值，以便 Samba 指向以特定变量命名的文件。

52. 继续到这一行：

    `; logon path = \\%L\Profiles\%U`

53. 如果您的域、工作组或子网中有 Windows 95 和 98 机器，但没有 Windows NT 机器来提供漫游配置文件，并且您希望为您的 Windows 用户利用此功能，请取消此行的注释，允许 Samba 为您处理这些配置文件。与 logon path 语句相关的值是可以找到这些文件的路径。再次强调，在设置此路径时，您可以使用表 18.3 中列出的变量。

54. 继续到以下语句：

    `; name resolve order = wins lmhosts broadcast`
