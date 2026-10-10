

## 15 教程：远程登录

在本地主机上运行 `rlogin` 或 `telnet` 实用程序，你可以登录并操作拥有账户的远程计算机系统。二者的区别在于：`rlogin` 实用程序仅允许你连接到另一个 UNIX 系统；而 `telnet` 也可以连接到非 UNIX 主机。`telnet` 还可以用于访问某些不需要你在远程主机上拥有账户的互联网服务。

### 15.1 运行 rlogin

在本节中，你将了解如何使用 `rlogin` 登录到远程 UNIX 主机上的账户。（如果在其他机器上没有账户，你可以使用本地账户进行练习。）

- 1. **启动 `rlogin` 程序，指定远程主机和远程登录名称。** 例如，如果你在远程 UNIX 主机 `merlin.podunku.edu` 上有一个名为 `jsmith` 的账户，你应该输入：
  ```
  $ rlogin merlin.podunku.edu -l jsmith <Return>
  ```
  在某些系统中，这样就足以进入远程系统，无需密码。其他系统则要求你输入密码：
  ```
  password:
  ```
- 2. **如有必要，输入你用于远程主机的密码。** 该密码可能与你本地主机上使用的密码不同。
- 3. **当你完成远程账户的操作后，请注销该账户。** 以下其中一个命令应该有效（参见第 3 章）：
  ```
  $ logout <Return>
  $ exit <Return>
  $ CONTROL-D
  ```

### 15.2 运行 telnet

在本节中，你将了解如何使用 `telnet` 登录到拥有账户的远程主机——无论是 UNIX 还是非 UNIX 计算机。（如果在其他机器上没有账户，你可以使用本地账户进行练习。）

- 1. **启动 `telnet` 程序。**
  ```
  $ telnet <Return>
  ```
  你将收到 `telnet` 提示符：
  ```
  telnet>
  ```
- 2. **输入 `Open` 命令，后接远程机器的 Internet 地址。** 例如，如果你在 `merlin.podunku.edu` 上有一个账户，你应该输入：
  ```
  telnet> open merlin.podunku.edu <Return>
  ```
  `telnet` 程序将尝试连接到远程主机。如果连接成功建立，远程主机将显示登录提示符：
  ```
  Trying ... 
  Connected to merlin.podunku.edu.
  Escape character is '^]'
  login:
  ```
  **SunOS UNIX (merlin.podunku.edu)**
- 3. **登录到你的远程账户。** 遵循第 3 章“入门”中所述的步骤。一旦登录成功，你就可以在远程主机上运行常规 UNIX 命令（但不能运行 X 窗口系统）。

### 15.3 telnet 命令

当你使用 `telnet` 登录时，你大概注意到了关于“转义字符”的消息，可能看起来像这样：

```
Escape character is '^]'
```

这意味着 `telnet` 程序使用 `Control-]` 键组合作为转义序列。（不要将其与用于 `vi` 编辑器的 `Esc` 键混淆。）`telnet` 转义字符允许你暂停在远程主机上的工作，并向 `telnet` 程序本身发出命令。

- 1. **输入 `telnet` 转义字符。** 在大多数系统上，这是 `^]` 组合：
  ```
  $ Control-]
  ```
  计算机将以 `telnet` 提示符响应：
  ```
  telnet>
  ```
- 2. **显示 `telnet` 命令列表。** 在提示符后输入问号（`?`）：
  ```
  telnet> ? <Return>
  ```
  程序将响应一个命令列表：
  ```
  close     close current connection
  display    display operating parameters
  mode       line-by-line or character-at-a-time mode
  open       connect to a site
  quit       exit telnet
  send       transmit special characters
  set        set operating parameters
  toggle     toggle operating parameters
  z          suspend telnet
  ?          print help information
  ```
- 3. **显示详细的命令描述。** 要获取这些命令中任何一个的更多信息，请输入命令名后接问号：
  ```
  telnet> close ? <Return>
  ```
  `telnet` 程序将显示 `close` 命令的描述：
  ```
  close closes current connection
  ```
  这并没有告诉你比你已经知道的更多信息。但是，其他一些命令提供了更多详细信息；花一点时间试一试。
