

## 第 20 章 新闻与其他协作通信

尽管这可以防止服务器磁盘空间不足，但根据缓冲区文件的大小，可能会导致文章过早过期。大多数使用此方法的新闻管理员通过尝试错误来学习处理其站点标准新闻流量负载所需的缓冲区文件大小。

> 注意事项
> 如果某个新闻组没有被特定的存储方法覆盖，INN 将不会存储接收到的该新闻组的文章，并会为每篇文章生成一条错误消息信息。这会对新闻服务器产生灾难性的影响。对于简单的新闻服务器，最好选择一种存储方法，并配置 `storage.conf` 文件，让所有新闻组都使用该方法。

默认情况下，Red Hat 的 `storage.conf` 文件没有定义任何默认存储方法，但它已完全配置并被注释掉。你必须定义至少一个使用的方法，以便 INN 正常工作；要做到这一点，你只需取消所需的章节即可。

### readers.conf 文件
你使用 `/etc/news/readers.conf` 配置文件为使用你新闻服务器的阅读者定义权限。如果你允许本地用户连接到你的新闻服务器阅读文章，必须配置 `readers.conf` 文件来支持他们。

`readers.conf` 文件由以下三类数据组成：

- 身份验证定义
- 访问定义
- 参数和值

身份验证定义规定了访问你新闻服务器的用户类别。你可以根据各种因素（如远程地址、访问的新闻组和使用的身份验证方法类型）创建多个不同的用户类别。身份验证章节的语法如下：

```
auth name {
    hosts: hostlist
    auth: auth-program
    res: res-program
    default: defuser
    default-domain: defdomain
}
```

`name` 值用作标签来唯一标识身份验证定义。身份验证定义使用参数和值来标识其操作。`hosts` 参数使用 `hostlist` 值来识别被身份验证定义覆盖的单个远程主机。这些可以使用主机名或数字 IP 地址列出，并带有匹配的通配符字符。

你可以使用 `res` 参数指定一个根据其网络信息对连接进行验证的身份验证程序。或者，你可以使用 `auth` 参数指定一个可以使用用户 ID/密码对对连接进行验证的身份验证程序。如果你对远程新闻服务器的身份验证感兴趣，应该咨询 IN 文档，因为这是一个相当复杂的过程。

访问定义为新闻阅读者组定义了访问限制和权限类别。访问定义的语法如下：

```
access name {
  users: identity-wildmat
  newsgroups: group-wildmat
  access: permissions
}
```

`name` 值必须与相应的身份验证定义匹配。访问定义中定义的参数仅适用于对应身份验证定义中定义的主机。`users` 参数将访问规则限制在值中列出的特定用户集中。如果不存在 `users` 参数，则适用于所有用户。`newsgroups` 参数定义了该组可以访问哪些新闻组，`access` 参数定义了该组拥有哪些权限。权限定义如下：

- R—允许只读访问。
- P—允许发布文章。
- A—允许发布已批准的文章（使用审核员）。
- N—允许执行 NEWNEWS 命令。
- L—允许该组发布到设置为不允许本地发布的新闻组。

这里是一个 `readers.conf` 示例文件，允许所有本地新闻阅读者在所有新闻组阅读并发布文章：

```
# readers.conf
auth "localhost" {
  hosts: "localhost, 127.0.0.1, 192.168.1.100, stdin
  default: "<localhost>"
}
```

```
access "localhost" {
  users: "<localhost>"
}
```

![](img/446debe023486a07fde575245cf7a3ff_704_0.png)

```
newsgroups: "*"
access: RPA
}
auth "localnet" {
  hosts: "192.168.*"
  default: "<user>"
  default-domain: "local"
}
```

```
access "localnet" {
  users: "<user>"
  newsgroups: "*"
  access: RP
}
```

身份验证定义规定了访问你新闻服务器的用户类别。你可以根据各种因素（如远程地址、访问的新闻组和使用的身份验证方法类型）创建多个不同的用户类别。身份验证章节的语法如下：

```
auth name {
    hosts: hostlist
    auth: auth-program
    res: res-program
    default: defuser
    default-domain: defdomain
}
```

`name` 值用作标签来唯一标识身份验证定义。身份验证定义使用参数和值来标识其操作。`hosts` 参数使用 `hostlist` 值来识别被身份验证定义覆盖的单个远程主机。这些可以使用主机名或数字 IP 地址列出，并带有匹配的通配符字符。

你可以使用 `res` 参数指定一个根据其网络信息对连接进行验证的身份验证程序。或者，你可以使用 `auth` 参数指定一个可以使用用户 ID/密码对对连接进行验证的身份验证程序。如果你对远程新闻服务器的身份验证感兴趣，应该咨询 IN 文档，因为这是一个相当复杂的过程。

访问定义为新闻阅读者组定义了访问限制和权限。访问定义的语法如下：

```
access name {
  users: identity-wildmat
  newsgroups: group-wildmat
  access: permissions
}
```

`name` 值必须与相应的身份验证定义匹配。访问定义中定义的参数仅适用于对应身份验证定义中定义的主机。`users` 参数将访问规则限制在值中列出的特定用户集中。如果不存在 `users` 参数，则适用于所有用户。`newsgroups` 参数定义了该组可以访问哪些新闻组，`access` 参数定义了该组拥有哪些权限。权限定义如下：

- R—允许只读访问。
- P—允许发布文章。
- A—允许发布已批准的文章（使用审核员）。
- N—允许执行 NEWNEWS 命令。
- L—允许该组发布到设置为不允许本地发布的新闻组。

（注：此处后续内容与前文重复，已按要求翻译并保持格式一致）

（此处重复内容的翻译翻译...）

访问定义为新闻阅读者组定义了访问限制和权限。访问定义的语法如下：

```
access name {
  users: identity-wildmat
  newsgroups: group-wildmat
  access: permissions
}
```

`name` 值必须与相应的身份验证定义匹配。访问定义中定义的参数仅适用于对应身份验证定义中定义的主机。`users` 参数将访问规则限制在值中列出的特定用户集中。如果不存在 `users` 参数，则适用于所有用户。`newsgroups` 参数定义了该组可以访问哪些新闻组，`access` 参数定义了该组拥有哪些权限。权限定义如下：

- R—允许只读访问。
- P—允许发布文章。
- A—允许发布已批准的文章（使用审核员）。
- N—允许执行 NEWNEWS 命令。
- L—允许该组发布到设置为不允许本地发布的新闻组。

