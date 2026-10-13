
`redirect` 功能将重发所有发送到 `address.REDIRECT` 的邮件，而不是本地；请尝试 `<address>` 邮件。这样，如果 Joe 去了 Whizzer，Gonzo 的电子邮件管理员可以将 Joe 别名设置为 `joe@whizzer.com.REDIRECT`，以方便 Joe 的朋友和联系人可以在他的新工作中联系到他。

第二个功能 `always_add_domain` 始终在本地投递的、`To:` 地址未完全限定的邮件上，添加本地主机的完全限定域名。例如，如果我将邮件发送到 `joe` 而不是 `joe@gonzo.gov`，`sendmail` 将在交付前自动向 `To:` 头部添加 `@gonzo.gov`。

`use_cw_file` 功能告诉 `sendmail` 在 `/etc/sendmail.cw` 文件中查找 `localhost` 的别名。例如，如果 `gonzo.gov` 也是徒步俱乐部 `hikers.org` 的主 MX，那么 `gonzo.gov` 和 `hikers.org` 都会在 `sendmail.cw` 文件中有目。

# 配置服务

## 第二部分

第二个功能 `always_add_domain` 始终在本地投递的、`To:` 地址未完全限定的邮件上，添加本地主机的完全限定域名。例如，如果我将邮件发送到 `joe` 而不是 `joe@gonzo.gov`，`sendmail` 将在交付前自动向 `To:` 头部添加 `@gonzo.gov`。

`use_cw_file` 功能告诉 `sendmail` 在 `/etc/sendmail.cw` 文件中查找 `localhost` 的别名。例如，如果 `gonzo.gov` 也是徒步俱乐部 `hikers.org` 的主 MX，那么 `gonzo.gov` 和 `hikers.org` 都会在 `sendmail.cw` 文件中有目。

# SMTP 与协议

## 第7章

现在我将为你简要解释这个示例 `mc` 文件的各个部分：

```
divert(-1)
include('../.m4/cf.m4')
```

这些指令确保 `m4` 处理器需要处理该文件。你会在其他一些 `mc` 文件中找到这些。

```
define('CONF_USER_ID', '8:12')
OSTYPE('linux')
undefined('UUCP_RELAY')
undefined('BITNET_RELAY')
```

`define` 表示你想要更改 `sendmail` 的设置，例如允许邮件的最大跳数或最大消息大小。在这种情况下，你正在定义运行 `sendmail` 程序时的 UID 和组（当它不在特权模式即以 `root` 身份运行时）。你可以定义的所有参数都列在 `README` 文件中。

不同的 UNIX 操作系统对于文件位置以及给邮件传递者提供哪些标志有不同的约定。这就是 `OSTYPE` 宏的用途。在示例中，`sendmail` 应该使用 Linux 的文件位置约定。

两个 `undefined` 删除了此 `sendmail` 主机接受 UUCP 和 BITNET 地址邮件的能力。

```
FEATURE(redirect)
FEATURE(always_add_domain)
FEATURE(use_cw_file)
FEATURE(local_procmail)
```

`FEATURE` 宏允许你添加你的站点所需的各种 `sendmail` 功能。

`redirect` 功能将重发所有发送到 `address.REDIRECT` 的邮件，而不是本地；请尝试 `<address>` 邮件。这样，如果 Joe 去了 Whizzer，Gonzo 的电子邮件管理员可以将 Joe 别名设置为 `joe@whizzer.com.REDIRECT`，以方便 Joe 的朋友和联系人可以在他的新工作中联系到他。

第二个功能 `always_add_domain` 始终在本地投递的、`To:` 地址未完全限定的邮件上，添加本地主机的完全限定域名。例如，如果我将邮件发送到 `joe` 而不是 `joe@gonzo.gov`，`sendmail` 将在交付前自动向 `To:` 头部添加 `@gonzo.gov`。

`use_cw_file` 功能告诉 `sendmail` 在 `/etc/sendmail.cw` 文件中查找 `localhost` 的别名。例如，如果 `gonzo.gov` 也是徒步俱乐部 `hikers.org` 的主 MX，那么 `gonzo.gov` 和 `hikers.org` 都会在 `sendmail.cw` 文件中有目。

现在我将为你简要解释示例 `mc` 文件的各个部分：

```
divert(-1)
include('../.m4/cf.m4')
```

这些指令确保 `m4` 处理器需要处理该文件。你会在其他一些 `mc` 文件中找到这些。

```
define('CONF_USER_ID', '8:12')
OSTYPE('linux')
undefined('UUCP_RELAY')
undefined('BITNET_RELAY')
```

`define` 表示你想要更改 `sendmail` 的设置，例如允许邮件的最大跳数或最大消息大小。在这种情况下，你正在定义运行 `sendmail` 程序时的 UID 和组（当它不在特权模式即以 `root` 身份运行时）。你可以定义的所有参数都列在 `README` 文件中。

不同的 UNIX 操作系统对于文件位置以及给邮件传递者提供哪些标志有不同的约定。这就是 `OSTYPE` 宏的用途。在示例中，`sendmail` 应该使用 Linux 的文件位置约定。

两个 `undefined` 删除了此 `sendmail` 主机接受 UUCP 和 BITNET 地址邮件的能力。

```
FEATURE(redirect)
FEATURE(always_add_domain)
FEATURE(use_cw_file)
FEATURE(local_procmail)
```

`FEATURE` 宏允许你添加你的站点所需的各种 `sendmail` 功能。

`redirect` 功能将重发所有发送到 `address.REDIRECT` 的邮件，而不是本地；请尝试 `<address>` 邮件。这样，如果 Joe 去了 Whizzer，Gonzo 的电子邮件管理员可以将 Joe 别名设置为 `joe@whizzer.com.REDIRECT`，以方便 Joe 的朋友和联系人可以在他的新工作中联系到他。

第二个功能 `always_add_domain` 始终在本地投递的、`To:` 地址未完全限定的邮件上，添加本地主机的完全限定域名。例如，如果我将邮件发送到 `joe` 而不是 `joe@gonzo.gov`，`sendmail` 将在交付前自动向 `To:` 头部添加 `@gonzo.gov`。

`use_cw_file` 功能告诉 `sendmail` 在 `/etc/sendmail.cw` 文件中查找 `localhost` 的别名。例如，如果 `gonzo.gov` 也是徒步俱乐部 `hikers.org` 的主 MX，那么 `gonzo.gov` 和 `hikers.org` 都会在 `sendmail.cw` 文件中有目。

现在我将为你简要解释示例 `mc` 文件的各个部分：

```
divert(-1)
include('../.m4/cf.m4')
```

这些指令确保 `m4` 处理器需要处理该文件。你会在其他一些 `mc` 文件中找到这些。

```
define('CONF_USER_ID', '8:12')
OSTYPE('linux')
undefined('UUCP_RELAY')
undefined('BITNET_RELAY')
```
