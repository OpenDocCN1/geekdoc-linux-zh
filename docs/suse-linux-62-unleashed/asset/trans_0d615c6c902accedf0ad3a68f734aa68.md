

# 网络与互联网服务

第二部分

第章 larry moe

为了方便起见，大型类可以继续在后续行中定义。以下对类 H 的定义与之前的相同：

```
CH larry
CH moe
CH curly
```

你也可以通过从文件中读取单词来定义一个类：

```
/usr/local/lib/localhosts
```

如果文件 `/usr/local/lib/localhosts` 包含 larry、moe 和 curly 单词，每行一个，则此定义等同于之前的两个。

为什么要使用宏和类？最好的理由是它们将信息集中在配置文件中。在先的示例中，如果你决定将邮件枢纽的名称从 mailer.gono.gov 更改为 mailhub.gono.gov，你只需要更改配置文件中 SR 补救措施的定义，使其能够像以前一样工作。如果 mailer.gono.gov 这个名称散布在整个文件中，你可能会忘记在某些地方更改它。此外，如果重要信息是集中的，你可以在一个地方对其进行大量的注释。因为配置文件充其量是晦涩的，大量的注释是缓解六个月后当你产生挫败感并怀疑自己为什么要进行某项更改时的良药。

# H 操作符：头部定义

你可能不想更改 V.8 sendmail 配置文件中提供的头部定义，因为它们已经遵循了被认可的标准。以下是一些头部文件：

```
H?Date: $a
H?F?Resent-From: $q
H?From: $q
Hx?Full-Name: $x
```

注意，头部定义可以使用宏，这些宏在插入邮件时会被展开。例如，在之前的 `Full-Name:` 头部定义中使用的 `$x` 会展开为发送者的全名。

可选的 `?mailerflag?` 结构告诉 sendmail 只有当所选邮件传输器设置了该传输器标记时才插入头部（参见本章后文“M 操作符：邮件传输器定义”）。

# SMTP 与协议
第 9 章

假设你的本地邮件传输器定义有一个标记 `q`，sendmail 选择该传输器来投递邮件。如果你的配置文件包含如下头部定义，sendmail 将该头部插入到通过本地邮件传输器投递的邮件中，并替换宏 `$` 的值：

```
H7QX-Fruit-of-the-day: $F
```

为什么要使用 `?mailerflag?`？不同的协议可能需要不同的头部。由于它们也需要不同的邮件传输器，你可以在传输器定义中为每个传输器定义相应的传输器标记，并在头部定义中使用 `?mailerflag?` 结构告诉 sendmail 是否插入该头部。

# o 操作符：设置选项

sendmail 有许多选项可以更改其操作或告诉它所使用的文件位置。大多数选项既可以在命令行指定，也可以在配置文件中指定。例如，你可以指定别名文件（aliases file）的位置。要在命令行上指定别名文件，使用 `-o` 选项：

```
$ /usr/bin/sendmail -oa/etc/aliases [other arguments...]
```

要在文件中执行相同的操作，你需要包含如下行：

```
OA/etc/aliases
```

两种用法是等效的，但别名文件位置等选项很少更改，大多数人在 `sendmail.cf` 中设置它们。V8 sendmail 选项在 SIG 中详细描述。

# p 操作符：邮件优先级

用户可以包含指示其邮件相对重要性的头部，sendmail 可以使用这些头部来决定竞争邮件的优先级。V8 sendmail 的优先级规定如下：

```
Pspecial-delivery=100
Pfirst-class=0
Plist=-30
Pbulk=-60
Pjunk=-100
```

如果运行大型邮件列表的用户在邮件中包含 `Precedence: bulk` 头部，sendmail 给这些邮件优先级将低于带有 `Precedence: first-class` 头的邮件。

# v 操作符：sendmail.cf 版本级别

随着 V.8 sendmail 版本的更新，其作者添加了新功能。`V` 操作符告诉 V.8 sendmail 它应该期望在你的配置文件中找到哪些功能。旧版本的 sendmail 不理解此命令。SIOG 详细解释了配置文件的版本级别。

