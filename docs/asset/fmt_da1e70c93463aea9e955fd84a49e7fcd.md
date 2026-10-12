
# 选择你的秘密密码

一次性密码短语列表是由一个名为 `opiekey` 的程序生成的。为了向该程序唯一标识你自己，你需要一个秘密密码。使用 `opiepassword` 来选择该秘密密码。

例如，假设我是 OPIE 的新手，我想在旅行之前生成一个密码短语列表。我用传统的可重复密码登录 OPIE 服务器的控制台，并运行 `opiepasswd` 选择秘密 OPIE 密码（该密码长度至少为 10 个字符），`opiepassword` 接受该秘密密码并显示第一个密码短语：

```
$ opielepassword -c

Updating cair:

Reminder - 仅从控制台使用此方法；

切勿从远程使用。如果你正在使用 telnet、xterm 或拨号连接，

现在输入 'c' 或不带密码。。在不带参数的情况下运行 opielepassword。

正在使用 MD5 计算响应。

Enter old secret phrase: OJ1CCftNt

Enter new secret phrase: N'pie.c,.na..o

Agree new secret phrase: N'pie.c,.na..o

ID CRAIG AGOY SAM OKEY is 499 P18318

DUG AGOY EMIL SAM JOT BERN
```

从控制台运行 `opielepassword` 是最安全的方法。如果不是从控制台运行，你必须拥有 `opiele` 软件副本，以生成进入你的旧新秘密密码所需的正确密码，因为明文密码仅接受来自控制台。

# 创建额外的密码短语

当然，仅有一个密码短语是不够的。生成额外的密码短语需要 `opiekey`。`opielepassword` 命令输出的倒数行包含重要信息。它显示了序列号 (449) 和种子 (p18318)。配合秘密密码，`opiekey` 需要这些值来生成 OPI 密码短语。

`opiekey` 将序列号、用户种子和用户秘密密码作为输入；输出正确的密码短语。使用 `-n` 参数请求多个密码。将它们打印出来或记录下来，你就可以出发了。列表 12.8 中的示例向 `opiekey` 请求了五个密码短语。

## 列表 12.8：生成 OPI 密码短语

```
$ opickey -n 499 p18318

Using MD5 algorithm to compute response.

Reminder: 不要从 telnet 或拨号会话中使用 opickey。

Enter new secret phrase: N'pie.c,.na..o

495: NEO BORN ABEL HANG YANG WISE

496: VERB JUKE BRAN LAWN NAIR WOOL

497: POE MORE HAVE UN DRAB MONTH

498: SACK WAND WAKE AURA SNUG HOOD

499: DUG AGOY EMIL SAM JOT BERN
```

注意，序列号从 499 开始倒计时且不可重用。当序列号降到 10 时，重新运行 `opielepassword` 并选择一个新的密码短语，以将序列号重置为 499。

`opiekey` 命令行从序列号 499 开始请求五个密码短语 (-n 5)。种子 (p18318) 在命令行中提供。`opiekey` 会提示你输入通过 `opielepassword` 命令定义的秘密密码。序列号、种子和秘密密码是 `opiekey` 生成密码短语所需的值。

密码短（passphrase）字面上完全可以是一个短语，因为允许包含空格。示例使用了歌词中的行句。虽然随机的单词组合可能更安全，但密码短必须易于记忆。如果你忘记了它，没有人能为你找回。

会创建两个密钥：`~/.ssh/identity` 是必须受保护的私钥，而 `~/.ssh/identity.pub` 是分发到远程站点用于加密会话的公钥。在客户端系统上创建密钥后，将 `identity.pub` 的内容添加到服务器上对应用户家目录下的 `~/.ssh/authorized_keys` 文件中。现在，每当用户从该客户端登录服务器时，系统会提示用户输入密码短。

默认配置提供了简单且安全的通信，并能完全免受密码窃取者的侵害。然而，对于服务器和客户端都有配置选项，你可以利用这些选项为你的环境定制安全外壳（secure shell）。

