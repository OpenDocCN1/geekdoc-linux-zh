
虽然 Fedora 自带了一些电子邮件客户端，但这里没有足够的空间涵盖所有它们。因此，我们将讨论两个最常用的客户端：默认的 Evolution 和 Thunderbird。两者都是强大的消息解决方案，因此它们与 LDAP 都工作得都很良好。在这两者中，Thunderbird 似乎更容易配置。在 Thunderbird 第一次就能成功的情况下，我们对 Evolution 遇到过各种问题。

## Evolution

要为 Evolution 配置 LDAP，点击 `New` 旁边的箭头并选择 `Address Book`。会出现一个新屏幕，其第一个选项提示你创建创建的地址簿类型。选择 `Address Book`。

第一个实体的 `jpegPhoto` 属性具有非常特殊的语法。在冒号之后，你使用一个左括号（`<`），后面跟着一个空格，然后是照片的位置。由于照片是本地的，因此它以 `file://` 为前缀。它位于 `/home/paul/paulhudson.jpg`，所以整个 URL 是 `file:///home/paul/paulhudson.jpg`。

编辑文件以包含你组织中的人员后，保存并关闭编辑器。以 root 身份执行这些命令：

```
ldapsearch -x -D "cn=root,dc=hudzilla,dc=org" -f base.ldif
ldapsearch -x -D "cn=root,dc=hudzilla,dc=org" -f people.ldif
```

`ldap` 命令用于将 LDIF 转换为实时目录内容，最重要的是，可以在你的 LDAP 服务器运行时执行。`-x` 参数意味着仅使用基本身份验证，这意味着你需要提供 root 用户名和密码。`-W` 意味着提示密码。`-D` 允许你为用户名指定 DN，紧接着 D 之后，我们指定了之前在 `ldap.conf` 中设置的 root DN。`-f` 表示使用后续文件的 LDIF。

当你运行它们时，系统会提示你输入之前设置的 root 密码。输入后，你应该看到条目被添加的确认消息，如下所示：

```
adding new entry "cn=Paul Hudson,ou=People,dc=hudzilla,dc=org"
```

如果你得到类似 `ldap_bind: Can't contact LDAP server (-)` 的错误，你需要通过输入 `service ldap start` 来启动 LDAP 服务器。其他错误的可能来源是拼写错误。LDIF 是一个精确的格式，甚至精确到空格。

要测试目录是否已填充以及你的配置设置是否正确，运行此命令：

```
ldapsearch -x "objectclass=*"
```

`ldapsearch` 命令的作用如你预期的那样：它从命令行查询 LDAP 目录。再次，`-x` 意味着使用简单身份验证，尽管在这种情况下你不需要提供任何凭据，因为你只是从目录中读取。`objectclass=*` 指定返回任何对象类的任何条目，因此搜索将返回你目录中的所有条目。你可以修改搜索使其更具体，例如：

```
ldapsearch -x "cn=Ni*"
```

这返回所有通用名称以 Ni 开头的人。如果搜索有结果，你就可以配置你的客户端了。

> OpenLDAP 对其文件有特定的权限。`/var/lib/ldap` 目录应该由用户 `ldap` 和组 `ldap` 所有，权限为 600。如果你遇到问题，尝试运行 `chmod 600 /var/lib/ldap`。

## Thunderbird

要为 Evolution 配置 LDAP，点击 `New` 旁边的箭头并选择 `Address Book`。会出现一个新屏幕，其第一个选项提示你创建的地址簿类型。选择 `Address Book`。

第一个实体的 `jpegPhoto` 属性具有非常特殊的语法。在冒号之后，你使用一个左括号（`<`），后面跟着一个空格，然后是照片的位置。由于照片是本地的，因此它以 `file://` 为前缀。它位于 `/home/paul/paulhudson.jpg`，所以整个 URL 是 `file:///home/paul/paulhudson.jpg`。

编辑文件以包含你组织中的人员后，保存并关闭编辑器。以 root 身份执行以下两个命令：