> 配置文件的版本级别并不对应于 sendmail 的版本。V.8 sendmail 理解第 1 到 5 版本的配置文件，不存在像具有 8 个配置文件的那样的版本。

# κ 操作符：关键文件

sendmail 一直使用关键数据库——例如别名数据库。给定关键邮局（postmaster），sendmail 会查找与该键关联的数据，并返回邮局邮件应投递到的账户名称。V.8 sendmail 将此扩展到任意数据库，包括 NIS 映射（Sun 的网络信息服务，以前称为黄页或 YP；详情请参见第 17 章）。`κ` 操作符告诉 sendmail 数据库的位置、类别以及如何访问它。V.8 sendmail 支持以下类用户自定义数据库：dbm、btree、hash 和 NIS。在 Linux 下编译时使用的默认是 hash 或 btree 格式之一。通过 SIOG 了解关键文件的详情。

# M 操作符：邮件传输器定义

邮件传输器可以是 MTA（邮件传输代理）或投递代理。回想一下别名文件允许你向登录名（该名可能被别名为远程用户）、程序或文件发送邮件。可以为每个目的定义特殊的邮件传输器，尽管 SMTP MTA 是

# SMTP 与协议
第 9 章

假设你的本地邮件传输器定义有一个标记 `q`，sendmail 选择该传输器来投递邮件。如果你的配置文件包含如下头部定义，sendmail 将该头部插入到通过本地邮件传输器投递的邮件中，并替换宏 `$` 的值：

```
H7QX-Fruit-of-the-day: $F
```

为什么要使用 `?mailerflag?`？不同的协议可能需要不同的头部。由于它们也需要不同的邮件传输器，你可以在传输器定义中为每个传输器定义相应的传输器标记，并在头部定义中使用 `?mailerflag?` 结构告诉 sendmail 是否插入该头部。

# o 操作符：设置选项

sendmail 有许多选项可以更改其操作或告诉它所使用的文件位置。大多数选项既可以在命令行指定，也可以在配置文件中指定。例如，你可以指定别名文件的位置。要在命令行上指定别名文件，使用 `-o` 选项：

```
$ /usr/bin/sendmail -oa/etc/aliases [other arguments...]
```

要在文件中执行相同的操作，你需要包含如下行：

```
OA/etc/aliases
```

两种用法是等效的，但别名文件位置等选项很少更改，大多数人在 `sendmail.cf` 中设置它们。V8 sendmail 选项在 SIG 中详细描述。

# p 操作符：邮件优先级

用户可以包含指示其邮件相对重要性的头部，sendmail 可以使用这些头部来决定竞争邮件的优先级。V8 sendmail 的优先级规定如下：

```
Pspecial-delivery=100
Pfirst-class=0
Plist=-30
Pbulk=-60
Pjunk=-100
```

如果运行大型邮件列表的用户在邮件中包含 `Precedence: bulk` 头部，sendmail 给这些邮件优先级将低于带有 `Precedence: first-class` 的邮件。

# v 操作符：sendmail.cf 版本级别

随着 V.8 sendmail 版本的更新，其作者添加了新功能。`V` 操作符告诉 V.8 sendmail 它应该期望在你的配置文件中找到哪些功能。旧版本的 sendmail 不理解此命令。SIOG 详细解释了配置文件的版本级别。

> 配置文件的版本级别并不对应于 sendmail 的版本。V.8 sendmail 理解第 1 到 5 版本的配置文件，不存在像具有 8个配置文件的那样的版本。

# κ 操作符：关键文件

