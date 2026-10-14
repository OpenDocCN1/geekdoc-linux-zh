
## 5 Debian 包管理系统

## 6.1 基础

这是适当的。例如，你通过向 `/etc/crontab` 添加一行来注册 cron 任务，还是通过将包含该行的文件丢入 `/etc/cron.d`，这并不重要，cron 都会安装 `/etc/crontab` 以及目录中的所有文件并使用它们。在 Debian 系统上，其他工具如 `APT`、`apache` 以及许多其他工具也是如此。这里的优势是，软件包可以将文件放入这些目录中，并让 `dpkg` 处理覆盖和配置文件的处理。虽然使用目录对 Debian 来说已不再特殊，但 Debian 系统是第一个引入该技术并使其普及的系统。

为了适应配置处理所需的规范，以及编辑器使用（且经常留下）的临时文件，只有名称包含字母、数字（`-`）和下划线（`_`）的文件（例如 `foo.dpkg-old` 和 `foo` 会被忽略）。此外，惯例是软件包安装与自身同名的文件，而管理员应该为本地提供的文件使用本地前缀。

对于许多用途的配置文件，以 cron 为例，你可能注意到系统中存在如 `/etc/cron.daily` 等目录。它包含了根据上述规则由软件包安装的标准可执行文件。这里的想法是，通过向此目录安装脚本，软件包只需请求该脚本每天运行一次，而无需必将脚本写在其他地方，并担心或受限于 cron 的配置语法。cron 的替代方案也可以尊重这些目录。

网络配置系统也是如此，它为连接建立后运行 cron 提供了类似的方向。这将在 6.8.1 节中进行详细讨论。

像 cron 这样的目录在本质上并不自然。事实上，如果你查看 `/etc/crontab`，单行代码就负责这种行为（略写）：

```
# grep '[[digit:]:]' /etc/crontab

17 * * * root run-parts --report /etc/cron.hourly

25 6 * * root run-parts --report /etc/cron.daily

47 6 * 7 root run-parts --report /etc/cron.weekly

52 6 1 * root run-parts --report /etc/cron.monthly
```

这种方法的核心，也是 Debian 系统最有用的发明之一，是 `run-parts`。该程序只需读取目录，并按照前面提到的命名方案（忽略临时文件）执行目录中的所有可执行脚本。通过 `--test` 选项，它可以仅打印它将执行的文件，通过指定 `--list`，你可以列出任何文件（仅可执行文件）。此列表在执行后可用于任何用途：

```
# touch /etc/cron.daily/foo /etc/cron.daily/bar.dpkg-old
# chmod +x /etc/cron.daily/bar.dpkg-old
# run-parts --list /etc/cron.daily | xargs -c
```

```
[...]
0 /etc/cron.daily/foo
[...]
2571 /etc/cron.daily/standard
1307 /etc/cron.daily/syslogd
```

尽管并不是所有工具都实际上使用 `run-parts` 来扫描目录，但人们普遍认为应该实现相同的行为。因此，`run-parts` 的行为是 Debian 配置文件处理策略的主要部分，也是系统管理最重要的范式之一。为了有效地处理 Debian 配置，你需要内化 `run-parts` 的功能。

### 6.1.2 覆盖权限

Debian 开发者在策略（见第 5.7 节）的帮助下，确保从 Debian 存档分发的软件包在安装时具有相同的所有者和权限。然而，本地策略可能要求某些文件具有不同的所有者或权限。一个有点过时但仍然相关的例子是 `wheel` 组，它被设置为 `wheel` 并具有 `754` 权限，以仅允许 `wheel` 组的成员使用该二进制文件¹。当包含 `/bin/su` 的软件包更新时，变化如下：

```
# chgrp wheel /bin/su
# chmod o-r /bin/su
# apt-get install --reinstall login
[...]
# ls -F /bin/su
-rwxr-xr-x 1 root wheel ... 8 ...
```

Debian 提供了 `dpkg-statoverride`，允许管理员告知 `dpkg` 下文件的特殊所有权和权限要求。在升级时，`dpkg` 将尊重通过 `dpkg-statoverride` 提出的请求。要让 `dpkg-statoverride` 立即实施设置，请使用 `--update` 标记：

```
# addgroup wheel
# dpkg-statoverride --update root wheel 754 /bin/su
# ls -F /bin/su
-rwxr-xr-x 1 root wheel ... 8 ...
[...]
# apt-get install --reinstall login
# ls -F /bin/su
-rwxr-xr-x 1 root wheel ... 8 ...
```

¹由于该二进制文件是免费提供的，因此没有必要让它不可读。请参见 Debian 策略第 10.9 节。

### 6.1.3 覆盖文件

`dpkg-divert` 是一个重重命名 `dpkg` 安装文件的工具，以便 `dpkg` 随后使用新位置。它被软件包用于覆盖功能。管理员也可以使用。例如，`postfix` 软件包安装传输代理。如果需要 TLS，可以安装 `postfix-tls` 软件包。它提供了 `postfix` 软件包的大部分内容。在后续，两个 `smtmp` 文件（带有后缀）的存在以及以下文件的关联：

```
# ls -F /usr/lib/postfix/smtmpd
/usr/lib/postfix/smtmp* /usr/lib/postfix/smtmp.postfix
# dpkg --search /usr/lib/postfix/smtmpd
diversion by postfix
diversion by postfix-tls to: /usr/lib/postfix/smtmp.postfix
```

对于 `dpkg` 来说，两个软件包都知道 `smtmp` 文件，但它也知道 `postfix-tls` 软件包被 `postfix` 重定向了。重点在于，当 `dpkg` 安装升级软件包时，它知道新的 `smtmp` 文件应该写入 `smtmp.postfix`；它不会覆盖属于 `postfix-tls` 的实际 `smtmp` 文件。

系统管理员可以使用重定向用自定义版本替换 `dpkg` 安装的文件，而不用担心这些自定义版本在升级时覆盖。假设你想提供 `/usr/share/misc/file` 的自定义版本，该文件由 `libmagic` 用于文件识别。以下对 `dpkg-divert` 的调用将起作用；`--rename` 关会导致文件重命名：

```
# ls -F /usr/share/misc/file
magic magic.mime
# dpkg-divert --add --rename /usr/share/misc/file to 'local diversion of /usr/share/misc/file/magic to /usr/share/misc/file.distrib'
# ln -s /etc/file/magic /usr/share/misc/file
# ls -F /usr/share/misc/file
@distrib magic.mime
```

当 `dpkg` 写入本地重定向的文件时，它使用文件的“真实名称”：用于重定向文件的名称。如果 `libmagic` 升级（或其他任何软件包）想要写入 `magic` 文件，`dpkg` 确保使用 `magic.distrib`。可以通过 `--diverion` 选项覆盖重定向中使用的文件名。准确的行为是，如果软件包重定向了文件 `bar`，`dpkg` 只允许 `foo` 写入原始文件的位置。如果任何其他软件包写入该文件，访问将被重定向。在下文中，我们使用 `echo` 命令模拟文件的更改：

```
# dpkg-divert --truename /usr/share/misc/file/magic /usr/share/misc/file.distrib
# echo >>/usr/share/misc/file/magic
# echo >>/usr/share/misc/file.distrib
# md5sum magic.distrib
68b329da9893e34097c8ad5bc9c940 magic
d80e7010c7dc1cfe7fd908b3a8c4f.distrib
# apt-get install --reinstall file
......
# md5sum magic.distrib
```
