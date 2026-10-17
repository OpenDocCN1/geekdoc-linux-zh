
```bash
-rw-r--r-- 1 user users     70 Jul 22 13:36 someFile.txt
drwxrwxrwx 2 user users  4096 Jul 21 07:18 test
```

权限格式为 `drwxrwxrwx`。第一个字符代表文件类型，如果是目录则为 `d`，否则不是。接下来的三个 `rwx` 是用户对文件的权限，再接下来的三个是组对文件的权限，最后三个是其他所有人对文件的权限。

`rwx` 中的 `r` 代表是否可以读取文件，`w` 代表是否可以修改文件，`x` 代表是否可以执行文件。如果未授予任何权限，则 `r`、`w` 或 `x` 的位置将是 `-`。

因此，从上例中可以看出，用户可以读取和修改 `someFile.txt`，但组只有只读权限。

如果你有 `sudo` 权限，可以使用 `chmod ### fileName` 命令来更改权限。`r` 由值 `4` 表示，`w` 由 `2` 表示，`x` 由 `1` 表示。因此，如果你只想能够修改 `test` 目录的内容

```bash
Owner rwx = 4+2+1 = 7
Group r-x = 4+0+1 = 5
Other r-x = 4+0+1 = 5
```

因此，整个命令是

```bash
chmod 755 test
```

现在执行 `ls -l` 将显示类似以下内容：

```bash
drwxr-xr-x 2 user users  4096 Jul 21 07:20 test
```

## 可读大小

与 `l` 选项一起使用的 `h` 选项显示人类可读的文件大小。运行

```bash
user@linux-computer:~$ ls -lh
```

将输出：

```bash
total 4166
-rw-r--r-- 1 user users     70 Jul 22 13:36 someFile.txt
drwxrwxrwx 2 user users  4.0K Jul 21 07:18 test
```

## 隐藏文件

要查看隐藏文件，使用 `a` 选项。例如

```bash
user@linux-computer:~$ ls -a
```

可能列出

## 总目录大小

要查看当前目录的大小，请使用 `s` 选项（也可以使用 `h` 选项使大小更易读）。

```
user@linux-computer:~$ ls -s
```

输出

```
total 4166
someFile.txt
test
```

## 递归视图

假设 `test` 目录中有一个名为 `anotherFile` 的文件，并且你希望从根文件夹查看它，你可以使用 `R` 选项，它会列出递归树。

```
user@linux-computer:~$ ls -R
```

输出

```
.
someFile.txt
test

./test:
anotherFile
```

# 第 2 章：检测 Linux 发行版名称和版本

## 2.1 节：检测你正在使用的基于 Debian 的发行版

只需执行 `lsb_release` `--a`。

在 Debian 上：

```
$ lsb_release --a
No LSB modules are available.
Distributor ID: Debian
Description:    Debian GNU/Linux testing (stretch)
Release:        testing
Codename:       stretch
```

在 Ubuntu 上：

```
$ lsb_release --a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 14.04.4 LTS
Release:        14.04
Codename:       trusty
```

如果没有安装 `lsb_release`，你可以尝试进行一些猜测，例如，`/etc/issue` 文件通常包含发行版名称。例如，在 ubuntu 上：

```
$ cat /etc/issue
Ubuntu 12.04.5 LTS \n \l
```

不要使用文件 `/etc/debian_version`，因为其内容不匹配发行版名称！

*注意，这在 Fedora、RHEL 或 openSUSE 等非 Debian 家族发行版上也能工作——但 `lsb_release` 可能未安装。*

## 2.2 节：检测你正在使用的基于 systemd 的发行版

此方法适用于 Arch、CentOS、CoreOS、Debian、Fedora、Mageia、openSUSE、Red Hat Enterprise Linux、SUSE Linux Enterprise Server、Ubuntu 及其他系统的新版本。这种广泛的适用性使其成为首选方法，如果还需要识别较旧的系统，可以回退到其他方法。

查看 `/etc/os-release`。具体来说，查看变量 `NAME`、`VERSION`、`ID`、`VERSION_ID` 和 `PRETTY_NAME`。

在 Fedora 上，该文件可能如下所示：

```
NAME=Fedora
VERSION="24 (Workstation Edition)"
ID=fedora
VERSION_ID=24
PRETTY_NAME="Fedora 24 (Workstation Edition)"
ANSI_COLOR="0;34"
CPE_NAME="cpe:/o:fedoraproject:fedora:24"
HOME_URL="https://fedoraproject.org/"
BUG_REPORT_URL="https://bugzilla.redhat.com/"
REDHAT_BUGZILLA_PRODUCT="Fedora"
REDHAT_BUGZILLA_PRODUCT_VERSION=24
REDHAT_SUPPORT_PRODUCT="Fedora"
REDHAT_SUPPORT_PRODUCT_VERSION=24
PRIVACY_POLICY_URL=https://fedoraproject.org/wiki/Legal:PrivacyPolicy
VARIANT="Workstation Edition"
VARIANT_ID=workstation
```

在 CentOS 上，该文件可能如下所示：

```
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```

该文件在 freedesktop 网站上有文档说明；原则上，它并不特定于 `systemd`——但它将存在于所有基于 `systemd` 的发行版中。

从 `bash` shell 中，你可以 `source` `/etc/os-release` 文件，然后直接使用各种变量，如下所示：

```
$ ( source /etc/os-release && echo "$PRETTY_NAME" )
Fedora 24 (Workstation Edition)
```

## 2.3 节：检测你正在使用的 RHEL / CentOS / Fedora 发行版

查看 `/etc/redhat-release` 的内容

```
cat /etc/redhat-release
```

这是一台 Fedora 24 机器的输出：Fedora release 24 (Twenty Four)

如基于 Debian 的回复中所述，你还可以使用 `lsb_release -a` 命令，该命令从 Fedora 24 机器输出以下内容：

```
LSB Version:        :   core-4.1-amd64:core-4.1-noarch:cxx-4.1-amd64:cxx-4.1-noarch:desktop-4.1-amd64:desktop-4.1-noarch:languages-4.1-amd64:languages-4.1-noarch:printing-4.1-amd64:printing-4.1-noarch
Distributor ID:     Fedora
Description:        Fedora release 24 (Twenty Four)
Release:            24
Codename:           TwentyFour
```
