
`remhost1`变量标识包含要发送的文件的远程主机，后跟冒号 (`:`) 和要发送的文件`filesend`。语句的最后一部分标识第二个远程主机`remhost2`以及文件名`file-recv`，`remhost1`上的文件将被复制到该文件。如果在`file-recv`中只给出目录名（如下面的示例中所示），`filesend`将以相同的文件名复制到那里。

以下示例使用`rcp`将远程主机`flint`上目录`/u/cave/fred`中的文件`spark`复制到远程主机`stone`上目录`/u/hut/barney`：

```
% rcp flint:/u/cave/fred/spark stone:/u/hut/barney
```

## 在远程主机上工作

本章解释了如何使用以下命令：

- 从本地终端登录到远程主机。
- 在远程主机上执行指定的命令。
- 使用 Telnet 协议登录到远程主机。如果不支持`rlogin`，请将`telnet`作为替代方案使用。

> Note
>
> 任何远程登录都受远程主机安全功能的限制。如果您在登录远程主机时遇到困难，请咨询您的系统管理员。

在使用这些命令之前，您可能需要知道正确的主机名或远程主机是否当前可达。使用`finger`、`who`、`rwho`、`uptime`和`ping`命令，这些命令在第 10 章中描述，以查找此信息。

### 13.1 使用 rlogin 登录到远程主机

您可以使用`rlogin`登录到远程主机，使用以下命令语法：

```
rlogin [-user] host_name
```

`-l`选项使您能够指定与本地用户名不同的远程用户名。`host_name`变量指定远程主机。

以下步骤显示如何登录到远程主机`boston`，其中登录名与本地主机上的相同：

- 1. 输入以下`rlogin`命令，后跟远程主机名。例如：

```
$ rlogin boston
```

Password:

- 2. 输入您的密码。

当系统提示符显示时，您已登录到远程主机，可以输入任何命令。

3. 按 Ctrl/D 关闭连接并返回到本地主机。

如果您在远程主机上有账户，而该主机的登录名与本地主机上的不同，您应使用`-l`选项登录到远程主机，如以下步骤所示。

- 1. 输入`rlogin -l`命令，后跟远程登录名和远程主机名。例如：

```
% rlogin -l celtic boston
Password:
```

- 2. 输入与登录名`celtic`对应的密码。
- 当系统提示符显示时，您已登录到远程主机，可以输入任何命令。
- 3. 按 Ctrl/D 关闭连接并返回到本地主机。

在以下情况下，`rlogin`不会提示输入密码：

- 如果您的本地主机列在远程主机的`/etc/hosts.equiv`文件中
- 如果您的主机名（以及可选的用户名）列在远程主机上您主目录中的`.rhosts`文件中

有关`rlogin`的更多信息，请参阅`rlogin(1)`参考页。

### 13.2 使用 rsh 在远程主机上运行命令

`rsh`命令使您能够在远程 UNIX 主机上运行单个命令，而无需在那里登录。如果您需要连续运行多个命令，必须使用`rlogin`或`telnet`登录到远程主机。

`rsh`命令具有以下语法：

```
rsh [-l user] host_name command
```

`-l`选项使您能够登录到远程主机，其中您的登录名`user`与本地主机上的不同。如果您未指定`-l`选项，`rsh`假定您的登录名在本地和远程主机上相同。`host_name`变量指定远程主机的名称。`command`变量指定您想要运行的命令。

Note

如果您未指定要远程运行的命令，`rsh`会提示您输入远程主机的登录信息。

要使用`rsh`，必须满足以下条件之一：

- 你的本地主机在远程主机的`/etc/hosts.equiv`文件中列出。
- 你的主机在远程主机上你的主目录中的`.rhosts`文件中列出。

在下面的示例中，`rsh`将远程主机上的一个文件追加到本地主机上的一个文件。位于主机`remhost2`上的远程文件`remfile2`被追加到名为`locfile`的本地文件：

```
% rsh remhost2 cat remfile2 >> locfile
```

