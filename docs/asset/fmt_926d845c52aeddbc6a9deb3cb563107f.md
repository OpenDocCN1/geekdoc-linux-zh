
第二步是防止远程主机——至少是你不希望访问服务器的远程主机。X 服务器有一个基于主机的访问列表，由 `xhost` 命令管理。要查看访问列表当前状态，只需输入 `xhost` 而不带参数：

```
gate% xhost
access control enabled, only authorized clients can connect
INET:gate.membrain.com
INET:localhost
```

这意味着基于主机的认证已开启。接下来列出了授予访问服务器的具体主机。在使用基于主机访问控制的系统上，初始设置为 `localhost` 和机器主机名。要完全禁用访问控制，使用命令 `xhost +`。这是危险的，因为任何拥有你机器 TCP 访问权限（可能是整个互联网）都可以访问你的显示器。

```
gate% xhost +
access control disabled, clients can connect from any host
INET:gate.membrain.com
INET:localhost
```

正如所说，这可能是一个坏主意，你可能想用 `xhost -` 重新开启限制：

```
gate% xhost -
access control enabled, only authorized clients can connect
INET:gate.membrain.com
INET:localhost
```

为了对允许访问的对象更加挑剔一些，你可以通过在 `xhost +` 语句上方添加你允许访问的主机主机名或 IP 地址来操纵访问列表：

```
gate% xhost +fritz.membrain.com
fritz.membrain.com being added to access control list
```

基于主机的访问控制的一个问题是，它仅仅是如此——所有人。membrain.com 都允许访问显示器。取决于环境的不同，这可能足够了。然而，允许从可能被你管理范围之外的人员访问的机器上的任何用户访问，可能是不可取的。为此，你需要 `xauth` 命令，并且你可能想要继续阅读。

> **注意**
>
> 关于 `xhost` 命令的更多信息，请参阅您的 X 分发版附带的手页。

## `xauth`: 更强的身份验证方法

访问控制的下一步是基于用户的，它依赖某些个性化信息来允许应用程序访问服务器。最后，设计的这些方法中的第一种被称为 MIT-MAGIC-COOKIE-1。它由 MIT 开发，与 `xdm`（此后某个时期）配合工作，在用户登录时生成一个随机字符串（“魔术饼干”），并将其存储在用户有权访问的文件中——通常是用户家目录下命名为 `.Xauthority` 的文件。然后 X 客户端读取此文件，找到与它尝试连接的主机对应的 cookie，并在建立连接时将其呈现给目标。如果你处于一个运行应用程序的机器之间共享家目录的环境中，那么 X 应用程序应该能够回到你登录的工作站，而无需通过 `xauth` 将它们添加。

这对于“共享文件空间”环境非常方便，但如果不使用它，使用 MIT-MAGIC-COOKIE-1 也并非不可能。这样做需要对 `.Xauthority` 文件中的数据进行操作，这是通过 `xauth` 命令完成的。这里列出了所需的基础：

1. 为想要连接的特定显示器提取 magic cookie。
2. 将提取出的信息复制到远程系统。
3. 将 magic cookie 导入远程系统或帐户的 `.Xauthority` 文件中。

有几种方法可以实现此。第一种是提取内容，将其保存到文件，将文件复制到远程机器，并从该文件导入。听起来有好几步，确实如此——使用 `rsh` 和管道有一种更简单的方法。（如果你在想，“为什么不使用 `ssh`？”，你确实应该这么想——只需假设你现在没有 `ssh`，因为如果有的话，你可能就不需要这样做了。）

```
xauth extract | $DISPLAY | rsh remotehost | xauth merge
```

当然，为了做到这一点，你需要在登录任何远程服务器并执行运行 X 应用程序之前运行此命令。这里有一个名为 `xrlogin` 的脚本，它可以做到这一点并确保你的 `DISPLAY` 变量在远程机器上被正确设置。由于它使用了 `login` 命令，它不会传播 `DISPLAY` 设置。然而，它会传播 `TERM` 设置，因此适当的 `DISPLAY` 设置附加在 `TERM` 设置上，要求目标系统在登录期间拆分此变量。相应的代码片段在后列出。

