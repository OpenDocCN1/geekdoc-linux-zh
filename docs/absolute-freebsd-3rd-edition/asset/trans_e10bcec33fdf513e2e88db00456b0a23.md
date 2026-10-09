

## 监狱配置参数

通过名称为每个监狱指定标识。在监狱名称后的花括号内给出监狱参数。每个参数定义以分号结尾。

许多监狱参数使用等号，用于将参数赋值为某个值。在此示例中，我将参数 `path` 设置为值 `/jail/mariadb`：

```
path="/jail/mariadb";
```

其他参数仅通过其存在即可启用或禁用某项功能。在此示例中，我指示该监狱启用 `mount.devfs` 功能：

```
mount.devfs;
```

监狱支持大量“mount”参数，并针对不同文件系统提供子参数。此特定参数专门用于挂载 devfs。

通过在特定参数前添加 *no*，可以关闭监狱中的切换项。如果不想启用 devfs，我不需要关闭整个 mount 参数；我只需在 *devfs* 前加上 *no*。

```
mount.nodevfs;
```

以下是我定义名为 *mariadb* 的监狱的方式：

```
mariadb {
    host.hostname="mariadb.mwl.io";
    ip4.addr='203.0.113.51';
    path="/jail/mariadb";
    mount.devfs;
    exec.clean;
    exec.start="sh /etc/rc";
    exec.stop="sh /etc/rc.shutdown";
}
```

参数 `host.hostname` 指定了监狱的主机名。虽然监狱名称为 *mariadb*，但该主机通过互联网主机名 *mariadb.mwl.io* 来标识自己。

IP 地址位于 `ip4.addr` 中。我已为此监狱分配了地址 203.0.113.51。该 IP 地址必须首先存在于宿主机上。

监狱的根目录放在 path 变量中。在此示例中，它被设置为 *jail/mariadb*。

几乎所有监狱都需要访问 /dev 中的特定设备节点，这要求在监狱内挂载 devfs（参见第 13 章）。使用 mount.devfs 设置来启用 devfs。监狱默认只能获取极少数的特定设备节点。不可信用户有时可以利用设备节点逃逸出监狱，因此切勿在未仔细研究的情况下添加额外的设备。你可以通过自定义 devfs 规则集来允许其他设备节点。使用 jail.conf 中的 devfs_ruleset 参数将自定义 devfs 规则集分配给监狱。我强烈建议以默认的监狱 devfs 规则为基础，并解除该监狱所需额外设备的隐藏，而不是尝试从零开始构建自定义 devfs 规则集。

被隔离（jailed）进程可以从父进程继承其环境的一部分。exec.clean 选项告知 jail(8) 剥离除 $TERM 之外的所有环境变量。环境变量 $HOME、$USER 和目标环境（通常是监狱 root 账户的环境）会被设置为该环境。你几乎总是需要 exec.clean。

exec.start 和 exec.stop 选项告知 FreeBSD 如何启动和停止监狱。

### 监狱内启动

监狱可以模拟完整运行的 FreeBSD 用户空间、运行单个进程，或介于两者之间的任何状态。你必须使用 jail.conf 中的 exec.start 参数来告知 FreeBSD 在监狱内运行什么进程，或者使用 persist 参数来声明即使监狱内没有进程运行，你也希望该监狱存在。在此示例中，我使用标准的 FreeBSD 启动脚本启动了完整的 FreeBSD 用户空间：

```
exec.start="/bin/sh /etc/rc"
```

如果你只需要在监狱内运行单个命令，你可以编写自己的启动脚本，并使用 exec.start 在监狱启动时运行它。你新建的监狱尚未有 rc.conf，因此它不会启动任何额外进程。

你可以代替 exec.start 而设置 persist 选项。这告知 FreeBSD 即使内部没有运行任何进程，监狱也可以存在。同时包含 persist 和 exec.start 意味着 FreeBSD 会为监狱启动一个进程，但当该进程停止运行时，监狱不会自行关闭。

你可以通过 exec.poststart 选项告知监狱在启动后运行额外命令。使用 exec.poststart 列出的任何命令或脚本会在正常的 /etc/rc 启动过程（包括任何已启用的软件包）完成后在宿主机上运行。这允许你编写脚本来粘合各个监狱。

类似地，你可以使用 exec.prestop 选项在停止监狱之前于宿主机上运行命令。当系统管理员关闭监狱时，宿主机首先运行此命令，然后监狱运行正常的关闭命令。

exec.stop 命令告知 FreeBSD 在监狱内部运行什么命令来关闭监狱。如果你在模拟完整监狱，你可能会运行 /bin/sh /etc/rc.shutdown，如上一节示例中所示。

## 监狱默认值