### 13.3 使用 telnet 登录到远程主机

你可以使用`telnet`命令登录到远程主机，该命令实现了 Telnet 协议。

使用`telnet`你可以：

- 登录到远程主机
- 在远程主机上执行任何操作系统命令
- 输入`telnet`子命令（参见表 13-1）以管理远程会话

`telnet`命令的语法如下：

```
telnet [host_name[port]]
```

`host_name`变量指定远程主机。如果省略主机名，你可以在激活 Telnet 实用程序后使用`open`子命令建立连接。示例 13-1 显示了如何使用`telnet`命令登录到名为`star`的远程主机，使用`telnet`子命令`status`，并关闭连接。

如果未指定端口，Telnet 协议将尝试在默认端口上联系 Telnet 服务器。

#### 示例 13-1：使用 telnet 命令

```
$ telnet star
Trying 16.69.224.1...
Connected to star.milkyway.galaxy.com.
Escape character is '^]'.

(star.milkyway.galaxy.com) (ttyra)

login: username
Password:

$ '^]'
 telnet> status
Connected to star.milkyway.galaxy.com.
Operating in single character mode
Catching signals locally
Remote character echo
Local flow control
Escape character is '^]'.

$ 
$ 
Connection closed by foreign host.
$ telnet star
Trying 16.69.224.1...
Connected to star.milkyway.galaxy.com.
Escape character is '^]'.

(star.milkyway.galaxy.com) (ttyra)

login: username
Password:

$ '^]'
 telnet> q
Connection closed.
```

1 `telnet`命令被输入，指定`host_name`为`star`。使用默认端口。

2 `telnet`实用程序标识它正在尝试连接的地址。

3 `telnet`实用程序完成连接并标识它所连接的主机。

4 远程主机系统标识自身并提示用户登录。

5 在主机系统上输入用户名。

6 远程系统提示输入用户密码。

7 在主机系统上输入用户的密码。出于安全原因，密码显示被抑制。

8 按下默认转义序列 Ctrl+] 以访问`telnet`子命令提示符`telnet>`。

9 在提示符下输入`status`子命令。

##### 示例 13-1：使用 telnet 命令（续）

15 在`telnet:`子命令提示符下输入`q`子命令以退出 Telnet 会话。按下 Ctrl/D 也可使用。

16 本地`telnet`实用程序关闭连接。

你可以不带任何参数输入`telnet`命令以访问`telnet`子命令模式，由`telnet>`提示符表示。

`telnet`子命令在表 13-1 中描述。在输入子命令之前，必须输入转义序列 Ctrl/]。该序列通知`telnet`程序以下信息不是文本；否则，`telnet`会将子命令解释为文本。

对于每个子命令，你只需输入足够字母以唯一标识该命令即可。例如，`q`已足够用于`quit`命令。有关`telnet`子命令的完整列表，请参阅`telnet(1)`参考页。

#### 表 13-1：telnet 子命令

| 子命令 | 描述 |
|---|---|
| `? [subcommand]` | 显示帮助信息。如果指定了子命令，则显示有关该子命令的信息。 |
| `close` | 关闭连接并返回到`telnet`命令模式。 |
| `displa [argument]` | 如果未指定参数，则显示所有`set`和`toggle`值；否则，仅列出与`argument`匹配的值。 |
| `open host [port]` | 打开与指定主机的连接。主机指定可以是主机名或以点分十进制形式表示的 Internet 地址。如果未给出端口，`telnet`将尝试在默认端口上联系`telnet`服务器。 |
| `quit` | 关闭连接并退出`telnet`程序。在命令模式下按下 Ctrl/D 也会关闭连接并退出。 |
| `status` | 显示`telnet`的状态，包括当前模式和当前连接的远程主机。 |
| `z` | 根据`SHELL`环境变量指定的方式在本地主机上打开一个`shell`。当你通过按下 Ctrl/D 退出`shell`时，`telnet`将返回到远程会话。 |