- 4. **退出 `telnet` 命令模式。** 这是在 `telnet` 提示符处按下 `Return` 键实现的：
  ```
  telnet> <Return>
  ```
  这将把你带回你的远程 UNIX 账户。

### 15.4 结束 telnet 会话

一旦你在远程主机上完成工作，你应该从该机器注销并结束 `telnet` 会话。

- 1. **从远程账户注销。** 这是按常规方式进行的（参见第 3 章）。以下其中一个命令应该有效：
  ```
  $ logout <Return>
  $ exit <Return>
  $ (CONTROL)-D
  ```
  当你注销后，你将看到一个 `telnet` 提示符：
  ```
  telnet>
  ```
  此时，如果你愿意，可以使用 `open` 命令打开另一个远程会话。
- 2. **退出 `telnet` 程序。** 在提示符后输入 `quit`：
  ```
  telnet> quit <Return>
  ```
  你将看到一个 UNIX shell 提示符：
  ```
  $
  ```

### 15.5 快捷方法

运行 `telnet` 会话有一种更快捷的方式：

- 1. **输入 `telnet` 命令，后接远程机器的 Internet 地址。** 例如，如果你在主机 `merlin.podunku.edu` 上有一个账户，你应该输入：
  ```
  $ telnet merlin.podunku.edu <Return>
  ```
  最终，你将看到 `login` 提示符：
  ```
  login:
  ```
- 2. **像往常一样登录到你的远程账户。**
- 3. **完成后，关闭连接。**
  ```
  telnet> close <Return>
  ```
  这通常会将你从远程账户注销并退出 `telnet`。你应该看到 UNIX shell 提示符：
  ```
  $
  ```

### 15.6 连接到 Guest 账户

通常，你必须在使用 `telnet` 连接的任何远程主机上拥有账户。然而，互联网上创建了一些特殊的 `telnet` 账户来为公众提供服务。登录此类账户有两种方式。

第一种——也许是最常见的方法——要求你使用 `telnet` 连接到主机计算机，然后使用特殊的登录名称和密码登录到该账户。（许多系统不需要密码。）例如，美国国家航空航天局（NASA）维护一个名为“Spacelink”的公共服务，提供有关 NASA 过去、当前和计划活动的信息。你可以使用 `telnet` 连接到此服务：

```
$ telnet spacelink.msfc.nasa.gov <Return>
```

当你到达服务器时，它会提示你登录：

```
login:
```

使用的登录名是 `guest`；该特定服务不需要密码。

第二种方法是通过由数字指定的特殊“端口”使用 `telnet` 登录服务器。通常无需提供登录名或密码。例如，密歇根大学维护一个提供地理信息（包括美国城镇和城市的纬度、经度、海拔和邮政编码）的服务器。你可以通过以下命令访问此服务器：

```
$ telnet martini.eecs.umich.edu 3000 <Return>
```

注意数字 3000；这是端口号。

这些命令都是在 UNIX 提示符后输入的，并且每个命令都以 **Return** 结束。`host` 代表远程主机的地址。

**远程登录命令 (UNIX shell 提示符)**

| 命令 | 描述 |
| :--- | :--- |
| `rlogin host` | 登录到名为 `host` 的远程 UNIX 计算机 |
| `telnet host` | 登录到名为 `host` 的远程计算机 |
| `telnet` | 启动 `telnet` 程序 |

**Telnet 命令 (Telnet 提示符)**

| 命令 | 描述 |
| :--- | :--- |
| `open host` | 打开与计算机 `host` 的连接 |
| `?` | 打印 `telnet` 帮助 |
| `close` | 关闭与远程主机的连接 |
| `quit` | 退出 `telnet` 会话 |

- 1. 如果你在远程 UNIX 机器上有一个账户，使用 `rlogin` 登录到该账户。
- 2. 如果你在连接到网络的非 UNIX 机器上有一个账户，使用 `telnet` 登录到该账户。
- 3. 使用 `telnet` 登录 NASA 的“Spacelink”公共服务器。该服务器上有哪些类型的信息可用？
- 4. 使用 `telnet` 登录密歇根大学的地理服务器。关于你居住的城市或城镇，有哪些类型的信息可用？

