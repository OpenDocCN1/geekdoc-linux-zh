
进入`/path/to/xxx`目录，找到`xxx.json`。

## 配置指令说明

- `Port`：指定 ProFTPTPD 监听传入连接的端口。默认值 21 应该保持不变，否则你必须指示你的 FTP 用户使用其 FTP 客户端软件连接到 FTP 服务器上的不同端口。
- `Umask`：指定默认的文件和目录创建 umask 设置。默认值 022 会创建权限为 755 的文件或目录，这太宽松了。建议使用值 027，它可以确保只有所有者和组可以访问该文件或目录。
- `MaxInstances`：指定同时运行多少个 ProFTPD 实例。此指令仅对独立模式有效。
- `User`：与必须以 root 运行的初始 ProFTPD 守护进程不同，为了安全，当 FTP 服务与客户端交互时，会切换到普通用户，从而减少客户端进程与特权进程交互的风险。
- `Group`：与 `User` 指令一样，`Group` 指令指定运行 ProFTPD 的用户组。

![](img/6d176ba5e3d859ca2b04a3bba254354c_481_1.png)

尽管 `User` 指令的默认值 (`nobody`) 适用于许多安装，但 `Group` 值 (`nroup`) 则不是。`/etc/group` 文件中没有 nogroup。要解决这个问题，你可以将 `Group` 值设置为 `nobody`（因为 `/etc/group` 中默认没有名为 nobody 的组）。如果你出于某些原因保留 `Group` 指令的默认值，可以运行 `groupadd nogroup` 命令添加名为 nogroup 的组。

- `<Directory/*>`：适用于特定目录路径的一组指令。默认指令适用于 `/*` 通配符路径（意味着目录中的所有文件）。包含在目录容器中的 `AllowOverwrite` 指令允许 FTP 客户端覆盖任何文件。这是一个坏主意，应设置为 `off`。当你尝试创建一个安全环境时，第一步是将其设置为 `off`。

![](img/6d176ba5e3d859ca2b04a3bba254354c_482.png)

- `<Anonymous>`：适用于特定目录路径的一组指令。默认指令适用于 `/*` 通配符路径（意味着目录中的所有文件）。包含在目录容器中的 `AllowOverwrite` 指令允许 FTP 客户端覆盖任何文件。这是一个坏主意，应设置为 `off`。当你尝试创建一个安全环境时，第一步是将其设置为 `off`。

## 第 18 章：FTP 服务器安全

![](img/6d176ba5e3d859ca2b04a3bba254354c_484_0.png)

在将 ProFTPPD 配置为由 xinetd 运行的服务之前，先确保你没有已经在以独立模式运行 ProFTPPD。运行 `ps auxww | grep proftpd` 命令来检查当前是否有正在运行的 ProFTPPD 实例。如有必要，请在按照以下步骤操作之前杀掉任何正在运行的实例。

1. 在 `/etc/xinetd.d/wu-ftpd` 文件添加 `disable = yes`，这可以确保当有新的 FTP 请求到来时，xinetd 不会启动你的 WU-FTPD 服务器。
2. 使用 `killall -USR1 xinetd` 命令重载 xinetd 配置。
3. 修改 `/etc/proftpd.conf` 文件，将 `ServerType` 指令设置为 `xinetd` 而不是 `standalone`。
4. 使用 `groupadd nogroup` 命令创建一个名为 `nogroup` 的新组。
5. 创建一个名为 `/etc/xinetd.d/proftpd` 的新 xinetd 配置文件，包含以下行：

```
service ftp
{
    flags           = REUSE
    socket_type     = stream
    instances       = 30
    wait            = no
    user            = root
    server          = /usr/local/sbin/proftpd

    log_on_success = HOST PID
    log_on_failure = HOST RECORD
    disable         = no
}
```

6. 使用 `killall -USR1 xinetd` 命令重载 xinetd 配置。
7. 使用 `ftp localhost` 命令从本地主机连接服务器。如果连接被拒绝，运行 `tail -f /var/log/messages` 命令并重试。注意 ProFTPD 输出的错误信息；相应解决问题。

## 监控 ProFTPPD

ProFTPPD 包含了一些可以帮助你监控服务的工具。例如，你可以运行 ProFTPD 绑定的工具来统计并发 FTP 连接，或确定哪些用户连接到了你的服务器。在本节中，我将详细介绍这些工具。

### 统计 FTP 连接

要查找有多少人连接到你的 FTP 服务器，请运行 `/usr/local/bin/ftpcount` 命令。以下是你获得的输出示例：

```
Master proftpd process 8322:
- 2 users
```

当你引入一个新的 FTP 服务时，请密切监控它至少几天。通常情况下，你应该使用 `watch` 功能运行类似上述的命令。例如，`watch -n 60 /usr/local/bin/ftpcount` 命令可以在终端或 xterm 上运行，每隔 60 秒显示一次 FTP 用户计数。

### 查找谁连接了 FTP

运行 `/usr/local/bin/ftpwho` 命令查看谁在连接中。示例输出：

```
Master proftpd process 8322:
8387 0ml1 sheila proftpd: reboot.intevo.com: IDLE
8341 3m59s proftpd: kabir - k2.intevo.com: IDLE
- 2 users
```

这里有两个用户（sheila 和 kabir）从局域网上的两台不同机器连接。输出显示：
- 服务这些用户的 ProFTPPD 进程
- 主 ProFTPPD 进程 ID

### 加固 ProFTPPD

ProFTPPD 有许多可以在 `/etc/proftpd.conf` 文件中使用的指令，用以创建一个安全且受限制的 FTP 服务。在本节中，我将展示如何使用此类指令来限制 FTP 连接。

## 466 第四部分：网络服务安全

```
</Limit>
</Directory>
```

同样地，你可以使用 `AllowUser` 指令来指定创建和删除目录的用户。如果你想仅对少数用户撤销这些权限，可以在 `/etc/group` 中创建一个组（badusers），并使用以下配置允许所有人创建和删除目录，但该组中的用户除外：

```
<Directory />
<Limit MKD RMD>
Order deny,allow
DenyGroup badusers
AllowAll
</Limit>
</Directory>
```

### 建立立项一个仅允许上传的 FTP 服务器

为了仅允许向你的 FTP 服务器上传文件，你可以在主服务器或虚拟主机容器中以下配置：

```
<Directory />
<Limit RETR>
DenyAll
</Limit>
</Directory>
```

### 限制对单个目录的访问

为了防止用户翻找他们不应该进入的目录，你可以使用以下配置将所有 FTP 用户限制在特定目录：

```
<Directory />
<Limit CWD>
DenyAll
</Limit>
</Directory>
```

启用此配置后，连接服务器的 FTP 用户无法更改目录。你可以使用 `DenyGroup` 组名代替 `DenyALL`，以将配置范围限制在 `/etc/group` 文件定义的某个用户组（group）。

### 为新用户简化文件传输

许多用户在看到可用目录或选项过多时会感到迷失。如果你简化了他们的计算机交互，大多数用户并不在意或不知。因此，如果你有一组用户

## 第 18 章：FTP 服务器安全

必须定期在 FTP 服务器中检索或存储文件的用户，你可能希望将他们的访问权限锁定在一个目录中。例如，你在 `/etc/group` 中定义了一个名为 `novices` 的组，并希望允许该组的用户从 `/files/download` 目录检索文件，并向 `/files/upload` 目录上传文件。你添加到 `/etc/proftftpd.conf` 文件中的配置如下所示：
