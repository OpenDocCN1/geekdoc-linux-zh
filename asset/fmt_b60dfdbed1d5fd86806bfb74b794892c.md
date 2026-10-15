
或者，你也可以用一行定义两个节点，格式如下：
`node primary.mydomain.com backup.mydomain.com`

`primary.mydomain.com` 和 `backup.mydomain.com` 条目应该替换为在安装 Linux 时你为那两台主机分配的名称（通过 `uname -n` 命令返回）。
主服务器和备份服务器的主机名通常与服务器提供的任何服务没有关联。例如，你的主服务器的主机名可能是 `primary.mydomain.com`，即使它拥有一个名为 `mystuff.mydomain.com` 的 Web 服务器。

在 Red Hat 系统上，主机名在 `/etc/sysconfig/network` 文件中使用 `hostname` 变量指定，并在启动时设置（尽管可以在运行中的系统上通过 `hostname` 命令进行更改）。

## 第 3 步：配置 `/etc/ha.d/haresources`

通常，`/etc/ha.d/haresources` 文件将包含主服务器应该拥有的资源名称。Heartbeat 通常使用随发行版自带的普通 init 脚本来控制其资源，或者使用你构建的脚本（例如第 6 节所示的 `iptakeover` 脚本），但现在我们将使用一个非常简单的测试脚本来查看它们是如何工作的。按照以下步骤操作：

- 使用以下命令在 `/etc/ha.d/resource` 目录下创建一个名为 `test1` 的脚本（该脚本也包含在第 7 节的子目录的 CD-ROM 中）：

```
#vi /etc/ha.d/resource.d/test1
```

- 现在按 `I` 键进入插入模式，然后输入以下简单的 bash 脚本：

```bash
#!/bin/bash

logger $0 called with $1

case "$1" in

    # 启动命令放在这里

    ;;

    stop)

    # 停止命令放在这里

    ;;

    status)

    # 状态命令放在这里

    ;;

esac
```

此脚本中的 `logger` 命令用于向 syslog 守护进程发送消息。然后 syslog 将根据 `/etc/syslog.conf` 文件中的规则将消息写入相应的日志文件中。（有关自定义消息日志的更多信息，请参阅 `logger` 和 `syslog` 的 man 页。）

**注意** 此脚本中的 `case` 语句没有执行任何操作。将其包含在此处仅作为进一步开发你自定义资源脚本的模板，该脚本可以处理 Heartbeat 用于控制的 start、stop 和 status 参数。

- 3. 退出此文件并保存更改（按 `ESC` 键，然后输入 `:wq`）。
- 4. 输入此命令使该脚本变为可执行：

```bash
chmod 755 /etc/ha.d/resource.d/test
```

- 5. 输入以下命令运行脚本：

```
#/etc/ha.d/resource.d/test start
```

- 6. 你应该返回到 shell 提示符，你可以在此处输入此命令查看消息的末尾：

```bash
tail /var/log/messages
```

`/var/log/messages` 文件中的最后一条消息看起来应该是这样的：
`[timestamp] localhost root: /etc/ha.d/resource.d/test called with start argument`

此行表示测试资源脚本已使用 `start` 参数被调用，并正确使用了脚本内部的 `case` 语句。

## 配置 haresources 文件

你可以使用这个简单的脚本，通过告诉 Heartbeat 某项是一个资源来观察它是如何处理资源的。为此，请使用以下命令找到并复制示例 `haresources` 文件到指定位置：

```bash
#rpm -qd heartbeat | grep haresources
#cp /usr/share/doc/packages/heartbeat/haresources /etc/ha.d
```

现在编辑 `/etc/ha.d/haresources`（此时它实际上只包含注释说明文档），并在文件末尾添加以下行：

```
primary.mydomain.com test
```

在此示例中，`primary.mydomain.com` 应该替换为 `-n` 命令返回的主服务器名称。

`haresources` 文件告诉 Heartbeat 程序由谁拥有资源。资源名称实际上是 `/etc/init.d` 目录或 `/etc/ha.d/resource.d` 目录下的一个脚本。（主服务器和备份服务器上必须存在该脚本的副本。）

Heartbeat 使用 `haresources` 配置文件来确定启动时执行的操作。例如，如果你指定 heartbeat 脚本 `/etc/init.d/httpd` 为资源，那么当你在主服务器上启动 heartbeat 守护进程时，Heartbeat 将运行此脚本并向其传递 `start` 命令。

如果你告诉 Heartbeat 停止（使用命令 `/etc/init.d/heartbeat stop` 或 `service heartbeat stop`），Heartbeat 将运行 `/etc/init.d/httpd` 脚本并向其发送 `stop` 命令。因此，如果 Heartbeat 未运行，资源守护进程（在此例中为 `httpd`）也不会运行。

如果你使用了发行版自带的现有 init 脚本（来自 `/etc/init.d` 目录），请确保使用 `chkconfig -del <scriptname>` 命令告诉系统在正常启动过程中运行此脚本。（有关 `chkconfig` 命令的详细说明请参见第 1 节。）

- 如果你没有使用 Red Hat 或 SuSE，还应该确保脚本在接收到 `status` 参数时打印 `OK`、`Running` 或 `running`。参见第 6 节关于使用脚本 Heartbeat 资源脚本的讨论。

使用 `haresources` 控制资源的强大和灵活性将在第 8 节中介绍。

## 使用 HEARTBEAT 重新启动守护进程

你可以告诉 Heartbeat 在每次启动时启动守护进程，并在它停止时重启它。为此，在 `ha.cf` 文件中使用如下行：

```
respawn /usr/bin/daemon
```

在此示例中，`testlab` 是用于数字签名心跳包的密钥，安全哈希算法 1 `sha1` 是使用的数字签名方法。将示例中的 `testlab` 修改为你创建的密码，并确保两个系统上相同。

---

## 第 7 节

## 第 4 步：配置 `/etc/ha.d/authkeys`

在这一步中，我们将安装名为 `/etc/ha.d/authkeys` 的安全配置文件。Heartbeat 发行版带的示例配置文件需要进行以下操作以保护配置：

- 1. 使用以下命令找到并复制示例 authkeys 文件：

```bash
#rpm -qd heartbeat | grep authkeys
#cp /usr/share/doc/packages/heartbeat/authkeys /etc/ha.d
```

- 2. 编辑 `/etc/ha.d/authkeys` 文件，使未注释的行看起来如下：

```
auth1
1 sha1 testlab
```

> 注意 在这些行中，不要将数字 1 误认为字母 L。第一行是 auth 后面跟着数字 1，第二行是数字 1 后面跟着 sha、数字 1 然后是 testlab。

在此示例中，`testlab` 是用于数字签名心跳包的密钥，和。

- 3. 确保 authkeys 文件仅对 root 可：

```bash
#chmod 600 /etc/ha.d/authkeys
```

> 警告 如果没有使用 `chmod` 命令更改此文件的安全性，Heartbeat 程序将无法启动，并在 `/var/log/messages` 文件中抱怨你设置此文件的安全性。

## 第 5 步：在备份服务器上安装 Heartbeat

按照本章“第 1 步：安装 Heartbeat”所述在备份服务器上安装 RPM 包，或者使用第 5 节描述的 SystemImage 包克隆主服务器。然后在主服务器上执行以下命令，将所有配置文件拷贝到备份服务器：

```bash
#scp -r /etc/ha.d backupnode:/etc/ha.d
```
