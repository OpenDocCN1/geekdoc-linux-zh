
如果在不使用 -s 标志的情况下运行 keyinit（参见第 125 页的示例 6-6），它必须在服务器上本地执行，因为它需要机密密码（再次强调，您不希望机密密码通过网络传输）。

### keyaudit 脚本

keyaudit 脚本位于 /usr/src/skey/tools 目录下，是一个 bourne shell 脚本，用于检查 /etc/skeykeys 中找到的每个用户剩余的 OTP 密码数量。如果某个用户剩余的一次性密码数量小于或等于 11 个，keyaudit 将向管理员发送电子邮件消息，提醒他或她为该用户或那些列表即将用完的用户生成新的列表。为了使 keyaudit 脚本在 Linux 上正常工作，您需要对其进行修改。将行

```
HOST='/usr/ucd/hostname'
```

更改为

```
HOST='/bin/hostname'
```

此外，您还需要更改脚本中的 ADMIN 变量，将其设置为一个会阅读邮件并对 keyaudit 发出的消息采取行动的人。例如，如果用户 bill 是管理员，我们将把行

```
ADMIN=chasin
```

更改为

```
ADMIN=bill
```

这样 keyaudit 脚本就能正常工作了。keyaudit 脚本还可以接受一个数字参数，表示剩余的 OTP 数量。例如，您可以执行 `keyaudit 15`，然后它会遍历 /etc/skeykeys 中所有序列号小于或等于 14 的用户。请记住，/etc/skeykeys 文件中的序列号比用户列表中实际剩余的一次性密码数量多 1。如果找到的序列号严格小于 3，邮件的主题行将反映出消息的重要性。您可以设置 keyaudit 在 cron 中定期运行。

### 使用 1.1b 版本的替代程序

到目前为止，我们只考察了使用 keysh 来普遍调用 S/Key 系统。在许多情况下，这是一种有效的方法。对于所有不允许在控制台登录的用户，这也是一种有效的方法。

您可能希望使用或额外使用 /usr/src/skey/misc 目录中提供的某个支持 S/Key 的替代程序。如前所述，这些程序包括 su、login 和 ftpd。如果您正在使用 PAM（您应该这样做），您可能不希望使用这些程序。但是，如果您选择或需要使用其中一个或多个，您可以编译它们并替换原始二进制文件。我们不会详细介绍 S/Key 1.1b 版本的具体步骤；相反，我们将更详细地讨论 OPIE 的替代程序（参见第 132 页的 OPIE），并建议在这种情况下认真考虑使用 OPIE 而非 S/Key 1.1b 版本。OPIE 相对于 S/Key 1.1b 版本提供了多项改进。此外，我们之前讨论的大部分内容也适用于 OPIE。

## S/Key 版本 2.2

S/Key 版本 2.2 在多个方面与 1.1b 版本不同：

- 1. 版本 2.2 对种子选择进行了伪随机化。
- 2. 它引入了访问控制列表。
- 3. 它整合了 MD4 和 MD5 两种算法。
- 4. keyinit 实用程序不再提示用户输入 Linux 密码。
- 5. 它只提供 login 替代程序；没有 keysh、su 或 ftpd。

版本 2.2 的主要优势是列表中的前三项。第 4 项以牺牲安全性为代价，提供了适度的便利性提升。第 5 项限制了其整体灵活性。第 1 至第 3 项中的所有优势都已整合到 OPIE 中，且不受第 5 项的限制。因此，我们的讨论将转向 OPIE。

## OPIE

OPIE 程序由海军研究实验室（NRL）的 Randall Atkinson、Dan McDonald 和 Craig Metz 创建。源代码和二进制文件根据随软件附带的许可条款公开可用。请确保您阅读并遵守所有许可协议和版权声明。所需的致谢声明显示在示例 6-15 中。

### 示例 6-15 OPIE 致谢

```
This product includes software developed by the University of California, Berkeley and its contributors.
This product includes software developed at the Information Technology Division, US Naval Research Laboratory.
This product includes software developed by Craig Metz, The Inner Net, and other contributors.
```

OPIE 与 S/Key 非常相似，实际上它是从 S/Key 衍生而来的。OPIE 的密钥生成算法与 S/Key 1.1b 版本的算法几乎完全相同，唯一的区别在于它提供了对 MD5 的支持。如果您目前使用的是 MD4 S/Key，您可以升级到 OPIE 并保留现有的 OTP 列表。表 6.1 列出了 OPIE 中的命令与 S/Key 中的对应关系。

