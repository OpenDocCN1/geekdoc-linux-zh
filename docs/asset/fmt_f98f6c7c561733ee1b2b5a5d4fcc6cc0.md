
SLIP 设备名称为 `sl0`、`sl1` 等。

### 内核编译选项：

```
Networking options --->
[*] slip (serial line) support
```

配置 SLIP 与配置以太网接口非常（参见“配置以太网设备”章节）。

这里有几个关键区别。

首先，SLIP 链路与以太网网络不同，网络上只有两个，分别位于链路的末端。以太网在你连接电缆时是可用的，而 SLIP 取决你拥有的链路类型，你可能需要以特殊的方式初始化网络连接。

如果你使用 `dip`，这通常不会在启动时完成，而是在稍后你准备好使用链路时。这个过程可以自动化。如果你使用 `scratch`，你可能想在 `rc.init` 文件中添加一个章节。这很快就会被描述。

SLIP 服务器有两种类型：动态 IP 地址服务器和静态 IP 地址服务器。每台 SLIP 服务器在拨号时都会提示你使用用户名和密码进行登录。

## 6.2.4 带有双工和线路的静态 SLIP 服务器。

SLIP 服务器是指为你提供了一个独占 IP 地址的服务器。每当你连接到服务器时，你都会用该地址配置你的 SLIP 端口。静态 SLIP 服务器会询问你的型号，立即提示你输入用户名和密码，然后将任何发往你地址的数据包路由到该连接。如果你有一个静态服务器，你可能想将你的主机和 IP 地址（因为你知道它是什么）输入你的 `hosts` 文件、`host.conf`、`resolv.conf` 等，`hostname` 和 `rc.local`。在配置 `rc.inet` 时，你不需要为 SLIP 连接添加任何特殊命令，因为是 `dip` 为你完成了配置接口的所有繁琐工作。你需要给 `dip` 适当的信息，它就会为你配置好接口。

如果你的 SLIP 服务器是这样工作的，那么你可以移动到“使用 Dip”章节学习如何进行相应配置。

## 6.2.5 带有双工和线路的动态 SLIP 服务器。

动态 SLIP 服务器是指每次登录时都从地址池中分配一个 IP 地址的服务器。这意味着无法保证每次都能获得特定的地址，而且该地址在你注销后可能会被其他人使用。配置 SLIP 服务器的网络管理员会为 SLIP 服务器分配一个地址池；当服务器接收到新的入站连接时，它会找到第一个未使用的地址，引导拨号者通过登录过程，然后向客户端显示一条消息，表示已为其分配了 IP 地址，并在持续期间使用该地址。

配置这种类型的服务器与配置静态服务器类似，不同之处是你必须添加一个步骤，获取服务器分配给你的 IP 地址，并用该地址配置你的 SLIP 设备。

再次，`dip` 会完成工作，而且新版本足够智能，不仅可以登录，还能自动读取欢迎消息中打印的 IP 地址并将其存储，以便你用它配置你的 SLIP 设备。

如果你的 SLIP 服务器是这样工作的，那么你可以移动到“使用 Dip”章节学习如何进行相应配置。

## 6.2.6 使用 Dip。

如前所述，`dip` 是一个强大的工具，可以简化并自动化拨号到 SLIP 服务器、登录、启动连接以及使用相应的 `ifconfig` 和 `route` 命令配置你的 SLIP 设备的过程。

本质上，你为 `dip` 使用一个“dip 脚本”，这基本上是一系列 `dip` 理解如何执行你想要执行的每个操作的命令列表。查看 `dip` 自带的 `sample.dip` 以了解它是如何工作的。`dip` 是一个非常强大的工具，有许多选项。这里不需要在这里深入介绍它的所有选项，你应该查看帮助你对应版本 `dip` 的 man 页面、README 和示例文件。

你可能会发现 `sample.dip` 假设你在使用静态 SLIP 服务器，因此你预先知道 IP 地址。对于动态 SLIP 服务器，新版本的 `dip` 包含一个命令，你可以用它自动读取并使用动态服务器分配给你的 IP 地址配置你的 SLIP 设备。以下示例是随 `dip337-uri.txt` 的 `sample.dip` 的修改版本，对你来说可能是一个很好的起点。你可能想将其保存为 `/etc/dipscript` 并根据你的配置进行编辑。

## 网络技术特定信息。

