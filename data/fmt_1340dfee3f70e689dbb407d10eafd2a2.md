
Red Hat 的`/etc/aliases`文件包含若干行注释。请忽略关于哪些邮件程序在邮件标头中显示别名的信息；重要的注释是提示你每次更新此文件时都要刷新别名。`newsam`不直接读取`/etc/aliases`文件。相反，它读取由`newsaliases`命令从该文件生成的数据库文件。

前 40 多行定义了特殊名称的别名。除了我们添加的`webmaster`别名外，所有的别名在 Red Hat aliases 文件中都是预配置的。前两个人们在任何运行默认设置的系统上预期找到的别名。其他大多数都分配给了`/etc/passwd`文件中出现的`daemon`用户。人们实际上无法使用`daemon`用户登录，因此任何可能指向这些伪账户的邮件都会被转发到真实的账户。在列表 5.1 中，所有这些邮件都路由到`root`账户——即使是发给`newsam`和`fpadm`的邮件，起初看起来是路由到`root`以外的其他账户。例如，`newsam`看起来被路由到用户账户，但仔细检查发现`news`是一个路由到`root`账户的别名。别名可以指向其他别名，但最终它们必须解析到一个真实的电子邮件，邮件才能成功投递。

当然，你并不真的希望人们登录`root`账户读取邮件，因此 aliases 文件也为`root`有一个别名。在示例中，我们修改了`root`条目，将所有发给`root`的邮件转发到`staff`，`staff`是另一个别名。注意别名指向其他别名的频率有多高。这样做非常有用，因为当投递邮件的真实用户账户发生变化时，只需要更新一个别名，而不是多个。

`staff`别名是一个邮件列表。邮件列表包含多个接收者。在示例中，有几个人负责维护此邮件服务器。发给`root`的信息通过`staff`邮件列表投送给这些人。

有两个特殊的别名与邮件列表相关。`owner-staff`别名是`sendmail`用于与`staff`别名相关的错误信息的特殊别名。如`list-`，其中`list`是邮件列表的。另一个特殊别名`request-`不是`sendmail`要求的，但远程用户期望如此。根据惯例，手动邮件列表维护请求（如添加或从列表中删除）被发送到`alias-request-`，其中`list`是邮件列表的名字。

最后八行是添加到文件中的用户别名。这些行将收到的邮件指向用户读取邮件的计算机。这些别名可以使用多种格式来处理发给用户的邮件。前三行将邮件转发到`norm@hawk.foobirds.org`的代码都说明了这一点。假设`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

## 定义个人邮件别名

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。

正如 Red Hat 文件中的八行代码所示，`sendmail`文件的功能之一是将邮件转发到其他账户。`/etc/aliases`文件不是`wren`，且 DNS 中的 MX 记录显示`wren`是`foobirds.org`的邮件交换服务器。那么，发给`norm.edwards@foobirds.org`的邮件实际上将被投递到`norm@hawk.foobirds.org`。正是别名和 MX 记录的结合使得许多组织使用的简化邮件地址方案成为可能。
