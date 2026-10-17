
这里变量 `EXCLUDE_FILES` 定义了不应拷贝到任何系统的文件。我们可以配合 `exclude` 指令使用该变量：

```
exclude (${EXCLUDE_FILES}) ;
```

你还可以使用 `exclude_pat` 指令排除匹配特定模式的文件。该命令支持基于 shell 类型的正则表达式进行匹配。然而，如果在配置文件中使用 `\` 和 `$`，必须对其进行转义。典型的示例包括 `exclude_pat *.h` 和 `exclude_pat .**`，它们将不会拷贝任何具有 `.h` 扩展的文件，也不会拷贝任何以点开头后跟数字的文件（通常情况下如此）。

## 调用命令

有时当远程系统上的特定文件或文件组已更新时，可能需要调用特定的命令。考虑这样一个例子：你同步了一个进程所需的配置文件，一旦文件更新，必须重启该进程以使用新配置。多个 UNIX 程序使用这种模型；在系统获取对配置所做的任何更改之前，你必须先通知系统。为了扩展这一点，请注意以下 rdist 配置：

```
HOSTS = ( dino wilma )
FILES = ( /etc/inetd/inetd.conf )
```

![](img/2928fe2a92e6fb43bbbe37680092f_637_0.png)

### UNIX 系统管理：入门指南

```
(${FILES}) -> (${HOSTS})
install -R;
notify root@pebble;
special "/usr/bin/kill -HUP"
```

此配置同时为 `dino` 和 `wilma` 使用 `/etc/inetd/inetd.conf` 文件。完成后，它通过 `special` 指令在两个系统上执行 `kill` 命令。此特殊命令接受一个参数并在所有目标系统上执行它。UNIX `kill` 命令将向 `inetd` 进程发送信号，导致其重新读取配置。因此，新推送的 `/etc/inetd/inetd.conf` 文件的任何更改将生效。如你所见，`rdist` 工具作为整体分发机制的一部分执行特定函数非常简单。

## 2.4 探索 rdist 示例

为了解释 `rdist` 如何在现实世界甚至可能的产品环境中使用，提供了一个更详细的示例。自然，该配置文件代表了解决典型的 UNIX 环境可能具有的需求的一种方法。此示例的某些需求包括

- 向不同的系统同步不同的文件集

- 在同步完成时发送通知

为了满足这些需求，提供了以下 rdist 配置：

| 行 | 内容 |
| :--- | :--- |
| 1 | `SERVERS = ( pebbles )` |
| 2 | `WORKSTATIONS = ( barney )` |
| 3 | `NETWORK_FILES = (` |
| 4 | `/etc/hosts` |
| 5 | `/etc/netmasks` |
| 6 | `/etc/resolv.conf` |
| 7 | `/etc/inetd.conf` |
| 8 | `/etc/passwd` |
| 9 | `/etc/nsswitch` |
| 10 | `/etc/profile` |
| 11 | `/etc/ftp` |
| 12 | `/etc/syslog` |
| 13 | `GENERAL_FILES = (` |
| 14 | `/etc/group` |
| 15 | `/etc/shadow` |
| 16 | `/etc/aliases` |
| 17 | `/etc/bash` |
| 18 | `/etc/cron` |
| 19 | `/etc/motd` |
| 20 | `/etc/fstab` |
| 21 | `SECURITY_MEDIA_FILES = (` |
| 22 | `/etc/issue` |
| 23 | `/etc/mail` |
| 24 | `/etc/rc` |
| 25 | `/etc/services` |
| 26 | `/etc/ssh` |
| 27 | `/etc/profile` |
| 28 | `/etc/bashrc` |
| 29 | `/etc/vimrc` |
| 30 | `/etc/gshadow` |
| 31 | `/etc/pamd` |
| 32 | `/etc/selinux` |
| 33 | `/etc/udev` |
| 34 | `/etc/systemd` |
| 35 | `/etc/iptables` |
| 36 | `/etc/ufw` |
| 37 | `/etc/utmp` |
| 38 | `/etc/wtmp` |
| 39 | `/etc/lastlog` |
| 40 | `/etc/securelog` |
| 41 | `/etc/ld.` |
| 42 | `/etc/ldd` |
| 43 | `APP_FILES = (` |
| 44 | `/usr/bin` |
| 45 | `/usr/sbin` |
| 46 | `/usr/lib` |
| 47 | `/usr/local` |
| 48 | `/usr/share` |
| 49 | `/bin` |
| 50 | `/sbin` |
| 51 | `/etc` |
| 52 | `/var` |
| 53 | `/root` |
| 54 | `/home` |
| 55 | `/opt` |
| 56 | `/dev` |
| 57 | `/proc` |
| 58 | `/sys` |
| 59 | `/tmp` |
| 60 | `/run` |
| 61 | `/boot` |
| 62 | `/media` |
| 63 | `/mnt` |
| 64 | `/srv` |
| 65 | `/root` |
| 66 | `/user` |
| 67 | `/bin` |
| 68 | `/sbin` |
| 69 | `/lib` |
| 70 | `/lib` |
| 71 | `/etc` |
| 72 | `/dev` |
| 73 | `/dev` |
| 74 | `/dev` |
| 75 | `/ptr` |
| 76 | `/etc` |
| 77 | `/run` |
| 78 | `/boot` |
| 79 | `/var` |
| 80 | `/var` |
| 81 | `/var` |
| 82 | `/var` |
| 83 | `/var` |
| 84 | `/var` |
| 85 | `/link` |
| 86 | `/etc` |
| 87 | `/etc` |
| 88 | `/etc` |
| 89 | `/etc` |
| 90 | `/etc` |
| 91 | `/etc` |
| 92 | `/etc` |
| 93 | `/etc` |
| 94 | `/etc` |
| 95 | `/etc` |
| 96 | `/etc` |
| 97 | `/etc` |
| 98 | `/etc` |
| 99 | `/etc` |
| 100 | `/etc` |
| 101 | `/etc` |
| 102 | `/etc` |
| 103 | `/etc` |
| 104 | `/etc` |
| 105 | `/etc` |
| 106 | `/etc` |
| 107 | `/etc` |
| 108 | `/etc` |
| 109 | `/etc` |
| 110 | `/etc` |
| 111 | `/etc` |
| 112 | `/etc` |
| 113 | `/etc` |
| 114 | `/etc` |
| 115 | `/etc` |
| 116 | `/etc` |
| 117 | `/etc` |
| 118 | `/etc` |
| 119 | `/etc` |
| 120 | `/etc` |
| 121 | `/etc` |
| 122 | `/etc` |
| 123 | `/etc` |
| 124 | `/etc` |
| 125 | `/etc` |
| 126 | `/etc` |
| 127 | `/etc` |
| 128 | `/etc` |
| 129 | `/etc` |
| 130 | `/etc` |
| 131 | `/etc` |
| 132 | `/etc` |
| 133 | `/etc` |
| 134 | `/etc` |
| 135 | `/etc` |
| 136 | `/etc` |
| 137 | `/etc` |
| 138 | `/etc` |
| 139 | `/etc` |
| 140 | `/etc` |
| 141 | `/etc` |
| 142 | `/etc` |
| 143 | `/etc` |
| 144 | `/etc` |
| 145 | `/etc` |
| 146 | `/etc` |
| 147 | `/etc` |
| 148 | `/etc` |
| 149 | `/etc` |
| 150 | `/etc` |
| 151 | `/etc` |
| 152 | `/etc` |
| 153 | `/etc` |
| 154 | `/etc` |
| 155 | `/etc` |
| 156 | `/etc` |
| 157 | `/etc` |
| 158 | `/etc` |
| 159 | `/etc` |
| 160 | `/etc` |
| 161 | `/etc` |
| 162 | `/etc` |
| 163 | `/etc` |