## 配置 sshd

运行运行安全的 ssh 所需极少的配置，但也可以进行大量的配置。书中讨论的许多软件软件包都符合这种模式：有许多配置选项，但这些选项的默认值在几乎所有情况下都适用，很少需要更改。sshd 也不例外。如果没有配置，它也可以正常工作，但你可以使用一些配置选项来针对你的特定站点进行修改。

sshd 通过 `/etc/ssh/sshd_config` 文件进行配置。该文件中的配置值是键值对。这里有 50 多种可能的配置值：

-   `AllowTokenPassing`: 指定服务器是否接受 PFS 令牌。
-   `AllowGroups`: 列出允许登录的组。用户必须属于列出的组之一才能登录系统。默认情况下，登录不限制于特定组。
-   `AllowTcpForwarding`: 指定是否允许转发。默认情况下是允许的。
-   `AllowUsers`: 列出允许登录的用户。默认情况下，登录不限制于特定组。
-   `Banner`: 标识一个文件，该文件包含在登录前显示的横幅页。
-   `ChallengeResponseAuthentication`: 指定是否应该使用挑战/响应认证。默认是 yes，但 sshd 仅对 S/Key 使用挑战/响应认证。
-   `Ciphers`: 指定服务器将支持的加密技术。默认是 `aes128-cbc`、`3des-cbc`、`blowfish-cbc`、`cast128-cbc` 和 `arcafour`。
-   `CheckMail`: 指定用户登录时 sshd 是否应该检查用户是否有新邮件。默认情况下，它不检查。
-   `ClientAliveInterval`: 定义了链路空闲时发送给客户端的时间间隔。这些消息目的是触发客户端的响应。默认是 0，意味着服务器不会发送这些消息。
-   `ClientAliveCountMax`: 定义了在服务器终止连接之前，向无响应客户端发送的最大消息数量。默认是 3。
-   `DenyGroups`: 列出不允许登录服务器的组。属于这些组的任何一个组的用户将不允许登录。默认情况下，允许所有用户登录。
-   `DenyUsers`: 列出不允许登录服务器的用户。默认情况下，允许所有有效用户登录。
-   `GatewayPorts`: 指定远程主机是否可以连接到为其转发的端口。默认是 no。
-   `HostbasedAuthentication`: 指定是否使用 `.hosts` 和 `/etc/hosts.equiv` 来认证客户端。默认是 no。`.hosts` 和 `/etc/hosts.equiv` 是传统上由 rlogin 使用的信任主机文件。但在这种情况下，它们不会被单独使用。这些文件与客户端的公钥认证结合使用。
-   `HostKey`: 标识包含主机私钥的文件。
-   `IgnoreRhosts`: 指定是否忽略 `.hosts` 和 `/etc/hosts.equiv`。默认是 yes。
-   `HostKeysFile`: 标识包含授权公钥的文件。
-   `PermitAuthenticationAuthentication`: 指定是否允许公密码认证。默认是 yes。
-   `UsePAM`: 指定是否应该 PAM 认证。默认是 yes。
-   `UsekeyAuthentication`: 指定是否使用公钥认证。默认是 yes。

`UseLogin` 指定是否使用交互式登录会话。默认情况下，不使用。

`X11DisplayOffset` 定义了 sshd 允许用于 X11 转发的最小显示编号。默认值为 10。

`X11Forwarding` 告诉 sshd 是否应该向客户端转发 X11 流量。默认为否（no）。

`XAuthLocation` 定义了 xauth 程序的路径。默认路径 `/usr/X11R6/bin/xauth`。

通过使用此参数列表的信息，你应该能够读取系统提供的配置，并在必要时针对你的环境进行修改。示例 Red Hat 系统自带的 `/etc/ssh/sshd-config` 文件见第 12.11 节。

# 列表 12.11：Red hat ssh_config 文件

```
