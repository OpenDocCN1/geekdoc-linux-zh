

## default

此参数仅适用于 *可打印* 服务。当 smbd 向 Windows NT/2k/XP 客户端提供打印机驱动程序时，Samba 服务器上的每个打印机都有一个设备模式（Device Mode），用于定义纸张大小、方向和双面打印设置等信息。该设备模式只能由打印机驱动程序本身正确生成（该驱动程序只能在 Win32 平台上执行）。由于 smbd 无法执行驱动程序代码以生成设备模式，因此默认行为是将此字段设置为 NULL。

向 Windows NT/2k/XP 客户端提供打印机驱动程序时的大多数问题都可以追溯到生成的设备模式存在问题。某些驱动程序会在 devmode 为 NULL 时导致客户端的 Explorer.exe 崩溃。然而，如果 devmode 不是由驱动程序本身创建的（即 smbd 生成默认 devmode），其他打印机驱动程序可能会导致客户端的后台打印服务（spoolsv.exe）终止。

应谨慎使用此参数，并使用相关打印机驱动程序进行测试。最好将设备模式保留为 NULL，让 Windows 客户端设置正确的值。由于驱动程序并不总是执行此操作，设置 `default devmode = yes` 将指示 smbd 生成一个默认的设备模式。

有关 Windows NT/2k 打印和 Device Modes 的更多信息，请参阅 MSDN 文档 [4]。

[^4]: http://msdn.microsoft.com/

## default service (G)

默认值： *无默认值*

示例： `default service = pub`

此参数指定在无法找到实际请求的服务时连接的服务名称。请注意，参数值中 *不包含* 方括号（见下文示例）。

此参数没有默认值。如果未指定此参数，尝试连接不存在的服务将导致错误。

通常，默认服务是一个 *guest ok, read-only* 服务。

另外请注意，表面服务名称将更改为等于请求的服务名称，这非常有用，因为它允许您使用 *%S* 等宏来创建通配符服务。

还需注意，默认服务中使用的服务名称中的任何 "*" 字符都会映射为 "/"。这可以实现一些有趣的功能。

## defer sharing violations (G)

默认值： `defer sharing violations = True`

Windows 允许在打开文件时指定该文件如何与其他进程共享。当使用违反其他进程指定共享设置的选项由不同进程打开文件时，就会发生共享冲突。此参数使 smbd 的行为与 Windows 服务器一致，并延迟返回“共享冲突”错误消息长达一秒，以便在此期间客户端可以关闭导致冲突的文件。

Unix 默认不具有此行为。

没有理由关闭此参数，因为其设计目的是使 Samba 能更准确地模拟 Windows。

## delete group script (G)

默认值： *无默认值*

这是完整的脚本路径名，当请求删除组时，smbd(8) 将以 *AS ROOT*（以 root 身份）运行该脚本。它将把任何 *%g* 扩展为传递的组名。此脚本仅适用于使用 Windows NT 域管理工具的安装环境。

## deleteprinter command (G)

默认值： *无默认值*

示例： `deleteprinter command = /usr/bin/removeprinter`

随着 Samba 2.2 引入基于 MS-RPC 的 Windows NT/2000 客户端打印机支持，现在可以通过发出 DeletePrinter() RPC 调用来在运行时删除打印机。

对于 Samba 主机而言，这意味着必须从底层打印系统中物理删除该打印机。 *deleteprinter command* 定义了一个要运行的脚本，该脚本将执行将打印机从打印系统和 *smb.conf* 中移除所需的必要操作。

`subcommand` 选项会自动调用，且仅包含一个参数：*打印机名称*。

*deleteprinter command* 执行后，**smbd** 将重新解析 **smb.conf**，因为相关打印机不再存在。如果共享名称仍然有效，则 **smbd** 将向客户端返回 ACCESS_DENIED 错误。

## delete readonly (S)

默认值： `delete readonly = no`

此参数允许删除只读文件。这不符合正常的 DOS 语义，但被 UNIX 允许。