```
#!/bin/sh
#
# 至少我们需要主机名
#
if [ $# -lt 1 ]; then
echo "usage: xrlogin hostname [ username ]"
exit
fi

#
# 设置主机和用户名
#
r_host=${1}
ruser=${2:-`whoami`}

#
# 显示器名称必须是完全限定
#
if [ "$DISPLAY" = ":*" -o "$DISPLAY" = ":0.0" ]; then
if [ "$REM_DISPLAY" != "" ]; then
disp="\$REM_DISPLAY"
else
disp=`hostname` \$DISPLAY
fi

#
# 如果我们有显示器和 magic cookie，则传播 cookie
#
if [ -n "$disp" ]; then
foo=`xauth extract - ${disp}` 2> /dev/null
if [ "$foo" = "" ]; then
echo "No authority propagated"
else
xauth extract ${disp} | rsh ${r_host} -l ${r_user} xauth merge -
echo "Ok to ${disp} from ${r_user}@${r_host}"
fi
# 变形 TERM 变量
TERM=$disp.$TERM
export TERM
fi
# 执行连接
# exec rlogin ${r_host} -l ${r_user} -e -8
```

对于目标系统 shell 的适当 magic（这是 `.xrc` 文件的 csh/tcsh 格式）——应该根据其他 shell 类型进行适当修改：

```csh
if ($TERM = *) then
set foo=$TERM
setenv TERM $foo:e
setenv DISPLAY $foo:r
unset foo
endif
```

此时，有必要提一下，如果你使用 `ssh` 或其任何功能等效物（如 OpenSSH），那么这一切都是必需的。为什么要使用 `ssh` 呢？它的功能之一 X Forwarding 为你的 X 窗口应用程序通过加密的 SSH 通道与本地 X 服务器通信建立了通道。它通过监听远程机器上的 TCP 端口来实现，该端口通常分配给 X 服务器——通常是显示器编号10 之后的第一个未使用端口。然后它会在远程设置 `DISPLAY` 变量。

## 其他身份验证方案

MIT-MAGIC-COOKIE-1 并不是唯一的，但它是最常用的。其他方案包括通过加密 cookie 的 DES 和 MIT-AUTH。

## 开启安全功能

并不是所有的 X 分发版都配置为使用 `host`。事实上，某些操作系统供应商（例如早期的 SGI）默认关闭了它。我们稍后会查看如何开启它。

## 定制环境（作为用户）

在大多数环境中，用户可以通过名为 `.xsession` 的脚本来自定义整个环境，该脚本位于用户的家目录下。例如，一个简单的 `.xsession` 可以包含：

```
#!/bin/sh
exit
```

当用户登录（通过 X）时，此脚本会被执行。为了让会话稍微有用一点，我们可以在脚本中添加 `xterm`：

```bash
#!/bin/sh
xterm
```

## X 窗口系统

为了增加更多功能，你应该在组合中添加一个窗口管理器。为了演示起见，我们将使用 X 自带的唯一窗口管理器：`twm`。（是的，`twm` 可能不是现在的首选窗口管理器，但有些人仍然喜欢它。）当它被执行时，窗口管理器在以某种方式被杀死之前不会退出，因此它必须在后台运行。

```bash
#!/bin/sh
twm &
xterm
```

现在你可以自由拖动你的窗口——你正走向使用 X 环境之路。要将其他应用程序添加到你的环境中，只需将它们（后台运行）添加到你的会话中——当然，在“终端”程序（那个不在后台运行的）之前。

许多更现代的窗口管理器（某些已经不仅仅是窗口管理器，而是整个环境）具有集成的管理启动和运行其他应用程序的设施，并且可以单独（且不在后台运行）放在用户的 `.xsession` 文件中。这些窗口管理器的示例包括 `fwm`、`enlightenment` 和 `AfterStep`。

## 关键子系统

第二部分