```
# 拨号 IP 连接程序。
# sample.dip
#    此文件（应显示）展示了如何使用 DIP
# 此文件对于 Annex 类型的动态服务器有效，如果你
# 使用静态地址服务器，则请使用作为 dip337-uri.tgz 包
# 携带的 sample.dip 文件。
#
# 版本：      (@sample.dip  1.40    07/20/93
#
# 作者：       Fred N. van Kempen, <waltje@uWalt.NL.Mugnet.ORG>
# main:
# 接下来，设置另一端的名称和地址。
# 我的拨号机名称为 'xs44all.hacktic.nl' (== 193.78.33.43)
get $remote xs44all.hacktic.nl
# 在 s0 上设置子网掩码为 255.255.255.0
netmask 255.255.255.0
# 设置所需的串口和速度。
port cua0
speed 3840

# 重置调制调器和终端线路。
# 这似乎给某些人带来了了麻烦！
reset

# 注意！“标准”预定义的错误值：
# 0 - OK
# 1 - CONNECT
# 2 - ERROR
# 准备拨号。
send ATQ0IE\r
wait OK
if $errvl != 0 goto modem_trouble
dial 556
if $errvl != 1 goto modem_trouble

# 我们已连接。登录系统。
login:
sleep 2
wait 20
if $errvl != 0 goto login_trouble
send LOGIN\n
wait 20
if $errvl != 1 goto password_error
send PASSWORD\n

# 我们现在登录了。
wait PROMPT 30
if $errvl != 0 goto prompt_error

# 命令服务器进入 SLIP 模式
send SLIP\n
wait SLIP 30
if $errvl != 0 goto prompt_error

# 从服务器获取并设置你的 IP 地址。
# 这里假设在命令服务器进入 SLIP
# 模式后打印你的 IP 地址
get $locip 30
if $errvl != 0 goto prompt_error

# 设置 SLIP 参数。
get mtu 296
# 确保 'route add -net default xs44all.hacktic.nl' 完成
# 并启动！
done:
print CONNECTED $locip
mode SLIP
goto error

prompt_error:
print TIME-OUT waiting for login...
goto error

login_trouble:
print Trouble waiting for Login...
goto error

password_error:
print Trouble waiting for the Password...
goto error

modem_trouble:
print Trouble occurred with the modem...
error:
print FAILED to $remote
quit

exit:
exit
```

上面的示例假设你正在调用动态 SLIP 服务器，如果你调用的是静态 SLIP 服务器，随 `dip337-uri.tgz` 的 `sample.dip` 文件应该对你有效。当 `dip` 搜索远端的类似于 IP 地址的入站文本时，这种修改是为了让从服务器获取的 IP 地址的过程能够自动化。上面的示例将自动通过你的 SLIP 链路创建默认路由，如果这不是你想要的，请从脚本中删除 `default` 命令。在此脚本完成后，如果你运行 `ifconfig` 命令，你会看到设备 `s0`。这就是你的 SLIP 设备。你可以在 `dip` 命令完成后使用 `ifconfig` 和 `route` 命令手动修改配置。

## 网络技术特定信息。

请注意，`dip` 允许通过 `mode` 命令选择不同的协议，最常用的是带压缩的 `cslip`。请注意链路的两端必须同意服务器的设置。

上面的示例是稳健的，应该处理大多数情况。请参考 `dip` 页面以获取更多信息。自然地，你可以使用示例代码，当服务器在规定时间内未连接时执行此类操作，或者如果你有多个服务器，可以尝试一系列服务器。

## 6.27 使用租用线路和 scratch 的 SLIP 连接。

如果你在两台机器之间幸运地拥有一条租用线路，或者你的机器与其他或其他连接，那么你不需要费力使用 `dip` 来设置串口线路。`scratch` 是一个非常易用的工具，将提供足够配置连接的功能。由于你的连接是永久性的，你需要在 `rc.inet` 文件中添加一些命令。对于永久连接，你需要做的是确保配置串口的速度，并将串口切换到 SLIP 模式。`scratch` 允许你通过一个命令完成这些。将以下内容添加到 `rc.inet` 文件：

```
# 附加租用静态 SLIP 连接
# 为 /dev/cu0 配置 19.2kbps 和 cslip
/sbin/scratch -p cslip -s 19200 /dev/cu0 &
/sbin/ifconfig sl0 IPA.IPA.IPA.IPA point IPR.IPR.IPR.IP up
# 结束静态 SLIP。
```