你会发现许多监狱共享通用设置。你可以在配置文件中定义这些设置。除非你进行覆盖，否则所有监狱都将使用这些设置。在使用单个监狱时，这似乎意义不大。

```
exec.start="/bin/sh /etc/rc";
exec.stop="/bin/sh /etc/rc.shutdown";
exec.clean;
mount.devfs;

mariadb {
    host.hostname="mariadb.mwl.io";
    ip4.addr="203.0.113.221";
    path="/jail/mariadb";
}
```

但是，鉴于此配置，添加另一个监狱只需包括花括号在内的五行代码。

```
httpd {
    host.hostname="httpd.mwl.io";
    ip4.addr="203.0.113.222";
    path="/jail/httpd";
}
```

在几十个监狱中，这节省了大量的麻烦。

你可以在监狱的定义内覆盖默认值。如果我不想在某个监狱中挂载 devfs(5)，我会为该特定监狱设置 mount.nodevfs。

### jail.conf 变量

你可以在监狱中使用变量替换。虽然你可以定义其中一些变量，但你也可以从监狱的设置中获取一些变量。变量会在双引号和未加引号的字符串中展开，但不会在单引号字符串中展开。

在此示例中，我为包含所有监狱的目录定义了一个变量，并在监狱定义内部使用它：

```
$j="/jail";
mariadb {
    path="$j/mariadb";
    --snip--
}
```

如果我必须将监狱移动到新的文件系统或池，我可以通过修改变量来更新 jail.conf，而不是编辑每个定义。

### 作为变量的参数

一旦你定义了监狱参数，就可以将其用作变量。每个监狱至少有一个参数：name。你可以使用这些参数来进一步扩展默认设置。

```
$j="/jail";
path="$j/$name";
host.hostname="$name.mwl.io";

mariadb {
    ip4.addr="203.0.113.221";
}
```

通过设置全局默认 path 为 `$j/$name`，我消除了为每个单独监狱定义 path 的需求。

你可以通过将参数括在花括号内来使用包含点号的多项参数。虽然这对 `mount.devfs` 这样的参数没有意义，但对于每个监狱的参数，如 `host.hostname`，则很有用。

```
path = "/jail/${host.hostname}";
```

我更喜欢将监狱放在以较短名称命名的目录中，而不是以主机名命名，但请随意遵循你自己的偏好。

将参数和变量与连贯的目录布局结合使用，可以让你将每个监狱定义压缩为单个配置语句。

## 测试和配置监狱

一旦你有了监狱的文件，就把自己锁定在里面。运行 jail(8) 命令在监狱内部运行单个命令。你需要四个参数：路径、监狱名称、主 IP 地址和要运行的命令。

```
# jail <path to jail> <jail name> <jail IP> <command>
```

在此示例中，我使用位于 `/jail/mariadb`、名为 `mariadb`、IP 地址为 203.0.113.51 的监狱，运行命令 `/bin/sh`：

```
# jail /jail/mariadb mariadb 203.0.113.51 /bin/sh
#
```

运行 ls(1)。你位于监狱文件系统的根目录中。这个监狱并非完全处于单用户模式，但这里除了 `/bin/sh` 外没有其他程序在运行。你可以进行一些基本设置，但即使 devfs(5) 也未挂载。

```
# ps
ps: /dev/null: No such file or directory
```

是的，正常的监狱启动过程会挂载 /dev —— 但监狱没有用户账户，没有 root 密码，没有运行中的守护进程，绝对没有任何可选组件。在启动监狱之前配置它。

## 从宿主机窃取的内容

一些宿主机设置信息在监狱内也很有用。你可以将这些信息从宿主机复制到监狱，但必须从宿主机执行此操作，而不是从监狱执行。

每个监狱执行自己的 DNS 解析。你可以将宿主机的 /etc/resolv.conf 复制到监狱中。

你的监狱可能共享与宿主机相同的时间区。将宿主机的 /etc/localtime 复制到监狱中，或在监狱内运行 tzsetup(8) 以选择新的时区。

## 创建 /etc/fstab

许多程序和脚本（包括 /etc/rc）期望找到 /etc/fstab，如果它不存在就会报错。在真实服务器上要求 /etc/fstab 是完全合理的，但被隔离的机器不需要文件系统表。创建一个空的文件系统表。

```
# touch /etc/fstab
```

我不介意不快乐的程序。我只是不想听它们抱怨。

## 创建 /etc/rc.conf

你要么从宿主机管理所有监狱，要么通过 SSH 管理监狱。你需要为 sshd 添加一个 /etc/rc.conf 条目。

```
sshd_enable="YES"
```

在创建此文件时添加你希望的任何其他设置。如果你知道某些设置是软件包需要的，提前设置它们并无坏处。

