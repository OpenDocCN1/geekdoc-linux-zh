
## 概要

```
setup-nsssysinit [on] [off] [status]
```

## 描述

**setup-nsssysinit**

是一个 shell 脚本，用于查询 nss-sysinit 模块的状态，并在以 root 权限运行时启用或禁用该模块。

通过编辑全局 PKCS #11 配置文件来开启或关闭 nss-sysinit 模块数据库，并显示状态。此脚本可由用户以超级用户身份调用。在 nss-sysinit 安装后处理阶段，它会以参数 `on` 被调用。

## 选项

- **on**

  开启 nss-sysinit。

- **off**

  关闭 nss-sysinit。

- **status**

  返回 nss-sysinit 是否已启用。

## 示例

以下示例查询 nss-sysinit 的状态：

```
/usr/bin/setup-nsssysinit status
```

以下示例在超级用户运行时开启 nss-sysinit：

```
/usr/bin/setup-nsssysinit on
```

## 文件

/usr/bin/setup-nsssysinit

## 参见

(1)

## 作者

nss 库由 Netscape、Red Hat、Sun、Oracle、Mozilla 和 Google 的开发人员编写和维护。

作者：Elio Maldonado <elio>.

## 许可证

本软件根据 Mozilla 公共许可证 v. 2.0 授权。如果此文件未随附 MPL 副本，您可以在以下网址获取：

---

## setup

## 名称

setup - 文本模式系统配置工具

## 概要

setup

## 描述

setup 工具程序（setup）是其他一组工具（主要是 system-config-*-tui 工具）的前端菜单程序。它呈现的选项列表是通过扫描 /etc/setuptool.d 和 /usr/share/setuptool/setuptool.d 中的文件生成的。

目录中的每个文件应包含一行或多行文本。每行包含一至四个字段，由“|”字符分隔。顺序如下：

- 要调用的二进制文件的路径（必需）
- 应显示的应用程序未翻译的名称（如果未设置，默认使用二进制文件的路径，但不要依赖此行为。）
- 可以找到应用程序名称翻译的 gettext 文本域（如果未设置，默认为“setup”。）
- 可以找到该文本域翻译的目录（如果未设置，默认为“/usr/share/locale”。）

如果存在多个具有相同未翻译名称的条目，则**首先**读取的条目优先。文件按正常排序顺序读取。

## 示例

一个虚构的示例创建 /etc/setuptool.d/00bogus，内容如下：

```
/bin/ls --color; /bin/sleep 5|Example "ls" invocation.
```

或者

```
/bin/ls --color; /bin/sleep 5|Give this help list|libc
to use one of libc’s (not meaningful here, but) translatable messages.
```

---

## SETXKBMAP

## 名称

setxkbmap - 使用 X Keyboard Extension 设置键盘

## 概要

**setxkbmap** [ *args* ] [ *layout* [ *variant* [ *option* … ] ] ]

## 描述

`setxkbmap` 命令将键盘映射为使用命令行中指定的选项确定的布局。

XKB 键盘映射由多个组件构建，仅在需要时编译。所有组件的源代码都可以在 `/usr/share/X11/xkb` 中找到。

## 选项

- **-compat name**
  指定用于构建键盘布局的兼容性映射组件名称。

- **-config file**
  指定描述要使用的键盘的 XKB 配置文件名称。

- **-device device**
  指定要使用新键盘布局更新的输入设备的数字设备 ID。如果未指定，则更新 X 服务器的核心键盘设备。

- **-display display**
  指定要使用新键盘布局更新的显示器。

- **-geometry name**
  指定用于构建键盘布局的几何组件名称。

- **-help**
  打印描述 setxkbmap 有效输入的消息。

- **-I directory**
  将一个目录添加到用于搜索指定布局或规则文件的目录列表中。

- **-keycodes name**
  指定用于构建键盘布局的 keycodes 组件名称。

- **-keymap name**
  指定用于构建键盘布局的 keymap 描述名称。

- **-layout name**
  指定用于确定组成键盘描述的组件的布局名称。-layout 选项只能使用一次，多个布局可以指定为逗号分隔的列表。

- **-model name**
  指定用于确定组成键盘描述的组件的键盘模型名称。命令行中只能指定一个模型。

- **-option name**
  指定用于确定组成键盘描述的组件的选项名称；可以指定多个选项，每个 -option 标志一个。请注意，setxkbmap 将命令行中指定的选项添加到之前设置的选项（保存在根窗口属性中）。如果要替换之前指定的所有选项，请先使用带有空参数的 -option 标志。

- **-print**
  设置此选项后，setxkbmap 仅以 xkbcomp（XKB 键盘映射编译器）可接受的格式打印组件名称并退出。该选项可用于测试，代替 verbose 选项，或在需要串联运行 setxkbmap 和 xkbcomp 的情况下使用（见下文）。

