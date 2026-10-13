
`session optional pam_ck_connector.so`

第五个 `session` 命令确保用户的主目录具有标准的 `/etc/skel` 文件。下面的命令即使被列为可选，也会撤销任何现有的唯一会话密钥环。跳过前面，最后一个命令允许登录与第 9 章中描述的 Console Kit 配合工作。其前面的命令包含来自 `system-auth` 文件的以下 `session` 模块类型命令：

```
session optional pam_keyinit.so revoke
```

```
session required pam_limits.so
```

```
session [success=1 default=ignore] pam_succeed_if.so service in crond quiet
```

```
session required pam_unix.so
```

这些命令中的第一个重复了在主 `/etc/pam.d/login` 文件中已完成的密钥环撤销操作。下一个命令通过 `/etc/security/limits.conf` 为单个用户设置限制（`pam_limits.so`）。下面的命令与 `cron` 作业相关。最后一个命令记录用户注销时的结果。

## EXERCISE 10-3
### Configure PAM

在本练习中，您可以尝试 Red Hat Enterprise Linux 6 的一些 PAM 安全功能。

- 1. 使用以下命令制作 `/etc/securetty` 的备份副本：
  - `# cp /etc/securetty /etc/securetty.sav`
- 2. 编辑 `/etc/securetty` 并删除 `tty3` 到 `tty11` 的行。保存更改并退出。
- 3. 使用 `ALT+F3`（如果正在运行 X Window 则为 `CTRL-ALT+F3`）切换到虚拟控制台 3。尝试以 `root` 身份登录。会发生什么？
- 4. 以普通用户身份重复步骤 3。会发生什么？你知道为什么吗？
- 5. 使用 `ALT+F2` 切换到虚拟控制台 2 并尝试以 `root` 身份登录。
- 6. 查看 `/var/log/secure` 中的消息。你能看到你在虚拟控制台 3 中尝试以 `root` 身份登录的地方吗？
- 7. 使用以下命令恢复原始的 `/etc/securetty` 文件：
  - `# mv /etc/securetty.sav /etc/securetty`

需要记住的一点是，`/etc/securetty` 文件控制着可以从哪些控制台以 `root` 用户身份登录 Linux。因此，所做的更改不会影响普通（非 `root`）用户。

## PAM and User-Based Security

在本节中，您将学习如何配置 PAM 以限制特定用户的访问。此安全功能的关键是 `pam_listfile.so` 模块。其位置因架构而异；可能位于 `/lib64/security` 或 `/lib/security` 目录中。如果您已安装 `vsFTP` 服务器，`/etc/pam.d/vsftpd` 文件包含此模块的示例。

如前所述，每个 PAM 配置命令都有四个设置。首先，以下行清除任何现有的密钥环，确保后续的身份验证选项确实被使用。

```
session optional pam_keyinit.so force revoke
```

为确保该命令尊重使用此模块所做的工作，应接下来使用此指令：

```
auth required pam_listfile.so
```

PAM 限制用户访问的方式在于命令的最后一部分——细节中。例如，如果您在 PAM 配置文件中添加了以下行，则对相关工具的访问将仅限于 `/etc/special` 中列出的任何用户：

```
auth required pam_listfile.so item=user sense=deny \ file=/etc/vsftpd/ftpusers onerr=succeed
```

要了解其工作原理，请将此命令分解为其组成部分。您已从上一节了解到命令的前三个部分。所示的开关与 `pam_listfile.so` 模块相关联，如表 10-6 所描述。

`pam_listfile.so` 模块的选项

表 10-6

| `pam_listfile` 开关 | 描述 |
|---|---|
| `item` | 此开关可用于限制对终端（`tty`）的访问、特定文件中的用户（`user`）、组（`group`）或更多内容。 |
| `sense` | 如果在指定文件中找到该项，则执行所注明的动作。例如，如果用户在 `/etc/special` 中，且 `sense=allow`，则此命令允许使用指定的工具。 |
| `file` | 配置包含列表的文件，例如 `file = /etc/special`。 |
| `onerr` | 如果出现问题，请告知模块该怎么做。选项为 `onerr=succeed` 或 `onerr=fail`。 |

因此，对于指定的命令（`onerr=succeed`），错误，奇怪的是，返回成功（`item=user`），基于特定用户列表。如果用户在指定列表中（`file=/etc/special`），则允许该用户（`sense=allow`）访问指定的工具。要了解其工作原理，请执行练习 10-4 中的步骤。

## exam watch

> 确保您了解 Red Hat Enterprise Linux 如何通过 `/etc/pam.d` 配置文件处理用户授权。在测试这些文件时，请务必在进行任何更改之前备份 PAM 中的所有内容，因为您对 PAM 配置文件所做的任何错误都可能完全禁用系统（PAM 就是这么安全）。

## EXERCISE 10-4
### Use PAM to Limit User Access

您也可以使用 PAM 系统来限制普通用户的访问。在本练习中，您将通过向 `/etc/nologin` 文件添加一个或多个用户来限制访问。它应与默认的 `/etc/pam.d/login` 安全配置文件配合使用，具体为以下行：

```
account required pam_nologin.so
```