其中：

`IPA.IPA.IPA.IPA` 代表你的 IP 地址。

`IPR.IPR.IPR.IPR` 代表远端的 IP 地址。

`scratch` 将第一个未分配的 SLIP 设备附加到指定的串口。`scratch` 从 `sl0` 开始。因此，第一次命令将 SLIP 设备 `sl0` 附加到指定的串口，下次是 `sl1`，以此此类推。`scratch` 允许通过 `-p` 参数配置多个协议。在你的情况下，使用 SLIP 还是 `cslip` 取于你是否使用压缩。注意：双方必须同意是否使用压缩。

## 6.27 SLIP 服务器。

如果你有一台联网良好的机器，希望其他人能够拨入并提供网络服务，那么目前你需要将你的 Linux 配置为服务器。如果你想使用 SLIP 作为串口线路协议，目前你有三种配置你的 Linux 机器的方法。我倾向于使用第一种方法 `slipin`，因为它看起来最容易配置和理解，但我将提供每种方法的总结，以便你做出自己的决定。

### 6.27.1 使用 slipin 的 SLIP 服务器。

`slipin` 是一个程序，可以替代 SLIP 用户的普通登录 shell，将终端线路转换为 SLIP 线路。它允许你将你的 Linux 配置为静态地址服务器（用户每次拨入都获得相同的地址）或动态地址服务器（用户获得分配的地址，且不一定与上次拨入时相同）。

拨号者将按照标准登录流程登录，输入用户名和密码，但在登录后不是呈现 shell，而是执行 `slipin`，它会在配置文件（`/etc/slip.hosts`）中搜索与拨号者登录名匹配的条目。如果找到了，它将线路配置为 8bit 清线路，并使用 `ioctl` 调用将线路规则转换为 SLIP。当此过程完成后，配置的最后阶段

## 1262

发生时，`sliplogin` 会调用一个 脚本，该脚本使用相关的 IP 地址、子掩码配置 SLIP 接口并设置相应的路由。这通常被称为 `/etc/slip.login`，或者类似于 `getty` 的方式，如果你有某些需要特殊初始化的调用者，你可以创建一个名为 `/etc/slip.login` 的配置脚本，它将接替默认脚本专门为这些用户运行。

你需要配置三个或四个文件才能让 `sliplogin` 正常工作。我将详细说明如何以及在哪里获取软件以及每个文件的详细配置方法。文件如下：

- `/etc/passwd`，用于拨号账户。
- `/etc/slip.hosts`，包含每个拨号用户的唯一信息。
- `/etc/slip.login`，用于管理用户需要使用的路由配置。
- `/etc/slip.tty`，只有在你为服务器配置了动态地址分配时才需要，它包含一个地址表。
- `/etc/slip.logout`，包含在用户挂断或注销后清理环境的命令。

### 在哪里获取 sliplogin

你可能已经作为发行版的一部分安装了 `sliplogin` 包，如果没有，可以从 `sunsite.unc.edu/(pub/linux/system/Network/serial/sliplogin-2.1.1.tar.gz)` 获取。`tar` 包包含源码、编译后的二进制文件和一个 man 手页。

为了确保只有授权用户才能运行 `sliplogin` 程序，你应该在 `/etc/group` 文件中添加一个类似下方的条目：

```
slip::13:radio,fred
```

当你安装 `sliplogin` 包时，`Makefile` 会将 `sliplogin` 程序的组所有权更改为 `slip`，这意味着只有该组的用户才能执行它。上面的示例将仅允许 `radio` 用户执行 `sliplogin`。

要将二进制文件安装到你的 `/sbin` 目录中，并将 man 手页安装到第 8 节，请执行以下操作：

```bash
# cd /usr/src
# gzip -dc ...sliplogin-2.1.1.tar.gz | tar xvf -
# cd sliplogin-2.1.1
# < 如果你不使用 shadow 密码，请编辑 Makefile..
# make install
```

如果你想在安装之前重新编译二进制文件，请在 `make install` 之前添加 `make clean`。如果你想将二进制文件安装在其他地方，则需要编辑 `Makefile` 中的 install 规则。

请阅读随包附的 README 文件以获取更多信息。