sendmail 一直使用关键数据库——例如别名数据库。给定关键邮局，sendmail 会查找与该键关联的数据，并返回邮局邮件应投递到的账户名称。V.8 sendmail 将此扩展到任意数据库，包括 NIS 映射（Sun 的网络信息服务，以前称为黄页或 YP；详情请参见第 17 章）。`κ` 操作符告诉 sendmail 数据库的位置、类别以及如何访问它。V.8 sendmail 支持以下类用户自定义数据库：dbm、btree、hash 和 NIS。在 Linux 下编译时使用的默认是 hash 或 btree 格式之一。通过 SIOG 了解关键文件的详情。

# M 操作符：邮件传输器定义

邮件传输器可以是 MTA 或投递代理。回想一下别名文件允许你向登录名（该名可能被别名为远程用户）、程序或文件发送邮件。可以为每个目的定义特殊的邮件传输器，尽管 SMTP MTA 是

# SMTP 与协议
第 9 章

假设你的本地邮件传输器定义有一个标记 `q`，sendmail 选择该传输器来投递邮件。如果你的配置文件包含如下头部定义，sendmail 将该头部插入到通过本地邮件传输器投递的邮件中，并替换宏 `$` 的值：

```
H7QX-Fruit-of-the-day: $F
```

为什么要使用 `?mailerflag?`？不同的协议可能需要不同的头部。由于它们也需要不同的邮件传输器，你可以在传输器定义中为每个传输器定义相应的传输器标记，并在头部定义中使用 `?mailerflag?` 结构告诉 sendmail 是否插入该头部。

# o 操作符：设置选项

sendmail 有许多选项可以更改其操作或告诉它所使用的文件位置。大多数选项既可以在命令行指定，也可以在配置文件中指定。例如，你可以指定别名文件的位置。要在命令行上指定别名文件，使用 `-o` 选项：

```
$ /usr/bin/sendmail -oa/etc/aliases [other arguments...]
```

要在文件中执行相同的操作，你需要包含如下行：

```
OA/etc/aliases
```

两种用法是等效的，但别名文件位置等选项很少更改，大多数人在 `sendmail.cf` 中设置它们。V8 sendmail 选项在 SIG 中详细描述。

# p 操作符：邮件优先级

用户可以包含指示其邮件相对重要性的头部，sendmail 可以使用这些头部来决定竞争邮件的优先级。V8 sendmail 的优先级规定如下：

```
Pspecial-delivery=100
Pfirst-class=0
Plist=-30
Pbulk=-60
Pjunk=-100
```

如果运行大型邮件列表的用户在邮件中包含 `Precedence: bulk` 头部，sendmail 给这些邮件优先级将低于带有 `Precedence: first-class` 的邮件。

# v 操作符：sendmail.cf 版本级别

随着 V.8 sendmail 版本的更新，其作者添加了新功能。`V` 操作符告诉 V.8 sendmail 它应该期望在你的配置文件中找到哪些功能。旧版本的 sendmail 不理解此命令。SIOG 详细解释了配置文件的版本级别。

> 配置文件的版本级别并不对应于 sendmail 的版本。V.8 sendmail 理解第 1 到 5 版本的配置文件，不存在像具有 8个配置文件的那样的版本。

# κ 操作符：关键文件

sendmail 一直使用关键数据库——例如别名数据库。给定关键邮局，sendmail 会查找与该键关联的数据，并返回邮局邮件应投递到的账户名称。V.8 sendmail 将此扩展到任意数据库，包括 NIS 映射（Sun 的网络信息服务，以前称为黄页或 YP；详情请参见第 17 章）。`κ` 操作符告诉 sendmail 数据库的位置、类别以及如何访问它。V.8 sendmail 支持以下类用户自定义数据库：dbm、btree、hash 和 NIS。在 Linux 下编译时使用的默认是 hash 或 btree 格式之一。通过 SIOG 了解关键文件的详情。

# S 和 R 操作符：规则集与重写规则

配置文件由一系列规则集组成，这些规则类似于程序中的子程序。规则集用于检测错误地址、将地址重写为远程邮件传输器可以理解的形式，并将邮件路由到 sendmail 的

![](img/cbac72550c7126a22162e94d91a0c360_326_0.png)

