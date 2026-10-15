
> 警告：并不强制要求存在 `/usr/lib64` 目录，且 LFS 编辑器决定不使用它。为了确保 LFS 和 BLFS 中的指令正确，该目录必须不存在。你应该不地验证它是否存在，因为很容易在无意中创建它，而这可能会破坏你的系统。

## 7.6. 创建基本文件和符号链接

在历史上，Linux 在 `/etc/mtab` 中维护一个挂载文件系统的列表。现代内核在内部维护此列表，并通过 `/proc` 文件系统将其暴露给你。为了满足期望找到 `/etc/mtab` 的工具程序，请创建一个符号链接

```bash
ln -sf /proc/self/mounts /etc/mtab
```

创建一个基础的 `/etc/hosts` 文件以便在某些测试中引用，并在 Perl 的配置文件中引用：

```bash
cat > /etc/hosts << EOF
127.0.0.1 localhost $(hostname)
:1 localhost
EOF
```

为了让 root 能够登录并识别 "root" 名称，`/etc/passwd` 和 `/etc/group` 文件中必须有相关的条目。

运行以下命令创建 `/etc/passwd` 文件：

```bash
cat > /etc/passwd << EOF
root:x:0:0:root:/bin/bash
bin:x:1:1:/bin:/sbin/nologin
daemon:x:2:2:/root:/sbin/nologin
sys:x:3:3:/root:/sbin/nologin
sync:x:4:65534:/sync:/bin
games:x:5:60:/usr/games:/sbin/nologin
man:x:6:6:/var/cache:/sbin/nologin
lp:x:7:7:/lp
mail:x:8:8:/var:/sbin/nologin
news:x:9:9:/var:/sbin/nologin
uu:x:65:65:/root:/sbin/nologin
sync:x:61:61:/games:/sbin/nologin
proxy:x:13:13:/root:/sbin/nologin
backup:x:34:34:/var:/sbin/nologin
irc:x:35:35:/var:/sbin/nologin
list:x:38:38:/root:/sbin/nologin
irc:x:39:39:/var:/sbin/nologin
gnats:x:41:41:/var/spool/gnats:/sbin/nologin
mod:x:42:42:/run:/bin/false
nobody:x:99:99:/nonexistent:/bin/false
systemd-network:x:96:96:/bin:/
messagebus:x:99:99:/run:/sbin/nologin
input:x:100:100:/run:/sbin/nologin
lpadm:x:101:101:/run:
video:x:102:102:/run:/sbin/nologin
audio:x:103:103:/run:/sbin/nologin
operator:x:104:104:/root:/sbin/nologin
ud:x:105:105:/run:/sbin/nologin
ubus:x:106:106:/run:/sbin/nologin
polkit:x:107:107:/run:/sbin/nologin
render:x:108:108:/run:/sbin/nologin
message:x:109:109:/run:/sbin/nologin
tss:x:110:110:/run:/sbin/nologin
iquid:x:111:111:/run:/sbin/nologin
ircd:x:112:112:/var/run/ircd:/sbin/nologin
dbus:x:113:113:/run:/sbin/nologin
bum:x:114:114:/run:/sbin/nologin
system-existent:x:115:115:/nonexistent:/sbin/nologin
system-times:x:116:116:/run:/sbin/nologin
system-machine:x:117:117:/run:/sbin/nologin
system-kernel:x:118:118:/run:/sbin/nologin
system-resolve:x:119:119:/run:/sbin/nologin
system-idle:x:120:120:/run:/sbin/nologin
system-backup:x:121:121:/run:/sbin/nologin
system-message:x:122:122:/run:/sbin/nologin
system-fs:x:123:123:/run:/sbin/nologin
system-reload:x:124:124:/run:/sbin/nologin
system-apt:x:125:125:/run:/sbin/nologin
system-cron:x:126:126:/run:/sbin/nologin
system-security:x:127:127:/run:/sbin/nologin
system-audit:x:128:128:/run:/sbin/nologin
system-update:x:129:129:/run:/sbin/nologin
system-log:x:130:130:/run:/sbin/nologin
system-network:x:131:131:/run:/sbin/nologin
system-network-manager:x:132:132:/run:/sbin/nologin
tester::/bin/bash
EOF
```

为了让 root 能够登录并识别 "root" 名称，`/etc/passwd` 和 `/etc/group` 文件中必须有相关的条目。

运行以下命令创建 `/etc/group` 文件：

```bash
cat > /etc/group << EOF
root:0
bin:1
daemon:2
sys:3
sync:65534
games:5
man:6
lp:7
mail:8
news:9
uu:65
sync:61
proxy:13
backup:34
irc:35
list:38
irc:39
gnats:41
mod:42
nobody:99
systemd-network:96
messagebus:99
input:100
lpadm:101
video:102
audio:103
operator:104
ud:105
ubus:106
polkit:107
render:108
message:109
tss:110
iquid:111
ircd:112
dbus:113
bum:114
system-existent:115
system-times:116
system-machine:117
system-kernel:118
system-resolve:119
system-idle:120
system-backup:121
system-message:122
system-fs:123
system-reload:124
system-apt:125
system-cron:126
system-security:127
system-audit:128
system-update:129
system-log:130
system-network:131
system-network-manager:132
tester:101
EOF
```

## 7.7. Gettext-0.22.4

Gettext 软件包包含了用于国际化和本地化的工具。这些工具允许程序在带有 NLS（本地语言支持）的情况下进行编译，使其能够以用户的母语输出消息。

预计编译时间：1.1 SBU

所需的磁盘空间：306 MB

### 77.7.1. 安装 Gettext

对于我们的临时工具集，我们只需要从 Gettext 中安装三个程序。

为编译准备 Gettext：

```bash
./configure --disable-shared
```

该 `configure` 选项的含义：

`--disable-shared`:

我们目前不需要安装任何 Gettext 共享库，因此没有必要构建它们。

编译软件包：

```bash
make
```

安装 `msgfmt`、`msgmerge` 和 `xgettext` 程序：

```bash
cp -v gettext-tools/src/{msgfmt,msgmerge,xgettext} /usr/bin
```

关于此软件包的详细信息，请参阅第 8.32.2 节，“Gettext 的内容”。

## 7.8. Bison-3.8.2

Bison 软件包包含一个解析器生成器。

预计编译时间：0.2 SBU

所需的磁盘空间：57 MB

### 7.8.1. 安装 Bison
