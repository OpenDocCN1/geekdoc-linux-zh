
每当你更改 `smb.conf` 时，运行此命令以使用新的更改更新 Samba 软件。现在就运行它，将更改传播到 Samba。完成后，检查 Windows 机器，看看你是否可以浏览 Linux 机器。如果一切操作正确，你将看到你的 SuSE Linux 机器出现在 Windows 网络上（见图 15.3）。

### 图 15.3
将安全选项设置为 share 后，你可以查看 SuSE Linux 机器提供的共享。

![](img/659f91d9da7b29976c0625e2e9628511_331_0.png)

> **警告** 请注意，当前的 Samba 配置极其不安全。你绝不应在包含你不信任用户的实际网络中使用此配置。此配置纯粹是实验性的，目的是帮助你理解 `smb.conf` 的基础知识。请继续阅读以了解如何使事情更加安全。

回顾一下，你现在已经知道如何编写基本的 `smb.conf` 文件、添加简单的共享，以及告诉 Samba 你已更改了配置。让我们进一步了解 `smb.conf`。

文件 `smb.conf` 有一些特殊的节：

- `global`
- `homes`
- `printers`

## global 节

如前所述，此节包含适用于 Samba 的所有基本配置参数。你已经看到了其中的三个——`workgroup`、`server string` 和 `security`。让我们看看你可以使用的其他一些参数。

## netbios name 参数

正如你所见，Samba 默认使用你的机器的主机名作为其网络名称。你可以通过使用 `netbios name` 参数轻松更改此行为。例如，要将你的机器命名为 SuSELinux，你可以在 `smb.conf` 文件的全局节中添加 `netbios name = SuSELinux`。稍后你会看到，此选项可以用于其他更高级的方式。

## keep alive 参数

当客户端机器连接到 Samba 服务器时，会建立一个打开的连接，这会消耗资源。如果客户端机器崩溃，这个连接会保持打开状态。Samba 可能需要相当长的时间才能发现这个打开的连接实际上并未被使用，这会浪费更多资源。为了强制 Samba 检查其客户端，请设置 `keep alive = 30`。

## security 参数

此选项定义 Samba 使用的安全性。如你之前所见，当未设置此选项时，Samba 默认为 `user` 安全级别，这会强制连接的客户端输入密码才能使用服务器。将此选项设置为 `share` 则允许任何人浏览该机器。稍后将讨论，你可以同时使用两者——既需要密码又不需要密码。

## interfaces 参数

此参数告诉 Samba 使用哪个网络接口。默认情况下，Samba 使用机器上所有可用的接口。如果你只有一个接口，例如以太网卡，你实际上不需要此选项。但是，如果你有多个接口，并且不希望 Samba 在所有接口上监听，你可以强制它只监听你指定的那些接口。要使用此参数，你需要为其提供要使用的接口的 IP 和子网掩码。在不同接口之间使用空格作为分隔符。该参数的最终形式为 `interfaces = xxx.xxx.xxx.xxx/xxx.xxx.xxx.xxx xxx.xxx.xxx.xxx/xxx.xxx`。以下是一个示例：

`interfaces = 192.168.17.17/255.255.255.0`

## hosts allow 和 hosts deny 参数

你可以使用这些选项来控制哪些机器可以连接到你的 Samba 服务器。例如，要允许所有机器连接到你的服务器，但来自子网 192.168.121 的机器除外，你可以输入 `hosts allow = ALL EXCEPT 192.168.121..` 这将拒绝来自该子网的任何机器的访问。

specific subnet. The parameter `hosts deny` is the opposite of `hosts allow`. Parameters are separated by a space. The following is the supported identification format:

- Hostnames of the machines—For example, `ftp.sales.com`
- Domain names—For example, `.yahoo.com`
- IP of subnet ending with a dot—For example, `192.168.121.`
- Full IP—For example, `192.168.121.17`
- Netgroups (for NIS/NIS+)—For example, `@netgroup`
- The `ALL` and `EXCEPT` keywords—For example, `ALL EXCEPT .yahoo.com`

> **CAUTION**
> It's good practice to make sure that localhost is in the allow list. If it is not, certain programs, for example `smbpasswd`, will have to communicate with the Samba server in order to work. And, if localhost is not in the allow list, Samba will not answer these programs. Samba version 2.0.5 and up have localhost in the `hosts allow` list by default. If you are not sure which version you have, just add localhost to the `hosts allow` list.

## The guest account Parameter

When a guest logs on to a Samba controlled server, Samba needs to map that user to a user that it already has. On SuSE Linux, this is the user `nobody`. So, when a guest accesses the machine, anything she does on the system is regarded to be under the ownership of the user `nobody`. This is relatively secure because this user has no privileges or home directory. To tell Samba to use nobody as the user, enter `guest account = nobody` in the global section of `smb.conf`.

## The homes Section

The `homes` section is a special section because it represents the homes of the users as a share. To further understand this, you need to understand a bit about how Samba treats users.

Users in Samba belong to one of two groups, users or guests. Guests are those who do not have an account on the machine. Users, on the other hand, are those who have actual accounts on the machine. This means that a guest would not have a `/home/` directory, but a user would. For example, if John is a user on the system, he has a directory `/home/john`. And, if Andrew is just browsing the Linux box as a guest, he doesn't have a `/home/andrew` on the physical machine because he isn't a user on it.

The `homes` section tells Samba what to do with the homes of the users. You can tell Samba to show the home of the user connecting to the server as a share. This way, when the user browses the machine, he gets to view the contents of his home directory. This does require the user to enter his password, even if the `security = share`.

The format of the `homes` section is very simple; it starts with the `[homes]` tag. The next tag you should enter is the `comment` tag. This is a text comment that can be used to describe the share. So far it should look like this:

```
[homes]
comment = Home Directories
```