```
ldapsearch -x -D "cn=root,dc=hudzilla,dc=org" -f base.ldif
ldapsearch -x -D "cn=root,dc=hudzilla,dc=org" -f people.ldif
```

`ldap` 命令用于将 LDIF 转换为实时目录内容，最重要的是，可以在你的 LDAP 服务器运行时执行。`-x` 参数意味着仅使用基本身份验证，这意味着你需要提供 root 用户名和密码。`-W` 意味着提示密码。`-D` 允许你为用户名指定 DN，紧接着 D 之后，我们指定了之前在 `ldap.conf` 中设置的 root DN。`-f` 表示使用后续文件的 LDIF。

当你运行它们时，系统会提示你输入之前设置的 root 密码。输入后，你应该看到条目被添加的确认消息，如下所示：

```
adding new entry "cn=Paul Hudson,ou=People,dc=hudzilla,dc=org"
```

如果你得到类似 `ldap_bind: Can't contact LDAP server (-)` 的错误，你需要通过输入 `service ldap start` 来启动 LDAP 服务器。其他错误的可能来源是拼写错误。LDIF 是一个精确的格式，甚至精确到空格。

要测试目录是否已填充以及你的配置设置是否正确，运行此命令：

```
ldapsearch -x "objectclass=*"
```

`ldapsearch` 命令的作用如你预期的那样：它从命令行查询 LDAP 目录。再次，`-x` 意味着使用简单身份验证，尽管在这种情况下你不需要提供任何凭据，因为你只是从目录中读取。`objectclass=*` 指定返回任何对象类的任何条目，因此搜索将返回你目录中的所有条目。

你可以修改搜索使其更具体，例如：

```
ldapsearch -x "cn=Ni*"
```

这返回所有通用名称以 Ni 开头的人。如果搜索有结果，你就可以配置你的客户端了。

> OpenLDAP 对其文件有特定的权限。`/var/lib/ldap` 目录应该由用户 `ldap` 和组 `ldap` 所有，权限为 600。如果你遇到问题，尝试运行 `chmod 600 /var/lib/ldap`。

## Evolution

要为 Evolution 配置 LDAP，点击 `New` 旁边的箭头并选择 `Address Book`。会出现一个新屏幕，其第一个选项提示你创建的地址簿类型。选择 `Address Book`。

第一个实体的 `jpegPhoto` 属性具有非常特殊的语法。在冒号之后，你使用一个左括号（`<`），后面跟着一个空格，然后是照片的位置（*注：此处原文存在重复逻辑*）。由于照片是本地的，它以 `file://` 为前缀。它位于 `/home/paul/paulhudson.jpg`，所以整个 URL 是 `file:///home/paul/paulhudson.jpg`。

编辑文件以包含你组织中的人员后，保存并关闭编辑器。以 root 身份执行这些命令：

```
ldapsearch -x -D "cn=root,dc=hudzilla,dc=org" -f base.ldif
ldapsearch -x -D "cn=root,dc=hudzilla,dc=org" -f people.ldif
```

`ldap` 命令用于将 LDIF 转换为实时目录内容，最重要的是，可以在你的 LDAP 服务器运行时执行。`-x` 参数意味着仅使用基本身份验证，这意味着你需要提供 root 用户名和密码。`-W` 意味着提示密码。`-D` 允许你为用户名指定 DN，紧接着 D 之后，我们指定了之前在 `ldap.conf` 中设置的 root DN。`-f` 表示使用后续文件的 LDIF。

当你运行它们时，系统会提示你输入之前设置的 root 密码。输入后，你应该看到条目被添加的确认消息，如下所示：

```
adding new entry "cn=Paul Hudson,ou=People,dc=hudzilla,dc=org"
```

如果你得到类似 `ldap_bind: Can't contact LDAP server (-)` 的错误，你需要通过输入 `service ldap start` 来启动 LDAP 服务器。其他错误的可能来源是拼写错误。LDIF 是一个精确的格式，甚至精确到空格。

要测试目录是否已填充以及你的配置设置是否正确，运行此命令：

```
ldapsearch -x "objectclass=*"
```
