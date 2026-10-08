

# pack, pcat, unpack 1009

- -f 强制打包文件。此选项用于打包整个目录，即使某些文件无法节省磁盘存储块。您可以使用 unpack 或 pcat 命令将打包后的文件还原到原始形式。

## 操作数

file 要打包、用 pcat 解包查看或解包的文件路径名。file 可以包含也可以省略 .z 后缀。

## 示例

在接下来的示例中，passwd 文件太小，无法节省任何磁盘存储块，因此未进行打包（未压缩）。termcap 文件足够大可以进行压缩，且压缩率为 29.8%。

```
castle@ pack passwd
pack: passwd: no saving - unchanged
castle@ pack termcap
pack: termcap: 29.8% Compression
castle@
```

在接下来的示例中，pcat 命令显示了压缩后的 termcap.z 文件的内容，并将输出通过管道传递给 `more` 命令。为了节省空间，这里只显示了输出的第一行。

```
castle@ pcat termcap.z | more
#ident "@(#) termcap 1.13 93/03/27 SMI* /* SunOS 4,1,3 termcap */
```

```
接下来的示例解包了 termcap.z。
castle@ unpack termcap.z
unpack: termcap: unpacked
castle@
```

## 环境变量

参阅 environ(5) 以获取以下影响 pack、pcat 和 unpack 执行的环境变量的描述：LC_TYPE、LC_MESSAGES 和 NLPATH。

## 退出状态

- 0 成功完成。
- >0 命令未能成功完成打包或解包的文件数。

## 属性

参阅 attributes(5) 以获取以下属性的描述：

| 属性类型 | 属性值 | 可用性 |
| :--- | :--- | :--- |
| CSI | 启用 | SunOS |

## 参见

cat(1), compress(1), zcat(1), attributes(5), environ(5)

## page — 浏览文本文件

## 概要

```
/usr/bin/page [-cd] [-pattern] [file...]
```

## 描述

详见 more(1)。

## pagesize — 显示内存大小

## 概要

```
/usr/bin/pagesize [-a]
```

## 描述

使用 pagesize 命令打印 pagesize(3) 返回的内存大小（字节）。此程序在构建 shell 脚本时有用。

## 选项

- -a 打印系统支持的所有可能的地址大小。Solaris 9 版本新增。

## 示例

```
castle@ /usr/bin/pagesize
819
```

接下来的示例显示了 pagesize -a 的输出。

```
castle@ pagesize -a
819
65536
5288
1934
```

## 属性

参阅 attributes(5) 以获取以下属性的描述：

| 属性类型 | 属性值 | 可用性 |
| :--- | :--- | :--- |
| SUNw | cs |

## 参见

pagesize(3), sizes(3), attributes(5)

## pargs — 打印命令参数、环境变量或辅助向量

## 概要

```
/usr/bin/pargs [-aeFx] [pid | core]...
```

## 描述

Solaris 9 版本新增。详见 proc(1)。

## passwd — 修改登录密码和密码属性

## 概要

```
/usr/bin/passwd [-r] [-nisplus] [name]
/usr/bin/passwd [-r files] [-r ldap] [-r nisplus] [name]
/usr/bin/passwd [-r files] [-e] [name]
/usr/bin/passwd [-r files] -s [-a]
/usr/bin/passwd [-r nis] -s [-a]
/usr/bin/passwd [-r files] [-d] [-f] [-min] [-w] [-x max] name
/usr/bin/passwd [-r ldap] [-e] [name]
/usr/bin/passwd [-e] [-D domainname]
/usr/bin/passwd -r nis -s [-a]
```

- passwd 命令取代了 passwd 和 ypasswd 命令，并应该替代它们。

使用 passwd 修改密码或列出与用户登录关联的密码属性。此外，超级用户（super）可以使用 passwd 安装或更改任何登录名的密码和属性。

当用于更改密码时，如果有旧密码，passwd 会提示输入旧密码。然后它再次提示输入新密码。当你输入密码时，passwd 会检查其有效期是否已足够。如果有效期不足，passwd 将终止。更多信息请参阅 pwcmd(1)、nlistdb(1) 和 shadow(4)。

如果是在 Solaris 8 版本中使用了 LDAP，或者系统启用了 NIS+，则 LDAP、NIS 或 NIS+ 密码可能与本地机器不同。如果 NIS 或 NIS+ 正在运行，请使用 passwd -r 更改本地机器上的密码信息。

该命令根据 /etc/passwd 中的信息更新 /etc/shadow，这依赖于 /etc/passwd 文件密码字段中 `x` 的特殊值。`x` 的值表示该用户的密码已在 /etc/shadow 中，不应进行修改。

## passwd

如果有效期足够，将进行检查以确保新密码符合构造要求。当你第二次输入新密码时，系统将比较两个新密码副本。如果两个副本不相同，则将重复提示新密码的循环，最多重复两次。密码的构造必须满足以下要求：

- 每个密码必须至少包含 PASSLENGTH 个字符，其中 PASSLENGTH 在 /etc/default/passwd 中定义并设置为 6。前八个字符具有意义。
- 每个密码必须包含至少两个字母和至少一个数字或特殊字符。在这种情况下，阿拉伯字母指的是所有大写或小写字母。
- 每个密码必须与用户的登录名以及该登录名的任何反转或循环位移不同。为了比较，大写字母与其对应的小写字母是等价。
- 新密码必须与旧密码至少不同三个字符。为了比较，大写字母与其对应的小写字母是等价。

如果满足所有要求，passwd 命令默认会咨询 /etc/nswitch.conf 以确定更新哪些存储。它会搜索 passwd 和 passwd_compat 条目。与这些条目相关的源（存储）将被更新。然而，密码配置限于以下情况：

- passwd: files
- passwd: ldap
- passwd: nis
- passwd: nisplus
- passwd: compat (== files)
- passwd: compat (== ldap)
- passwd: compat (== nis)
- passwd: compat (== nisplus)

用户可以使用 -s 选项显示其登录名的密码属性，前提是使用了 -r nisplus。否则，-s 参数限制超级用户使用。

显示格式为：
name status mm/dd/yy min warn

或者，如果没有密码有效期信息：
name status

name 是用户的登录 ID。status 是用户的密码状态。PS 表示有密码或已锁定，LK 表示已锁定，NP 表示无密码。
该日期最后更改日期。请注意，所有密码有效期日期都是根据格林尼治标准时间（世界时间）定的，因此在时区之间可能存在一天的差异。

## passwd 使用 pam(3) 进行密码管理。/etc/pam.conf 中的 PAM 配置策略指定了用于 passwd 的模块。以下是 pam.conf 文件中使用 UNIX 密码模块的 passwd 项。

```
passwd required      /usr/lib/security/pam_unix.so.1
```

如果 passwd 服务没有条目，将使用下面的其他服务的条目：

```
# Password management
#nother password required      /usr/lib/security/pam_unix.so.1
```

如果列出了多个密码模块，则可能会提示用户输入密码。

## 选项

- -a 显示所有条目的密码属性。仅配合 -s 选项使用；不能指定 name。对于 nisplus 存储，此选项仅显示本地域中调用者授权读取的 NIS+ 密码表中的条目。对于 files 存储，此选项限制超级用户使用。

