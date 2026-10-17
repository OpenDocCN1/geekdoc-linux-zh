
```
$ cat /etc/apt/sources.list
#deb cdrom:[Ubuntu 20.04 LTS _Focal Fossa_ - Release amd64 (20200423)]/ focal main restricted

# See http://help.ubuntu.com/community/UpgradeNotes for how
# to upgrade to
# newer versions of the distribution.
deb http://us.archive.ubuntu.com/ubuntu/ focal main
deb http://us.archive.ubuntu.com/ubuntu/ focal-updates main
deb http://us.archive.ubuntu.com/ubuntu/ focal-updates main
# deb-src http://us.archive.ubuntu.com/ubuntu/ focal main
deb http://us.archive.ubuntu.com/ubuntu/ focal main restricted
deb http://us.archive.ubuntu.com/ubuntu/ focal-updates main restricted
# deb-src http://us.archive.ubuntu.com/ubuntu/ focal-updates main restricted

## Major bug fix updates produced after the final release of the
## distribution.
deb http://us.archive.ubuntu.com/ubuntu/ focal-updates main restricted
# deb-src http://us.archive.ubuntu.com/ubuntu/ focal-updates main restricted

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT
## receive any
## review or updates from the Ubuntu security team.
deb http://us.archive.ubuntu.com/ubuntu/ focal universe
deb http://us.archive.ubuntu.com/ubuntu/ focal-updates universe
deb http://us.archive.ubuntu.com/ubuntu/ focal-updates universe
# deb-src http://us.archive.ubuntu.com/ubuntu/ focal-updates universe

## N.B. software from this repository is ENTIRELY UNSUPPORTED
## by the Ubuntu
## team, and may not be under a free licence. Please satisfy
## yourself as to
## your rights to use the software. Also, please note that
software in
## multiverse WILL NOT receive any review or updates from the
Ubuntu
## security team.
deb http://us.archive.ubuntu.com/ubuntu/ focal multiverse
# deb-src http://us.archive.ubuntu.com/ubuntu/ focal
multiverse
deb http://us.archive.ubuntu.com/ubuntu/ focal-updates
multiverse
# deb-src http://us.archive.ubuntu.com/ubuntu/ focal-updates
multiverse

## N.B. software from this repository may not have been
## tested as
## extensively as that contained in the main release,
although it includes
## newer versions of some applications which may provide
useful features.
## Also, please note that software in backports WILL NOT
receive any review
## or updates from the Ubuntu security team.
deb http://us.archive.ubuntu.com/ubuntu/ focal-backports main
restricted universe multiverse
# deb-src http://us.archive.ubuntu.com/ubuntu/ focal-
backports main restricted universe multiverse

## Uncomment the following two lines to add software from
Canonical's
## 'partner' repository.
## This software is not part of Ubuntu, but is offered by
Canonical and the
## respective vendors as a service to Ubuntu users.
# deb http://archive.canonical.com/ubuntu focal partner
# deb-src http://archive.canonical.com/ubuntu focal partner

deb http://security.ubuntu.com/ubuntu focal-security main
restricted
# deb-src http://security.ubuntu.com/ubuntu focal-security
main restricted
deb http://security.ubuntu.com/ubuntu focal-security universe
# deb-src http://security.ubuntu.com/ubuntu focal-security
universe
deb http://security.ubuntu.com/ubuntu focal-security
multiverse
# deb-src http://security.ubuntu.com/ubuntu focal-security
multiverse

# This system was installed using small removable media
# (e.g. netinst, live or single CD). The matching "deb cdrom"
# entries were disabled at the end of the installation
# process.
# For information about how to configure apt package sources,
# see the sources.list(5) manual.
```

首先，请注意该文件充满了有用的注释和警告。指定的库源使用以下结构：

```
deb (或 deb-src) 地址 发行版名称
软件包类型列表
```

`deb` 或 `deb-src` 值指示软件包类型。`deb` 值表示它是编译后程序的资源，而 `deb-src` 值表示它是源代码的资源。

`地址` 条目是软件库的 Web 地址。`发行版名称` 条目是该特定软件库的 `distribution` 版本名称。在示例中，`distribution` 名称为 `focal`。这并不一定意味着你正在运行的 `distribution` 是 Ubuntu 的 Focal Fossa；它仅表示该 Linux `distribution` 使用的是 Ubuntu Focal Fossa 软件库。例如，在 Linux Mint 的 `sources.list` 文件中，你会看到 Linux Mint 和 Ubuntu 软件库的混合使用。
