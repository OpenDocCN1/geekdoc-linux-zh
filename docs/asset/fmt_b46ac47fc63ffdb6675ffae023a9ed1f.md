
nameserver 10.0.0.5

search mydomain.org

### 持久化注册

我们手动注册了 `mydomain.org`。将此注册自动化可能不是一个坏主意，这样它就可以在系统初始化期间发生，无需人工干预。此外，自定义名称服务器和搜索域可能是为了覆盖 DHCP 服务器（或类似设备）定义的项，并且应该始终排在自动生成的项之前。长话来说，事实我们可以简单地向 `lo` 段中添加类似的参数即可完成（删除注册后）：`lo` 接口的名称服务器和搜索域具有最高优先级。

```
# resolvconf -d mydomain
# grep -v '^# ' /etc/network/interfaces
```

```
face lo inet loopback
dns-nameserver 10.0.0.5
search mydomain.org
```

```
# ifdown lo; ifup lo
# grep -v '^# ' /etc/resolv.conf
nameserver 10.0.0.5
nameserver 192.168.40.5
search mydomain.org debianbook.info
```

自定义设置也可以写入标准 `/etc/resolv.conf` 对应的 `/etc/resolvconf/resolv.conf.d/base` 中。该文件中的项始终会被 `resolvconf` 放置在其他项之前。因此，以下操作与通过接口配置名称服务器和搜索域的效果相同：

```
# cat <<EOF > /etc/resolvconf/resolv.conf.d/base
nameserver 10.0.0.5
search mydomain.org
EOF
```

`resolvconf` 根据 `/etc/resolvconf/resolv.conf.d` 下的文件和动态内容如下组装 `/etc/resolv.conf` 文件：首先，它包含头文件的内容，随后按定义的顺序唯一的解析器指令列表。然后，它将尾文件的内容连接到 `/etc/resolv.conf` 的末尾。

> ¹¹`/etc/resolvconf/update.d/libc` 脚本实际上处理了组装。

### 钩子 (Hooks)

`/etc/resolvconf` 目录包含三个影响向 `resolvconf` 注册的解析器数据处理的目录。然而，`update.d` 目录属于 `resolvconf`。在编写本文时，`resolvconf` 包提供了两个脚本：`bind` 将 DNS 服务器更改绑定到转发集合，而 `libc` 创建 `/etc/resolvconf` 文件。另外两个目录 `resolvconf.d` 和 `update-libc.d` 由后者脚本使用：`resolvconf.conf` 包含组装 `/etc/resolvconf` 的文件（见上文），当文件更改时，`libc` 脚本会对 `update-libc.d` 目录执行 `run-parts`，这可以通知运行中的进程变更。

（注：原文此处存在大量重复的 OCR 错误文本，已根据核心逻辑进行清理翻译。）

# Debian 系统管理

已建立。后者在连接成功后，在不影响正常操作的情况下诊断连接问题时特别有用。要断开连接，你使用 `poff`。它接受连接名称作为参数并导致相应的 `ppd` 进程终止。如果没有指定提供者，只有在恰好打开了一个连接时（无论其是什么），`poff` 才会关闭连接。通过 `-a` 选项，你可以使用 `poff` 终止所有运行中的 `ppd` 连接。或者，你可以使用 `poff` 来控制运行中的 `ppd` 进程。当指定选项 `-d` 时，将切换相应的 `ppd` 进程的调试模式。指定选项 `-c` 告诉运行的 `pppd` 守护进程重新协商双方之间使用的压缩算法（这种情况很少），而 `-r` 则挂断连接并退出。

## pppd 配置文件

一个用于拨入提供商调制器以访问互联网的典型文件如下。名称是任意的，仅编码了国家和提供者名称。此文件可以手动创建或使用 `ppconfig` 管理，我们稍后会介绍它。每一行本质上都是 `pppd` 的一个选项，`ppd (8)` 手册描述了可用选项。

```
# cat /etc/ppp/peers/ch.sunrisendebug
hide-password
connect "/usr/bin/chat -v f /etc/chatscripts/pap -T 0041840556666"
115200
/dev/modem
noauth
remename ch.sunrise
user "madduck"
noipdefault
defaultroute
ippam ch.sunrise
```

注意这里缺少认证信息。虽然包含了用于与 PPP 服务器进行身份验证的用户名，但没有找到 `ppd`。将其包含在 `dip` 可读配置文件中，`ppd` 会遵循 `/etc/ppp/secrets` 和 `chap-secrets` 来处理 PAP 和 CHAP 认证协议，取决于使用哪一种（密码认证协议 `PAP` 是默认设置）。这些文件仅对 `root` 可读，且 `ppp` 设置为 `setuid root`。这两个文件都可以通过 `ppconfig` 管理，或使用任何普通编辑器。考虑这三列结构，每个密码（第三列）都绑定到一个用户名（通过 `user` 选项传递给 `pppd`）和一个提供者名称（`remename`）。例如：

```
# grep `madduck[[:space:]]*ch.sunrise` pap-secrets
sunset ch.sunrise topsecret
```

## 6.8 网络配置管理

在从 `/etc/ppp/peers` 读取特定连接配置之前，`pppd` 先从 `/etc/ppp/options` 读取选项，然后是 `.ppprc` 和 `/etc/ppp/options/<ttname>`，其中 `<ttname>` 是 `/dev` 中用于连接的设备名称。因此，可以通过在命令行传递参数，为每个用户覆盖全局选项，然后是每个设备、每个连接，最后是每次的调用。

## 连接脚本

`pppd` 的许多灵活性源于 `connect` 参数，该参数预期用于配置连接。`pppd` 在早期阶段执行指定的命令，并在完成后假设它正在与连接另一端的 PPP 服务器会话。如果提供连接的设备是模拟调制器，则 `chat` 是建立通信的工具。调制器（AT 命令）语言本质上是一种请求-响应协议，而这正是 `chat` 的擅长之处：它发送命令并等待响应，然后根据条件选择要发送的下一个命令。

在大多数情况下，通用脚本 `/etc/scripts/pap` 就是你所需要的。脚本期望使用 `-T` 选项为 `chat` 调用提供拨号数字（参见上述 `pppd` 对端 `peer` 配置中的 `connect` 行）。如果你的调制器需要特殊的初始化，或者由于某些原因你无法使用通用脚本，你可以创建一个副本并随心所欲地修改。为了防止调制器等待拨音，请使用以下脚本，并在对端配置文件中相应引用它。

```
$ grep -v '^# ' /etc/chatscripts/ch.sunrise
...
'' ATZ X3
...
OK-AT OK ATDT0041840556666
CONNECT \d/c
```
