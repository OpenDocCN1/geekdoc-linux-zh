
或者：
`UNIXgroupname DomainGroupName`

在 Samba 是域控制器或使用 `security = domain` 的域成员的情况下，可以使用后一种格式：默认域名是 Samba 服务器的域名，由 `workgroup = MYGROUP` 指定。
映射文件中任何未指定的组都被假设为本地组或域组，取决于 Samba 服务器的角色。

在 Samba 是域控制器的情况下，Samba 将优先将所有未指定的 UNIX 组作为自身的同名域组。
在 Samba 是使用 `security = domain` 的域成员的情况下，Samba 将与其域控制器（参见 `password server`）检查 UNIX 名称以其是否为 NT 域组。如果域控制器表示不是，则未指定的（未映射的）UNIX 组视为 Samba 服务器本地数据库中的本地组。NT 管理员会将这些识别为工作站本地组，通过运行 `USGRMEXE` 并选择名为 `\WORKSTATION_NAME` 的远程域，或者在本地工作站上运行 `MUSGRMEXE` 来管理。

### 域管理员组 (G)

这是一个`EXPERIMENTAL`参数，属于未完成的 Samba 域代码。它已于 98 年删除，以便配合支持域功能的最新代码。

### 域管理员用户 (G)

这是一个`EXPERIMENTAL`参数，属于未完成的 Samba 域代码。它已于 98 年删除，以便配合支持域功能的最新代码。

## 附录 C: Samba 手页

这听起来可能很复杂，但这意味着 Samba 服务器作为域成员或实验性`EXPERIMENTAL`域控制器，将分别像 NT 工作站（带有本地 SAM 数据库）或 NT PDC（带有域 SAM 数据库）一样运行，完全不需要任何映射文件。如果你想玩得复杂点，也可以。

请注意，将任意域中的任意 NT 组添加到任意 UNIX 组**需要**满足以下条件：

- UNIX 组存在于 UNIX 服务器上。
- NT 域组存在于指定的 NT 域中。
- UNIX 服务器知道指定的域；
- UNIX 中的所有 UNIX 用户（他们期望以正确的 NT 用户身份和正确的 NT 组权限访问 Samba 服务器）都已使用`domain user map`映射到指定 NT 域中正确的 NT 域用户。

未能满足上述任何要求都可能导致日志文件中报告某项（或全部）错误，或者（以及）授予用户的访问权限不正确或缺失。

- `domain groups (G)`

这是一个实验性`EXPERIMENTAL`的参数，是未完成的 Samba NT 域控制器的一部分。它已于 1998 年 11 月移除。要使用可能对 Samba NT 域控制器功能支持更多的最新代码，请向 `listproc@samba.com` 发送邮件订阅 Samba-ntdom 邮件列表。

- `domain guest group (G)`

这是一个实验性`EXPERIMENTAL`的参数，是未完成的 Samba NT 域控制器代码的一部分。它已于 1998 年 11 月移除。要使用可能对 Samba NT 域控制器功能支持更多的最新代码，请向 `listproc@samba.com` 发送邮件订阅 Samba-ntdom 邮件列表。

- `domain logons (G)`

这是一个实验性`EXPERIMENTAL`的参数，是未完成的 NT 域控制器代码的一部分。它已于 1998 年 11 月移除。要使用可能对 Samba NT 域控制器功能支持更多的最新代码，请向 `listproc@samba.com` 发送邮件订阅 Samba-ntdom 邮件列表。

- `domain logons (G)`

如果设置为 true，Samba 将为其所在的工作组提供 Windows 95/98 域登录。有关设置此项的更多细节，请参阅源码随带的 Samba 文档目录中的 `DOMA.txt` 文件。

注意，Win95/98 域登录不同于 Windows NT 域。NT 登录需要一个域主控制器（PDC）。旨在未来的版本中 Samba 能为 Windows NT 客户端提供此功能。

默认值：`domain logons = no`

`smb.conf (5) 259`

- `domain master (G)`

告诉 `nmbd` 启用广域浏览列表排序。设置此选项会导致 `nmbd` 声明一个特殊的特定域的 NetBIOS 名称，标识其为给定工作组的域主。在广播隔离子网的同一工作组内的本地主浏览器将向 `nmbd` 提供它们的本地浏览列表，然后向 `smbd` 请求整个广域浏览列表的完整副本。浏览器客户端将联系其本地主浏览器，并将接收全域浏览列表，而不仅仅是针对广播隔离子网的列表。

注意，Windows NT 主域控制器默认期望能够声明该工作组的特殊 NetBIOS 名称，标识其为该工作组的域主浏览器（没有办法阻止 Windows NT DC 尝试这样做）。这意味着如果设置了此参数，且 `nmbd` 在 Windows NT DC 能够做到之前抢占了工作组的特殊名称，那么子网浏览将表现异常并失败。

默认情况下（`"auto"`），Samba 仅在它是主域控制器时才会尝试成为域主浏览器。

```
Default: domain master = auto

Example: domain master = no
```

- `user master (G)`

此选项允许你指定一个文件，其中包含单个 NT 用户名（任意域）到 UNIX 名称的唯一映射。这使得 NT 域用户能够正确地呈现 NT 系统，尽管 UNIX 缺乏对 NT 安全模型（基于 VAX/VMS）的原生支持。建议读者熟悉 NT 域系统及其管理。

此选项与`local group map`和`domain group map`结合使用。在 Samba 不预期与任何其他 SAM 数据库（无论是本地工作站还是域控制器）交互的情况下，使用这三个选项非常简单且通常没有必要。

此选项提供了（并维护了） UNIX 和 NT 用户之间的一一对应的链接，它不同于`username map`，后者并不维护其可以映射的名称与所映射名称之间的区别。

映射文件按行解析。如果任何行以 `#` 或 `;` 开头，则该行被忽略。每行左侧应包含单个 UNIX 用户名，右侧包含单个 NT 域名，用制表符或 `=` 分隔。如果任名称包含空格，则应用引号括起来。行可以是：

```
UNIXusername \DOMAIN_NAME\DomainUNIXName
```

或：

```
UNIXusername DomainName
```
