
```
# /opt/asu/lanman/bin/net share

Sharename         Resource                Remark
--------------------
ADMIN$            C:\OPT\ASU\LANMAN      Admin Share
IPC$                               IPC Share
C$               C:\                               Root Share
D$               C:\VAR\OPT\ASU\LANMAN\SHARES...  SystemRootShare
ASTOOLS          C:\VAR\OPT\ASU\LANMAN\SHARES...  Advanced Server Tools
DOSUTIL           C:\VAR\OPT\ASU\LANMAN\SHARES...  DOS Utilities
NETLOGON         C:\VAR\OPT\ASU\LANMAN\SHARES...  Logon Scripts Directory
PATCHES          C:\VAR\OPT\ASU\LANMAN\SHARES...  Patches
PRINTLOG         C:\VAR\OPT\ASU\LANMAN\SHARES...  Printer messages
USERS             C:\HOME\LANMAN          Users Directory
LASER                                 Spooled
```

命令执行成功。

列表中的最后一项是使用 `net` 命令在运行 Advanced Server/9000 的 UNIX 系统上添加的 `laser`。我们现在可以通过 Windows 资源管理器查看这些共享设备，如图 27-2 ![](img/6969df54e516231f8e64fd1177ac1127_1701.png) 所示。图 27-2 共享打印机

## 共享文件系统

在设置了打印机默认共享后，在运行 Advanced Server/9000 的 UNIX 系统上设置的共享如下：

```
# /opt/asu/lanman/bin/net share
```

| 共享名称 | 资源 | 备注 |
|---|---|---|
| ADMIN | C:\OPT\ASU\LANMAN | 管理共享 |
| IPCS | | IPC 共享 |
| CS | C:\ | 根共享 |
| DS | C:\VAR\OPT\ASU\LANMAN\SHARES... | 系统根共享 |
| ASTOOLS | C:\VAR\OPT\ASU\LANMAN\SHARES... | 高级服务器工具 |
| DOSUTIL | C:\VAR\OPT\ASU\LANMAN\SHARES... | DOS 程序 |
| NETLOGON | C:\VAR\OPT\ASU\LANMAN\SHARES... | 登录脚本目录 |
| PATCHES | C:\VAR\OPT\ASU\LANMAN\SHARES... | 客户端补丁 |
| PRINTLOG | C:\VAR\OPT\ASU\LANMAN\SHARES... | 打印机消息 |
| USERS | C:\HOME\LANMAN | 用户目录 |
| LASER | | 打印机 |

命令执行成功。

要共享 UNIX 系统上的 `/home` 目录，我们将执行以下命令：

```
# /opt/asu/lanman/bin/net share home=c:
home was successfully shared
```

注意，目录的 UNIX 表示法使用的是斜杠（`/`）而不是反斜杠（`\`），正如你在 Windows 系统上执行的那样。我们现在可以使用 `net share` 命令查看 `dloaner` 上的共享，包括新增的 `home`：

| 共享名称 | 资源 | 备注 |
|---|---|---|
| ADMIN | C:\OPT\ASU\LANMAN | 管理共享 |
| IPCS | | IPC 共享 |
| CS | C:\ | 根共享 |
| DS | C:\VAR\OPT\ASU\LANMAN\SHARES... | 系统共享 |
| ASTOOLS | C:\VAR\OPT\ASU\LANMAN\SHARES... | 高级服务器工具 |
| DOSUTIL | C:\VAR\OPT\ASU\LANMAN\SHARES... | DOS 程序 |
| HOME | C: | |
| NETLOGON | C:\VAR\OPT\ASU\LANMAN\SHARES... | 登录脚本目录 |
| PATCHES | C:\VAR\OPT\ASU\LANMAN\SHARES... | 客户端补丁 |
| PRINTLOG | C:\VAR\OPT\ASU\LANMAN\SHARES... | 打印机消息 |
| USERS | C:\HOME\LANMAN | 用户目录 |
| LASER | | 打印机 |