- **-query**
  设置此选项后，`setxkbmap` 仅打印当前的 rules、model、layout、variant 和 options，然后退出。

- **-rules** `file`
  指定用于将请求的布局和模型解析为一组组件名称的规则文件名称。

- **-symbols** `name`
  指定用于构建键盘布局的 symbols 组件名称。

- **-synch**
  强制 X 请求同步。

- **-types** `name`
  指定用于构建键盘布局的 types 组件名称。

- **-variant** `name`
  指定应使用哪个键盘布局变体来确定组成键盘描述的组件。*-variant* 选项只能使用一次。多个变体可以指定为逗号分隔的列表，并将与使用 *-layout* 指定的布局匹配。

- **-verbose**|-v [level]
  指定输出消息的详细级别。有效级别范围从 0（最少详细）到 10（最详细）。默认详细级别为 5。如果未指定级别，每个 -v 或 -verbose 标志将使级别提高 1。

- **-version**
  打印程序的版本号。

## 与 XKB COMP 配合使用

如果 X 服务器和客户端 shell 运行在不同的计算机上，并且这些机器上的 XKB 配置文件不同，指定键盘映射（通过模型、布局和选项名称）时可能会遇到问题。这是因为 **setxkbmap** 根据客户端计算机上的文件将其参数转换为 XKB 配置文件名称，然后将这些文件名发送到服务器，服务器上的 **xkbcomp** 需要使用服务器拥有的文件来组合完整的键盘映射。因此，如果文件集以某种方式不同，**setxkbmap** 生成的名称在服务器端可能不可接受。通过在客户端也运行 **xkbcomp** 可以解决此问题。使用 *-print* 选项，**setxkbmap** 仅以适当的格式将文件名打印到其标准输出，并且此输出可以直接管道传输到 **xkbcomp** 输入。例如，命令

```
setxkbmap us -print | xkbcomp - $DISPLAY
```

使两个步骤在同一台（客户端）机器上运行，并将键盘映射加载到服务器中。

## 参见

(1), (7)

## 文件

/usr/share/X11/xkb

---

## SFTP

## 名称

**sftp** - 安全文件传输程序

## 概要

**sftp** *[-1246aCfPqrV]* *[-B buffer_size]* *[-b batchfile]* *[-c cipher]* *[-D sftp_server_path]* *[-F ssh_config]* *[-i identity_file]* *[-l limit]* *[-o ssh_option]* *[-P port]* *[-R num_requests]* *[-S program]* *[-s subsystem]* *sftp_server*
**sftp** *[user @ host [: file ...]]*
**sftp** *[user @ host [: dir [file ...]]]*
**sftp -b batchfile** *[user @ host]*

## 描述

**sftp** 是一个交互式文件传输程序，类似于 ftp(1)，它通过加密的 ssh(1) 传输层执行所有操作。它还可以使用 *ssh* 的许多功能，如公钥认证和压缩。**sftp** 连接到指定的 *host* 并登录，然后进入交互式命令模式。

第二种用法格式如果使用非交互式认证方法会自动检索文件；否则，它将在成功的交互式认证后执行。

第三种用法格式允许 **sftp** 在远程目录中启动。

最后的用法格式允许使用 **-b** 选项进行自动化会话。在这种情况下，必须配置非交互式认证以避免在连接时需要输入密码（详见 sshd_config(8) 和 *ssh-keygen(1)*）。

由于某些用法格式使用冒号字符来分隔主机名和路径名，IPv6 地址必须用方括号括起来以避免歧义。

选项如下：

- **-1**
  指定使用协议版本 1。

- **-2**
  指定使用协议版本 2。

- **-4**
  强制 **sftp** 仅使用 IPv4 地址。

- **-6**
  强制 **sftp** 仅使用 IPv6 地址。

- **-a**
  尝试继续中断的传输，而不是覆盖现有的部分或完整文件副本。如果部分内容与正在传输的内容不同，则结果文件可能会损坏。

- **-B** *buffer_size*
  指定 **sftp** 在传输文件时使用的缓冲区大小。较大的缓冲区可以减少往返次数，但会增加内存消耗。默认值为 32768 字节。

- **-b** *batchfile*
  批处理模式从输入 *batchfile* 读取一系列命令，而不是从 *stdin* 读取。由于缺乏用户交互，应与非交互式认证配合使用。*batchfile* 可以是 '` '` 以指示标准输入。如果以下任何命令失败，**sftp** 将中止：**get, put, reget, reput, rename, link, mkdir, chdir, ls, lchdir, chmod, chown, chgrp, lpwd, df, symlink** 和 **lmkdir**。通过在命令前加上 '` ' 字符（例如 **-rm /tmp/blah\***），可以逐条抑制错误终止。

- **-C**