此选项对于运行 rcs 等应用程序可能很有用，因为 UNIX 文件所有权阻止更改文件权限，而 DOS 语义阻止删除只读文件。

## delete share command (G)

默认值： *无默认值*

示例： `delete share command = /usr/local/bin/delshare`

为了成功执行 `delete share command`，smbd 要求管理员使用 root 账户连接（即 uid == 0）。执行时，smbd 将自动调用 `delete share command` 并传递两个参数：

- `configFile` - 全局 `smb.conf` 文件的位置。
- `shareName` - 现有服务的名称。

此参数仅用于删除文件共享。要删除打印机共享，请参阅 `deleteprinter` 命令。

## delete user from group script (G)

默认值： No default

示例： `delete user from group script = /usr/sbin/deluser %u %g`

这是使用 Windows NT 域管理工具将用户从组中移除时要调用的脚本的完整路径。它将作为 smbd(8) 以 AS ROOT 身份运行。任何 %g 都将被替换为组名，任何 %u 都将被替换为用户名。

## delete user script (G)

默认值： No default

示例： `delete user script = /usr/local/samba/bin/delUser %u`

这是 smbd(8) 在使用远程 RPC (NT) 工具管理用户时运行的脚本的完整路径名。

当远程客户端从服务器移除用户时（通常使用 'User Manager for Domains' 或 rpcclient），将调用此脚本。

此脚本应删除给定的 UNIX 用户名。

## delete veto files (S)

默认值： `delete veto files = no`

当 Samba 试图删除包含一个或多个否决目录（参见 `veto files` 选项）的目录时，会使用该选项。如果将此选项设置为 no（默认值），则如果否决目录中包含任何未被否决的文件或目录，目录删除将失败。通常这正是您想要的。

如果将此选项设置为 yes，则 Samba 将尝试递归删除否决目录内的任何文件和目录。这对于与文件服务系统（如 NetAtalk）集成很有用，这些系统会在您通常禁止 DOS/Windows 用户查看的目录中创建元文件（例如 .AppleDouble）。

设置 `delete veto files = yes` 允许在删除父目录时透明地删除这些目录（只要用户拥有相应的权限）。

## dfree command (G)

默认值： `默认使用内部例程来确定磁盘容量和剩余空间`

示例： `dfree command = /usr/local/samba/bin/dfree`

*dfree command* 设置仅应在内部磁盘空间计算出现问题的系统上使用。已知 Ultrix 会发生这种情况，但其他操作系统也可能出现。观察到的症状是每个目录列表末尾出现“Abort Retry Ignore”错误。

此设置允许使用外部例程替换计算总磁盘空间和可用量的内部例程。下面的示例给出了一个可能实现此功能的脚本。

外部程序将接收一个参数，指示正在查询的文件系统中的目录。这通常由字符串 ./ 组成。脚本应返回两个 ASCII 整数。第一个应为块单位的总磁盘空间，第二个应为可用块的数量。可选的第三个返回值可以给出以字节为单位的块大小。默认块大小为 1024 字节。

注意：您的脚本 *不应* 设置为 setuid 或 setgid，并且应由 root 拥有（且仅 root 可写）！

脚本 dfree（必须使其可执行）可能是：

```sh
#!/bin/sh
df $1 | tail -1 | awk '{print $2" "$4}'
```

或者（在基于 Sys V 的系统上）：

```sh
#!/bin/sh
/usr/bin/df -k $1 | tail -1 | awk '{print $3" "$5}'
```

注意，在某些系统上可能必须将命令名称替换为完整路径名称。

## directory mode

此参数是 *directory mask* 的同义词。

## directory mask (S)

默认值： `directory mask = 0755`

示例： `directory mask = 0775`

此参数是八进制参数，用于在创建 UNIX 目录时将 DOS 模式转换为 UNIX 模式。

创建目录时，根据从 DOS 模式到 UNIX 权限的映射计算所需的权限，然后将生成的 UNIX 模式与此参数进行按位“与”运算。可以将此参数视为目录 UNIX 模式的按位 MASK（掩码）。任何在此 *未* 设置的位都将从创建目录时设置的模式中移除。

