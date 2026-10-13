
| `/dev/hda4` | | `ext2` `rw` 0 0 |

| `denon:export/home` | `/home` | `nfs` `rw,bg,intr,soft` 0 0 |

| `denon:export/usr/local` | `/usr/local` | `nfs` `rw,bg,intr,soft` 0 0 |

| `rane:export/mail` | `/var/spool/mail` | `nfs` `rw,bg,intr,soft` 0 0 |

# 使用 PPP 连接到网络

Red Hat Linux 已使通过 PPP（点对点协议）连接互联网的过程变得非常简单，并带有 GUI 界面。在继续之前，你需要确保以下几点：

- 你的 X Window 正在工作。这对于你将要用于配置 PPP 的工具是必要的。
- 你已经与本地 ISP 建立了账户。ISP 应该已经为你提供了电话号码、登录名、密码以及其 DNS 服务器的 IP 地址。
- PPP 服务已编译到你的内核中。如果你使用的是 Red Hat 发行版自带的内核，则不需要进行任何更改。
- 你的调制解调器已经连接并使用 `modemtool` 配置完成。`modemtool` 仅是将 `/dev/modem` 文件设置指向你调制解调器端口的相应设备名称的符号链接。

你没有默认路由。如果你在启动时设置了默认路由，请编辑 `/etc/sysconfig/network` 文件，使 `GATEWAY` 行显示为 `GATEWAY=` 并重启。

在完成这些必要设置后，你就可以开始配置 PPP 了。

> 注意
> 除非另有说明，否则本节中的所有命令必须以 root 用户身份运行。

## 简单客户端

如果 Red Hat 机器是一台没有配置其他网络的独立单元，或者你只想让你的 Red Hat 机器通过 PPP 连接到互联网，那么这就是你需要的全部配置。另一方面，如果你计划构建一个更复杂的网络，让 Red Hat 机器作为你访问互联网的接口，那么这只是开始，但也是必要的。

从启动 `netcfg` 工具开始来配置你的网络。如果你已经配置了 DNS，将将你的主机主机信息。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa_314_0.png)

要配置此窗口中的信息，请执行以下步骤：

- 1. 如果你还没有指定主机名，点击 Hostname（主机名）框并输入一个。
- 2. 在 Domain（域）框中，输入你 ISP 的域名。
- 3. 留 Search for hostnames in additional domains（在其他域中搜索主机名）框为空并跳到下方的 Nameservers（名称服务器）框。在这里，输入你的 ISP 提供的 DNS 服务器 IP 地址（每行一个 IP）。

## 硬件连接与设备

### 第三部分

你现在已准备好配置 PPP 设备。要做到这一点，请点击窗口顶部的 Interfaces（接口）按钮。窗口将变为看起来像图 13.6 一样。

### 图 13.6.

配置 PPP 之前的网络配置器接口菜单。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa_315_0.png)

- 4. 点击窗口底部的 Add（添加）按钮。将出现另一个另一个列出你的接口选项的窗口。选择 PPP 作为 Interface Type（接口类型）并点击 OK。Interface Options（接口选项）窗口将关闭，并出现 Create PPP Interface（创建 PPP 接口）窗口。

### 图 13.7.

网络创建 PPP 接口菜单。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa_315_1.png)

在继续之前，确保没有没有 PPP 密码的人在场。在 PPP 密码提示处，密码将以明文形式显示在屏幕上，任何从你肩后看的人都能看到。

- 5. 点击 Phone Number（电话号码）框并输入你 ISP 的电话号码。确保包含你可能为了禁用呼叫等待或接入外部线路而需要的任何特殊拨号前缀。
- 6. 跳过 Use PAP authentication（使用 PAP 身份验证）按钮，除非你的 ISP 有要求。在 PPP login name（PPP 登录名）框和 PPP password（PPP 密码）框中输入相应信息。

输入完 PPP 信息后，点击底部的 Customize（自定义）按钮。Create PPP Interface（创建 PPP 接口）窗口将出现。

### 13.8.

网络配置 PPP 窗口。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa_316_0)

## TCP/IP 网络管理

第 13 章