**表 6.1 S/Key 与 OPIE 命令和文件对照表**

| S/Key 命令和文件 | OPIE 命令和文件 |
| :--- | :--- |
| keyinit | opiepasswd |
| key | opiekey |
| keyinfo | opieinfo |
| /etc/skeykeys | /etc/opiekeys |
| /etc/skey.access (v2.2) | /etc/opieaccess |

S/Key 1.1b 版本和 OPIE 都提供 su、login 和 ftpd 的替代程序。OPIE 不提供 keysh 或 keyaudit 的等效替代物。

### 顺便提一下...

修改 keyaudit 脚本以使其适用于 OPIE 非常简单，而且非常值得花费精力。除了在第 131 页“keyaudit 脚本”中已经提到的那些行之外，请将 keyaudit 中的以下行

```text
KEYDB=/etc/skeykeys
SECHO "Type \ `keyinit -s' to reinitialize your sequence number."
```

更改为

```text
KEYDB=/etc/opiekeys
SECHO "Type \ `opiepasswd' to reinitialize your sequence number."
```

并将所有对 S/Key 的引用更改为 OPIE。您可能还希望将该脚本重命名为 opieaudit。为了获得最紧密的安全性，请将脚本的权限设置为 500，并使其由 root 拥有。别忘了将其放入 cron！

## 获取和安装 OPIE

截至撰写时，OPIE 的当前版本为 2.32。您可以从以下地址获取

```
ftp://ftp.innert.net/pub/opie/
```

不幸的是，再次出现的情况是，压缩 tar 文件没有关联的数字签名。您获取的文件命名可能类似于 opie-2.32.tar.gz。第一步是应用 gunzip，然后使用 tar 提取文件。这将创建一个子目录，opie-2.32。在我们的示例中，我们假设 OPIE 文件位于 /usr/src/opie-2.32。

OPIE 版本 2.32 分发使用 GNU 自动配置实用程序 configure，该程序用于为系统自动配置 Makefile。有关此实用程序的更多信息，请查阅系统文档以及第 148 页“延伸阅读”中列出的参考资料。

成功配置、编译和安装 OPIE 所需的步骤是：

- 在 /usr/src/opie-2.32 中执行 configure。
- 在 /usr/src/opie-2.32 中执行 make。
- 在 /usr/src/opie-2.32 中执行 make install。

这些步骤中的每一步可能需要一个或多个可选参数，以根据您站点的需求实现 OPIE。以下部分讨论了最常用的选项，但请务必阅读包括 opie-2.32 子目录中找到的 README 和 INSTALL 文件在内的支持文档。

**在 /usr/src/opie-2.32 中执行 configure。** OPIE 的 configure 实现有许多选项。您可以通过执行 `configure --help` 来查看选项，如示例 6-16 部分所示。

### 示例 6-16 使用带有 --help 选项的 configure

```
# ./configure --help
Usage: configure [options] [host]
Options: [defaults in brackets after descriptions]
Configuration:
--cache-file=FILE       cache test results in FILE
--help                  print this message
--no-create             do not create output files
--quiet, --silent       do not print `CHECKING...' messages
...
<lots of output snipped>...
Features and packages:
--disable-FEATURE       do not include FEATURE (same as --enable-FEATURE=no)
--enable-FEATURE[=ARG]  include FEATURE [ARG=yes]
--with-PACKAGE[=ARG]    use PACKAGE [ARG=yes]
--without-PACKAGE       do not use PACKAGE (same as --with-PACKAGE=no)
--x-includes=DIR        X include files are in DIR
--x-libraries=DIR       X library files are in DIR
--enable and --with options recognized:
--enable-access-file=FILENAME
                        Enable the OPIE access file FILENAME
--enable-server-md4     Use MD4 instead of MD5 for the server
--disable-user-locking  Disable user locking
--enable-user-locking[=DIR]
                        Put user lock files in DIR [ /etc/opielocks ]
--enable-retype         Ask users to re-type their secret pass phrases
--enable-su-star-check  Refuse to switch to disabled accounts
--disable-new-prompts   Use more compatible (but less informative) prompts
--enable-insecure-override
                        Allow users to override insecure checks
--enable-anonymous-ftpp Enable anonymous FTP support
--disable-wtmp          Disable wtmp logging
#
```

显而易见的是，OPIE 的 configure 有很多选项。不幸的是，如果您不在命令行中指定某些选项，此输出并不总是清楚地告知您各个选项的默认值。在许多情况下，默认值是很明显的；例如，如果 --enable-
