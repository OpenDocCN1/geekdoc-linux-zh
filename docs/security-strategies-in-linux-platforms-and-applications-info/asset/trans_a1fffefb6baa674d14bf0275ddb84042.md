
接下来，有四种不同的控制标志可用。标志的成功或失败决定了配置文件的下一步操作：

- **required**（强制）：当前行中的 Module 必须在 PAM 继续处理文件中的下一行之前正常工作。或者，如果该模块未正常工作，则认证尝试将失败。然而，PAM 仍会继续测试后续行。
- **requisite**（必须）：当前行中的 Module 必须在 PAM 继续处理文件中的下一行之前正常工作。如果模块未正常工作，则认证尝试将失败且 PAM 不再继续后续行。
- **sufficient**（足够）——假设之前没有 `required` 或 `requisite` 控制标志失败，那么该标志的成功意味着访问请求已获得批准。
- **optional**（可选）——除非没有其他控制标志返回成功或失败，否则此标志通常会被忽略。

掌握这些信息后，请查看 /etc/pam.d/ 目录下文件中的一些指令。这里显示了 Red Hat 系统 `system-auth` 中的两个重要的 `password_module` 类型指令：

```
password requisite pam_cracklib.so try_first_pass retry=3
```
第一条命令使用了 `pam_cracklib` 模块。当输入新密码时，该模块会将新密码与字典词进行比对。`try_first_pass` 参数允许使用之前输入的任何密码。`retry=3` 参数允许用户尝试输入三次密码。

```
password sufficient pam_unix.so md5 shadow nullok
try_first_pass use_authtok
```

## 用户的 PAM 配置

你可以进一步配置 PAM 配置文件来限制对服务或命令的访问，或者指定它们。这是通过 `pam_listfile` 模块实现的。一个例子是该模块应用于非常安全的 FTP 守护进程 `vsftpd`。在 Red Hat 版本的该 FTP 守护进程中，通过 /etc/pam.d/vsftpd 配置文件限制了对该服务的访问，这得益于以下指令：

```
auth required pam_listfile.so item=user sense-deny
file=/etc/vsftpd/ftpusers onerr=succeed
```
此行与认证管理有关。`required` 意味着根据 `pam_listfile` 模块，任何尝试都必须通过测试。`sense-deny` 拒绝访问上述文件 `/etc/vsftpd/ftpusers` 中列出的用户。如果该文件不存在，`onerr=succeed` 意味着任何限制都会被忽略。

## 第 4 章 | 用户权限与许可

# 105

PolicyKit 的主要开发者属于 freedktop.org。创建 freedktop.org 组是为了管理不同 Linux X Window 系统桌面环境之间的互操作性项目。该小组与 Linux Foundation 的 Free Standards Group 有松散的关联，而该小组恰好是 Linus Torvalds 的 Linux 内核工作的当前赞助者。

在尝试整合他们的工作后，K 桌面环境 (KDE) 的开发者已不再从事 PolicyKit 的开发。作为替代方案，KDE 开发者正在开发 KAuth 作为一种替代认证框架。本书未涵盖 KAuth，因为所涉及的发行版的默认 GUI 桌面环境是 GNOME。此外，本书的意图是鼓励通过命令行界面进行管理。

## 使用 PolicyKit 授权访问

PolicyKit 是另一种为普通用户自定义访问的方法，侧重于 GUI 工具。它可以帮助相对于 /etc/sudoers 文件以更细粒度的波来定制对管理工具的访问。虽然 Red Hat 正通过其 Fedora 版本开发 PolicyKit，但它可能直到 Red Hat Enterprise Linux 6 才会实现在官方 Red Hat 发布版中。尽管如此，他们通过相关的 Fedora 项目在 PolicyKit 开发中发挥了领先作用。

编写本文时，Red Hat 对 PolicyKit 的工作尚未完成。本节将总结其某些功能和配置目录。当工作完成后，你将不仅能够根据用户，还可以根据用户的终端位置为许多单独的管理工具分配访问权限。换句话说。