### 为 Slip hosts 配置 /etc/passwd

通常情况下，你会在 `/etc/passwd` 文件中为 Slip 拨号者创建一些特殊的登录账户。通常遵循的惯例是使用带有 'S' 前缀的调用者主机名。例如，如果调用者名为 `radio`，那么你可以创建一个看起来如下所示的 `/etc/passwd` 条目：

`Srado:FVKrok73:1427:1 SLIP login:/tmp:/sbin/sliplogin`

账户叫什么并不紧要，只要它对你有意义即可。

注意：调用者不需要任何特殊的家目录，因为他们将不会从这台机器上获得 shell 界面，或者 `/tmp` 是一个不错的选择。另外请注意，`sliplogin` 是用来代替普通登录 shell 的。

## 网络技术特定信息。

### 配置 /etc/slip.hosts

`/etc/slip.hosts` 文件是 `slip` 搜索与登录名匹配的选项详情的文件。在该文件中，你指定将分配给调用者并配置使用的 IP 地址和子掩码。两个主机的示例（一个是主机 `radio` 的静态配置，另一个是用户 `albert` 的动态配置）可能如下：

```
# Sradio 44.136.8.99 44.136.8.100 255.255.255.0 normal -1
Salbert 44.136.8.99 DYNAMIC 255.255.255.0 compressed 60
```

`/etc/slip.hosts` 文件的条目如下：

1. 调用者的名称。
2. 服务器机器的 IP 地址，即本机器。如果此字段编码为 `DYNAMIC`，则将根据讨论过的 `/etc/slip.tty` 文件中的信息分配 IP 地址。注意：执行此操作必须至少使用版本 1.3 的 `sliplogin`。
3. 分配给调用机器的子掩码，采用 C 类网络掩码的点点十进制表示法 255.50。
4. `slip` 模式，允许你启用/禁用压缩和其他 `slip` 其他功能。
5. 超时参数指定了线路在自动断开之前可以保持空闲（未接收数据）的时间。负值表示禁用此功能。
6. 优化参数。

注意：你可以在字段 2 和 3 中使用主机名或点点十进制法的 IP 地址。如果你使用主机名，这些名称必须被解析，因此你的机器必须能够为这些主机名找到 IP 地址，否则脚本在调用时将失败。你可以通过尝试 `telnet` 主机名来测试，如果你收到 "Trying nnn.nnn.nnn..." 消息，说明你的机器已经为该名称找到了 IP 地址。如果你收到 "Unknown host" 消息，说明没有。如果是任一种情况，请使用点点十进制法的 IP 地址，或修复你的名称解析器配置（见 Name 节）。

最常见的 `slip` 模式是：

- `normal`
- `compressed`（启用压缩）

配置 `/etc/slip.hosts` 允许你启用/禁用压缩和其他 `slip` 功能。超时参数指定了线路在自动断开之前可以保持空闲（未接收数据）的时间。负值表示禁用此功能。优化参数。

注意：你可以在字段 2 和 3 中使用主机名或点点十进制法的 IP 地址。如果你使用主机名，这些名称必须被解析，因此你的机器必须为这些主机名找到 IP 地址，否则脚本在调用时将失败。你可以通过尝试 `telnet` 主机名来测试，如果你收到 "Trying nnn.nnn.nnn..." 消息，说明你的机器已经为该名称找到了 IP 地址。如果你收到 "Unknown host" 消息，说明没有。如果是任一种情况，请使用点点十进制法的 IP 地址，或修复你的名称解析器配置（见 Name 节）。

最常见的 `slip` 模式是：

- `normal`
- `compressed`（启用压缩）

配置 `/etc/slip.hosts` 允许你启用/禁用压缩和其他 `slip` 功能。超时参数指定了线路在自动断开之前可以保持空闲（未接收数据）的时间。负值表示禁用此功能。优化参数。（此处注：原文此处存在大量重复段落，译文已按要求完整翻译并保持格式一致）

最常见的 `slip` 模式是：

- `normal`
- `compressed`（启用压缩）

配置 `/etc/slip.hosts` 允许你启用/禁用压缩和其他 `slip` 功能。超时参数指定了线路在自动断开之前可以保持空闲（未接收数据）的时间。负值表示禁用此功能。优化参数。

最常见的 `slip` 模式是：

- `normal`
- `compressed`（启用压缩）
