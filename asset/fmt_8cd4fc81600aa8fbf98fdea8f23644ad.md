
# 第 4 章 · 保护您的用户

启动具有不同组员权限的 shell。组密码防止了该系统访问受限文件。虽然这在 Solaris 中已不再是一个问题，但在新组的组密码字段中放置一个星号（`*`）是一种惯性做法。

组密码字段之后是 GID。与 UID 一样，GID 应该是唯一的。字段列表列出了该组的用户名。

在单机系统或 NIS 系统上创建新组非常简单。如果你正在使用 NIS，请务必在 NIS 主服务器上编辑 `/etc/group` 文件，因为对客户端进行的更改可能不会被识别。假设您想创建一个名为 `operators` 的新组，该组将包含允许管理打印系统某些方面的用户。请准备好一个新的 GID，并记住以下规则：

- 诸如 `daemon`、`mail`、`sysadmin` 等项的现有 GID 留给特定的系统功能使用。重用这些 GID 之一可能会导致命令出现意想不到的行为，更糟糕的是，产生安全的安全漏洞。
- 100 以下的 GID 通常保留给系统使用，60,000 以上的 GID 也是如此。
- 在向新组添加用户时，请记住每个用户仅限于一个主组，且不少于 16 个辅助组。如果一个用户属于超过 16 个辅助组，则某些命令（`sudo` 就是其中之一）的行为可能是不可预测的，并且推送 NIS 映射的尝试可能会失败。

假设您的两个用户 `jackson` 和 `tealc` 预期将管理打印系统。在为将责任委托给他们做准备时，您想创建一个新组并将他们添加为成员。打开 `/etc/group` 并添加：

```
operators::*:150:jackson,tealc
```

如果这是 NIS 主服务器，您可以使用以下命令立即推送映射：

```bash
# cd /var/yp
# make
```

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_126_0.png)

## 基于角色的访问控制 (RBAC)

Solaris 的一个新新增概念是基于角色的访问控制 `RBAC`。熟悉 `sudo` 实用程序的系统管理员应该认为 RBAC 易于使用。RBAC 的目的是将有限权限扩展到某些账户。通常在 UNIX 系统中，个人要么拥有 `root` 权限（以及与之相关的所有风险和权力），要么是普通、无特权的用户。相比之下，RBAC 允许委托某些特定的任务。

RBAC 使用四个文件来控制对某些操作的访问。第一个文件 `/etc/user_attr` 用于匹配用户、角色与他们的权限以及他们拥有的配置（profiles）。`/etc/user_attr` 中的默认条目如下：

```text
# Copyright (c) 1999 by Sun Microsystems, Inc. All rights
# reserved.
#
# /etc/user_attr
#
# user attributes. see user_attr(4)
#
#pragma ident "(#)user_attr 1.2 99/07/14 SMI"
```

```
root::type=normal;auths=solaris.*,solaris.grant;profiles=All
```

此条目表示 `root` 用户被授予了访问所有定义配置的权限。

第二个文件 `/etc/security/auth_attr` 定义了授权列表，并对这些授权授予的权力进行了简要描述，同时提供了指向帮助文件的链接。`auth_attr` 文件很长，所以我们只取单行作为示例：

```text
solaris.device.grant::Delegate\
DeviceAdministration::help=DevGrant.html
```