### 图 13.10.

带有 PPP 信息的网络配置器接口（Interfaces）菜单。

![](img/740d39911bdfa3e996ee27a7e4e7e4fa_318_0.png)

要恢复连接，只需运行 `netcfg`，从顶部菜单选择“Interfaces（接口）”，高亮 `ppp` 接口并点击“Activate（激活）”。

> **提示** 无需在每次想激活 PPP 连接时都启动 `netcfg` 程序，可以使用 `/etc/sysconfig/network-scripts` 目录下的命令行脚本。启动 PPP 的命令为：

```
./ifup-ppp ifcfg-ppp &
```

关闭 PPP 连接的命令为：

```
./ifdown-ppp ifcfg-ppp &
```

## 需需拨号 (On-Demand Dialing)

当你变得精通网络后，你可能会发现让机器自动拨号到互联网服务提供商（ISP）非常有用，每当检测到指向特定 IP 地址（例如你的 ISP DNS 服务器）的数据包时，它就会拨号。

当内核尝试连接到一个它没有路由的 IP 时，它会调用 `/sbin/request-route` 并传入目标 IP 地址。`request-route` 会检查是否存在与该地址对应的脚本。如果有，就会调用该脚本，该脚本据测会启动必要的连接以建立所需的路由。在大多数情况下，这就是 PPP 连接。

## 硬件连接与设备

然而，目前的设置存在轻微的局限性。如果你尝试连接到一个 PPP 连接应该是开启状态、但没有专门通过 `request-route` 设置以启动连接的 IP，内核将向调用程序返回错误。为了绕过这个问题，你可以使用稍微修改过的脚本，为所有无法访问的 IP 建立默认脚本调用。如果你运行自己的 DNS 服务器，此功能将别有用。

在使用新的 `request-route` 脚本之前，使用以下命令对原始脚本进行备份：

```
cp /sbin/request-route /sbin/request-route-orig
```

如果你决定恢复原始脚本，只需将 `/sbin/request-route-orig` 脚本复制回 `/sbin/request-route` 即可。

接下来，将以下行

```
if [ ! -f $chatfile ]; then chatfile=/etc/ppp/chat-default; fi
```

添加到 `request-route` 这一行之前

```
chatfile=/etc/ppp/chat.1
```

使用 `request-route` 时，你需要准备好调用 PPP 连接的脚本文件。你已经使用 `netcfg` 工具配置了 PPP，因此脚本已经完成，只需复制到 `/etc/ppp/chat-default` 即可

```
cp /etc/sysconfig/network-scripts/chat-ppp@ /etc/ppp/chat-default
```

这样做将设置你的默认 PPP 服务。如果由于某些原因你需要为特定的 IP 地址设置不同的网络连接，可以为该地址创建一个特定的脚本，并命名为 `/etc/ppp/chat.xxx.xxx.xxx.xxx.xxx.xxx`（即 IP 地址）。`request-route` 脚本会自动选择特定 IP 的脚本而非默认脚本。

默认情况下，PPP 连接将在空闲五分钟后自动关闭。你可以通过编辑 `request-route` 脚本，将字符串 `idle-disconnect` 后面的数字更改为你想要等待自动断开的时间。

如果你想在空闲超时之前强制断开连接，只需杀死 `pppd` 进程即可。然而，执行此操作时不要对 `kill` 使用 `-9` 选项，因为 `pppd` 会拦截标准终止信号并在退出前进行清理。

### 总结

正如在本章中所看到的，为系统添加网络访问和网络工具是一项极好的资产。在 Red Hat Linux 中，通过这些网络工具共享数据相对简单，考虑到这些工具为你的系统带来的强大，这令人印象深刻。

## TCP/IP 网络管理

第 13 章

以下是本章要点的总结：

- IP 地址是用于在网络唯一标识机器的数字。
- `net` 工具用于配置基本网络服务，例如设置网卡或 PPP 连接、建立路由、设置主机名和 DNS 信息以及设置 `/etc/hosts` 文件。
- 你可能需要手动配置网络接口，使用 `ifconfig` 命令设置你的 IP 号、子网掩码和广播地址。
